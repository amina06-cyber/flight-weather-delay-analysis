# notebooks
Six notebooks, meant to be run in order. Each one picks up where the last one left off.

## `01_data_acquisition.ipynb`
Loads the raw Kaggle CSV and previews it, shape, columns, first few rows. Just getting a feel for what we're working with before touching anything.

## `02_fetch_weather_api.ipynb`
This is where the weather data comes from. I couldn't realistically call the API for every single flight (millions of them), so I narrowed it down to the 10 busiest airports and just June across all 5 years, that brought it down to about 1,500 unique airport-date combinations, which is actually doable on the free API tier. Loops through each one, hits the Open-Meteo API, and saves the results.

## `03_cleaning.ipynb`
Fixes the date column (it loads in as plain text otherwise), fills in the delay-cause columns with 0 where they're blank (blank there just means no delay was recorded, not that data is missing), and drops a handful of insane outliers, one flight in the raw data was apparently delayed 2,690 minutes which is over 44 hours, clearly not normal. Also does the same basic cleanup on the weather data, though that one came back from the API pretty clean already.

## `04_integration.ipynb`
The actual merge, flights joined with weather on flight date + origin airport. I also measured how many rows failed to find a weather match (turned out to be tiny, like 0.15%) since that's basically the integration error rate.

## `05_relational_DBMS.ipynb`
Takes the final integrated dataset and dumps it into a SQLite database. Then runs two SQL queries on it, one for average delay per airport, one comparing rainy vs clear days.

## `06_EDA_analysis.ipynb`
Where the actual analysis happens. Makes the 4 charts and answers all four research questions, this is basically the notebook that the whole project builds up to.

---

**Heads up:** these were built and run in Google Colab, so they expect to mount Google Drive and read/write from specific Drive paths. If you're running locally you'll need to swap those paths out.
