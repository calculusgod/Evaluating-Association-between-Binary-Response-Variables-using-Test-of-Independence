
# Evaluating Association between Binary Response Variables using Test of Independence Based on Survey Data

## Overview
This project investigates the association between two binary response variables — voting behavior and income status — using classical and model-based statistical approaches. The analysis is conducted using survey data from the `voteincome` dataset available in the `ZeligChoice` package in R.

The study compares:
- Finite population chi-square tests
- Sample-based tests under SRSWOR
- Stratified sampling methods
- Model-based inference using the Bivariate Probit Model

The project also includes simulation studies to examine the empirical behavior of the test statistics under repeated sampling.

---

## Objectives
- Study the relationship between voting behavior and income status.
- Apply the Chi-square Test of Independence on finite population and sample data.
- Compare sample-based and model-based inference methods.
- Use auxiliary information through a Bivariate Probit Model.
- Evaluate the effect of stratified sampling.
- Verify whether the model-based test statistic follows a chi-square distribution.

---

## Dataset
The analysis uses the `voteincome` dataset from the `ZeligChoice` package.

### Variables Used
- `vote` → Binary voting status
- `income` → Income level
- `education` → Education level
- `age`
- `female`

### Data Transformation

```r
binary_income_status = 1 if income > median(income)
binary_income_status = 0 otherwise
```

---

## Methodology

### 1. Finite Population Analysis
- Construct a 2×2 contingency table.
- Apply Pearson’s Chi-square Test of Independence.

### 2. SRSWOR Sampling
- Draw repeated samples of size 200.
- Compute chi-square statistics and p-values.

### 3. Simulation Study
- Repeat sampling 1000 times.
- Compare empirical distributions with theoretical chi-square distributions.

### 4. Model-Based Inference
- Fit a Bivariate Probit Model using:

```r
zelig(cbind(vote, binary_income_status) ~ education,
      model = "bprobit")
```

- Estimate joint probabilities.
- Construct model-based test statistics.

### 5. Stratified Sampling
- Divide population using `binary_income_status`.
- Draw proportional stratified samples.
- Compare performance with SRSWOR.

### 6. Synthetic Population Generation
- Generate independent binary variables using the Bivariate Probit framework.
- Study asymptotic behavior of the test statistic.

---

## Statistical Framework

### Chi-square Test Statistic

```math
\chi^2 = \sum_{i=1}^{2}\sum_{j=1}^{2}\frac{(f_{ij}-E_{ij})^2}{E_{ij}}
```

where:
- \(f_{ij}\) = observed frequency
- \(E_{ij}\) = expected frequency under independence

---

## Bivariate Probit Model

```math
U_{1t} = \beta_0 + \beta x_t + \varepsilon_{1t}
```

```math
U_{2t} = \gamma_0 + \gamma x_t + \varepsilon_{2t}
```

with correlated error terms:

```math
\begin{pmatrix}
\varepsilon_{1t} \\
\varepsilon_{2t}
\end{pmatrix}
\sim
N\left(
\begin{pmatrix}
0 \\
0
\end{pmatrix},
\begin{pmatrix}
1 & \rho \\
\rho & 1
\end{pmatrix}
\right)
```

---

## Simulation Results

### Sample-Based Test
- 1000 SRSWOR simulations
- Empirical distribution approximately follows:

```math
\chi^2_1
```

- Approximate rejection rate: **53.8%**

### Model-Based Test
- Uses estimated probabilities from the Bivariate Probit Model
- Rejection rate: **89.3%**
- Produces more stable p-values compared to sample-only inference

### Stratified Sampling
- Provides more stable estimates than SRSWOR
- Model-based stratified inference produced rejection rates close to population-level inference

---

## Key Findings
- Voting behavior and income status show statistically significant association.
- Sample-based chi-square tests approximate theoretical distributions well.
- Model-based inference improves stability and accuracy.
- Stratified sampling reduces variability in estimation.
- Under independence, the model-based test statistic follows a chi-square distribution with 1 degree of freedom.

---

## Technologies Used
- **R Programming**
- `dplyr`
- `sampling`
- `Zelig`
- `ZeligChoice`
- `pbivnorm`

---

## Installation

Install required packages:

```r
install.packages("dplyr")
install.packages("sampling")
install.packages("pbivnorm")
install.packages("devtools")

devtools::install_github("IQSS/Zelig")
devtools::install_github("IQSS/ZeligChoice")
```

---

## Running the Project

Load required libraries:

```r
library(dplyr)
library(sampling)
library(Zelig)
library(ZeligChoice)
library(pbivnorm)
```

Load dataset:

```r
data(voteincome)
```

Run the analysis scripts for:
- Contingency tables
- Chi-square tests
- Simulations
- Stratified sampling
- Bivariate probit estimation

---

## References
1. Raymond L. Chambers and Robert G. Clark  
   *An Introduction to Model-Based Survey Sampling with Applications*

2. Takeshi Amemiya (1974)  
   *Bivariate Probit Analysis: Minimum Chi-square Methods*

3. A.M. Gun, M.K. Gupta, B. Dasgupta  
   *Fundamentals of Statistics (Volume 1)*

4. Zelig Statistical Software  
   https://zeligproject.org/

---

## Author

**Pritika Saha**  
Department of Statistics  
Presidency University, Kolkata

Under the supervision of:

**Dr. Sumanta Adhya**  
Assistant Professor  
West Bengal State University

---

## License
This project is intended for academic and educational purposes.
````
