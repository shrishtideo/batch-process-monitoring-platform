# batch-process-monitoring-platform
Synthetic Batch Process Monitoring Source Data
This is a learning dataset only. All batches, events, sensor readings, tests, and specification limits are synthetic and illustrative. They are not real pharmaceutical records, validated process limits, or approved quality specifications.
Files
`source_data/automation/automation_report_20261008.csv` — automation/audit events (20 rows)
`source_data/scada/scada_sensor_export_20261008.csv` — sensor time-series readings (20 rows)
`source_data/analytical/analytical_test_sheet_20261008.csv` — laboratory/analytical test records (20 rows)
Intentional data-quality cases
Duplicate IDs/rows: EVT019, RDG019, TST019
Nulls: blank sensor measurement, blank analytical result, blank expected/actual values where not applicable
Numeric formatting: decimal commas such as `42,1`, `6,9`, `94,5`, and `2,0 L`
Invalid values: `ERROR`, negative temperature, extreme temperature
Out-of-range analytical results: purity below illustrative minimum, pH outside illustrative range
Status and case normalization opportunities: `Valid`/`Invalid`, `COMPLETED`, `WARNING`, `FAILED`, `Pending`
Date parsing: one analytical timestamp uses `DD/MM/YYYY` instead of ISO-like format
Cross-source reconciliation: batch IDs appear across sources, but not every batch appears in every source
Suggested first transformations
Preserve raw files unchanged in Bronze.
Trim strings and standardize status casing in Silver.
Parse timestamps with explicit formats.
Cast numeric columns safely; do not silently convert `ERROR` or blank values to zero.
Detect duplicates by source ID and quarantine or mark them rather than deleting evidence from Bronze.
Flag sensor values outside configurable practice-only ranges.
Compare analytical results with the row's illustrative min/max only when result and specification are valid and units match.
Keep missing/pending/invalid tests separate from pass/fail.batch-process-monitoring-platform
