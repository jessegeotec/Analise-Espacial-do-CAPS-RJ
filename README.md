[🇺🇸 English](README.md) | [🇧🇷 Português](README-pt.md)

# Territorialization and Flows of the Psychosocial Care Network (RAPS) in Rio de Janeiro State
### Spatial Analysis of Outpatient Commutes in CAPS using SIA/DATASUS Microdata (2025)
![capa](capa.png)
---

## 1. Context and Objective
- Regionalization, decentralization, and hierarchization are core principles of the Brazilian Unified Health System (SUS) designed to ensure integrated, equitable, and territorialized access to health services. Within the Psychosocial Care Network (RAPS), Psychosocial Care Centers (CAPS) play a strategic role in providing community-based care to individuals experiencing mental distress, disorders, or needs arising from the harmful use of alcohol and other drugs.
- This repository presents the analytical and cartographic pipeline developed to evaluate the territorialization and accessibility of RAPS in the state of Rio de Janeiro in 2025. By processing 1,608,875 outpatient procedures from SIA/DATASUS (SIGTAP Organizational Format 03.01.08 - Psychosocial Care/Monitoring), the project maps Origin-Destination (O-D) flow matrices to quantify the intra- and intermunicipal retention capacity of CAPS assistance. The goal is to diagnose healthcare deserts (care gaps) and absolute external dependency. The codebase provides reproducible spatial analysis tools for SUS researchers and public health managers.
- This work was developed as the Final Project for the Winter Course in "Introduction to R Language with Health Data," offered by ICICT/Fiocruz and taught by Professor Raphael Saldanha, developer of the `microdatasus` package. 
Furthermore, the study was accepted for presentation at the II Health Geography Workshop at UERJ, titled "Territorialization of the Psychosocial Care Network in Rio de Janeiro State: Spatial Analysis of Flows."

- For this project, I used RStudio with the following packages:
  - 1.1 **microdatasus:** Processing and preprocessing of DATASUS microdata.
  - 1.2 **geobr:** Downloading state and municipal spatial grids (shapefiles) with latitude and longitude data.
  - 1.3 **ggplot2:** Crafting advanced maps and charts.
  - 1.4 **sf:** Geographic operations (e.g., extracting municipal centroids).
  - 1.5 **tidyr:** Cleaning null values (NA).
  - 1.6 **dplyr:** Data wrangling and manipulation.
  - 1.7 **stringr:** String manipulation.
---

## 2. Territorial Highlights and Findings
- **Intramunicipal Flow (High Retention):** Out of the 1,608,875 psychosocial outpatient procedures analyzed in the state in 2025, **99.4%** occurred within the user's municipality of residence. This rate indicates a highly effective overall regionalization of RAPS in Rio de Janeiro, with local networks absorbing nearly all demand and fulfilling the premise of territorialized community care. Municipalities like Rio de Janeiro, São João de Meriti, and Volta Redonda lead the ranking for the highest absolute volume of procedures provided to their own population.
![Gráficos do Fluxo Intramunicipal](fluxo_intramunicipal.png)

- **Intermunicipal Flow (Healthcare Deserts):** The remaining **0.6%** of the state's volume (**n = 9,415**) corresponded to intermunicipal commutes, where most municipalities exported few procedures relative to their total volume.
![Gráficos do Fluxo Intermunicipal](fluxo_intermunicipal.png)

- To determine the relevance of intermunicipal commutes, a percentage table was generated comparing destinations that matched the origin municipality (==) versus those that differed (!=).
![Gráficos do Fluxo Intramunicipal](dependencia_externa.png)

- **Absolute External Dependency (100%):** Network analysis identified small municipalities with an absence or insufficiency of localized care. **Varre-Sai** accounted for **7.32%** of all intermunicipal traffic in the state, exporting 100% of its psychosocial demand (with 99.7% absorbed by the neighboring municipality of Natividade). Similarly, **Rio das Flores** showed 100% external healthcare dependency, exporting its patients entirely to Valença. The third highest exporting municipality was Quatis, with **47.1%** of procedures performed in other locations (**n = 178**).
*Note: Municipalities presenting 100% dependency but with a statistically insignificant flow of procedures were excluded.*
---

## 3. Cartography of RAPS Flows (Rio de Janeiro - 2025)
- **Metropolitan Pressure and Centrality:** In absolute terms of intermunicipal traffic, the **São Gonçalo → Niterói** route recorded the highest volume of patient evasion in the state (**n = 1,902 procedures**). This finding highlights intense socio-spatial conurbation and the regional reference role played by Niterói's specialized network in Metropolitan Region II, even considering that São Gonçalo maintains an internal retention rate of 97.9%.
- **Highest Reception Municipality:** The state capital, Rio de Janeiro, received forwarded procedures from over 40 municipalities, leading as the top receiving hub, in addition to managing the largest intramunicipal flow (**n = 529,948**).
- **Cartographic Modeling of Displacements:** To map intermunicipal dynamics without excessive visual overlap, municipal centroids (extracted from the IBGE 2022 Census grid via the `geobr` package) were connected using directed arcs (`geom_curve` in `ggplot2`). The line width (`linewidth`) and opacity (`alpha`) of the curves were scaled across five brackets of annual outpatient volume. This approach allows for visual identification ranging from residual flows to the main mobility axes of patients seeking specialized care.

![mapadefluxo](mapa_fluxo_caps.png)

---

## 4. Reproduction Script
- Open the [`proj_caps_rj.qmd`](proj_caps_rj.qmd) file in RStudio.
- The codebase is structured as a Quarto / R Markdown document, integrating the study's narratives with the processing chunks for DATASUS microdata (`microdatasus`), O-D matrix aggregation, and high-resolution cartographic modeling (`geobr` and `ggplot2`).
- The first code block was engineered to prevent memory crashes and bypass the need for manual, month-by-month downloads from SIA/DATASUS for the selected procedure (given that each monthly dataset contains over 5 million raw rows). The implemented structure allows for a lightweight, continuous download process, performing automated cleaning and filtering of target variables on the fly.
- Feel free to run the code line-by-line or chunk-by-chunk, but please remember to cite the author of this work in your bibliography, as well as the authors of the respective R packages used ;).

### **Thank you!**
