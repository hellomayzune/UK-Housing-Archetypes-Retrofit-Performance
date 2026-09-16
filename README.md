<p align="left">
• <a href="https://github.com/hellomayzune"><strong>GitHub</strong></a> •
<a href="https://orcid.org/0000-0003-0282-2633"><strong>ORCID</strong></a> •
<a href="https://scholar.google.com/citations?user=LmP8B_4AAAAJ&hl=en"><strong>Google Scholar</strong></a> •
<a href="https://www.researchgate.net/profile/May-Zune"><strong>ResearchGate</strong></a> •
<a href="https://www.linkedin.com/in/mayzune/"><strong>Linkedin</strong></a> •
</p>

# 🏠 UK Housing Archetypes Retrofit Performance

This repository contains the Jupyter notebooks and processed data tables used to produce the results, figures, and tables presented in the manuscript:

- *Project Title*: Fabric retrofit of UK homes reduces heating demand but increases future overheating and ventilation risk
- *Notebook Author*: May Zune
- *Acknowledgement*: This work was supported by Research England through the South Yorkshire Sustainability Centre. D.D.T. and H.A. also acknowledge support from the Engineering and Physical Sciences Research Council (EPSRC) through the BuildZero research programme [EP/Y530578/1]. 
- *Project website*: [South Yorkshire Sustainability Centre](https://www.sysustainabilitycentre.org)

📬 Contact: If you have any questions, suggestions, or would like to discuss this work, please open an issue or contact from the links above.

🆚 Version: v1.x (under review)

©️ Licence: MIT Licence

📖 This *README* describes the following contents.

- [Methodological information and source database](#-methodological-information-and-source-database)
- [Repository information](#️-repository-information)
- [Methods](#️-methods)
    - [Subdirectory guide & executable notebooks](#️-subdirectory-guide--executable-notebooks)
    - [Software requirements & setup](#-software-requirements--setup)
    - [Reproducibility steps](#-reproducibility-steps)

---

# 📚 Methodological information and source database

Methodological information is available in:

> 📌 Under review. All notebooks and datasets will be made available.   
> 📄 Citation. TBD

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

---

# 🗂️ Repository information
- Contents: Jupyter notebooks (`.ipynb`) and processed data tables (`.xlsx`, `.csv`)
- Programming language: `Python` (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `openpyxl`)
- Simulation software (generates the raw inputs the notebooks consume): EnergyPlus v9.4, DesignBuilder v7.0.2
- README file date created: 16 September 2025
- README file date modified: *TBD*
- Licence: *MIT open source*
- 📌 Repository map:


```
├── data-analysis-archetype/     # Exploratory morphology–performance association analysis 
├── data-analysis-co2/           # Indoor CO2 analysis
├── data-analysis-heat-index/    # Indoor heat index driven overheating study
├── data-analysis-temperature/   # Indoor temperature driven overheating study
├── data-analysis-tre-cities/    # Multi-city comparative analysis scripts
├── streamlit-dashboard-sysc/    # Source code for the interactive Streamlit dashboard
├── README.md                    # Project overview and documentation
└── DATASHEET.md                 # Detailed data dictionary and metadata
```

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

# ⚙️ Methods

## 🗺️ Subdirectory guide & executable notebooks

### 📊 Housing archetype classification & morphology–performance analysis
*(Manuscript Methods; Supplementary Information — Archetype categorisation, Exploratory morphology–performance association analysis; Supplementary Figures 2–5, Supplementary Table 3)*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `typology-dependent-performance.ipynb` | Rule-based archetype classification (built form, footprint complexity, construction-age banding) | `archetype-info.xlsx` | Supplementary Figure 2, Supplementary Table 1–2 inputs |
| `exploratory-morphology-existing-heat-eui.ipynb` | Spearman ρ / OLS R² of Form Factor, OFAR, GFR, WWR, façade exposure vs **existing-building heating EUI** | `energy-data.xlsx` (`Fig5a`), `Supplementary_Table_Robustness_Check_Existing_Heating.xlsx` | Supplementary Figure 4(a), Supplementary Figure 5(a) |
| `exploratory-morphology-wh-heat-eui.ipynb` | Same association analysis for **whole-house retrofit heating EUI** | `Supplementary_Table_Robustness_Check_WH_Heating.xlsx` | Supplementary Figure 4(b), Supplementary Figure 5(b) |
| `exploratory-morphology-wh-coolvent-eui.ipynb` | Same association analysis for **whole-house retrofit cooling + ventilation EUI** | `Supplementary_Table_Robustness_Check_WH_CoolVent.xlsx` | Supplementary Figure 4(c), Supplementary Figure 5(c) |
| `exploratory-morphology-permutation.ipynb` | 10,000-iteration permutation test + leave-one-out robustness check on the correlations above | `Supplementary_Table_Robustness_Check.xlsx` | Supplementary Figure 5(d) permutation heatmap |

Morphological indicators (Form Factor, OFAR, façade exposure, roof-to-floor ratio, WWR, GFR) for all 14 archetypes are tabulated in `energy-data.xlsx` sheets `Table4` (envelope areas) and `Table5` (compactness/glazing ratios) — these correspond to **Supplementary Table 2** and **Supplementary Table 3** respectively.

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

### 📊 TM59 overheating assessment (Criterion a & b) and secondary benchmarks
*(Figures 3 and 4)*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `TM59-Criterion-a-b-2030-Template.ipynb` | Computes CIBSE TM52/TM59 Criterion (a) (3% hours-of-exceedance, adaptive comfort) and Criterion (b) (4-night sleeping-hours limit) from raw hourly operative-temperature output, **2030 weather year**. Template re-run once per weather scenario | `T2030Existing.csv`, `T2030RetrofitEXT.csv`, `T2030RetrofitINT.csv` (raw hourly sim output; one row per hour, columns per archetype/room) | `TM59_Criterion_a_2030*.csv`, `TM59_Criterion_b_2030*.csv` (one pair per scenario) |
| `TM59-Criterion-a-b-2050-Template.ipynb` | Same, **2050 weather year** | `T2050Existing.csv`, `T2050RetrofitEXT.csv`, `T2050RetrofitINT.csv` | `TM59_Criterion_a_2050*.csv`, `TM59_Criterion_b_2050*.csv` |
| `TM59-Secondary-Assessment.ipynb` | Secondary/supplementary overheating benchmarks: Passivhaus PHPP 25 °C annual-hours threshold and NOAA Heat Index 27 °C ("Caution") threshold, for 2030 and 2050 | Same 6 raw hourly CSVs as above (+ paired relative-humidity files for Heat Index) | `secondary-overheating-assessment-T*.csv` (6 files) |
| `TM59-Visualisation-Criterion-a.ipynb` | Combines and plots the 6 Criterion (a) result files | `TM59_Criterion_a_*.csv` (glob-loaded from `DATA_DIR`) | **Figure 3(a)** |
| `TM59-Visualisation-Criterion-B.ipynb` | Combines and plots the 6 Criterion (b) result files | `TM59_Criterion_b_*.csv` | **Figure 3(b)** |
| `TM59-Visualisation-Secondary.ipynb` | Plots Passivhaus/Heat Index secondary benchmark results (annual % and hours above threshold, by room × scenario) | `secondary-overheating-assessment-T*.csv` (6 files) | **Figure 4** (a, and related sub-panels) |

Scenario codes used throughout: `Existing` (existing construction / system-only retrofit), `RetrofitINT` (fabric retrofit + internal blind shading), `RetrofitEXT` (fabric retrofit + external shutter shading) — matching scenarios A/B/C in the manuscript figures.

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

### 📊 Heat Index and indoor air/heat-index temperature mapping
*(Figure 5(a)–(b))*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `heat-index-calculation.ipynb` | Computes NOAA Heat Index from paired hourly dry-bulb temperature and relative-humidity output | `T2030Existing.csv`/`T2050Existing.csv` (+ RetrofitINT/EXT equivalents), `RH2030Existing.csv`/`RH2050Existing.csv` (+ RetrofitINT/EXT equivalents) | Per-scenario hourly Heat Index series (feeds visualisation notebook and `TM59-Secondary-Assessment.ipynb`) |
| `heat-index-visualisation.ipynb` | Hourly air-temperature and Heat Index heat maps for the example end-terrace archetype (T-RE), Bedroom 1 and Bedroom 3 | Heat Index series above | **Figure 5(a)–(b)** |

### 📊 Indoor CO₂ concentration modelling
*(Figure 6; referenced in Methods — single-zone mass-balance model)*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `2030-co2-calc.ipynb` | Single-zone mass-balance CO₂ model (metabolic generation, room volume, air permeability, exposed envelope area, indoor–outdoor ΔT) per NIST TN-2213 method, **2030** | `2030Existing_FullOccupancy.xlsx`, `2030Existing_RespOccupancy.xlsx`, `2030RetroIntSHFullOccupancy.xlsx`, `2030RetroIntSHRespOccupancy.xlsx`, `2030RetroExtSHFullOccupancy.xlsx`, `2030RetroExtSHRespOccupancy.xlsx` | `2030CO2.xlsx` (hourly CO₂ concentration by archetype/room/scenario) |
| `2050-co2-calc.ipynb` | Same, **2050** | 2050 equivalents of the six occupancy workbooks above | `2050CO2.xlsx` |
| `co2-summary-metric.ipynb` | Annual mean CO₂ and % occupied hours exceeding the 900 ppm screening threshold, by archetype/room/scenario | `2030CO2.xlsx`, `2050CO2.xlsx` | `CO2_2030_Summary_Metrics.xlsx`, `CO2_2050_Summary_Metrics.xlsx` |
| `co2-2030-box-plots.ipynb` | Boxplots of annual hourly CO₂ distribution by room type across archetypes and scenarios | `2030CO2.xlsx` | **Figure 6(a)** (2030 panel) |
| `co2-plots-for-paper.ipynb` | Mean-CO₂ and %-exceedance dot plots by archetype, 2030 and 2050 | `CO2_2030_Summary_Metrics.xlsx`, `CO2_2050_Summary_Metrics.xlsx` | **Figure 6(b)–(c)** |

"Full occupancy" vs "Resp occupancy" workbooks correspond to the two occupancy/CO₂ generation-rate assumptions described in Table 2(a) of the manuscript (one occupant per bedroom, two in the living room).

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

### 📊 Energy demand, savings, cost and carbon
*(Figures 2, 7, 8; Supplementary Figures 6–8)*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `example-TRE-and-energy.ipynb` | Hourly indoor temperature heatmaps for the example T-RE archetype (upper-floor and attic bedrooms) and daily cooling+ventilation demand CDF comparisons (system-only vs whole-house retrofit) | `read-excel-TRE-and-cities.xlsx` | **Figure 5(c)**, **Figure 7(c)–(d)** |

`energy-data.xlsx` is a consolidated results workbook (no executable notebook — feeds plotting
notebooks/manual charting directly). Sheet-to-figure mapping (working label → manuscript
figure/table):

| Sheet | Content | Manuscript figure/table |
|---|---|---|
| `Fig2` | Treated floor area per archetype vs national/South Yorkshire average floor areas | **Figure 2** |
| `Fig7a` | Annual heating EUI (kWh/m²/a), existing archetypes, 2030 & 2050, with GFA | **Figure 7(a)** |
| `Fig7b` | Post-retrofit heating / cooling+ventilation EUI by archetype, 2030 & 2050 | **Figure 7(b)** |
| `Fig8a` | Post-retrofit heating & cooling+ventilation demand (kWh/year, absolute) | **Figure 8(a)** main panel |
| `Fig8ab` | Existing-scenario gas-boiler heating demand (kWh/year) | **Figure 8(a)** inset |
| `Fig8b` | Net annual heating energy savings (kWh) by retrofit type, 2030 | **Figure 8(b)** |
| `Fig8c` | Net annual heating energy savings (kWh) by retrofit type, 2050 | **Figure 8(c)** |
| `Fig8bc` | Mean heating-savings % and standard deviation, by retrofit type/year | **Figure 8(b)–(c)** inset boxes |
| `STable2` | External wall/party wall/ground/roof/window/door areas, treated floor area | **Supplementary Table 2** |
| `STable3` | Form Factor, OFAR, façade exposure, roof-to-floor ratio, WWR, GFR | **Supplementary Table 3** |
| n/a | See Zune (2025) study | **Supplementary Table 6-8** |


### 📊 Cross-city climate comparison
*(Figure 9)*

| Notebook | Purpose | Key inputs | Produces |
|---|---|---|---|
| `compare-cities.ipynb` | Heating/cooling degree-hours (CDH 22 °C / HDH 16 °C) and summer GHI/RSI/peak-GHI comparison across 7 European Köppen-Cfb cities (Amsterdam, Brussels, Copenhagen, Dublin, London, Paris, Sheffield) under SSP2-4.5 (2050) and SSP5-8.5 (2080) | `read-excel-TRE-and-cities.xlsx` (sheets `T_SSP245_2050`, `T_SSP585_2080` — 8,760 hourly rows × one column per city) | **Figure 9(a)–(b)** |


[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

---

## 💻 Software requirements & setup

**Building-energy simulation** (generates the raw hourly CSVs consumed by the notebooks above —
not reproducible from this repository alone):
- EnergyPlus v9.4
- DesignBuilder v7.0.2
- Future weather files: PROMETHEUS/CIBSE 2030 (A1B, 50th percentile) and 2050 (A1FI, 90th
  percentile) probabilistic morphed weather sets for Sheffield, UK

**Notebook environment:**
- Python ≥ 3.9, Jupyter Notebook or JupyterLab
- Core packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `openpyxl` (for `.xlsx` read/write)
- Additional packages used in specific notebooks: `scipy` (Spearman correlation, permutation testing in the archetype classification & morphology–performance section), `re`/`glob`/`pathlib`(standard library; used for scenario-file discovery in the TM59 visualisation notebooks)
- Suggested environment setup: If you use **Anaconda** or **Miniconda**, you can set up the environment and install the required dependencies using the following commands in your terminal (or Anaconda Prompt):

```bash
# 1. Create a new conda environment (Python 3.10+ recommended)
conda create -n retrofit-env python=3.10

# 2. Activate the environment
conda activate retrofit-env

# 3. Install required packages (via conda-forge)
conda install -c conda-forge pandas numpy matplotlib seaborn openpyxl scipy jupyter streamlit
```

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

---

## 🔁 Reproducibility steps

Raw hourly simulation output (`T*.csv`, `RH*.csv` — one file per archetype × scenario ×
weather-year combination) must be generated first via EnergyPlus/DesignBuilder following the
model assumptions in Tables 1–2 of the manuscript, then placed alongside the relevant notebooks
(or with `CSV_PATH`/`DATA_DIR` edited to point at their location).

Recommended run order:

1. **Archetype classification** — `typology-dependent-performance.ipynb`
2. **TM59 overheating (per weather year)** — `TM59-Criterion-a-b-2030-Template.ipynb` and
   `TM59-Criterion-a-b-2050-Template.ipynb` (re-run once per scenario, editing `CSV_PATH`),
   then `TM59-Secondary-Assessment.ipynb`
3. **Heat Index** — `heat-index-calculation.ipynb`, then `heat-index-visualisation.ipynb`
4. **TM59 visualisation** — `TM59-Visualisation-Criterion-a.ipynb`,
   `TM59-Visualisation-Criterion-B.ipynb`, `TM59-Visualisation-Secondary.ipynb` (each expects
   its six scenario CSVs to already exist in `DATA_DIR`)
5. **CO₂ modelling** — `2030-co2-calc.ipynb` and `2050-co2-calc.ipynb`, then
   `co2-summary-metric.ipynb`, then `co2-2030-box-plots.ipynb` and `co2-plots-for-paper.ipynb`
6. **Morphology–performance association** — `exploratory-morphology-existing-heat-eui.ipynb`,
   `exploratory-morphology-wh-heat-eui.ipynb`, `exploratory-morphology-wh-coolvent-eui.ipynb`,
   then `exploratory-morphology-permutation.ipynb` for the robustness/permutation check
7. **Energy, cost and cross-city comparison** — `example-TRE-and-energy.ipynb`,
   `compare-cities.ipynb` (both require `read-excel-TRE-and-cities.xlsx`)

Each notebook is self-contained given its listed inputs; there is no single top-level "run all"
script, as notebooks were developed and run per figure/table during analysis.

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)

---

### What are not included

Due to file size constraints, raw hourly simulation outputs (EnergyPlus/DesignBuilder CSVs, $\sim 8,760$ rows each per archetype, scenario, and weather year) are not included in this repository.

**Included in this Repository**

* **Analysis & Processing Notebooks:** Jupyter notebooks used to generate, process, and visualize the simulation outputs.
* **Aggregated Data:** Smaller processed data tables (Excel workbooks and summary CSVs) required directly by the plotting notebooks.

**Regenerating Raw Data**

If you need the raw simulation outputs, they can be regenerated from the original building-energy models outlined in the manuscript's **Methods** section. Expected file structures and naming conventions are documented directly within the notebooks.

[Back To The Top](#-uk-housing-archetypes-retrofit-performance)
