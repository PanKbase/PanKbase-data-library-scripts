# PanKbase Data Library 

**Examples of code to interface with the data library for PanKbase**  

## Overview

This repository contains R-based Jupyter notebooks that proviede examples of extracting, cleaning, and visualizing metadata and data from the data library in PanKbase. The notebooks also provide examples of handling complex API interactions to derive insights from data across human donor demographics, biosample characteristics, experimental assays, and downstream analysis sets.  


## Key Features

- **Extract data**: Examples of how to extract donor demographics, biosample metadata, and analysis set information from the data library  
- **API Handling**: Examples of error handling for inconsistent data structures (arrays vs objects, UUIDs vs accessions)  
- **Visualizations**:  Generate visualiations and charts from data with reference lines and annotations  

##  Quick Start

### Prerequisites

```r
# Required R packages (automatically installed in notebook)
packages <- c("httr", "jsonlite", "dplyr", "ggplot2", "DT", "plotly")
```

### Usage

1. **Open the notebook**: `PanKBase_data_library_usecase_1.ipynb`
2. **Configure your dataset** (only change needed):
   ```r
   # Base URLs - modify these to explore different datasets
   base_url <- "https://api.data.pankbase.org"
   analysis_set_id <- "PKBDS0470WCHR"  # <-- Change this ID based on the dataset of interest  
   analysis_url <- paste0(base_url, "/analysis-sets/", analysis_set_id, "/")
   ```
3. **Run all cells** - the notebook handles everything else automatically!

*Find more dataset IDs at: https://data.pankbase.org/search/?type=AnalysisSet&file_set_type=principal+analysis

## What The Notebook Analyzes

### 1. Human Donor Demographics
- **Age Distribution**: Histograms with statistical summaries
- **Sex Distribution**: Categorical breakdowns  
- **BMI Analysis**: Medical threshold overlays (underweight/normal/overweight/obese)
- **Diabetes Status**: Clinical classification visualization
- **Ethnicity Patterns**: Multi-ethnic demographic analysis

### 2. Biosample Characterization  
- **Tissue Types**: Anatomical classification (islets, exocrine, etc.)
- **Preservation Methods**: Sample processing techniques
- **Collection Protocols**: Standardized vs custom procedures
- **Sample Quality Metrics**: Completeness and integrity scores

### 3. Analysis Set Profiling
- **Dataset Composition**: Sample and donor counts per study
- **Cohort Characteristics**: Demographics specific to research collections  
- **Data Completeness**: Field availability across datasets
- **Cross-Dataset Comparisons**: How your chosen dataset compares to the full database

##  Technical Challenges Solved

### API Complexity
- **Mixed Data Types**: Handles arrays, objects, and primitives in the same field
- **Inconsistent Identifiers**: UUID vs accession number resolution  
- **Nested JSON Structures**: Recursive data extraction with safe fallbacks
- **Rate Limiting**: Intelligent request throttling and retry logic

### Data Quality Issues
- **Missing Values**: Comprehensive NA handling strategies
- **Duplicate Records**: UUID-based deduplication
- **Inconsistent Formatting**: Standardized field parsing
- **Array Flattening**: Proper handling of multi-value fields (e.g., ethnicities)

##  File Structure

```
PanKBase_data_library_usecase_1.ipynb    # Main analysis notebook
├── Cell 1: Setup & Dependencies         # Package installation
├── Cell 2: API Helper Functions         # Core extraction utilities  
├── Cell 3: Donor Data Extraction        # Human donor analysis
├── Cell 4: Donor Visualizations         # Demographics plots
├── Cell 5: Biosample Extraction         # Tissue sample analysis
├── Cell 6: Biosample Visualizations     # Sample characteristic plots
├── Cell 7: Analysis Set Processing      # Dataset-specific analysis
├── Cell 8: Comparative Analysis         # Cross-dataset comparisons
├── Cell 9: Interactive Tables           # Searchable data exports
└── Cell 10: load and explore the single cell object           # search the object
```

## Example Outputs

### Automatically Generated Visualizations
- **Age Distribution Histogram**: Shows donor age patterns with mean/median lines
- **BMI Categories Bar Chart**: Medical classification with obesity thresholds
- **Diabetes Status Breakdown**: T1D, T2D, and non-diabetic proportions
- **Sample Type Distribution**: Tissue composition analysis
- **Data Completeness Matrix**: Field availability heatmap

### Exported Data Files
```
pankbase_donors_[DATASET_ID].csv         # Donor demographics
pankbase_biosamples_[DATASET_ID].csv     # Sample metadata  
pankbase_analysis_summary_[DATASET_ID].csv # Dataset overview
```

## Customization Options

### Change Dataset (Primary Use Case)
```r
# Simply modify this line to explore different research datasets:
analysis_set_id <- "YOUR_DATASET_ID_HERE"
```

### Adjust Visualization Parameters
```r
# Modify plot aesthetics
age_bins <- 20          # Number of age histogram bins
bmi_threshold <- 30     # Obesity threshold line
plot_theme <- "minimal" # ggplot theme
```

### Filter Data Subsets
```r
# Focus on specific populations
target_sex <- "female"           # Gender-specific analysis
min_age <- 18                    # Age range filtering  
diabetes_only <- TRUE           # Diabetic donors only
```

## Important Notes

### System Requirements
- **R Version**: 4.0+ recommended
- **Memory**: 4GB+ RAM for large datasets
- **Internet**: Stable connection for API calls
- **Jupyter**: R kernel properly configured

### API Limitations
- **Rate Limiting**: ~50 requests/minute (handled automatically)
- **Large Downloads**: Files >1GB may timeout (alternative download methods included)
- **UUID Dependencies**: Some records require UUID access (handled transparently)

## Contributing

Found a bug or want to add features? 

1. Fork this repository
2. Modify `PanKBase_data_library_usecase_1.ipynb`
3. Test with multiple dataset IDs
4. Submit a pull request with clear documentation

##  License

MIT License - feel free to use, modify, and distribute.

## Acknowledgments

- **PankBase Consortium** for open data access
- **HPAP Program** for standardized donor characterization  


##  Support

### Quick Troubleshooting
- **API Errors**: Check internet connection and dataset ID validity
- **Memory Issues**: Restart kernel and run cells individually
- **Plot Rendering**: Ensure all required packages are installed

### Get Help
- **Issues and Questions**: [GitHub Issues](https://github.com/PanKbase/data_analysis/issues)
- **Documentation**: Check cell comments in the notebook

---

*Last updated: June 2025*
