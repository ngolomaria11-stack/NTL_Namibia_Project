<p align="right"><a href="methodology.fr.md">Français</a></p>

# Methodology — Namibia (2014–2025)

## Data and cleaning

VIIRS DNB monthly (VCMSLCFG) and annual VNL V2, harmonised DMSP–VIIRS, daily Black Marble, GHSL/WorldPop, Sentinel-5P NO₂/SO₂, MODIS LST, World Bank. Cleaning: pixels valid if cf_cvg ≥ 2, unit-month kept if ≥ 80% of pixels observed, spikes replaced, background and gas flares masked.

## 📈 Use case 1 — Time dynamics

- **Question** — Is activity accelerating or slowing down, net of seasonality?
- **Data** — VIIRS VCMSLCFG (monthly), VIIRS VNL V2 (annual), Harmonised DMSP–VIIRS (Li et al., 2020)
- **Method** — Robust STL (period 12) on log(sum of lights); Theil–Sen slope and Mann–Kendall test on annual composites; anomaly and break detection.
- **Validation** — Trend significance (Mann–Kendall) and monthly/annual consistency (**p-value = < 0.0001**)
- **Uncertainty** — 95% CI of annual growth: +4.1% to +6.4%
- **Limits** — Cloud cover and short summer nights; light is not value added.
- **Status** — `experimental` · Confidence: high
- **References** — Cleveland et al. (1990) STL; Sen (1968); Elvidge et al. (2017).
- **Dashboard page** — [`#time`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#time)

**Results of this run**

- `F02` Between 2014 and 2025, night-time light in Namibia changed by +5.6% per year (95% CI: +4.1% to +6.4%). Over the last 12 months, the seasonally adjusted level is -1.6% relative to the previous 12 months. (confidence high: significant trend (p < 0.01; n = 12))
- `F70` Validation: Trend significance (Mann–Kendall) and monthly/annual consistency (p-value = < 0.0001). Uncertainty: 95% CI of annual growth: +4.1% to +6.4% Limitations: Cloud cover and short summer nights; light is not value added. Status: experimental statistic; confidence high.

## 🗺️ Use case 2 — Regional growth and convergence

- **Question** — Which regions take off, which fall behind?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, Sentinel-5P NO₂
- **Method** — Robust growth per unit (Theil–Sen, Mann–Kendall), growth/stagnation/decline classes, β- and σ-convergence, Herfindahl index.
- **Validation** — Rank correlation with tropospheric NO₂ (independent source) (**Spearman ρ = -0.21**)
- **Uncertainty** — Class assigned only if |slope| ≥ threshold and p < α; CI of β (robust errors).
- **Limits** — Small units: noise and light blooming between neighbours.
- **Status** — `experimental` · Confidence: medium
- **References** — Barro & Sala-i-Martin (1992) convergence; Henderson, Storeygard & Weil (2012).
- **Dashboard page** — [`#regions`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#regions)

**Results of this run**

- `F03` Of 103 ADM2 units, 87 show significant growth, 16 are stagnating and 0 are declining. Light remains concentrated: Erongo accounts for 17% of national light. (confidence medium: classification of 103 units, threshold ±1%/yr and p < 0.10)
- `F04` Across ADM2 units, light per capita converges: the least-lit units are catching up. (confidence medium: β = −0.033 [−0.045; −0.020], n = 103)
- `F24` Erongo (ADM1, 2025): share of national light 16.7%, annual growth +7.4% (CI +4.8% to +9.8%, class Growth), light per capita 0.892, population 0.01 M, in the dark 37%, estimated GDP (experimental) 2.07 bn USD.
- `F25` Khomas (ADM1, 2025): share of national light 16.4%, annual growth +2.3% (CI +1.4% to +3.0%, class Growth), light per capita 0.442, population 0.02 M, in the dark 23%, estimated GDP (experimental) 2.04 bn USD.

## 💹 Use case 3 — Light–GDP relationship

- **Question** — Can growth be estimated before its release, and regional GDP?
- **Data** — VIIRS, Real GDP (World Bank, WDI)
- **Method** — log(light) ~ log(GDP) in levels and growth, OLS with HAC errors; out-of-sample nowcast; regional GDP = national GDP allocated pro rata of light.
- **Validation** — Out-of-sample tracking of official growth (**correlation / MAE (pp) = -0.55 / 3.6**)
- **Uncertainty** — 95% CI of the elasticity: -0.48 to 4.17; 80% and 95% prediction intervals.
- **Limits** — Short annual sample; regional GDP is an experimental statistic to be checked against regional accounts.
- **Status** — `experimental` · Confidence: low
- **References** — Henderson et al. (2012) AER; Chen & Nordhaus (2011) PNAS; Gibson et al. (2021) JDE.
- **Dashboard page** — [`#time`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#time)

**Results of this run**

- `F05` The elasticity of light with respect to real GDP is 1.85 in levels (95% CI: −0.48 to 4.17, R² = 0.22, 12 years) and −0.24 in growth rates (CI: −0.82 to 0.33). Out of sample, light growth tracks GDP growth with a correlation of −0.55 (mean absolute error: 3.6 percentage points of growth). (confidence low: n = 12, not significant (p = 0.12))
- `F40` Light–real GDP elasticity in levels: β = 1.85 (95% CI -0.48 to 4.17, R² = 0.22, n = 12, confidence low: n = 12, not significant (p = 0.12)). +1% GDP ↔ +β% light.
- `F41` Light–real GDP elasticity in growth rates: β = -0.24 (95% CI -0.82 to 0.33, R² = 0.03, n = 11, confidence low: n = 11, not significant (p = 0.41)). +1% GDP ↔ +β% light.
- `F42` Light–real GDP elasticity in long DMSP–VIIRS series: β = 0.85 (95% CI 0.59 to 1.10, R² = 0.92, n = 30, confidence high: n = 30, p < 0.01, narrow CI). +1% GDP ↔ +β% light.

## ⚡ Use case 4 — Shocks and resilience

- **Question** — How deep was a shock, and how fast the recovery?
- **Data** — VIIRS (monthly), Black Marble VNP46A2 (daily), event catalogue
- **Method** — Gap to the pre-shock level on the seasonally adjusted series; structural breaks; daily Black Marble index.
- **Validation** — Does the trough exceed ordinary variability? (**trough (main shock) = -2.9% — no**)
- **Uncertainty** — Pre-shock month-to-month variability (robust SD); unexplained breaks flagged.
- **Limits** — Shocks hitting poorly lit activities (agriculture, daytime services) are underestimated.
- **Status** — `experimental` · Confidence: low
- **References** — Román et al. (2018); Elvidge et al. (2020) COVID-19 lockdown lights.
- **Dashboard page** — [`#shocks`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#shocks)

**Results of this run**

- `F06` The most pronounced shock in the seasonally adjusted series is “COVID-19”: trough of -2.9% (03/2021), return to the pre-shock level after 13 months. (confidence low: trough compared with pre-shock month-to-month variability)
- `F44` COVID-19 (2020-03-01 → 2021-06-30): trough of -2.9% on 2021-03-01, back to the pre-shock level after 13 months. Distinguishable from noise: no.
- `F45` Structural breaks: 2017-01-01 (13.4 %); 2023-02-01 (11.6 %). Without a known event within ±6 months: 2.
- `F46` Hardest-hit regions (trough): Hardap -30.0 % (covid19), Khomas -26.6 % (covid19), Omaheke -22.7 % (covid19), Erongo -16.9 % (covid19), Otjozondjupa -15.0 % (covid19).

## ⚖️ Use case 5 — Inequality and electrification

- **Question** — Where do people without electricity live?
- **Data** — VIIRS VNL V2, GHSL / WorldPop, GHSL SMOD, electricity access (WDI)
- **Method** — Population-weighted Gini and Theil; population of inhabited pixels below the detection threshold; sensitivity to three thresholds; bootstrap CI of the Gini change.
- **Validation** — Gap with the World Bank electricity-access rate (**mean gap (pp) = 28.9**)
- **Uncertainty** — Range across radiance thresholds; bootstrap CI of the Gini.
- **Limits** — Proxy of outdoor lighting, not of connection: a connected but dimly lit household looks “in the dark”.
- **Status** — `experimental` · Confidence: medium
- **References** — Theil (1967); Falchetta et al. (2020) electricity access from lights.
- **Dashboard page** — [`#inequality`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#inequality)

**Results of this run**

- `F07` The Gini coefficient of light per capita (ADM2) is 0.44 in 2025 (significant decrease since 2014). About 0.01 million people live in inhabited areas with no detectable light (17% of the inhabited population). (confidence medium: sensitive to the radiance threshold (from 0.01 to 0.01 M depending on the threshold); a proxy for outdoor lighting, not for grid connection)
- `F47` Gini of light per capita (ADM2): 0.533 in 2014 → 0.442 in 2025 (change -0.091, bootstrap CI -0.142 to -0.049). Theil T 0.332; between-region share 33%.
- `F48` People in inhabited areas without detectable light: 0.01 M (19%) in 2014 → 0.01 M (17%) in 2025. Urban/rural light-per-capita ratio 0.7. Proxy of electricity access, sensitive to the threshold.
- `F49` Average gap between the share of people in lit areas and the World Bank electricity-access rate: 28.9 points.

## 🏭 Use case 6 — Industrial zones

- **Question** — Where is industry, and is its activity growing?
- **Data** — VIIRS VNL V2, GHSL BUILT-S, Sentinel-5P NO₂/SO₂, MODIS MOD11A2, OpenStreetMap
- **Method** — Concordance of six signals per pixel (≥ 3 including light), 8-connected clusters, typology and confidence.
- **Validation** — Comparison with the reference list (OpenStreetMap) (**precision / recall / F1 = 51% / 14% / 0.22**)
- **Uncertainty** — Per-cluster confidence from the number of strong signals; isolated sites to verify.
- **Limits** — Sentinel-5P (≈ 5 km) and MODIS (1 km) resolution: signals describe a neighbourhood.
- **Status** — `experimental` · Confidence: low
- **References** — Elvidge et al. (2016) gas flares; Pesaresi et al. (2023) GHSL.
- **Dashboard page** — [`#industry`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#industry)

**Results of this run**

- `F08` 45 industrial clusters detected from concordant satellite signals: 10 heavy industry, 10 business parks & logistics, 8 oil & gas sites and 17 isolated sites to verify. They emit 17.8% of national light (latest year); their light changes by +2.0% per year. Oshana has the most industrial activity. (confidence low: precision 51% and recall 14% against the reference list)
- `F50` 45 industrial clusters (≥ 3 of 6 signals): Isolated site to verify 17, Heavy industry 10, Business park & logistics 10, Oil, gas & flares 8. Share of national light: 17.8%; annual growth +2.0%. Validation (OpenStreetMap): precision 51%, recall 14%.
- `F51` IND-001 — Isolated site to verify in Otjinene (Oshana) (55.04 km², 3 signals, confidence low); IND-002 — Isolated site to verify in Onesi (Oshana) (27.09 km², 3 signals, confidence low); IND-003 — Heavy industry in Rundu Urban (Kavango) (23.435 km², 4 signals, confidence medium); IND-008 — Oil, gas & flares in Opuwo (Erongo) (6.235 km², 3 signals, confidence low); IND-004 — Heavy industry in Karibib (Karas) (16.34 km², 3 signals, confidence low); IND-007 — Oil, gas & flares in Walvisbay Urban (Khomas) (7.095 km², 3 signals, confidence low); IND-012 — Oil, gas & flares in Windhoek West (Khomas) (3.01 km², 3 signals, confidence low); IND-005 — Isolated site to verify in Katima Muliro Urban (Caprivi) (11.395 km², 3 signals, confidence low); IND-006 — Isolated site to verify in Okatana (Ohangwena) (7.955 km², 3 signals, confidence low); IND-035 — Oil, gas & flares in Windhoek Rural (Khomas) (0.86 km², 3 signals, confidence low)
- `F52` Oshana: 3 industrial cluster(s), 83.8 km², 68.3% of the region's light.

## 🏖️ Use case 7 — Seasonal tourism

- **Question** — Which areas live from tourism, and how does the season evolve?
- **Data** — VIIRS (monthly), hotel nights or WDI arrivals
- **Method** — Summer excess net of comparable units at the same latitude; one-sided test; season index base 100; seasons overlapping Ramadan flagged.
- **Validation** — Correlation with international tourist arrivals (WDI) (**r = -0.13**)
- **Uncertainty** — p-value per unit; 2020–2021 excluded from the classification.
- **Limits** — Any summer activity (diaspora, second homes, festivals) is captured, not only tourism.
- **Status** — `experimental` · Confidence: low
- **References** — Seasonal light analyses of tourism, e.g. Hu et al. (2021).
- **Dashboard page** — [`#tourism`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#tourism)

**Results of this run**

- `F09` 4 of 103 units show a net summer light excess of at least 10%: Otavi (Oshana), Ongenga (Ohangwena), Aminius (Ohangwena), Tsumkwe (Kunene). The median net excess reaches +17% in the most touristic zone. The season index (base 100 = 2019) falls to 309 in 2020 and stands at 266 in 2025. (confidence low: correlation of -0.13 with international tourist arrivals (WDI) (7 years))
- `F62` 4 tourist zone(s) out of 103 ADM2 units (net summer excess ≥ 10%, peak months [12, 1]): Otavi (Oshana) (+17%, confidence medium), Ongenga (Ohangwena) (+11%, confidence high), Aminius (Ohangwena) (+11%, confidence medium), Tsumkwe (Kunene) (+10%, confidence medium).
- `F63` Season index (base 100 = 2019): 2014: 263, 2015: 200, 2016: 204, 2017: 544, 2018: 277, 2019: 100, 2020: 309, 2021: -65, 2022: 257, 2023: 480, 2024: -159, 2025: 266. Years when Ramadan overlaps the season: 2021, 2022, 2023, 2024, 2025.
- `F64` Correlation between the season index and international tourist arrivals (WDI): -0.13 (7 years; in growth rates: -0.62).

## 🏙️ Use case 8 — Urbanisation signals

- **Question** — Where do cities spread, where do villages get electrified, and where does population grow without light?
- **Data** — VIIRS VNL V2, GHSL GHS-POP / WorldPop, GHSL GHS-BUILT-S R2023A, urban population (WDI)
- **Method** — Lit area (pixels above the threshold) and population per unit; Theil–Sen growth rates; newly lit pixels (dark two years in a row at the start, lit two years in a row at the end), split between electrification of inhabited areas and new settlements; light/population typology.
- **Validation** — Rank correlation with GHSL built-up area growth (independent source) (**Spearman ρ = 0.71**)
- **Uncertainty** — Persistence required over two years to limit noise; ± 1 pp margin between growth rates before classifying.
- **Limits** — Light measures outdoor lighting, not urbanisation in the administrative sense; blooming widens cities; GHSL population is interpolated between epochs.
- **Status** — `experimental` · Confidence: high
- **References** — Zhou et al. (2015) urban extent from lights; Pesaresi et al. (2023) GHSL; Min et al. (2013) village electrification.
- **Dashboard page** — [`#urban`](https://ngolomaria11-stack.github.io/NTL_Namibia_Project/?country=NAM#urban)

**Results of this run**

- `F65` National lit area: +11.0% per year; population: +1.7% per year. Classes (ADM2): Electrified urbanisation 86, Balanced growth 7, Unlit growth 7, Stable or declining 3.
- `F66` Between 2014 and 2025: 2,678 km² newly lit, of which 30 km² already inhabited (electrification, ≈ 1k people) and 2,648 km² of new settlements; 71 km² lost their light.
- `F67` Fastest lit-area expansion: Outapi (Oshana) (+39.2%/yr), Oshikuku (Oshana) (+35.9%/yr), Kalahari (Ohangwena) (+33.9%/yr), Okongo (Omusati) (+32.7%/yr), Okalongo (Oshana) (+31.0%/yr), Epembe (Omusati) (+30.4%/yr). Unlit growth (population faster than light): Mariental Rural (Karas), Windhoek East (Khomas), Epupa (Khomas), Khorixas (Khomas), Opuwo (Erongo), Eenhana (Khomas), Okakarara (Khomas).
- `F68` Spearman rank correlation between lit-area growth and GHSL built-up growth: 0.71 (p = 0.000, 103 units).

## General limits of night-time lights

- **What lights measure** — Upward radiance emitted around 01:30: agriculture, daytime trade, poorly lit services and the rural informal economy are poorly captured.
- **Saturation and blooming** — DMSP saturates in city centres (DN 63) and “blooms” beyond lit areas; VIIRS is much better, but blooming still inflates the lit area of cities.
- **Gas flares and isolated sites** — The automatic mask may remove isolated mines, ports or power plants, and miss small flares; candidates are exported for verification.
- **Clouds, seasons, moon** — Cloudy months are only partially observed; STL removes average seasonality but not an abnormal season (snow, late monsoon).
- **Product breaks** — DMSP and VIIRS are not directly comparable: the harmonised long series (Li et al., 2020) is a modelled product, to be read for trends only.
- **NTL–GDP elasticity** — Estimated on 10 to 30 annual observations: wide intervals, possible instability, a non-causal relationship that varies with the level of development.
- **Access to electricity** — “Inhabited without light” ≠ “not connected”: a connected household with low consumption is invisible; the indicator depends strongly on the radiance threshold and the population data.
- **Administrative boundaries** — geoBoundaries/GAUL may differ from official boundaries; small ADM2 units are sensitive to light spilling over from neighbouring units.
- **Industrial zones** — Detection relies on thresholds: a power plant, a port or a large shopping centre can meet the signals; a dimly lit factory without visible emissions is missed. Sentinel-5P (≈ 5 km) and MODIS (1 km) are coarser than VIIRS: NO₂/SO₂/heat signals describe a neighbourhood, not a building.
- **Summer tourism** — The summer excess captures any rise in summer light (second homes, diaspora visits, festivals, construction), not only tourism; at high latitudes, very short summer nights reduce VIIRS observations. Ramadan changes night-time activity: the summers concerned are flagged.
- **Urbanisation** — The lit area depends on the detection threshold and on light blooming around cities; a connected but dimly lit neighbourhood stays invisible. Population (GHSL/WorldPop) is modelled from censuses: its growth is not an independent observation, and years between two epochs are interpolated.


---
<sub>Generated by the notebook on 2026-10-30 · version 2.1.0</sub>
