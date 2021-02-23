Vitamin D Analysis
================
Carlos Dobler
February 22, 2021

Bivariate plots
===============

### Vit D vs. Edad

<img src="02_vitd_analysis_files/figure-markdown_github/edad-1.png" style="display: block; margin: auto;" />

### Vit D vs. Entidad

<img src="02_vitd_analysis_files/figure-markdown_github/entidad-1.png" style="display: block; margin: auto;" />

### Vit D vs. Latitude

<img src="02_vitd_analysis_files/figure-markdown_github/latitude-1.png" style="display: block; margin: auto;" />

### Vit D vs. Altitude

<img src="02_vitd_analysis_files/figure-markdown_github/altitude-1.png" style="display: block; margin: auto;" />

### Vit D vs. Ethnicity

<img src="02_vitd_analysis_files/figure-markdown_github/ethnicity-1.png" style="display: block; margin: auto;" />

Multivariate regression
=======================

Note: data used in this section include both tables (20-50 and over 60)

### Pairwise correlation matrix

First I assessed what explanatory variables may be intercorrelated (to avoid collinearity).

    ##             edad latitude altitud ethnicity
    ## edad       1.000    0.035  -0.033     0.060
    ## latitude   0.035    1.000   0.140     0.625
    ## altitud   -0.033    0.140   1.000    -0.200
    ## ethnicity  0.060    0.625  -0.200     1.000

As expected, ethnicity and latitude are highly correlated, so I only use one of them in the multivariate regressions.

### Regression (using latitude)

    ## 
    ## Call:
    ## lm(formula = vit_d ~ edad + latitude + altitud, data = db_20_60)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -59.148 -12.629  -1.028  11.188 129.095 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 74.9022876  1.5945853  46.973  < 2e-16 ***
    ## edad        -0.1637514  0.0215382  -7.603 4.28e-14 ***
    ## latitude     1.0023634  0.2927225   3.424 0.000628 ***
    ## altitud     -0.0073250  0.0004585 -15.977  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 19.35 on 2178 degrees of freedom
    ## Multiple R-squared:  0.1225, Adjusted R-squared:  0.1213 
    ## F-statistic: 101.4 on 3 and 2178 DF,  p-value: < 2.2e-16

The model shows a significant but very little capacity to predict Vit D levels using age, altitude, and latitude (these variables explain ~0.014 % of the variance in Vit D). However, the effect of all variables is significant. When controlling for the rest of the variables, edad and altitud have a negative relation with Vit D levels, while latitude has a positive relation with Vit D levels.
