# PanKbase Analysis Scripts

Comprehensive R-based analysis toolkit for exploring pancreatic data from the PanKbase Data Library. This repository contains three complementary scripts for 1) snATAC metadata and single cell object exploration, and donor demographics visualization, 2) scRNA metadata and single cell object exploration, and donor demographics visualization, 3) differential expression analysis

---

## Scripts Overview

### 1. Metadata Analysis Script
Comprehensive metadata extraction and analysis for donor demographics, sample quality metrics, and experimental parameters.

**Key Features:**
- Robust API data extraction  
- Donor demographic analysis (age, BMI, diabetes status)  
- Sample quality metrics (yield, viability, isolation centers)  
- Correlation analysis and visualization  
- Configurable plot themes and parameters  

---

### 2. RDS Object Loading for Visualization and Downstream Analysis

1. **Direct Streaming (Recommended):**  
   Use `readRDS(url(rds_url, open = "rb"))` with extended timeout (`options(timeout = 3600)`) to stream the ~10GB file directly from S3 into memory.  

2. **Local Download Method:**  
   Download with `curl` or `download.file()` and load using `readRDS(local_file)`. Requires disk space but works offline.  

3. **Robust Error Handling:**  
   Built-in checks for file size, network conditions, fallback mechanisms, and timing metrics.  

4. **Performance Monitoring:**  
   Logs download speeds, file metadata, and load time for diagnostics.  

5. **Expected Performance:**  
   Direct streaming: 10–20 mins; local method requires space but enables reuse.  

---

### 3. DEG Analysis Script

Performs metadata extraction and analysis for differential expression gene (DEG) results across multiple pancreatic cell types (Alpha, Beta, Acinar, Ductal, and Active Stellate cells).

**Key Features:**
- Automated data loading from S3  
- Volcano plots and summary statistics  
- Comparative analysis across cell types  
- Customizable statistical thresholds  
- Publication-ready visualizations  

---

## Prerequisites

### System Requirements
- **R Version:** 4.0 or higher  
- **RAM:** 4GB minimum (8GB+ recommended)  
- **Internet:** Stable connection for PanKbase Data Library API/S3 access  
- **Storage:** Minimal (data streams from cloud)  

### Required R Packages

```r
# Automatically installed by scripts
packages <- c("httr", "jsonlite", "ggplot2", "dplyr", "readr", "tidyr", 
              "RColorBrewer", "gridExtra", "knitr", "viridis")
````

---

## Quick Start

### Metadata Analysis

1. Set `ANALYSIS_SET_ID` to your PanKbase dataset
2. Configure plot themes and parameters
3. Run complete script or execute cell-by-cell
4. Explore demographic and quality visualizations

### DEG Analysis

1. Set statistical thresholds in configuration section
2. Run script for automatic analysis of all cell types
3. Review volcano plots and summary statistics
4. Export gene lists for functional enrichment
---

## Configuration Options

| Parameter         | Default         | Description                               |
| ----------------- | --------------- | ----------------------------------------- |
| ANALYSIS\_SET\_ID | "PKBDS1349YHGQ" | PanKbase dataset identifier               |
| LOG2FC\_THRESHOLD | 1.0             | Minimum fold change for significance      |
| PVALUE\_THRESHOLD | 0.05            | Maximum adjusted p-value                  |
| PLOT\_THEME       | "minimal"       | ggplot theme (`minimal`, `bw`, `classic`) |
| COLOR\_PALETTE    | "Set2"          | Color scheme for visualizations           |
| HISTOGRAM\_BINS   | 15              | Number of histogram bins                  |

---

## Example Datasets

* `PKBDS1349YHGQ`: scRNA reference map
* `PKBDS0470WCHR`: ATAC-seq reference map
* `PKBDS5505XMWS`: Alpha cell-specific analysis

---

## Output Interpretations

### Metadata Analysis

* **Demographics:** Age, BMI, sex, diabetes status
* **Sample Quality:** Yield, viability, isolation center
* **Correlations:** Between metabolic variables
* **UMAP Plots and Cell Distribution**
  
### DEG Analysis

* **Volcano Plots:** Log2 fold change vs significance
* **Summary Statistics:** Gene counts by direction
* **Gene Lists:** Ready for enrichment analysis
---

## Troubleshooting

### Common Issues

#### Dataset Not Found

* Verify `ANALYSIS_SET_ID` is correct
* Check dataset at [PanKbase Data Library Search](https://data.pankbase.org/search/)

#### API Connection Problems

* Check your internet connection
* Increase timeout settings

#### Memory Issues

* Close unused apps
* Use `memory.limit(size = 8000)`
* Filter data more strictly

#### Package Installation

* Use `install.packages("package_name")`
* Update R
* Ensure internet access

---

## Performance

### Expected Runtime


* **Metadata Analysis:** \~5 minutes
* **DEG Analysis:** 2–5 minutes
* **Streaming/Downloading single cell object:** 10–20 minutes
    

---

## Integration

### Single-Cell Data

```r
# Direct S3 streaming (recommended)
rds_url <- "https://pankbase-data-v1.s3.us-west-2.amazonaws.com/analysis_resources/single_cell_objects/PanKbase_snatac_v1.rds"
seurat_obj <- readRDS(url(rds_url, open = "rb"))

# Combine with metadata
combined_analysis <- merge(donor_metadata, seurat_obj@meta.data, by = "donor_id")
```

---

## Data Export

```r
# Export processed data
write.csv(donor_metadata, "donor_demographics.csv", row.names = FALSE)
write.csv(all_deg_data, "deg_results.csv", row.names = FALSE)

# Save plots
ggsave("volcano_plots.pdf", combined_plots, width = 12, height = 8, dpi = 300)
```

---

## Resources

* [PanKbase Data Library](https://data.pankbase.org)
* [Dataset Search](https://data.pankbase.org/search/)
* [R Documentation](https://cran.r-project.org/)

---

## Citation

If you use these analysis scripts in your research, please cite:
**pankbase.org**

---

## License

MIT License - Free to use, modify, and distribute with attribution.

---

### Get Help
- **Issues and Questions**: [GitHub Issues](https://github.com/PanKbase/data_analysis/issues)
- **Documentation**: Check cell comments in the notebook

---

**Version:** 2.0
**Last Updated:** June 2025
**Compatible with:** R 4.0+, PanKbase Data Library API v1
