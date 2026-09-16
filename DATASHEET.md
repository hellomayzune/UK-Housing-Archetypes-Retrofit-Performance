<p align="left">
• <a href="https://github.com/hellomayzune"><strong>GitHub</strong></a> •
<a href="https://orcid.org/0000-0003-0282-2633"><strong>ORCID</strong></a> •
<a href="https://scholar.google.com/citations?user=LmP8B_4AAAAJ&hl=en"><strong>Google Scholar</strong></a> •
<a href="https://www.researchgate.net/profile/May-Zune"><strong>ResearchGate</strong></a> •
<a href="https://www.linkedin.com/in/mayzune/"><strong>Linkedin</strong></a> •
</p>

# 📋 Datasheet — UK Housing Archetypes Retrofit Performance

This datasheet describes the raw and processed data tables used in Jupyter notebooks to produce the results, figures, and tables presented in the manuscript:

- *Project Title*: Fabric retrofit of UK homes reduces heating demand but increases future overheating and ventilation risk
- *Notebook Author*: May Zune
- *Acknowledgement*: This work was supported by Research England through the South Yorkshire Sustainability Centre. D.D.T. and H.A. also acknowledge support from the Engineering and Physical Sciences Research Council (EPSRC) through the BuildZero research programme [EP/Y530578/1]. 
- *Project website*: [South Yorkshire Sustainability Centre](https://www.sysustainabilitycentre.org)

📬 Contact: If you have any questions, suggestions, or would like to discuss this work, please open an issue or contact from the links above.

🆚 Version: v1.x (under review)

©️ Licence: MIT Licence

>*🔗 This datasheet is structured according to Gebru, T., Morgenstern, J., Vecchione, B., Wortman Vaughan, J., Wallach, H., Daumé, H. and Crawford, K., 2021. Datasheets for datasets. Communications of the ACM, 64(12), pp.86–92.*

📖 This *Datasheet* describes the following contents.

- [Motivation](#-motivation)
- [Composition](#-composition)
- [Collection / Pre-processing](#-collection--pre-processing)
- [Analysis](#-analysis)
- [Uses](#️-uses)
- [Distribution and maintenance](#-distribution-and-maintenance)


## 📚 Methodological information and source database

Methodological information is available in:

> 📌 Under review. All notebooks and datasets will be made available.   
> 📄 Citation. TBD

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 🎯 Motivation

**For what purpose was the dataset created?**

This dataset evaluates the impacts of domestic retrofit measures—specifically those targeting space-heating reduction in UK dwellings—on future summer overheating, indoor carbon dioxide concentrations (as a proxy for ventilation adequacy), and associated cooling and ventilation energy demands. Incorporating current and projected (2030 and 2050) weather data for Sheffield, this dataset serves as the empirical foundation for all quantitative claims, tables, and figures presented in the associated manuscript.

**Who created the dataset and on whose behalf?**
May Zune, Hadi Arbabi and Danielle Densley Tingley, School of Mechanical, Aerospace and Civil Engineering, University of Sheffield.

**Who funded the creation of the dataset?**
Research England, through the South Yorkshire Sustainability Centre; the Engineering and Physical Sciences Research Council (EPSRC) through the BuildZero research programme (EP/Y530578/1).

**Any other comments?**
This dataset is entirely synthetic and deterministic, generated through simulation without incorporating empirical building measurements or human-subject records.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 🧩 Composition

**What do the instances that comprise the dataset represent?**
Each simulation instance represents a specific performance metric, either an hourly time series or an aggregated annual summary, generated via dynamic building-energy modelling. These values correspond to combinations of 14 housing archetypes, three retrofit scenarios (existing construction, system-only, fabric-only, and whole-house), two future climate projections (2030 A1B 50th percentile and 2050 A1FI 90th percentile), and, where applicable for visualization-ready tables, specific thermal zones (Bedroom 1, Bedroom 2, Bedroom 3/attic, and the living room).

**How many instances are there in total?**
The simulation matrix encompasses 14 building archetypes, evaluated across up to 4 rooms per archetype, 6 to 12 retrofit and shading scenarios, and 2 distinct weather years. Raw simulation outputs are generated at an hourly resolution—yielding 8,760 records per year for each unique combination of archetype, room, and scenario—while aggregated summary tables present a single record per combination for metrics such as TM59 Criteria a and b results, carbon dioxide indicators, and Energy Use Intensity (EUI) values.

**Does the dataset contain all possible instances or is it a sample?**
These fourteen archetypes represent built-form prototypes derived through a rule-based classification of UK Energy Performance Certificate (EPC) and Verisk GIS datasets, validated against South Yorkshire housing stock statistics and national architectural histories. Rather than serving as a prevalence-weighted statistical sample, the prototypes are structured to encompass the primary structural typologies—detached, semi-detached, terraced, and bungalow—and construction eras ranging from the pre-1919 period to post-2012, as reflected in both regional and national records. For each archetype, the modelled scenarios encompass all combinations of rooms and weather years detailed in the Methods section, ensuring exhaustive coverage without additional sub-sampling.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

**What data does each instance consist of?** The collected data comprises both primary simulation outputs and secondary derived metrics, structured by archetype, room, and operational scenario:

* Primary Simulation Outputs (EnergyPlus / DesignBuilder)
  * Hourly operative and dry-bulb air temperatures
  * Relative humidity (RH)
  * CO₂-relevant occupancy schedules

* Thermal Comfort and Overheating Metrics
  * TM59 Criteria (a) and (b) pass/fail statuses and associated exceedance metrics
  * Passivhaus and Heat Index secondary-benchmark exceedance metrics

* Indoor Air Quality (IAQ) Metrics
  * Single-zone mass-balance indoor CO₂ concentration time series
  * Summary statistics, including mean concentrations and the percentage of annual hours exceeding 900 ppm

* Energy Performance Metrics
  * Annual energy use intensity (EUI) in kWh/m²/a and absolute annual energy demand in kWh/a for heating, cooling, and ventilation
  * Net heating energy savings disaggregated by retrofit type

* Building Morphological and Geometric Indicators
  * Form Factor and Opening-to-Floor Area Ratio
  * Façade exposure and roof-to-floor ratio
  * Window-to-wall ratio (WWR) and glazing-to-floor ratio


**Is there a label or target associated with each instance?**
Because a single canonical label is not defined, several derived metrics function as outcome variables across the exploratory association analyses. Depending on the analytical framework, these dependent variables—such as heating EUI or combined cooling and ventilation EUI—are evaluated against morphological predictors using the Spearman correlation and OLS regression methods detailed in the Supplementary Information.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)


**Is any information missing from individual instances?**
Due to file size constraints, raw hourly simulation datasets (`T*.csv`, `RH*.csv`) are omitted from this repository. The provided materials comprise the computational notebooks—which both generate and consume these data—along with secondary processed and aggregated tables. A complete inventory of included and excluded assets is detailed in the accompanying README.

**Are relationships between individual instances made explicit?**
The filenames and configuration dictionaries (`SCENARIO_FILES`, `ARCHETYPES`, and `ROOMS`) explicitly embed metadata for the archetype, scenario, weather year, and room. This structured encoding enables data instances to be reliably tracked and joined across analytical stages—such as tracing raw temperature CSVs through TM59 criterion evaluations to final visualizations.

**Are there recommended data splits?**
Not applicable: As this study does not utilize a machine-learning training dataset, data partitioning (train/validation/test splits) is neither required nor applicable.

**Are there any errors, sources of noise, or redundancies in the dataset?**
Because the dataset is derived from deterministic simulations rather than empirical measurements, traditional experimental noise does not apply. Instead, output variability is driven by sensitivity to core modelling assumptions—such as occupancy schedules, behavioural controls (window-opening and shading), U-values, and air permeability (detailed in Tables 1–2 and the Limitations section). Additionally, sheet labels within the working data file (`energy-data.xlsx`) reflect preliminary nomenclature from the drafting phase. A corrected mapping between these internal labels and the final manuscript figure numbers is provided in the accompanying README.

**Is the dataset self-contained, or does it rely on external resources?**
The analytical notebooks incorporate external, third-party datasets that were not generated by the authors. These inputs comprise PROMETHEUS future weather files, specifically morphed Test Reference Year (TRY) and Design Summer Year (DSY) datasets for Sheffield corresponding to the 2030 and 2050 epochs. Additionally, supplementary comparisons utilise national domestic gas consumption figures published by the Office of Gas and Electricity Markets (Ofgem) alongside UK gas and electricity tariff data for 2025. While these sources are formally cited within the text, the raw data files are excluded from this repository due to redistribution restrictions.

**Does the dataset contain data that might be considered confidential?**
The methodology relies entirely on aggregated, public, and synthetic data sources, including simulated archetypal buildings, national Energy Performance Certificate (EPC) registries, GIS-derived floor-area statistics, and publicly accessible weather and tariff datasets. Consequently, no individual dwellings, specific postal addresses, or household occupants are featured or identifiable within the dataset.

**Does the dataset contain data that, if viewed directly, might be offensive, insulting, threatening, or might otherwise cause anxiety?** No.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 🔍 Collection / Pre-processing

**How was the data associated with each instance acquired?**
The dataset consists of simulated outputs rather than empirical measurements, generated via dynamic thermal simulation using the DesignBuilder v7.0.2 platform with the EnergyPlus v9.4 engine. Fourteen building archetype geometries were established by tracing representative architectural floor plans from local property listings. These archetypes were classified using a rule-based approach combining UK Energy Performance Certificate (EPC) data and Verisk GIS footprint data (detailed in Supplementary Information, "Archetype categorisation"). Fabric thermal transmittances (U-values) reflect UK Approved Document L requirements for retrofits and typical construction-era values for existing conditions. Furthermore, operational schedules, thermal set points, and ventilation provisions comply with CIBSE TM59, Approved Documents F and O, and BS EN 16798-1, as summarised in Tables 1 and 2 of the manuscript.

**What mechanisms or procedures were used to collect the data?**
Building performance simulations were conducted using EnergyPlus and DesignBuilder, configured in accordance with the aforementioned modelling assumptions. Post-processing and data analysis were performed within a Python and Jupyter Notebook environment. This workflow incorporated pandas-based data aggregation alongside custom implementations of the CIBSE TM52 and TM59 adaptive comfort frameworks, the NOAA Heat Index equation, and the NIST TN-2213 single-zone carbon dioxide mass-balance method.

**If the dataset is a sample from a larger set, what was the sampling strategy?**
The selection of archetypes does not constitute a statistical sample in the traditional probabilistic sense; instead, as established in the Composition section above, these archetypes function as representative built-form prototypes.

**Who was involved in the data collection process and how were they compensated?**
The named authors completed this work as part of their funded research roles under Research England and the Engineering and Physical Sciences Research Council (EPSRC) initiative, BuildZero. This study did not involve human subjects.

**Over what time frame was the data collected?**
Simulations utilised future weather years corresponding to the 2030 A1B scenario (50th percentile) and the 2050 A1FI scenario (90th percentile). All associated modelling and analysis were conducted during the primary research programme (see Acknowledgements for funding details).

**Were any ethical review processes conducted?**
This study utilised exclusively simulation-derived data. Consequently, protocols concerning human subjects, personal data acquisition, and field measurements were not applicable.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 📊 Analysis

**Was any preprocessing/cleaning/labelling of the data done?** The raw hourly simulation outputs were processed and aggregated into the following analytical categories:

  * **(i) Overheating Assessment:** TM59 Criterion (a) hours-of-exceedance percentages and Criterion (b) exceedance-night counts calculated per archetype, room, and scenario.
  * **(ii) Thermal Thresholds:** Annual exceedance-hour counts based on the Passivhaus (25 °C) and Heat Index (27 °C "Caution") criteria.
  * **(iii) Indoor Air Quality:** Single-zone mass-balance $CO_2$ concentration time series, yielding derived annual means and percentage-exceedance metrics.
  * **(iv) Energy Performance:** Annual and absolute heating, cooling, and ventilation energy demands, alongside overall Energy Use Intensity (EUI).
  * **(v) Morphological Indicators:** Geometric parameters computed directly from archetype configurations, including form factor, open-to-floor area ratio (OFAR), window-to-wall ratio (WWR), glazing-to-floor ratio (GFR), façade exposure, and roof-to-floor ratio.

**Was the "raw" data saved in addition to the preprocessed data?**
While raw hourly simulation CSV files are excluded from this repository (refer to the README section titled "Not included in this upload"), the repository provides the computational notebooks necessary to regenerate or consume them, alongside the final processed and aggregated outputs.

**Is the software used to preprocess/clean/label the data available?**
Yes — all preprocessing is performed in the Jupyter notebooks included in this repository (see README's Subdirectory guide for the full notebook-to-output mapping).

**What analyses were performed on the data, and what were the findings used for?** To evaluate the energy and environmental performance of the retrofits, the analytical framework employs the following methods:

  * **Thermal Comfort and Overheating Assessment:** Evaluation of overheating risk using CIBSE TM52 and TM59 adaptive-comfort criteria (Criteria a and b), supplemented by secondary benchmark screenings based on Passivhaus (25 °C) and Heat Index (27 °C) thresholds.
  * **Ventilation Adequacy Modelling:** Single-zone mass-balance indoor carbon dioxide ($\text{CO}_2$) concentration modelling utilised as a proxy for ventilation performance.
  * **Energy Demand and Intensity Quantification:** Calculation of annual heating, cooling, and ventilation energy use intensity (EUI) and demand under a temperature-controlled hybrid operation model.
  * **Morphological Statistical Analysis:** Exploratory, non-causal Spearman rank correlations and ordinary least squares (OLS) regressions examining the relationship between archetype morphological indicators and heating, cooling, and ventilation EUIs ($n = 14$). Given the small sample size, these models are treated strictly as associative rather than predictive, supported by 10,000-iteration permutation testing and leave-one-out robustness checks.
  * **Comparative Climate Analysis:** Cross-city evaluation of heating and cooling degree-hours alongside solar irradiance metrics across seven European Köppen-Cfb cities.


[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 🛠️ Uses

**Has the dataset been used for any tasks already?**
The aforementioned contribution was restricted solely to the generation of the results, figures, and tables presented in the manuscript.

**Is there a repository that links to any or all papers or systems that use the dataset?**
The same archetypes are used in the other studies: 
* > Zune, M., Arbabi, H., Densley Tingley, D. (Published 27 August 2026). Regional Retrofit, Net-Zero Aspirations, and their Whole Life Carbon Burden. Available at Environmental Research: Infrastructure and Sustainability, (2026);6(3):035015. doi: [10.1088/2634-4505/ae9984](https://iopscience.iop.org/article/10.1088/2634-4505/ae9984)
* > Zune, M. (Published 1 December 2025). Towards net-zero archetypes: The performance of system-only, fabric-only, staged and whole-house retrofit, Building Services Engineering Research & Technology (2025); 47(2): 195-225 doi: [10.1177/01436244251403042](https://doi.org/10.1177/01436244251403042)

**What (other) tasks could the dataset be used for?**
The processed datasets and computational notebooks offer a versatile resource for future research, methodological benchmarking, and education. Specifically, these outputs enable the replication and extension of the overheating and $\text{CO}_2$ risk screening methodology across alternative UK building archetypes and urban contexts. Furthermore, they support comparative analyses—such as testing alternative overheating criteria or $\text{CO}_2$ models against standardized simulation outputs—and provide practical pedagogical examples for teaching TM59, Heat Index, and mass-balance post-processing workflows.

**Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses?**
The dataset relies on deterministic modelling assumptions tailored to a single urban context (Sheffield) and incorporates standardized boundary conditions, including CIBSE TM59 occupant schedules and non-adaptive window-opening protocols. As noted in the study limitations, these outputs reflect typology-driven overheating risk rather than absolute national or regional forecasts. Consequently, the data should not be used to infer absolute performance metrics for specific real-world dwellings, occupants, or locations without prior validation against empirical, measured data.

**Are there tasks for which the dataset should not be used?**
The findings and models presented in this study should not be used to:
  1. **Make population-level claims:** The 14 archetypes function as representative prototypes rather than a statistically representative probability sample of the UK housing stock.
  2. **Represent empirical building performance:** All data are derived from computational simulation rather than real-world physical monitoring.
  3. **Establish regulatory compliance:** Frameworks such as CIBSE TM59, Passivhaus standards, and carbon dioxide benchmarks are applied strictly as comparative screening indicators rather than comprehensive indoor air quality or formal regulatory compliance tests.
  4. **Account for behavioural variance:** The reliance on fixed-schedule assumptions precludes drawing definitive conclusions regarding diverse real-world occupant behaviors.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)

---

# 📦 Distribution and maintenance

**Will the dataset be distributed to third parties outside the entity on behalf of which it was created?**
Yes — via a public GitHub repository linked from the manuscript's SSRN entry, made available under the MIT Licence.

**How will the dataset be distributed?**
GitHub repository (link/DOI to be added upon publication).

**When will the dataset be distributed?**
Upon publication of the associated manuscript.

**Will the dataset be distributed under a copyright or other IP licence, and/or under applicable terms of use?**
MIT Licence for the notebooks and processed data tables created by the authors. Third-party inputs referenced but not redistributed here (PROMETHEUS, Ofgem statistics)
remain subject to their original providers' terms — see in-text citations in the manuscript and Supplementary Information.

**Have any third parties imposed IP-based or other restrictions on the data associated with the instances?**
No restrictions are imposed on the authors' own simulation-derived data. External data sources used for comparison (Ofgem, PROMETHEUS/CIBSE) are cited but not redistributed, consistent with their respective terms.

**Do any export controls or other regulatory restrictions apply to the dataset or to individual instances?**
No.

**Who will be supporting/hosting/maintaining the dataset?**
The corresponding author (May Zune, University of Sheffield; m.zune@sheffield.ac.uk) will maintain the repository.

**Is there an erratum?**
Any corrections identified after publication will be documented via the GitHub repository's issue tracker/commit history.

**Will the dataset be updated?**
No.

**If the dataset relates to people, is there a retention limit?**
This study is exempt from ethical review and considerations regarding human subjects, as the dataset contains no personal or identifiable human data.

**Will older versions of the dataset continue to be supported/hosted/maintained?**
Versioning details will be finalised prior to publication and will follow standard GitHub release protocols if implemented.

**If others want to extend/augment/build on/contribute to the dataset, is there a mechanism for doing so?**
Post-publication contributions can be submitted via issues or pull requests on the project's GitHub repository. Given the study's noted limitations, particularly valuable areas for future development include:
  * Extending the existing archetype library.
  * Incorporating additional UK cities.
  * Validating simulated outputs against empirical measurement data.

[Back To The Top](#-datasheet--uk-housing-archetypes-retrofit-performance)
