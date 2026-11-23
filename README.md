# AquaSafe

AquaSafe studies whether three water measurements and preceding weather can help prioritize laboratory testing for E. coli at untreated drinking-water intakes. The study covers Alpes-Maritimes, France, from 2020 through 2025 and supports SDG 6.1.

## Files

| File | Contents |
| --- | --- |
| AquaSafe.ipynb | Executed notebook with data preparation, weather matching, exploratory analysis, model evaluation and interpretation. |
| data/sise_eaux_capture_observations.csv | Original French Ministry of Health SISE-Eaux measurements and sampling metadata for the study scope. Measurement identifiers and official archive URLs are included. |
| surname1_surname2_assignment2.pdf | One-page model results report. |

## Run the notebook

Open a terminal in the extracted project directory. Use Python 3.11 or later.

```bash
python -m pip install jupyterlab pandas==2.2.3 scikit-learn==1.8.0 matplotlib
python -m jupyterlab
```

Open **AquaSafe.ipynb** and run all cells. On first run, the notebook downloads official API Géo and Météo-France files over HTTPS. The downloaded files are cached in `.weather_cache/`. The notebook writes the aligned cohort to `outputs/water_weather.csv` and generates the descriptive tables, missingness audit, predictions, split and figures.

To extend the dataset, join the official **CAP_RES** and **CAP_PLV** extracts by `referenceprel` and place the resulting CSV with the same headers in `data/`. Preserve the original sample references, units, qualifiers, quality fields and municipality codes. The variables `START_YEAR` and `END_YEAR` set the time window. New eligible samples are matched to weather and included when the grouped split is computed.

## Data and evaluation

- The cohort has **989 samples**, including **497 E. coli detections** and **492 non-detects**. All three sensor variables are complete. pH is generally a field reading. Most conductivity and all turbidity measurements are laboratory readings. Turbidity is reported in NFU and conductivity in µS/cm at 25 °C. Source water is untreated groundwater or surface water intended for supply. The complete-case filter and laboratory rules are recorded in the notebook.
- WHO Table 7.10 specifies no detectable E. coli in 100 mL. TS 266 April 2005 Table 1 specifies 0 per 100 mL for Class 2 Type 2. The pH indicator uses the strict 6.5–9.5 interval in TS 266 Table 3. Reported turbidity and conductivity remain in their original NFU and 25 °C measurement definitions.
- Capture coordinates are withheld in the source archive. Official municipality reference centers provide the location approximation for Météo-France matching. All 989 complete events have eligible weather. Weather station IDs, source URLs, quality flags and aligned values are retained in the generated output.
- The test holds out 197 samples from 21 municipalities. The selected Random Forest flagged 66 of 99 detections and 10 of 98 non-detects. Its balanced accuracy was 0.782. A rule flagging every surface-water sample reached 0.777. Weather did not consistently improve results. Source-specific performance and the detection misses are reported in the notebook.

## Sources

- [French Ministry of Health SISE-Eaux surveillance](https://www.data.gouv.fr/datasets/resultats-du-controle-sanitaire-de-leau-du-robinet)
- [Météo-France daily measurements](https://www.data.gouv.fr/datasets/donnees-climatologiques-de-base-quotidiennes)
- [French government API Géo](https://www.data.gouv.fr/dataservices/api-decoupage-administratif-api-geo)
- [WHO Table 7.10](https://cdn.who.int/media/docs/default-source/wash-documents/water-safety-and-quality/dwq-guidelines-4/gdwq_4ed_with_third-addenda_microbial-aspects.pdf)
- [TS 266, April 2005](https://sandoramuhendislik.com/TS_266.pdf)
