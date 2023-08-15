# Predicting Life Expectancy Using Various Fundamental Global Demographical, Economic, Envirnomental, and Health Indicators

**Note: This is a much shorter version of the actual paper. The README does not contain many crucial plots used to conduct the following analysis. The html file to view the entire project can be found [here]().**

# Introduction

Our team is interested in modeling **Life Expectancy** using a
combination of various fundamental global indicators available at the 
[World Bank](https://databank.worldbank.org/home). Among the
various indicators for which data was available, we chose only those
with sufficient data provided for most countries, had the latest data no
older than three years, and were seemingly unrelated to other indicators
to mitigate any multi-collinearity issues.

After careful consideration, we chose **Population Density, GDP per
Capita, Fertility Rate, CO2 emissions, Unemployment Rate, Death Rate,
Urban Population, Diabetes** and **Inflation** as our leading indicators
to try and predict Life Expectancy. We collated the latest available
data for all indicators into one excel sheet and loaded the data set in
Rstudio to run our analysis.

Our main goal with this was to apply a Multiple Linear Regression Model
(MLRM) using the most useful and significant indicators to accurately
model and predict Life Expectancy.

# Question of Interest

Using nine various fundamental global indicators, i.e., Population
Density, GDP Per Capita, Fertility Rate, Unemployment, CO2, Death Rate,
Urban Population, Diabetes, and Inflation, which ones are the most
significant to model and predict Life Expectancy using Multiple Linear
Regression Model (MLRM)?

# About the Dataset

`Life.Exp`: **Life expectancy at birth, total (years) (2019)** - Life
expectancy at birth indicates the number of years a newborn infant would
live if prevailing patterns of mortality at the time of its birth were
to stay the same throughout its life. [Life.Exp
Dataset](https://data.worldbank.org/indicator/SP.DYN.LE00.IN?view=chart)

`Pop.Dens`: **Population density (people per sq. km of land area)
(2020)** - Population density is midyear population divided by land area
in square kilometers. Population is based on the de facto definition of
population, which counts all residents regardless of legal status or
citizenship–except for refugees not permanently settled in the country
of asylum, who are generally considered part of the population of their
country of origin. Land area is a country’s total area, excluding area
under inland water bodies, national claims to continental shelf, and
exclusive economic zones. In most cases the definition of inland water
bodies includes major rivers and lakes. [Pop.Dens
Dataset](https://data.worldbank.org/indicator/EN.POP.DNST?view=chart)

`GDP.PerCap`: **GDP per capita (current US$) (2020)** - GDP per capita
is gross domestic product divided by midyear population. GDP is the sum
of gross value added by all resident producers in the economy plus any
product taxes and minus any subsidies not included in the value of the
products. It is calculated without making deductions for depreciation of
fabricated assets or for depletion and degradation of natural resources.
Data are in current U.S. dollars. [GDP
Dataset](https://data.worldbank.org/indicator/NY.GDP.PCAP.CD?view=chart)

`Fert.Rate`: **Fertility rate, total (births per woman) (2020)** - Total
fertility rate represents the number of children that would be born to a
woman if she were to live to the end of her childbearing years and bear
children in accordance with age-specific fertility rates of the
specified year. [Fert.Rate
Dataset](https://data.worldbank.org/indicator/SP.DYN.TFRT.IN?view=chart)

`Unemp`: **Unemployment, total (% of total labor force) (modeled ILO
estimate) (2021)** - Unemployment refers to the share of the labor force
that is without work but available for and seeking employment. [Unemp
Dataset](https://data.worldbank.org/indicator/SL.UEM.TOTL.ZS?view=chart)

`CO2`: **CO2 emissions (metric tons per capita) (2019)** - Carbon
dioxide emissions are those stemming from the burning of fossil fuels
and the manufacture of cement.nThey include carbon dioxide produced
during consumption of solid, liquid, and gas fuels and gas flaring. [CO2
Dataset](https://data.worldbank.org/indicator/EN.ATM.CO2E.PC?view=chart)

`Death.Rate`: **Death rate, crude (per 1,000 people)** - Crude death
rate indicates the number of deaths occurring during the year, per 1,000
population estimated at midyear. Subtracting the crude death rate from
the crude birth rate provides the rate of natural increase, which is
equal to the rate of population change in the absence of migration.
[Death.Rate
Dataset](https://data.worldbank.org/indicator/SP.DYN.CDRT.IN?view=chart)

`Urban.Pop`: **Urban population (% of total population) (2021)** - Urban
population refers to people living in urban areas as defined by national
statistical offices. The data are collected and smoothed by United
Nations Population Division. [Urban.Pop
Dataset](https://data.worldbank.org/indicator/SP.URB.TOTL.IN.ZS?view=chart)

`Diabetes`: **Diabetes prevalence (% of population ages 20 to 79)
(2021)** - Diabetes prevalence refers to the percentage of people ages
20-79 who have type 1 or type 2 diabetes. It is calculated by adjusting
to a standard population age-structure. [Diabetes
Dataset](https://data.worldbank.org/indicator/SH.STA.DIAB.ZS?view=chart)

`Inflation`: **Inflation, consumer prices (annual %) (2019)** -
Inflation as measured by the consumer price index reflects the annual
percentage change in the cost to the average consumer of acquiring a
basket of goods and services that may be fixed or changed at specified
intervals, such as yearly. [Inflation
Dataset](https://data.worldbank.org/indicator/FP.CPI.TOTL.ZG?view=chart)

*Note: some data points have no values associated to it. In order to fix
this, we ran the na.omit() function to eliminate all rows with empty
parameters. That being said, it is essential to acknowledge that
omitting rows with empty parameters may cause a bias in our data as we
will be removing many developing/under-developed from our dataset
thereby causing us to only look at those countries which have the data
to provide.*

Many of the predictor variables are heavily skewed to the right due to the presence of extreme outliers. 
In order to rectify these issues, our team chose to use the logarithmic scaling for the necessary variables in order to make our predictors resemble a Gaussian distribution and reduce the effect of outliers.

```{r, echo = F}
data$Pop.Dens <- log(data$Pop.Dens)
data$GDP <- log(data$GDP)
data$Fert.Rate <- log(data$Fert.Rate)
data$Infl <- sign(data$Infl) * log(abs(data$Infl))
data$CO2 <- log(data$CO2)
data$Diabetes <- log(data$Diabetes)
data$Unemp <- log(data$Unemp)
```

# Fitting Preliminary MLRM and Checking for Multi-Collinearity

Life Expectancy ~ Log Unemployment and Life Expectancy ~
Death Rate do not follow a linear trend, i.e., they cannot be
effectively modeled by a linear function. Therefore, our team chose to
remove those variables from our MLR model as we deemed that they are not
useful in predicting Life Expectancy.

## Fitting first MLRM with 7 Variables, i.e., Model 0

``` r
model_0 <- lm(Life.Exp ~ Pop.Dens + GDP + Fert.Rate + CO2 + Urban.Pop + Diabetes + Infl, data)
summary(model_0)
```

    ## 
    ## Call:
    ## lm(formula = Life.Exp ~ Pop.Dens + GDP + Fert.Rate + CO2 + Urban.Pop + 
    ##     Diabetes + Infl, data = data)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -10.548  -1.554   0.262   1.822   7.620 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 54.24551    3.95919  13.701  < 2e-16 ***
    ## Pop.Dens     0.21206    0.18816   1.127   0.2611    
    ## GDP          2.20161    0.40122   5.487 1.23e-07 ***
    ## Fert.Rate   -7.71249    0.90983  -8.477 5.16e-15 ***
    ## CO2         -0.48984    0.38295  -1.279   0.2023    
    ## Urban.Pop    0.03247    0.01566   2.074   0.0394 *  
    ## Diabetes     1.84017    0.45015   4.088 6.31e-05 ***
    ## Infl        -0.42070    0.22911  -1.836   0.0678 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.074 on 199 degrees of freedom
    ## Multiple R-squared:  0.8191, Adjusted R-squared:  0.8127 
    ## F-statistic: 128.7 on 7 and 199 DF,  p-value: < 2.2e-16

## Checking for Multi-Collinearity for Model 0

``` r
vif(model_0)
```

    ##  Pop.Dens       GDP Fert.Rate       CO2 Urban.Pop  Diabetes      Infl 
    ##  1.200707  6.384505  3.458967  5.642539  2.424800  1.265287  1.175767

As we can see that two predictors have a Variance Inflation Factor
(VIF) \> 5, i.e., Log GDP Per Capita and Log CO2. This suggests that
there is a multi-collinearity issue between those two predictors.

The multi-collinearity can be explained as a high GDP Per Capita implies
that, on average, there is more production in the economy by resident
producers, which implies that there is more CO2 emissions to facilitate
those productions.

Therefore, in order to address this multi-collinearity issue, our team
chose to remove Log CO2 from our model and continue our analysis on the
MLRM with the remaining variables.

## Fitting second MLRM with remaining 6 Variables, i.e., model 1

``` r
model_1 <- lm(Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + Infl, data)
summary(model_1)
```

    ## 
    ## Call:
    ## lm(formula = Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + 
    ##     Diabetes + Infl, data = data)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -10.4430  -1.6313   0.2067   1.8116   7.2264 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 56.42119    3.58088  15.756  < 2e-16 ***
    ## Pop.Dens     0.26197    0.18436   1.421 0.156885    
    ## GDP          1.92928    0.34061   5.664 5.09e-08 ***
    ## Fert.Rate   -7.37950    0.87318  -8.451 5.93e-15 ***
    ## Urban.Pop    0.02815    0.01531   1.838 0.067490 .  
    ## Diabetes     1.62119    0.41699   3.888 0.000138 ***
    ## Infl        -0.42881    0.22939  -1.869 0.063032 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.079 on 200 degrees of freedom
    ## Multiple R-squared:  0.8176, Adjusted R-squared:  0.8121 
    ## F-statistic: 149.4 on 6 and 200 DF,  p-value: < 2.2e-16

## Checking for Multi-Collinearity for model 1

``` r
vif(model_1)
```

    ##  Pop.Dens       GDP Fert.Rate Urban.Pop  Diabetes      Infl 
    ##  1.149079  4.586719  3.175784  2.311755  1.082286  1.174867

As all our predictors have VIF \< 5, we can conclude that our model no
longer shows a multi-collinarity issue. Thus allowing us to run Goodness
of Fit and F-tests to see which of our variables are most useful.

## Conducting Goodness of Fit Test and F-tests to Check for Useful Predictors

### To check if at least one predictor is useful in model 1

In order to know if any of our predictors are useful, we can do the
Goodness of Fit Test and calculate an F-statistic where:

Null Model (*H*<sub>0</sub>) is that none of the variables are useful,
i.e.,
*H*<sub>0</sub> : *β*<sub>*j*</sub> = 0   ∀*j*

Alternative Model (*H*<sub>*A*</sub>) is that at least one variable is
useful, i.e.,
*H*<sub>*A*</sub> : *β*<sub>*j*</sub> ≠ 0   ∃*j*

``` r
Y = data$Life.Exp
n = length(Y)
SST = sum((Y - mean(Y))^2)
SSE = sum(resid(model_1)^2)
MSE = SSE / model_1$df.residual
SSR = SST - SSE
MSR = SSR / (n - 1 - model_1$df.residual)
F = MSR / MSE
alpha = 0.05
pval = 1 - pf(F,6,200) # from the summary(model_1) table
out = data.frame(SSE_RM = SST,SSE_FM = SSE, F=F, pval = pval,Fcrit=qf(1-alpha,6,200))

print(out)
```

    ##     SSE_RM   SSE_FM        F pval    Fcrit
    ## 1 10392.01 1895.768 149.3897    0 2.144133

As our F-statistic 149.39 is much greater than F-critical 2.14, which
has an extremely low corresponding p-value ≈ 0, we favor the alternative
hypothesis over the null hypothesis, i.e., at least one of the
predictors is useful.

### To check the usefulness of each predictor in model 1, assuming all other predictors remain constant

In order to test if each individual predictor is useful, we conduct
F-tests (assuming all other predictors remain constant) by running an
ANOVA (reduced model, full model) tests where reduced model = full model
without *j* variable, and:

Null Model (*H*<sub>0</sub>) is that *j* variable is not useful, i.e.,
*H*<sub>0</sub> : *β*<sub>*j*</sub> = 0   for  *j*

Alternative Model (*H*<sub>*A*</sub>) is that *j* variable is useful,
i.e.,
*H*<sub>0</sub> : *β*<sub>*j*</sub> ≠ 0   for  *j*

**For Log Population Density:**

``` r
RM = lm(Life.Exp ~ GDP + Fert.Rate + Urban.Pop + Diabetes + Infl, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ GDP + Fert.Rate + Urban.Pop + Diabetes + Infl
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F Pr(>F)
    ## 1    201 1914.9                           
    ## 2    200 1895.8  1    19.139 2.0191 0.1569

**For Log GDP Per Capita**

``` r
RM = lm(Life.Exp ~ Pop.Dens + Fert.Rate + Urban.Pop + Diabetes + Infl, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ Pop.Dens + Fert.Rate + Urban.Pop + Diabetes + Infl
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)    
    ## 1    201 2199.9                                 
    ## 2    200 1895.8  1    304.11 32.083 5.09e-08 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

**For Log Fertility Rate**

``` r
RM = lm(Life.Exp ~ Pop.Dens + GDP + Urban.Pop + Diabetes + Infl, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ Pop.Dens + GDP + Urban.Pop + Diabetes + Infl
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)    
    ## 1    201 2572.8                                 
    ## 2    200 1895.8  1    677.02 71.424 5.93e-15 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

**For Urban Population**

``` r
RM = lm(Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Diabetes + Infl, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Diabetes + Infl
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F  Pr(>F)  
    ## 1    201 1927.8                              
    ## 2    200 1895.8  1    32.035 3.3796 0.06749 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

**For Log Diabetes**

``` r
RM = lm(Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Infl, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Infl
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    201 2039.0                                  
    ## 2    200 1895.8  1    143.28 15.115 0.0001376 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

**For Log Inflation**

``` r
RM = lm(Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes, data)
anova(RM, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F  Pr(>F)  
    ## 1    201 1928.9                              
    ## 2    200 1895.8  1    33.124 3.4946 0.06303 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

### Using Holm-Bonferroni method to control family-wise error rate (FWER) and conduct our F-tests

Since we are conducting a non-trivial number of tests, it is essential
to first control our Family-Wise Error Rate (FWER) and Type I error rate
before conducting our hypothesis analysis.

In order to control our FWER, we first sort our test p-values from
lowest to highest.

    ## [1] 5.929998e-15 5.090365e-08 1.375582e-04 6.303207e-02 6.748985e-02
    ## [6] 1.568848e-01

Then, we match the smallest p-value with the significance level *α*/*m*,
then match the next smallest one to *α*/(*m*−1), then match the next to
*α*/(*m*−2), etc… until we match the largest to *α*.

``` r
pvals2 <- c(0.05/6)

for(i in 1:5)
{
  new_value = 0.05/(6 - i)
  pvals2 <- c(pvals2, new_value)
}
pvals2
```

    ## [1] 0.008333333 0.010000000 0.012500000 0.016666667 0.025000000 0.050000000

We then look for the first time a p-value is greater than a significance
level, and reject every p-value before that point

    ## [1] 5.929998e-15 5.090365e-08 1.375582e-04

Therefore, by conducting F-tests with Holm-Bonferroni method to control
our FWER and Type 1 error rate, we conclude that our significant
predictors are **Log GDP Per Capita, Log Fertility Rate**, and **Log
Diabetes.**

### Confidence Interval Test

```{r, echo = F}
confint(model_1, level = 0.95)
```

    ##                    2.5 %      97.5 %
    ## (Intercept) 49.360064886 63.48232090
    ## Pop.Dens    -0.101569838  0.62550621
    ## GDP          1.257629404  2.60092698
    ## Fert.Rate   -9.101322909 -5.65768374
    ## Urban.Pop   -0.002044203  0.05833624
    ## Diabetes     0.798933032  2.44345103
    ## Infl        -0.881131650  0.02351654

As the predictors with 0 in their respective 95% confidence interval are
not significant, we can conclude that **Log Population Density, Urban
Population** and **Log Inflation** are not significant, and thus we
remove them from our model.

# Fitting Final MLRM with the remaining 3 Predictors (model 2)

``` r
model_2 <- lm(Life.Exp ~ GDP + Fert.Rate + Diabetes, data)
summary(model_2)
```

    ## 
    ## Call:
    ## lm(formula = Life.Exp ~ GDP + Fert.Rate + Diabetes, data = data)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -10.9648  -1.8005   0.1864   1.8503   7.6034 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  55.8584     3.1189  17.909  < 2e-16 ***
    ## GDP           2.3237     0.2707   8.585 2.38e-15 ***
    ## Fert.Rate    -7.6453     0.8442  -9.057  < 2e-16 ***
    ## Diabetes      1.5410     0.4188   3.680 0.000299 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.122 on 203 degrees of freedom
    ## Multiple R-squared:  0.8096, Adjusted R-squared:  0.8068 
    ## F-statistic: 287.7 on 3 and 203 DF,  p-value: < 2.2e-16

## Running Goodness of Fit test to check if model 2 is more useful than model 1

To verify our conclusion, we can run another F-test using anova(model 2,
model 1), where:

Null hypothesis (*H*<sub>0</sub>) is that the subset of predictors are
not useful, i.e.,
*H*<sub>0</sub> : *β*<sub>*j*</sub> = 0   *w**h**e**r**e* *j* ∈ *I*

Alternative hypothesis (*H*<sub>*A*</sub>) is that at least one of the
subset of predictors is useful, i.e.,
*H*<sub>*A*</sub> : *β*<sub>*j*</sub> ≠ 0   *w**h**e**r**e* *j* ∈ *I*
and *I* is our set of subset predictors

``` r
anova(model_2, model_1)
```

    ## Analysis of Variance Table
    ## 
    ## Model 1: Life.Exp ~ GDP + Fert.Rate + Diabetes
    ## Model 2: Life.Exp ~ Pop.Dens + GDP + Fert.Rate + Urban.Pop + Diabetes + 
    ##     Infl
    ##   Res.Df    RSS Df Sum of Sq      F  Pr(>F)  
    ## 1    203 1978.6                              
    ## 2    200 1895.8  3    82.874 2.9144 0.03545 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

As p-value \< 0.05, we reject the null hypothesis and conclude that
**model 2 is a more useful in predicting Life Expectancy than model 1**.

## Running Necessary Diagnostics and Interpreting Final MLR model

### Checking for multi-collinearity

```
vif(model_2)
```

    ##       GDP Fert.Rate  Diabetes 
    ##  2.816757  2.886539  1.061568

As all our VIF values are \< 5, we can conclude that there is no issues
of multi-collinearity in our model. This can also be confirmed by
looking at the correlation heat map, i.e., all combinations of
predictors have different shades of color.

### Running Diagnostic Tests to check for MLR Assumptions

The Residuals vs Fitted plot is uniformly distributed along the 0 line.
This confirms our assumption that the model is relatively linear.

The Scale-Location shows no clear pattern among the residuals. This
satisfies Homoskedasticity assumption for our multiple linear model.

The Normal Q-Q plot is more or less consistent with the straight line
with minor deviations in the bottom left. Therefore, we can conclude
that our model has residuals that are approximately normally
distributed.

The Residuals vs Leverage plot shows us that there exists no extreme
points with high leverage or within the cooks distance which could
hugely influence our linear model.

### Interpreting Summary Table for Model 2

<table style="border-collapse:collapse; border:none;">
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">
 
</th>
<th colspan="8" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">
Life.Exp
</th>
</tr>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  text-align:left; ">
Predictors
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">
Estimates
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">
std. Error
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">
std. Beta
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">
standardized std. Error
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">
CI
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  col7">
standardized CI
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  col8">
Statistic
</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  col9">
p
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">
(Intercept)
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
55.86
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
3.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
-0.00
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.03
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
49.71 – 62.01
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col7">
-0.06 – 0.06
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col8">
17.91
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col9">
<strong>\<0.001</strong>
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">
GDP
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
2.32
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.27
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.44
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
1.79 – 2.86
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col7">
0.34 – 0.54
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col8">
8.58
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col9">
<strong>\<0.001</strong>
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">
Fert Rate
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
-7.65
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.84
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
-0.47
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.05
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
-9.31 – -5.98
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col7">
-0.57 – -0.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col8">
-9.06
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col9">
<strong>\<0.001</strong>
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">
Diabetes
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
1.54
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.42
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.12
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.03
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">
0.72 – 2.37
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col7">
0.05 – 0.18
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col8">
3.68
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  col9">
<strong>\<0.001</strong>
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">
Observations
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="8">
207
</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">
R<sup>2</sup> / R<sup>2</sup> adjusted
</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="8">
0.810 / 0.807
</td>
</tr>
</table>

<br> Therefore, we can see that our MLRM is of the form
$$\hat{(\text{Life.Exp})}\_i = (55.86) + (2.32) \cdot (\text{Log GDP})\_{i} - (7.65) \cdot (\text{Log Fert.Rate})\_{i} + (1.54) \cdot (\text{Log Diabetes})\_{i}$$

We can also see that all our predictors (including the intercept) are
significant, and our model explains ≈ 81% of variation in Life
Expectancy.

# Summary and Conclusion

We created a dataset by choosing various fundamental global indicators
from the World Bank in an attempt to try and predict Life Expectancy.
Our chosen indicators were Population Density, GDP per Capita, Fertility
Rate, CO2 emissions, Unemployment Rate, Death Rate, Urban Population,
Diabetes and Inflation.

Next, we plotted histogram/boxplots/density plots for all predictors,
and did the required log transformation to try and get our data to be
more normally distributed and to account for extreme outliers.

After the transformations, we plotted 9 scatter plots, each with Life
expectancy in the y-axis and the predictors in the x-axis. We noticed
that Life Expectancy ~ Log Unemployment and Life Expectancy ~ Death Rate
had negligible R squared (and negative Adjusted R squared), thus we
removed those predictors from our model.

With the remaining predictors, we fit a preliminary MLRM and ran the
variance Inflation Factor (VIF) function to check for
multi-collinearity. As Log GDP and Log CO2 had a VIF  \> 5, we chose to
eliminate Log CO2 as a predictor and checked that the new VIFs  \< 5.

We used the Goodness of Fit Test using nested models to check the
usefulness of each predictor, i.e., to see if the predictors are
significant to our model (assuming all other predictors remain fixed).
We chose to run Holm-Bonferroni method to control the family-wise error
and type 1 error rate. We noticed that Log GDP Per Capita, Log Fertility
Rate and Log Diabetes were the significant variables to our model. We
also confirmed our analysis by looking at the confidence intervals and
running a final Goodness of Fit Test to check if our newest model was
more useful in predicting Life Expectancy than our previous model.

Finally, we fit final MLR model, plotted some exploratory graphs, and
ran some basic diagnostic plots to confirm that all assumptions of MLR
have been met and concluded that our model is a good fit where all
predictors (including intercept) are significant and explains
approximately 81% of the variation in Life Expectancy.
