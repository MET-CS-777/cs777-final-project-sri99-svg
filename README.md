
# CityEats Recommender - MET CS 777

## How to run (quickcheck)
```powershell
spark-submit --master local[*] `
  --conf spark.driver.bindAddress=127.0.0.1 `
  --conf spark.driver.host=127.0.0.1 `
  --conf spark.sql.shuffle.partitions=120 `
  --conf spark.driver.memory=8g `
  .\jobs\train_als_local.py `
  --in .\data\silver_explicit.parquet `
  --out .\data\als_model_explicit `
  --run-name quickcheck `
  --k 50 `
  --global-split 0.9 `
  --disable-batch `
  --skip-recs-json
```

## Repo layout
- jobs/train_als_local.py – training & evaluation
- src/common/spark_utils.py – SparkSession helper
- conf/config.yaml – ALS + eval params
- data/sample/SAMPLE_RATINGS.csv – tiny sample for graders
- DATA.md – data path/notes

## Results (snapshot)
- Precision@50: 0.0011
- Recall@50: 0.0129
- NDCG@50: 0.0042

Notes: metrics computed with exclude-seen recommendations on a global split. Full run artifacts (metrics.json, manifest.json) will be added after the longer run.
