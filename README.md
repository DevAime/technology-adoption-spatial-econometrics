# Nairobi Companies Technology Adoption: Spatial Analysis

A spatial econometric analysis examining technology adoption patterns among small and medium enterprises (SMEs) across Nairobi's subcounties using Spatial Durbin Models.

## Overview

This project investigates how companies in Nairobi adopt and adapt to modern technology, with a specific focus on spatial dependencies between neighboring subcounties. The analysis examines four distinct dimensions of technology adaptation:

- **Adoption (y)**: Overall level of new technology uptake
- **Access (y_11)**: Availability and accessibility of technology
- **Openness (y_12)**: Willingness and receptiveness toward new technology
- **Coping (y_13)**: Ability to handle and manage modern technological changes

## Project Structure

```
project/
├── Combined_Data.csv              # Main dataset with company responses
├── gadm41_KEN_2.shp              # Spatial data for Nairobi subcounties
├── SDM_analysis.Rmd               # R Markdown analysis file
└── README.md                      # This file
```

## Data Description

### Geographic Coverage

The analysis covers 17 subcounties in Nairobi:
- Dagoretti North & South
- Embakasi Central, East, North, South, and West
- Kamukunji
- Kasarani
- Kibra
- Langata
- Makadara
- Mathare
- Roysambu
- Ruaraka
- Starehe
- Westlands

<img width="583" height="393" alt="image" src="https://github.com/user-attachments/assets/720ee9c7-9f46-45a3-9ea7-d62a98f9d6a7" />


### Sample Data Structure

| y_11 | y_12 | y_13 | y | x_1 | x_2 | x_3 | x_4 | x_5 | x_6 | x_7 | x_8 | x_9 | ADM2_EN |
|------|------|------|---|-----|-----|-----|-----|-----|-----|-----|-----|-----|---------|
| Very High | Very High | Very High | Very High | Very High | Very High | Very High | No | 0 | Physical business | 0 | 0 | 1 | Dagoreti |
| High | Very High | Very High | Very High | High | Very High | Very High | No | 0 | Online business | 3 | 0 | 0 | Dagoreti |

Total observations: 1,215 companies across all subcounties

### Variables

#### Dependent Variables
- **y** (Adoption): Level of Adoption of New Technology
- **y_11** (Access): Level of Access to new technology
- **y_12** (Openness): Level of Openness, reception, and utilization of new technology
- **y_13** (Coping): Level of Coping with modern technology

All dependent variables are measured on a 5-point ordinal scale:
1. Very Low
2. Low
3. Medium
4. High
5. Very High

#### Independent Variables
- **x_1** (ICTComp): Level of Competency in ICT
- **x_2** (Trainedu): Level of Willingness to continuous training, education, and qualification
- **x_3** (Mdigtech): Level of Mastering digital transformation
- **x_4** (Newtech): Employees with new technology (Binary: 1=Yes, 0=No)
- **x_5** (Techemployees): Number of employees with digital technical skills
- **x_6** (Moperate): SMEs operating online, physical, or both (Binary: 1=Online business, 0=Physical business)
- **x_7**: Total number of employees
- **x_8** (Fininstmain): Financial Institutions as main financiers (Binary: 1=Yes, 0=No)
- **x_9** (Finbarrier): Finance as the main barrier (Binary: 1=Yes, 0=No)

## Methodology

### Spatial Analysis Approach

The analysis follows a systematic approach to determine whether spatial effects are present:

1. **Moran's I Test**: For each dependent variable, we test for spatial autocorrelation to determine if neighboring subcounties exhibit similar values.
2. **Model Selection**: 
   - If Moran's I is not significant (p > 0.05): Use Ordinary Least Squares (OLS) regression
   - If Moran's I is significant (p < 0.05): Use Spatial Durbin Model (SDM)

### Spatial Weights Matrix

A spatial weights matrix was constructed using:
- Queen contiguity: Subcounties sharing borders are considered neighbors
- Row-standardized weights: Each neighbor's influence is proportionally scaled

### Model Comparison

Model performance was evaluated using the Akaike Information Criterion (AIC):

| Model | AIC |
|-------|-----|
| Adoption | 1099.727 |
| Access | 1606.262 |
| Openness | 1632.464 |
| Coping | 1177.026 |

## Results

### Model 1: Technology Adoption

**Spatial Autocorrelation Test**
- Moran's I statistic: -0.0025
- p-value: 0.9236
- Conclusion: No significant spatial autocorrelation detected

**Model Type**: Ordinary Least Squares (OLS)

**Model Performance**
- R²: 0.6625
- Adjusted R²: 0.6599
- F-statistic: 262.8 (p < 2.2e-16)
- Residual standard error: 0.3786


<img width="698" height="541" alt="image" src="https://github.com/user-attachments/assets/81d27d73-a81e-4ff8-97e8-897d8f24fc7d" />


**Key Findings**
The model explains approximately 66% of the variance in technology adoption levels. Three variables emerged as highly significant drivers:

- **ICT Competency (x_1)**: Coefficient = 0.430, p < 0.001
  - The strongest predictor of adoption
  - Each unit increase in ICT competency is associated with a 0.43-unit increase in adoption
  
- **Mastering Digital Transformation (x_3)**: Coefficient = 0.289, p < 0.001
  - Second strongest predictor
  - Demonstrates the importance of understanding digital business processes
  
- **Willingness to Training (x_2)**: Coefficient = 0.151, p < 0.001
  - Significant positive effect
  - Continuous learning culture promotes technology adoption

- **Technical Employees (x_5)**: Coefficient = 0.004, p = 0.0495
  - Marginally significant
  - More technically skilled employees slightly increase adoption

Variables with no significant effect: Employee new technology use (x_4), operational mode (x_6), total employees (x_7), financial institutions (x_8), and finance as barrier (x_9).

**Geographic Distribution**

<img width="862" height="532" alt="image" src="https://github.com/user-attachments/assets/88e4c05b-7369-48a5-9a4f-3e6dad59732e" />


*Orange (High adoption): Westlands, Dagoreti, Embakasi, Kasarani*  
*Red (Medium adoption): All other subcounties*

### Model 2: Technology Access

**Spatial Autocorrelation Test**
- Moran's I statistic: -0.0075
- p-value: 1.0
- Conclusion: No significant spatial autocorrelation detected

**Model Type**: Ordinary Least Squares (OLS)

**Model Performance**
- R²: 0.5400
- Adjusted R²: 0.5366
- F-statistic: 157.2 (p < 2.2e-16)
- Residual standard error: 0.4663

<img width="643" height="550" alt="image" src="https://github.com/user-attachments/assets/ddf0b304-fd22-4df6-9412-5ce51b9c3674" />


**Key Findings**
The model explains 54% of variance in technology access. Significant predictors include:

- **Mastering Digital Transformation (x_3)**: Coefficient = 0.351, p < 0.001
  - Strongest predictor of access
  - Understanding digital systems facilitates access to technology

- **ICT Competency (x_1)**: Coefficient = 0.338, p < 0.001
  - Strong positive effect
  - Technical skills enable better technology access

- **Willingness to Training (x_2)**: Coefficient = 0.140, p < 0.001
  - Significant positive effect
  - Continuous learning improves access opportunities

- **Operational Mode (x_6)**: Coefficient = 0.065, p = 0.0304
  - Online businesses have better access to technology

- **Technical Employees (x_5)**: Coefficient = 0.007, p = 0.0077
  - More skilled employees improve access

- **Total Employees (x_7)**: Coefficient = -0.004, p = 0.0138
  - Small negative effect, possibly indicating that larger firms face different access challenges

**Geographic Distribution**

<img width="917" height="538" alt="image" src="https://github.com/user-attachments/assets/2009879c-5ed6-4794-a1b9-1130ef6ecedb" />

*Orange (High access): Westlands, Kasarani, Embakasi, Dagoreti, Kamukunji, Mathare*  
*Purple (Low access): Ruaraka*  
*Red (Medium access): All other subcounties*

### Model 3: Technology Openness

**Spatial Autocorrelation Test**
- Moran's I statistic: -0.0021
- p-value: 0.8615
- Conclusion: No significant spatial autocorrelation detected

**Model Type**: Ordinary Least Squares (OLS)

**Model Performance**
- R²: 0.5339
- Adjusted R²: 0.5304
- F-statistic: 153.4 (p < 2.2e-16)
- Residual standard error: 0.4714

<img width="655" height="542" alt="image" src="https://github.com/user-attachments/assets/c0f81c0a-5acc-4007-84cb-5613d362fac6" />


**Key Findings**
The model explains 53% of variance in openness to technology. Significant predictors:

- **ICT Competency (x_1)**: Coefficient = 0.361, p < 0.001
  - Strongest predictor
  - Higher technical competency increases receptiveness to new technology

- **Mastering Digital Transformation (x_3)**: Coefficient = 0.299, p < 0.001
  - Strong positive effect
  - Understanding digital business models promotes openness

- **Willingness to Training (x_2)**: Coefficient = 0.165, p < 0.001
  - Significant positive effect
  - Learning orientation enhances receptiveness

- **Technical Employees (x_5)**: Coefficient = 0.005, p = 0.0449
  - Small but significant positive effect

- **Finance as Barrier (x_9)**: Coefficient = 0.049, p = 0.0944
  - Marginally significant
  - Surprisingly, perceiving finance as a barrier slightly increases openness, possibly reflecting awareness and ambition

**Geographic Distribution**

<img width="899" height="527" alt="image" src="https://github.com/user-attachments/assets/0cbc7d9b-833c-4d55-b609-92bb6bb71711" />


*Orange (High openness): Westlands, Dagoreti, Kamukunji, Embakasi*  
*Red (Medium openness): All other subcounties*

### Model 4: Technology Coping (Spatial Durbin Model)

**Spatial Autocorrelation Test**
- Moran's I statistic: 0.0101
- p-value: < 2.2e-16
- Conclusion: Highly significant positive spatial autocorrelation detected

**Model Type**: Spatial Durbin Model (SDM)

**Model Performance**
- Log likelihood: -554.6067
- AIC: 1139.2 (OLS AIC: 1147.0)
- ML residual variance (σ²): 0.1451
- Rho: -2.4411 (p < 0.001)
- LR test: 9.8273 (p = 0.0017)
- 
<img width="1194" height="597" alt="image" src="https://github.com/user-attachments/assets/6b7f92dc-73dc-490f-ab57-97ee3d415327" />


The SDM significantly outperforms OLS, as evidenced by the lower AIC and significant likelihood ratio test.

**Key Findings**

This model reveals both direct effects (impact on a firm's own coping ability) and indirect effects (spillover impacts from neighboring subcounties).

**Direct Effects (Within-Subcounty)**

Highly significant direct effects:
- **ICT Competency (x_1)**: 0.550 (p < 0.001)
  - Strongest direct predictor
  - Firms with higher ICT skills cope better with technology changes

- **Mastering Digital Transformation (x_3)**: 0.189 (p < 0.001)
  - Understanding digital business processes improves coping

- **Willingness to Training (x_2)**: 0.135 (p < 0.001)
  - Continuous learning enhances coping ability

**Indirect Effects (Spatial Spillovers)**

Highly significant spillover effects from neighboring subcounties:

- **Employees with New Technology (lag.x_4)**: 3.222 (p < 0.001)
  - Largest positive spillover effect
  - When neighboring firms have employees using new technology, it significantly improves coping in adjacent areas
  - Likely due to knowledge diffusion and peer learning

- **Willingness to Training (lag.x_2)**: 1.160 (p < 0.001)
  - Strong positive spillover
  - Training culture in one subcounty benefits neighboring areas

- **Financial Institutions as Financiers (lag.x_8)**: -1.232 (p < 0.001)
  - Negative spillover effect
  - When neighbors rely heavily on financial institutions, it may create competitive pressures

- **Operational Mode (lag.x_6)**: -3.281 (p < 0.001)
  - Strong negative spillover
  - Online businesses in neighboring areas create competitive pressure

- **Technical Employees (lag.x_5)**: 0.060 (p < 0.001)
  - Positive spillover
  - Skilled workers in neighboring areas create beneficial knowledge networks

**Total Effects**

The total effect combines direct and indirect impacts:

- **Willingness to Training (x_2)**: 1.293 (p < 0.001)
  - Highest total effect
  - Strong within-firm impact plus significant spillovers

- **Employees with New Technology (x_4)**: 3.250 (p < 0.001)
  - Second highest total effect
  - Primarily driven by massive spillover effects

- **Operational Mode (x_6)**: -3.255 (p < 0.001)
  - Large negative total effect
  - Competition from online businesses in neighboring areas

**Geographic Distribution**

<img width="888" height="563" alt="image" src="https://github.com/user-attachments/assets/d71cb5ae-9711-4ce4-ae63-93b7448d0498" />

*Red (Medium coping): Kibra, Mathare*  
*Orange (High coping): All other subcounties*

The relatively uniform high coping levels, combined with significant spatial autocorrelation, suggest that technology coping spreads across subcounties through knowledge spillovers and regional business networks.

**Impact Visualization**

<img width="866" height="548" alt="image" src="https://github.com/user-attachments/assets/5b5da157-f1cf-445a-86bf-19f17bf8bbf1" />


The bar chart illustrates the decomposition of effects into direct, indirect, and total components for each significant variable. The chart clearly shows that variables like x_4 (Employees with New Technology) and x_6 (Operational Mode) have their largest impacts through spatial spillovers rather than direct effects.

## Key Insights

### Main Findings

1. **Spatial Effects Matter for Coping**: Among the four dimensions of technology adaptation, only coping with technology exhibits significant spatial dependence. This suggests that companies learn to manage technological challenges through regional networks and knowledge spillovers from neighbors.

2. **Universal Importance of ICT Competency**: ICT competency (x_1) is the strongest or among the strongest predictors across all four models, explaining variance in adoption, access, openness, and coping. This highlights the critical role of technical skills in all aspects of technology adaptation.

3. **Training Culture Creates Spillovers**: Willingness to continuous training (x_2) not only benefits individual firms but also creates significant positive spillovers to neighboring subcounties, especially for coping ability (total effect = 1.293).

4. **Technology Adoption Through Employees**: The presence of employees using new technology (x_4) has the largest spillover effect (3.222) on coping ability. Companies benefit substantially when neighboring firms have technologically proficient employees, likely through knowledge sharing and peer learning.

5. **Competitive Pressures from Online Operations**: Online business operations in neighboring areas (x_6) create significant negative spillovers (-3.281), suggesting competitive pressures that make it harder for nearby physical businesses to cope with technological change.

6. **Financial Barriers Are Not Universal**: Contrary to expectations, financial constraints (x_8, x_9) show limited or no significant effects across most models, suggesting that technology adaptation barriers are more related to skills and knowledge than pure financial capacity.

### Regional Patterns

- **High-performing subcounties**: Westlands, Dagoreti, and Embakasi consistently show higher levels across adoption, access, and openness dimensions
- **Emerging areas**: Kasarani shows high levels in adoption and access
- **Areas needing support**: Ruaraka (low access), Kibra and Mathare (medium coping)

### Policy Implications

1. **Invest in Regional Training Networks**: Given strong spillover effects from training (lag.x_2 = 1.160), regional training programs can benefit entire clusters of subcounties, not just individual firms.

2. **Promote Technology User Groups**: Encourage employees to share technology knowledge across companies and subcounties, leveraging the massive spillover effect (lag.x_4 = 3.222).

3. **Support Digital Transformation Education**: Mastering digital transformation (x_3) is consistently significant across all models, suggesting need for comprehensive digital business training.

4. **Address Competitive Pressures**: The negative spillover from online operations (lag.x_6 = -3.281) suggests physical businesses need support to compete with neighboring online businesses.

5. **Targeted Interventions**: Focus support on subcounties with lower performance (Ruaraka, Kibra, Mathare) while leveraging high-performing areas (Westlands, Dagoreti, Embakasi) as regional hubs for knowledge diffusion.

## Requirements

### R Packages

```r
library(readr)           # Data import
library(geodata)         # Geospatial data handling
library(sf)              # Simple features for spatial data
library(spdep)           # Spatial dependence analysis
library(spatialreg)      # Spatial regression models
library(dplyr)           # Data manipulation
library(tidyverse)       # Data wrangling ecosystem
library(ggplot2)         # Data visualization
```

### R Version
- R version 4.0 or higher recommended

### System Requirements
- Sufficient RAM for spatial computations (minimum 4GB recommended)
- GDAL libraries for spatial data processing

## Usage

### Running the Analysis

1. **Prepare your workspace**:
```r
setwd("path/to/your/project")
```

2. **Ensure data files are in the correct location**:
   - `Combined_Data.csv` in the working directory
   - `gadm41_KEN_2.shp` and associated files in the specified folder

3. **Open and run the R Markdown file**:
```r
rmarkdown::render("analysis.Rmd")
```

### Modifying the Analysis

To adapt this analysis for other regions or variables:

1. **Change the geographic filter** (line for Nairobi filtering):
```r
nairobi_spatial_data <- kenya_spatial_data %>%
  filter(NAME_1 == "YourRegion")
```

2. **Add or remove variables** in the model formulas:
```r
ols_model <- lm(y ~ x_1 + x_2 + your_new_variable, data = data_merged)
```

3. **Adjust spatial weights** if using different neighbor definitions:
```r
nb <- knn2nb(knearneigh(coordinates, k = 5))  # K-nearest neighbors instead
```

## Reproducibility Notes

- Random seed is not set for Monte Carlo simulations in impact measures. Results may vary slightly across runs.
- Spatial weights are based on shared borders (Queen contiguency). Alternative definitions may yield different results.
- Ordinal variables are treated as continuous (numeric 1-5). Alternative approaches include ordered logit/probit models.

## Limitations

1. **Cross-sectional data**: Analysis captures relationships at one point in time; causal inference is limited
2. **Self-reported measures**: Variables are based on company self-assessments, which may include response bias
3. **Aggregation level**: Analysis is at subcounty level; within-subcounty variation is not captured
4. **Temporal stability**: Spatial relationships may change over time as technology and business environments evolve

## Author

Aime 232

## Date

July 16, 2025


## References

- Anselin, L. (1988). Spatial Econometrics: Methods and Models. Kluwer Academic Publishers.
- LeSage, J., & Pace, R. K. (2009). Introduction to Spatial Econometrics. CRC Press.
- Bivand, R. S., Pebesma, E., & Gomez-Rubio, V. (2013). Applied Spatial Data Analysis with R. Springer.

## Contact

For questions or collaboration opportunities, please contact aimmug200507@gmail.com.
