
# CityEats Recommender (ALS) — MET CS 777

## How to run (quickcheck)
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

## Repo layout
jobs/ (training script)  
src/common/ (spark utils)  
conf/config.yaml (ALS + eval params)  
data/sample/SAMPLE_RATINGS.csv (tiny sample for graders)  
DATA.md (data link/notes)

## Results (fill after run)
Precision@K: ___  |  Recall@K: ___  |  NDCG@K: ___
"@ | Out-File -Encoding utf8 .\README.md -Force
