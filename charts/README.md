# charts
Four charts, one per research question. All were generated in `notebooks/06_EDA_analysis.ipynb`.

## `chart1_RQ1_rainy_vs_clear.png`
Average departure delay on rainy days vs clear days. Rainy days come out about 51% worse, 18.5 minutes average vs 12.3 minutes.

## `chart2_RQ2_reporting_accuracy.png`
This is the one I'd show first if I only had time for one chart. Compares what the airlines' own data says caused a delay against what the weather was actually doing. Out of every flight that happened in genuinely bad weather, only 4% had the airline flag weather as the cause. The other 96% just got attributed to something else.

## `chart3_RQ3_delay_by_airport.png`
Average delay broken down by the 10 busiest airports. Orlando (MCO) is the worst offender, Seattle (SEA) is the best, somewhat ironic given Seattle's reputation for rain.

## `chart4_RQ4_model_comparison.png`
R² comparison between two basic regression models, one using the airline's reported weather flag, one using the actual API weather measurements, to see how well either one predicts delay length. Both score pretty low, which says more about how many other factors affect delays than it does about the models being bad.
