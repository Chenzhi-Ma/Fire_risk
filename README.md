# From Occurrence to Consequence: Unraveling Urban Building Fire Risk

Chenzhi Ma, Shengzhi Luan, Ensheng Dong, Lauren Gardner, Hongru Du\*, Thomas Gernay\*

\* *Corresponding Authors*

Building fires remain a critical public safety concern, threatening lives, property, and infrastructure within cities globally. Despite substantial investments in fire safety, significant disparities in fire risk persist in urban landscapes across the U.S., underscoring the need for a holistic, data-driven strategy to reduce vulnerabilities. Here, we present an extensive analysis of U.S. building fires, integrating over one million fire incident reports with a novel synthesis of community-level data, encompassing socioeconomic indicators, building inventories, weather conditions, and incident-specific fire characteristics. Our work yields two pivotal contributions: a comprehensive framework that systematically traces fire risk from occurrence to consequence, and a novel city-level fire risk ranking system for U.S. cities. By systematically tracing fire occurrence and its consequences, we uncover structural, environmental, and social drivers that disproportionately endanger urban communities with older infrastructure and economic disadvantages. Our findings reveal that community-level factors, including outdated buildings and socioeconomic disparities, magnify both the frequency and severity of fire incidents. Incident-specific features, such as ignition sources and locations, further shape fire spread and injury outcomes, with buildings equipped with detectors and automatic extinguishing systems showing markedly lower risks. Lower-risk cities, where the fire incident rate can be as low as 1/3 of that of high-risk cities, tend to exhibit more favorable socioeconomic conditions and a higher prevalence of buildings equipped with fire safety measures compared to high-risk cities.

# Repository Overview

## Data
* `cbsa_fire_rate_summary.txt`: Post-processed dataset containing the calculated fire rates for all considered CBSA cities based on the NFIRS fire data.  
* `df_all_events_with_outcome.rar`: Compressed archive containing a `.pkl` DataFrame with detailed records for all considered fire events, including event ID, location, and associated consequences.  
* `inj_specific.pkl`: DataFrame with detailed records of fire events involving injuries. Includes event ID, injury severity, sex, age, and other related attributes.  
* `list1_2023.xlsx`: List of CBSA cities with corresponding CBSA codes, names, and additional city-specific details.  
* `zip_cbsa_122022.xlsx`: Mapping table between ZIP codes and CBSA cities.  
* `raw_data_with_city_info.pkl`: DataFrame containing CBSA and region details for each fire event.  
* `step2_consequence_fire_spread.pkl`: DataFrame of valid fire events used for fire spread risk analysis. Includes socio-economic, demographic, and incident-specific features. Events missing key features have been removed.  
* `step2_consequence_injury_severity.pkl`: DataFrame of fire events used for human injury risk analysis. Includes socio-economic, demographic, and incident-specific features. Events without injuries or with missing key features have been removed.  
* `step2_consequence_loss.pkl`: DataFrame of valid fire events used for economic loss risk analysis. Includes socio-economic, demographic, and incident-specific features. Events with zero economic loss or missing key features have been removed.  
## Code
* `fire_indexes.ipynb`: Code for generating the city-level fire risk index.
* `step1_occurrence_cbsa.ipynb`: Code for fire occurrence risk analysis by fitting multiple GAMs to examine risk from multiple perspectives, including overall risk, regional variation, and seasonal patterns.
* `step2_ceosequence_injury_severity.ipynb`: Code the FireCat framework for predicting injury severity resulting from fire incidents.
* `step2_consequence_fire_spread.ipynb`: Code the FireCat framework for predicting fire spreading risk.
* `step2_consequence_loss.ipynb`: Code the FireCat framework for predicting economic loss resulting from fire incidents.
