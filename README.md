#  Geothermal District Energy Assessment
### ThermoGIS Datathon | Utrecht Science Park
The Geothermal_Thermo_GIS notebook is the main notebook for challenge 1, open with Git Dev if file is too big after clicking on the notebook

## Overview
This project presents a full-stack geothermal resource assessment for the **Utrecht Science Park (USP)**, Netherlands — a high-density institutional campus hosting universities, academic medical centres, and research facilities with a year-round demand for district heating and cooling.

The analysis spans two linked engineering challenges: evaluating whether the geothermal resource base is sufficient to support the district, and designing an integrated system to deliver that energy reliably.


## Business Challenges
**Challenge 1 — Resource Assessment**
 *Assess the geothermal potential of the area using the provided well data and determine whether the geothermal resources can support district heating and cooling.*

**Challenge 2 — System Design**
*Design an integrated heating and cooling system capable of supplying the neighbourhood demand of 15 MW using geothermal energy.*

## Dataset

| Attribute | Detail |
|-----------|--------|
| Source | ThermoGIS (Dutch national geothermal database) |
| Wells | 6 (BLT-01, ZST-01, ODK-01, JUT-01, PKP-01, EVD-01) |
| Observations | 18 |
| Features | 16 reservoir parameters |
| Target Reservoir | Rotliegend sandstone — Slochteren Formation (1,700–2,600 m depth) |
| Temperature Range | 72°C – 88°C (low-enthalpy system) |

## Methodology

Well Data (ThermoGIS)
       │
       ▼
Data Cleaning & EDA ──► Correlation Analysis, Statistical Summary
       │
       ▼
Reservoir Characterisation ──► Temperature · Flow Rate · Permeability · Power (MW)
       │
       ▼
Spatial GIS Analysis ──► Well Locations · Temperature Hotspots · Power Distribution Maps
       │
       ▼
Multi-Criteria Well Scoring ──► Composite Reservoir Quality Index (Min-Max Normalised)
       │
       ▼
Probabilistic Scenario Analysis ──► P10 (Optimistic) · P50 (Base Case) · P90 (Conservative)
       │
       ▼
Heat Pump Integration ──► COP = 4 · HP Thermal Output · Coverage % · Surplus MW
       │
       ▼
System Design (ASPEN Plus ) ─

## Key Results
### Challenge 1 — Geothermal Potential

Three wells — **BLT-01, ZST-01, and ODK-01** — were selected as primary development targets after screening all six candidates across power output, flow rate, permeability, recoverable heat, and economic potential.

| Well | Flow Rate | Power Output | Economic Potential | Decision |
|------|-----------|-------------|-------------------|----------|
| BLT-01 | Excellent (469 m³/h) | ~23 MW | High | Selected |
| ZST-01 | Excellent (420 m³/h) | ~17 MW | High | Selected |
| ODK-01 | Excellent (390 m³/h) | ~15 MW | High | Selected |
| JUT-01 | Moderate (180 m³/h) | ~2 MW | Poor |  Reserve |
| PKP-01 | Poor (30 m³/h) | <1 MW | Poor |  Excluded |
| EVD-01 | Poor (45 m³/h) | <1 MW | Poor |  Excluded |

### Challenge 2 — Heat Pump Integration (COP = 4)

Raw P50 geothermal output (13.2 MW) falls marginally below the 15 MW target, requiring heat pump amplification.

| Scenario | Raw Output | HP Output (COP=4) | Demand Coverage | Meets 15 MW? |
|----------|-----------|-------------------|----------------|--------------|
| P10 (Optimistic) | 63.0 MW | 252.0 MW | 1,680% | Yes |
| P50 (Base Case) | 13.2 MW | 52.8 MW | 352% |  Yes |
| P90 (Conservative) | 0.6 MW | 2.4 MW | 16% |  No — backup required |

**Planning basis: P50.** The system delivers **52.8 MW** — covering **352% of the 15 MW district demand** with 37.8 MW surplus for future network expansion.


## System Design — 8 Stages (ASPEN Plus)

The integrated plant was modelled end-to-end across 8 unit operation stages:

| Stage | Description | Key Equipment |
|-------|-------------|---------------|
| 1 | Geothermal Production Wells | BLT-01, ZST-01, ODK-01 (264 m³/h combined) |
| 2 | Brine Gathering & Treatment | MIX-01, SD-01 Desander, FIL-01A/B (5 µm), CI-01, SI-01 |
| 3 | Primary Heat Exchangers | PHE-01/02/03 — ~14.3 MWth total |
| 4 | Heat Pump System | EVAP-01, COMP-01 (R134a), COND-01, EXP-01 — ~16.8 MWth |
| 5 | Thermal Storage | HT-01 (1,000–1,500 m³ hot), CT-02 (500–800 m³ cold) |
| 6 | District Heating Distribution | DS-01, PB-01A/B, Metering Skids MS-01/02/03 |
| 7 | Cooling Distribution | AC-01 (LiBr absorption chiller), CW-01A/B |
| 8 | Brine Cooling & Reinjection | MIX-03, FIL-02A/B (10 µm), Injection Pumps (120–180 bar) |



## Technologies Used

- **Python** — pandas, numpy, matplotlib, seaborn
- **GeoPandas + Contextily** — spatial analysis and GIS mapping
- **Scikit-learn** — Min-Max normalisation for Reservoir Quality Index
- **ASPEN Plus V14** — 8-stage integrated plant simulation
- **ThermoGIS** — Dutch national geothermal resource database


## Conclusions

The Utrecht Science Park geothermal field is **technically and economically viable** for district energy supply. With heat pump integration at COP = 4, the three selected wells comfortably satisfy the 15 MW district demand under the P50 base-case scenario, with substantial surplus capacity available for future network growth.

 *"Under P50, the system delivers 52.8 MW — 352% of the required district demand, with a surplus of 37.8 MW for future expansion."*


## Author

**Geothermal Analytics Team** — ThermoGIS Datathon, June 2025


*Dataset sourced from ThermoGIS — the national geothermal data portal of the Netherlands.*
