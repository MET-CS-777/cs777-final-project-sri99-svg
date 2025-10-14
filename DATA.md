
# Data Files / Links

## Primary Ratings Parquet
- Path (local): `data/silver_explicit.parquet`
- Schema: `user_id`, `item_id`, `rating` (double)
- Size: large - cannot commit to repo. Will provide access via a shared drive or university storage if required.

## Small Sample
- `data/sample/SAMPLE_RATINGS.csv` (included here) with the same schema and a few rows.

## Notes
- The training script automatically maps to internal columns (`business_id`, `stars`). No manual renaming needed.
