# Google Cloud x MLB Hackathon Resources

Welcome to the Google Cloud x MLB Hackathon! This repository contains resources and instructions to help you get started with accessing MLB's data services for your hackathon project. Stay tuned to this repo as more datasets become available.

## MLB GUMBO Data Access

A primary data source for this hackathon will be MLB's GUMBO (Grand Unified Master Baseball Object) data feeds, which are available without authentication.

### About GUMBO
The GUMBO (Grand Unified Master Baseball Object) live data feed provides a standardized JSON response that summarizes the entire state of a selected game upon each update. Unlike previous live event data feeds, GUMBO provides complete game information with every object creation, rather than incremental updates.

### Key Benefits

- **Complete Game State**: No need to maintain game state locally or build upon message sequences - each GUMBO object includes complete and current dataset for the entire game
- **Standard JSON Format**: GUMBO follows true JSON standards, unlike previous feed formats
- **Flexible Access Methods**: Available via:
  - Websocket listener (push updates every 1-2 seconds)
  - Stats API (pull updates every 12 seconds)
- **Development-Friendly**: Use actual production data for development at any time without requiring scheduled test data delivery

### API Endpoints

Access GUMBO data using these base URLs (replace `{game_pk}` with the specific game ID):

1. **Current Game State**:
   ```
   https://statsapi.mlb.com/api/v1.1/game/{game_pk}/feed/live
   ```

2. **Specific Game Timestamp**:
   ```
   https://statsapi.mlb.com/api/v1.1/game/{game_pk}/feed/live?timecode=yyyymmdd_######
   ```

3. **List of Game Update Timestamps**:
   ```
   https://statsapi.mlb.com/api/v1.1/game/{game_pk}/feed/live/timestamps
   ```

### Common API Query Examples

Here are some useful examples of common Stats API queries:

1. **Get 2024 MLB Regular Season Schedule**:
   ```
   https://statsapi.mlb.com/api/v1/schedule?sportId=1&season=2024&gameType=R
   ```
   Parameters explained:
   - `sportId=1`: MLB (1 represents Major League Baseball)
   - `season=2024`: The season year
   - `gameType=R`: Regular season games (R = Regular Season, P = Postseason, S = Spring Training)

2. **Get Los Angeles Dodgers 2024 Roster**:
   ```
   https://statsapi.mlb.com/api/v1/teams/119/roster?season=2024
   ```
   Parameters explained:
   - `119`: Team ID for LA Dodgers
   - `season=2024`: The season year

3. **Get Team Information**:
   ```
   https://statsapi.mlb.com/api/v1/teams/119
   ```
   - Returns detailed information about a specific team (119 = Dodgers)
   - Add `?season=2024` to get team info for a specific season

4. **Get Player Information**:
   ```
   https://statsapi.mlb.com/api/v1/people/660271
   ```
   - Returns detailed information about a specific player (660271 = Shohei Ohtani)
   - Add `?season=2024` to get player info for a specific season

5. **Get Live Game Data**:
   ```
   https://statsapi.mlb.com/api/v1.1/game/716463/feed/live
   ```
   - Returns live GUMBO feed for a specific game
   - Game PKs can be obtained from the schedule endpoint

Common Query Parameters:
- `hydrate`: Add additional data to the response (e.g., `?hydrate=stats,team`)
- `fields`: Limit the response to specific fields
- `season`: Specify a season year
- `date`: Specify a specific date (format: MM/DD/YYYY)

Note: All endpoints return JSON data. You can use tools like `curl` or Python's `requests` library to fetch the data:

```python
import requests

# Example: Get Dodgers roster
url = "https://statsapi.mlb.com/api/v1/teams/119/roster?season=2024"
response = requests.get(url)
data = response.json()
```

### Getting Started

1. Review the provided [documentation](https://github.com/MajorLeagueBaseball/google-cloud-mlb-hackathon/tree/main/datasets/mlb-statsapi-docs) in this repository for detailed information about:
   - Available endpoints
   - Data structure
   - Query parameters
   - Response formats

### Historical Data Availability

The MLB data feeds provide different levels of historical data granularity depending on the time period:

- **1901-1968**: Boxscore level only
- **1969-1988**: Play-by-play level
- **1989-2007**: Pitch-by-pitch level
- **2008-2014**: Pitch-by-pitch with pitch speed/break information (Pitch F/x)
- **2015-Present**: Pitch-by-pitch with enhanced metrics:
  - Pitch speed
  - Exit velocity
  - Home Run distance

#### Minor League Coverage
- **2021**: Florida State League (A) added
- **2022**: Pacific Coast League (AAA) added
- **2023**: International League (AAA) added

## Accessing Dataset Files

All datasets for the hackathon are available in our public Google Cloud Storage bucket. The datasets are organized into the following categories:

- MLB Caption Data
- MLB Fan Content Interaction Data
- MLB StatsAPI Documentation
- Game Data (including 2024 home runs dataset)

### Access Methods

1. **Direct Browser Access**:
   Access the datasets through the Google Cloud Console:
   [GCP MLB Hackathon 2025 Bucket](https://console.cloud.google.com/storage/browser/gcp-mlb-hackathon-2025)

2. **Command Line Access**:
   Using `gsutil` (part of Google Cloud SDK):
   ```bash
   # Download all files
   gsutil -m cp -r gs://gcp-mlb-hackathon-2025/* .
   
   # Download specific dataset
   gsutil cp gs://gcp-mlb-hackathon-2025/datasets/2024-mlb-homeruns.csv .
   ```

## Additional Resources

### MLB Glossary
For help understanding baseball terminology and statistics, refer to the [MLB Glossary](https://www.mlb.com/glossary). This comprehensive resource explains baseball terms, statistics, and metrics used throughout MLB's data services.

More information about available datasets and hackathon themes will be provided in this repository. Stay tuned for updates! 
