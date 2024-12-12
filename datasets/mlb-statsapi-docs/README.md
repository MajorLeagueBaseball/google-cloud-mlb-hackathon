# MLB StatsAPI Documentation

This directory contains documentation and resources related to MLB's Stats API, including information about the GUMBO (Grand Unified Master Baseball Object) data feeds. The data is stored in the Google Cloud Storage bucket.

## Dataset Access

You can access these files through:

1. **Google Cloud Console**:
   - [MLB StatsAPI Documentation Folder](https://console.cloud.google.com/storage/browser/gcp-mlb-hackathon-2025/datasets/mlb-statsapi-docs)

2. **Command Line (using gsutil)**:
   ```bash
   # Download all StatsAPI documentation files
   gsutil -m cp -r gs://gcp-mlb-hackathon-2025/datasets/mlb-statsapi-docs/* .
   ```

## Contents

This directory contains documentation for MLB's Stats API, including:
- API endpoint descriptions
- Data structure documentation
- Usage examples
- GUMBO feed documentation

For more information about the overall dataset structure and access methods, please refer to the main [README](../../README.md) in the root directory. 