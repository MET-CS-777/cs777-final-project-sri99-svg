
# CityEats Recommender - MET CS 777 Term Project

**Course:** MET CS 777 - Big Data Analytics  
**Student:** Srivatsav Shrikanth (sri99-svg)  
**Project type:** Large scale recommendation (Matrix Factorization with ALS) in PySpark  
**Dataset:** Explicit user-item ratings prepared from a Yelp review subset (parquet with columns: `user_id, item_id, rating`).

---

## 1) Project Summary
We build a top-N recommendation system using Alternating Least Squares (ALS) on a multi-million-row ratings table.
The pipeline loads ratings, maps IDs to integer indices, trains ALS, and evaluates Precision@K, Recall@K, NDCG@K on a held-out split. We export recommendation artifacts and run metrics for inspection.

---

## 2) Repository Layout
```
.
├─ jobs/
│  ├─ train_als_local.py      # main training & evaluation entrypoint (PySpark)
├─ src/
│  └─ common/
│     └─ spark_utils.py       # SparkSession helper
├─ conf/
│  └─ config.yaml             # ALS + eval params (rank, regParam, maxIter, k, pos_thresh,...)
├─ data/
│  ├─ silver_explicit.parquet # ratings parquet: user_id, item_id, rating  (provided / linked)
│  └─ runs/                   # output artifacts (created on run)
└─ README.md (this file)
```

---

## 3) Environment & Requirements
- Java 8, Spark 3.5.x, Python 3.10+ recommended
- PySpark available via local Spark distribution

**Local environment (PowerShell):**
```powershell
# from repo root
$env:PYTHONPATH = "$PWD"
```

---

## 4) How to Run (Local Spark)
### Quick smoke test (fast / low resource)
```powershell
spark-submit --master local[*] `
  --conf spark.driver.bindAddress=127.0.0.1 `
  --conf spark.driver.host=127.0.0.1 `
  --conf spark.sql.shuffle.partitions=200 `
  --conf spark.driver.memory=8g `
  .\jobs\train_als_local.py `
  --in .\data\silver_explicit.parquet `
  --out .\data\als_model_explicit `
  --run-name quickcheck `
  --k 50 `
  --metrics-sample-frac 0.05 `
  --global-split 0.9 `
  --disable-batch `
  --skip-recs-json
```

### Full run (higher quality)
- Increase `rank` and `maxIter` in `conf/config.yaml` (e.g., rank=50, maxIter=15).
- Remove `--disable-batch` and `--skip-recs-json`.
- Optionally set `--k 100` and `--global-split 0.8`.

**Spark UI:** http://localhost:4040 during execution.

---

## 5) Inputs
- Ratings parquet (`data/silver_explicit.parquet`) with schema:
  - `user_id` (int or string), `item_id` (int or string), `rating` (double/float).
- The training script automatically aliases to internal columns (`business_id`, `stars`).

If the parquet cannot be hosted in the repo, include a link where TAs can download it, or a small sample under `data/sample/`.

---

## 6) Outputs (under `data/runs/<run-name>/`)
- `model/` - saved ALS model
- `ui_map/`, `bi_map/` - user/item index mappings
- `seen.parquet` - items each user already interacted with (train)
- `batch_csv/` (optional) - flat recommendations for batch scoring
- `recs_json/` (optional) - per user top-N recommendations as JSON
- `metrics.json` - Precision@K, Recall@K, NDCG@K and counts
- `manifest.json` - paths and config snapshot for the run

---

## 7) Evaluation
- Split mode: global random split (default 0.8 or 0.9 train fraction).
- Metrics: Precision@K, Recall@K, NDCG@K at the configured K.
- Positive threshold: `pos_thresh` from `conf/config.yaml` (e.g., stars >= 4).

Tip: for quick marking, use `--metrics-sample-frac 0.05` which computes metrics on a 5% sample of users to reduce shuffle time.

---

## 8) Reproducibility & Notes
- Set a fixed `--split-seed` (default 42) for deterministic splits.
- All run artifacts are self contained in `data/runs/<run-name>/`.
- If running on a small laptop, keep `spark.sql.shuffle.partitions` around 200 for quickcheck, and raise slowly if needed.

---

## 9) Academic Honesty
Only original code is included; external references (if any) are cited in code comments per course policy.

---

## 10) Results (fill after run completes)
- Run name: `quickcheck`
- K: 50
- Metrics:
  - Precision@K: <value>
  - Recall@K: <value>
  - NDCG@K: <value>
- Counts: users=<n_users>, items=<n_items>, rows=<n_rows>
- Observations:
  - <bullet 1>
  - <bullet 2>
