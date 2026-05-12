# Nortexit: una mirada empírica al discurso del separatismo regional en México

**Spatial analysis of Mexico's Municipal Human Development Index (HDI) to test the "two Méxicos" hypothesis.**

## Research question

A recurring narrative in Mexican public discourse argues that the northern states ("Nortexit") are economically and socially distinct enough from the rest of the country to justify separation. This project asks:

> *Does the available data support the idea of "two Méxicos", or is it a political simplification?*

The analysis compares HDI distribution, central tendency, and dispersion between the nine northern states associated with the separatist narrative and the rest of the country, at the municipal level.

## Datasets

| Source | Content | Use |
|---|---|---|
| **UNDP Mexico** — Municipal HDI, Results 2010–2020 | HDI values for 1,197 municipalities | Main variable of analysis |
| **INEGI** — Marco Geoestadístico Nacional | Municipal boundaries (shapefiles) and CVEGEO codes | Geometry and spatial join |
| **INEGI** — Population data | Total population per municipality | Urban/rural classification |

Final dataset: **2,457 municipalities** with HDI, geometry, regional classification, and urban/rural category.

## Methodology

### 1. Data cleaning and standardization (Excel)
- Standardized CVEGEO codes across UNDP and INEGI datasets (leading zeros, text/numeric format, accent handling).
- Resolved naming inconsistencies between sources.
- Verified 1:1 match for all 2,457 municipalities.

### 2. Urban/rural classification (own criterion)
The official INEGI threshold (2,500 inhabitants = urban) was insufficient for HDI analysis, as it groups a 3,000-person town with a 14,000-person small city. I built a three-tier classification:

| Category | Population threshold |
|---|---|
| Rural | < 2,500 |
| Transition | 2,500 – 14,999 |
| Urban | ≥ 15,000 |

### 3. Regional aggregation
Municipalities were grouped into five economic-geographic regions: **Norte, Centro-Norte, Centro, Occidente, Sur-Sureste**.

### 4. "Nortexit" classification (key analytical decision)

A binary variable flags the nine states most frequently invoked in northern separatist discourse: **Baja California, Baja California Sur, Coahuila, Chihuahua, Durango, Nuevo León, Sinaloa, Sonora, Tamaulipas**.

The selection of these specific nine states was not arbitrary nor based on formal academic regionalization. It was derived from the widely-circulated "Nortexit" maps shared across Mexican social media, where users themselves defined which states should hypothetically separate from the rest of the country. Using the popular framing as the operational definition allows the analysis to test the narrative on its own terms, rather than imposing an external geographic criterion.

This is the variable used to test the central hypothesis.

### 5. Spatial analysis and visualization (QGIS)
- Spatial join between attribute table and municipal vector layer using CVEGEO.
- Categorized symbology by HDI quintiles to visualize spatial patterns.
- CRS standardization across layers from different sources.
- Statistical comparison via boxplot using the **Data Plotly** plugin.

## Key findings

### 1. The "Nortexit" has higher HDI — but the gap is modest

| Bloc | Mean HDI | Std. dev. | N |
|---|---|---|---|
| Nortexit (9 states) | 0.720 | 0.058 | 335 |
| Rest of Mexico | 0.694 | 0.057 | 2,117 |

The North does sit higher, but by only **0.026 HDI points (~3.8%)**. It is not a different country; it is the same country one rung up.

### 2. Internal inequality is virtually identical in both blocs

Standard deviation is **0.058 in the Nortexit vs. 0.057 in the rest of Mexico**. The myth of a "uniform North vs. unequal South" does not hold: the North has the same spread of inequality as the rest of the country.

### 3. The poorest municipality is NOT in the South

- **Lowest HDI nationwide:** Cochoapa el Grande, Guerrero (0.445)
- **Second lowest:** Batopilas, **Chihuahua** (0.456) — in the Sierra Tarahumara, within the Nortexit.

Extreme poverty exists in the North too. The separatist narrative often ignores this.

### 4. The richest municipality is NOT in the North

- **Highest HDI nationwide:** Benito Juárez, **Mexico City** (0.908)
- **Second highest:** San Pedro Garza García, Nuevo León (0.903)

The wealth ceiling is shared between Center and North, not exclusive to either.

### 5. Sur-Sureste is the most lagging region, but not dramatically

Mean HDI by region (ascending): Sur-Sureste 0.686 < Centro-Norte 0.700 < Centro 0.702 < Occidente 0.702 < Norte 0.724. The gap between the lowest and highest region is **0.038 points**.

## Conclusion

The separatist narrative is not empirically baseless: northern states do show a moderately higher HDI. However, the magnitude is small, internal inequality is comparable across blocs, and both the highest and lowest extremes of national development are distributed across regions. The "two Méxicos" framing oversimplifies a more textured reality: **a single country with a slightly elevated North, a lagging Southeast, and comparable internal heterogeneity within each region.**

## Tech stack

- **QGIS** — spatial join, symbology, CRS management, layer composition
- **Data Plotly (QGIS plugin)** — statistical visualization (boxplots)
- **Microsoft Excel** — data cleaning, standardization, classification logic
- **qgis2web** — web export

## Repository structure

```
