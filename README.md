# Spotify Chart Data Analysis Project

A Big Data Analytics (BDA) term project that collects and enriches Spotify chart data with audio features using the Spotify API.

## Overview

This project downloads Spotify top chart data and enriches it with detailed audio features and artist information using the Spotify Web API. The resulting dataset can be used for music analytics, trend analysis, and machine learning applications.

## Project Structure

```
├── Download_SpotifyAPI_Data.py    # Main Python script to download Spotify data
├── Download_SpotifyAPI_Data.ipynb # Jupyter notebook version of the download script
├── merge_outputs.py               # Script to merge all output files into a single dataset
├── dataset/                       # Contains the source and final datasets
│   ├── unique_min_rank.csv        # Source data with unique tracks
│   └── spotify_chart_and_api_dataset.csv  # Final enriched dataset
├── outputs/                       # Intermediate output files from data collection
└── merged_outputs/                # Merged intermediate files
```

## Dataset Features

The enriched dataset includes the following features for each track:

### Chart Information
- `title` - Track title
- `rank` - Chart position
- `date` - Chart date
- `artist` - Artist name(s)
- `url` - Spotify track URL
- `region` - Geographic region
- `chart` - Chart type (e.g., top200)
- `trend` - Chart trend (NEW_ENTRY, MOVE_UP, etc.)
- `streams` - Number of streams
- `min_rank` - Minimum rank achieved

### Audio Features (from Spotify API)
- `danceability` - How suitable a track is for dancing (0.0 to 1.0)
- `energy` - Intensity and activity measure (0.0 to 1.0)
- `key` - Musical key of the track
- `loudness` - Overall loudness in decibels
- `mode` - Major (1) or minor (0) modality
- `speechiness` - Presence of spoken words (0.0 to 1.0)
- `acousticness` - Acoustic confidence measure (0.0 to 1.0)
- `instrumentalness` - Predicts whether a track has no vocals (0.0 to 1.0)
- `liveness` - Detects presence of a live audience (0.0 to 1.0)
- `valence` - Musical positiveness (0.0 to 1.0)
- `tempo` - Estimated tempo in BPM
- `duration_ms` - Track duration in milliseconds

### Artist Information
- `artist_url` - Spotify artist URL
- `track_popularity` - Popularity score of the track
- `artist_genres` - List of genres associated with the artist
- `artist_popularity` - Popularity score of the artist

## Requirements

- Python 3.x
- pandas
- numpy
- spotipy
- tqdm

Install dependencies:
```bash
pip install pandas numpy spotipy tqdm
```

## Usage

### 1. Set Up Spotify API Credentials

You need Spotify API credentials to run the data collection scripts. Create an app at [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).

**Security Note:** It is recommended to store your credentials as environment variables rather than hardcoding them in the scripts:

```bash
export SPOTIPY_CLIENT_ID='your_client_id'
export SPOTIPY_CLIENT_SECRET='your_client_secret'
```

Never commit credentials to version control.

### 2. Download Data

Run the download script to fetch audio features and artist information:

```bash
python Download_SpotifyAPI_Data.py
```

Or use the Jupyter notebook for an interactive experience:
```bash
jupyter notebook Download_SpotifyAPI_Data.ipynb
```

### 3. Merge Outputs

After data collection is complete, merge all output files:

```bash
python merge_outputs.py
```

The final dataset will be saved to `dataset/spotify_chart_and_api_dataset.csv`.

## Notes

- The data collection process uses chunked requests to handle Spotify API rate limits
- Timeout handling is implemented to gracefully handle API delays
- The scripts split the data into multiple parts for processing resilience
