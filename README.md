# Lake 16-Tishreen: September Water-Area Method Comparison

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/mosalloum14/tishreen-lake-method-comparison/blob/main/Tishreen_Method_Comparison.ipynb)

A compact Python analysis comparing thesis-reported surface-water areas for Lake 16-Tishreen with previously exported Google Earth Engine (GEE) Landsat NDWI estimates.

## Research question

Does a threshold-based Landsat NDWI series reproduce the September water-area decline reported in the master’s thesis?

September was selected because the thesis selected it to represent conditions after summer and the dry season (§2.2.4). This keeps the seasonal window consistent while testing a different mapping workflow.


## Data and methods

- Thesis areas: Salloum (2021), Table 5; object-based supervised classification with SVM and visual correction.
- GEE estimates: Tishreen_September_2002_2020_QC.csv, field area_NDWI_015_km2; September monthly-median Landsat 5/7/8 Collection 2 Level-2 composites, NDWI > 0.15, 30 m.
- Primary comparison: the 11 Tishreen image-years with dates listed in thesis Table 2: 2002, 2004–2007, 2012, 2015, 2017–2020. GEE values are year-level September composites, not the exact thesis scenes.
- The thesis Table 5 also reports 2016 (5.61 km²), but Table 2 lists no Tishreen image date for 2016; that value is flagged and excluded from the primary paired comparison.
- The paired values are embedded in the notebook, so no data upload or Earth Engine authentication is needed to run the statistical analysis.

The notebook calculates paired percentage differences, OLS slopes and 95% confidence intervals, Sen slopes, exact Mann–Kendall p-values, and a comparison figure.

## Results

| Series | n | OLS slope (km²/year) | OLS p | Mann–Kendall p |
|---|---:|---:|---:|---:|
| Thesis classification | 11 | −0.125 | 0.0049 | 0.0165 |
| GEE Landsat NDWI > 0.15 | 11 | −0.008 | 0.7116 | 0.7612 |

Estimates of the Normalized Difference Water Index (NDWI) show an average decrease of 11.8% compared to the values presented in the thesis. The mean difference is -19.2% for the 2002–2007 period and -5.5% for the 2012–2020 period.

These results indicate that the estimated trend depends on the data and the mapping procedures used. They do not clarify which of the two methods is more accurate, nor do they provide an independent validation for either dataset; furthermore, they do not attribute the observed changes to climate factors or the operation of dams.

## Run

### Google Colab

Click **Open in Colab** above, then select **Runtime → Run all**. The notebook displays the table and figure and saves tishreen_method_comparison.png and tishreen_paired_areas.csv.

### Local Python

Install the listed packages and run the notebook in Jupyter with: python -m pip install -r requirements.txt

## Scope and reproducibility

This repository reproduces the statistical comparison based on stored area estimates. It does not reprocess raw satellite imagery. The original hand-drawn ROI geometry was not included in the archived export, so the exact raster-area extraction cannot be independently rerun from this repository. Trend p-values are exploratory and do not adjust for serial dependence.


## References

- Salloum, M. (2021). *Climate Change Consequences and Scenarios: Syria as a Case Study*. MSc thesis, University of Tübingen. Table 2, Table 5, and §2.2.4.
- McFeeters, S. K. (1996). The use of the Normalized Difference Water Index (NDWI) in the delineation of open water features. *International Journal of Remote Sensing*, 17(7), 1425–1432. https://doi.org/10.1080/01431169608948714.
- Google Earth Engine Data Catalog: Landsat 5, 7, and 8 Collection 2 Tier 1 Level-2.
