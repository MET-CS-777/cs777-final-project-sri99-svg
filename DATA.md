
# Data Files / Links

## Primary Ratings Parquet
- Path (local): `data/silver_explicit.parquet`
- Schema: `user_id`, `item_id`, `rating` (double)
- Size: large - do not commit to repo. Provide access via a shared drive or university storage.

## Optional Small Sample (for grading convenience)
- `data/sample/SAMPLE_RATINGS.csv` (included here) with the same schema and a few rows, so TAs can validate the code path.

## Notes
- The training script automatically maps to internal columns (`business_id`, `stars`). No manual renaming needed.
