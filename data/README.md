# data/

```
raw/           → straight from the source, untouched
cleaned/       → after fixing dates, nulls, and outliers
integrated/    → flights + weather merged together, this is the final dataset used for analysis
flights_weather.db → SQLite database with the integrated data loaded in
```

## raw/
`weather_api_raw.csv` — the weather data exactly as it came back from the Open-Meteo API, before any cleaning. About 1,500 rows, one per airport-date combination.

The raw Kaggle flight dataset is too big to upload here (500MB+), so it's not included. Grab it directly from Kaggle:
https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023

## cleaned/
`flights_cleaned.csv` and `weather_cleaned.csv` — same data, but with dates fixed, missing values handled properly, and extreme outliers removed.

## integrated/
`flights_weather_integrated.csv` — the final dataset. Every flight row here has the real weather conditions (temperature, precipitation, wind speed) attached based on the airport and date it departed. This is what all the analysis in notebook 06 actually runs on.

## flights_weather.db
SQLite database containing the integrated dataset in a single table called `flights`. Built so I could run actual SQL queries instead of just doing everything in pandas.
