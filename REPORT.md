
# MET CS 777 - Term Project Report (Template)

**Project:** CityEats Recommender (PySpark ALS)  
**Student:** Srivatsav Shrikanth (sri99-svg)  
**Date:** <MM/DD/YYYY>

---

## 1. Introduction
- Problem: Recommend top-N items to users from historical explicit ratings.
- Motivation: Scalable recommendation for large user-item graphs using Spark.
- Approach: Matrix factorization with ALS; evaluate ranking quality at K.

## 2. Data
- Source: Yelp review subset (converted to explicit ratings parquet).
- Shape: ~20M rows (local subset acceptable); columns: `user_id, item_id, rating`.
- Preparation:
  - Null drop, type casting.
  - StringIndexer to integer indices (`user_idx`, `biz_idx`).
  - Train/test split (global random).

## 3. Methodology
- Algorithm: Alternating Least Squares (ALS) in PySpark.
- Hyperparameters: `rank`, `regParam`, `maxIter`, `nonnegative`, `coldStartStrategy`.
- Training details: block counts and checkpoint interval for stability.
- Evaluation:
  - Precision@K, Recall@K, NDCG@K with a positive threshold on `stars`.
  - Report means across users.

## 4. Implementation
- Entry script: `jobs/train_als_local.py`.
- Config: `conf/config.yaml` stores ALS and evaluation params.
- Commands: see README for exact spark-submit calls and Spark UI notes.

## 5. Results
- Dataset split: Train <%>, Test <%> (seed 42).
- K: <K>
- Metrics:
  - Precision@K: <value>
  - Recall@K: <value>
  - NDCG@K: <value>
- Counts: users=<n_users>, items=<n_items>, rows=<n_rows>.
- Sample recommendations: user <id> - <item, score> ...

## 6. Discussion
- Interpretation of metrics; effect of `rank` and `regParam`.
- Cold start handling (dropped predictions).
- Runtime and memory notes on local versus cluster runs.

## 7. Conclusion and Future Work
- Summary of findings.
- Next steps: implicit feedback, side features, Dataproc/Databricks cluster run, serving API.

## 8. References
- PySpark ALS documentation.
- Yelp academic dataset (if applicable).
- Any additional references (follow two-line rule).
