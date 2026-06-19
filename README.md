# Does Weather Actually Cause Flight Delays?

A data project where I tried to figure out whether bad weather really messes up flight schedules in the US, and whether airlines are even honest about blaming the weather when things go wrong (spoiler: they're really not).

## The idea

So everyone always blames "weather" when their flight is late. I wanted to actually check if that's true using real data, instead of just assuming. I took a massive Kaggle dataset of US flights from 2019-2023 and combined it with real historical weather data pulled from a free API, then dug into whether the two are actually connected.

Turns out the most interesting part of this project wasn't even the weather-delay connection, it was finding out that airlines basically never admit when weather is the real reason for a delay. More on that below.

## What I was trying to answer

1. **Do rainy/windy days actually cause more delays than clear days?**
2. **When the weather IS bad, do airlines honestly report it as the cause?**
3. **Which airports get hit hardest by weather delays?**
4. **Can you actually predict a delay just from weather data?**

## Where the data came from

This project needed two different data sources, and I leaned into making them genuinely connect rather than just sitting next to each other.

**Source 1 — Kaggle**
[Flight Delay and Cancellation Dataset (2019-2023)](https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023) by Patrick Zelazko, originally from the US Dept. of Transportation. It's huge (millions of rows) so I didn't upload the raw file here — grab it from the Kaggle link if you want to reproduce this.

**Source 2 — Open-Meteo API**
A completely free historical weather API ([open-meteo.com](https://open-meteo.com)), no API key needed. For every flight I cared about, I pulled the actual temperature, rainfall, and wind speed at that airport on that exact date.

I matched the two datasets using the flight date + airport code, so every flight row ends up enriched with the real weather that was happening that day.

## How I actually built this

I split everything into 6 notebooks because honestly trying to do this in one giant notebook was a nightmare the first time I tried. See the `notebooks/` folder for details on each one and the order to run them in.

## What I actually found

**Rainy days are genuinely worse for delays.** Average delay jumps from 12.3 minutes on clear days to 18.5 minutes on rainy ones, about 51% worse.

**Airlines barely ever admit weather caused the delay.**  I checked every flight that happened during objectively bad weather (decent rain or wind), and only 4% of those flights had the airline's own data flagging weather as the cause. The other 96% just, didn't get flagged. Make of that what you will.

**Orlando (MCO) has the worst delays, Seattle (SEA) has the best** which is kind of funny because Seattle is famously rainy. So clearly it's not just about how much it rains, it's about how well an airport handles it.

**Weather alone can't really predict delays.** I built two basic regression models, one using the airline's own weather flag, one using the real API weather data, and both scored really low (under 8% R²). Basically, weather matters, but it's nowhere near the whole story. Late aircraft, staffing, air traffic control, there's a lot more going on.

## Tools I used

Python, pandas, the `requests` library for hitting the API, SQLite for storage, matplotlib for charts, and scikit-learn for the basic prediction models. All run in Google Colab.

## Repo structure

```
notebooks/      → all 6 notebooks, run in order (own README inside)
data/            → raw, cleaned, and integrated datasets + the SQLite db (own README inside)
charts/          → the 4 charts answering each research question (own README inside)
```

Note: the raw Kaggle flight CSV isn't in here because it's way too big for GitHub, download it directly from the [Kaggle link](https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023) above if you want to run this yourself.

## If you want to run this yourself

1. Download the Kaggle dataset and drop it in `data/raw/`
2. Open the notebooks in Google Colab in order, 01 → 06
3. No API key needed for the weather data — Open-Meteo is free and open
4. Each notebook saves what the next one needs, so don't skip around

---

If you spot something I got wrong or could improve, feel free to open an issue.
