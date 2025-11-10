# STAT 5410 Final Project: Analysis of Area Codes

## Project Overview

This was a comprehensive project to combine all of the material learned in STAT 5410 at the University of Connecticut (Statistical Computing for Data Science), meant to showcase my proficiency in data cleaning and wrangling using R, advanced data visualization, application of statistical and computational methods, reproducible analysis with R Markdown, and the ability to derive insights from complex datasets using a variety of data science techniques.

This project investigates the historical assignment of North American telephone area codes, with a focus on how area code assignments related to county population sizes, dialing speed on rotary phones, and potential demographic disparities in 1947. The analysis includes:

- Mapping original area code regions for selected states.
- Examining the relationship between population size and dial pulls.
- Identifying counties assigned unfairly fast or slow area codes.
- Investigating potential racial disparities in area code assignment.
- Predicting the modern proliferation of area codes from historical data.

## Data Sources

The project uses the following datasets:

| Dataset | Description |
|---------|-------------|
| `sf_data` | Simple features polygons of U.S. counties, including FIPS codes, county names, and geometry. |
| `splits_overlays` | Original area codes with associated years and current territory coverage. |
| `cities_area_codes_final` | Cities with associated area codes in the U.S. |
| `censusdata` | County-level census data (population, births, telephones, age distribution, and Black population). |
| `merged_counties_1950` | Historical records of counties merged since 1950. |
| `new_counties_1950` | Records of new counties formed since 1950. |
| `state_fips` | State FIPS codes for reference. |

Additional references:  
- [FCC FIPS codes](https://transition.fcc.gov/oet/info/maps/census/fips/fips.txt)  
- [Hand-drawn numbering plan maps](https://lincmad.com/map1947.html)  
- [Bell Labs technical report](https://underunderstood.com/podcast/wp-content/uploads/2021/03/NPA-History-and-Map.pdf)  

## Analysis Components

### Component 1: Mapping Original Area Codes

- Created maps for six states (California, Connecticut, Massachusetts, Minnesota, Washington, Wisconsin).  
- Imputed missing area codes for low-population counties using K-Nearest Neighbors.  
- Visualizations illustrate county-level assignments of original area codes before and after prediction.

### Component 2: Population vs. Dial Pull Analysis

- Investigated whether regions with higher population received faster-to-dial area codes.  
- Used log-transformed 1950 population counts vs. dial pulls.  
- Linear regression results indicated a significant negative relationship:
  - Every 1 unit increase in dial pulls corresponds to a 0.0575 decrease in log(population).  
  - T-statistic = -11.6, p-value = 2.62e-30.  
- Visualized with scatter plots, linear regression lines, and boxplots.

### Component 3: Identifying “Unfair” Assignments

- Counties were classified as having unfairly fast or slow area codes based on residuals from predicted population vs. dial pull regression.  
- Counties exceeding ±2 standard deviations from the mean residuals were flagged.  
- Generated visualizations of residuals.

### Component 4: Investigating Racial Disparities

- Examined relationships between dial pulls and both Black population and non-Black population.  
- Linear regression models indicate:
  - Non-Black population shows a negative relationship with dial pulls.  
  - Black population shows a slight positive relationship with dial pulls, suggesting possible discrimination in area code assignment speed.  
- Visualizations show trends across dial pulls for both populations.

### Component 5: Predicting Modern Area Code Proliferation

- Aggregated historical data by original area code to predict the current number of area codes assigned.  
- Summarized features: population, births, area, perimeter, age distribution, telephones, and Black population.  
- Candidate models tested: linear regression, LASSO, Ridge, KNN regression, and random forest.  
- Cross-validation used to select the best performing model.  
- Results provide insights into historical factors influencing modern area code proliferation.

## Key Insights

1. **Dial Pulls & Population**: Higher population regions tended to receive area codes that required fewer dial pulls, supporting the dial pull theory.  
2. **Unfair Assignments**: Some counties received area codes that were faster or slower than expected given their population.  
3. **Racial Disparities**: Evidence suggests counties with larger Black populations were assigned area codes requiring more dial pulls on average.  
4. **Predicting Modern Codes**: Historical demographic and geographic factors can partially explain the current distribution and proliferation of area codes.

## Technology, Tools & Packages

- **Languages:** R
- **Libraries:** `tidyverse`, `readxl`, `sf`, `janitor`, `broom`, `tidymodels`, `glmnet`, `kknn`, `rsample`, `knitr`  
- **Other Tools:** Quarto Markdown File, GitHub, R Studio

## Visualizations

The project includes a series of visualizations:

- State-level maps of original area codes.
- Scatter plots and regression lines showing population vs. dial pulls.
- Boxplots of population distribution by dial pulls.
- Residual plots identifying unfairly assigned area codes.
- Predicted vs. observed modern area code proliferation.

## How to Reproduce

1. **Clone the repository:**
    ```bash
    git clone https://github.com/schgrz/area-code-analysis.git
    ```
2. **Ensure R, RStudio, and Quarto Markdown are Installed** 
    *(RStudio 4.2.0 or higher)*

    > Download [R](https://posit.co/download/rstudio-desktop/)

    > Download [RStudio](https://posit.co/download/rstudio-desktop/)
   
    > Download [Quarto](https://quarto.org/docs/get-started/) *Choose quarto for RStudio*
3. **Install dependencies**
   
    **Option 1 - GUI method**
    1. Open a new RStudio session
    2. Go to: **Tools > Install Packages...**
    3. Add the following packages:
    ```
    tidyverse, readxl, janitor, broom, tidymodels, glmnet, sf, stringr
    ```

    **Option 2 - Code method**

    With a *.qmd* file open, create a new code chunk and run:
    ```
    install.packages(c(
    "tidyverse", "readxl", "janitor", "broom", "tidymodels",
    "glmnet", "sf", "stringr"
    ))
    ```
4. **Verify folder structure**

    ```
    area-code-analysis (Working Directory)
    ├── data/ # Contains raw datasets
    ├── STAT_5410_Final_Project.html # Contains a pre-rendered output file for review
    └── STAT_5410_Final_Project.qmd # Working file
    ```
5. **Run the notebook**
    1. With RStudio, open `STAT_5410_Final_Project.qmd`
    2. Click *Render* or use *Run All* to execute the analysis