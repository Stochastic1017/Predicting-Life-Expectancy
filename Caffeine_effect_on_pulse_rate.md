# Introduction

I am interested in conducting a rigorous statistical analysis to study
how caffeine affects pulse rate. In order to conduct this experiment, I
chose three of my friends as participants and had them consume 50 mg,
100 mg, and 200 mg caffeine pills on separate days and then recorded the
change in average pulse rate before and after the consumption of each
caffeine pill. It is well-studied in papers like [Gonzaga LA et
al.](https://www.nature.com/articles/s41598-017-14540-4) and [Karapetian
GK et al.](https://pubmed.ncbi.nlm.nih.gov/22499570/) that caffeine is
attributed to a subsequent decrease in pulse rate. This research however
studies the effect of caffeine on decrease in pulse rate specifically
based on quantity of caffeine consumed (50 mg, 100 mg, and 200 mg).

# Experimental Design

I chose a 3-by-3 Latin Square Design for this experiment with the
following parameters:

-   **`Day` \[blocking\]:**
    -   1: 04/24/2023
    -   2: 04/25/2023
    -   3: 04/26/2023

-   **`Participant` \[blocking\]:**
    -   1: age - 21, sex - female
    -   2: age - 20, sex - male
    -   3: age - 21, sex - male

-   **`Caffeine` \[treatment\]:**
    -   A: 50 mg
    -   B: 100 mg
    -   C: 200 mg.

-   **`Decrease` *y*<sub>*i**j**k*</sub> \[response\]:**
    -   *i*: `Day`, i.e., *i* = 1, 2, 3
    -   *j*: `Participant`, i.e., *j* = 1, 2, 3
    -   *k*: `Caffeine`, i.e., *k* = *A*, *B*, *C*

## Advantages of Design

1.  Allows us to block two nuisance variables we wish to keep separate
    (`Day` and `Participant`).

2.  Permits us to study 3 treatments simultaneously, with 2 blocking
    variables, each at 3 levels, i.e., test each caffeine pill (*k*),
    once on each participant (*j*), and on each day (*i*).

3.  Only 9 number of runs required, making our experiment both time and
    cost effective.

## Shortcomings of Design

1.  The number of levels of each blocking variable must be the same as
    the levels of treatment factor. As two of my participants are male,
    and one is female, the design does not allow us to block the
    confounding effect of gender.

2.  The experiment was not conducted in a controlled setting, any
    underlying confounding effects could not be controlled (such as the
    time of day at which a caffeine pill was consumed).

3.  Due to the non-replication nature of the design, no interaction
    effect between treatment and blocking variable can be studied.

# Setting Up Design

After randomizing experimental participants, along with the day, and
capsule consumption, the design used for this experiment is given below:

         Participant 1 Participant 2 Participant 3
    [1,] "A (y_11A)"   "C (y_12C)"   "B (y_13B)"  
    [2,] "B (y_21B)"   "A (y_22A)"   "C (y_23C)"  
    [3,] "C (y_31C)"   "B (y_32B)"   "A (y_33A)"  

The interpretation of the matrix is as follows:

-   **Day 1 \[04/24/2023\]:**

    -   Participant 1 takes 50 mg caffeine pill, i.e.,
        **y**<sub>**11****A**</sub>.
    -   Participant 2 takes 200 mg caffeine pill, i.e.,
        **y**<sub>**12****C**</sub>.
    -   Participant 3 takes 100 mg caffeine pill, i.e.,
        **y**<sub>**13****B**</sub>.

-   **Day 2 \[04/25/2023\]:**

    -   Participant 1 takes 100 mg caffeine pill, i.e.,
        **y**<sub>**21****B**</sub>.
    -   Participant 2 takes 50 mg caffeine pill, i.e.,
        **y**<sub>**22****A**</sub>.
    -   Participant 3 takes 200 mg caffeine pill, i.e.,
        **y**<sub>**23****C**</sub>.

-   **Day 3 \[04/26/2023\]:**

    -   Participant 1 takes 200 mg caffeine pill, i.e.,
        **y**<sub>**31****C**</sub>.
    -   Participant 2 takes 100 mg caffeine pill, i.e.,
        **y**<sub>**32****B**</sub>.
    -   Participant 3 takes 50 mg caffeine pill, i.e.,
        **y**<sub>**33****A**</sub>.

# Apparatus Used

To administer caffeine pills, I bought the [Nutricost Caffeine
Pills](https://www.amazon.com/dp/B01MY5CW7S?ref=ppx_yo2ov_dt_b_product_details&th=1)
100 mg per serving, 250 capsules bottle.

-   For 50 mg (A) caffeine, I administered half a capsule.

-   For 100 mg (B) caffeine, I administered one entire capsule.

-   For 200 mg (C), I administered two capsules.

To measure pulse rate, I used the [EMAY Bluetooth Pulse Oximeter
Fingertip](https://www.amazon.com/dp/B08FFHG69C?psc=1&ref=ppx_yo2ov_dt_b_product_details).

-   For initial measurements, I used the Oximeter for five minutes and
    recorded the data.

-   I then administered the designated dosage of caffeine pill, waited
    for approximately 45 minutes, then re-took measurements for 5
    minutes and recorded the data.

# Data Collected

## Day 1

### Participant 1 \[50 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-3-1.png)

    [1] "The difference in average pulse rate before and after consuming 50 mg pill for Participant 1 is 8.997 (y_11A)"

### Participant 2 \[200 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-6-1.png)

    [1] "The difference in average pulse rate before and after consuming 200 mg pill for Participant 2 is 12.323 (y_12C)"

### Participant 3 \[100 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-9-1.png)

    [1] "The difference in average pulse rate before and after consuming 100 mg caffeine pill for Participant 3 is 8.193 (y_13B)"

**Visualizing Data for Day 1**

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-11-1.png)

## Day 2

### Participant 1 \[100 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-13-1.png)

    [1] "The difference in average pulse rate before and after consumption of 100 mg pill in the afternoon for Participant 1 is 10.043 (y_21B)"

### Participant 2 \[50 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-16-1.png)

    [1] "The difference in average pulse rate before and after consuming 50 mg pill for Participant 2 is 9.667 (y_22A)"

### Participant 3 \[200 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-19-1.png)

    [1] "The difference in average pulse rate before and after consuming 200 mg pill for Participant 3 is 8.547 (y_23C)"

**Visualizing Data for Day 2**

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-21-1.png)

## Day 3

### Participant 1 \[200 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-23-1.png)

    [1] "The difference in average pulse rate before and after consuming 200 mg pill for Participant 1 is 14.547 (y_31C)"

### Participant 2 \[100 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-26-1.png)

    [1] "The difference in average pulse rate before and after consuming 100 mg pill for Participant 2 is 15.6 (y_32B)"

### Participant 3 \[50 mg\]

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-29-1.png)

    [1] "The difference in average pulse rate before and after consuming 50 mg pill for Participant 3 is 9.997 (y_33A)"

**Visualizing Data for Day 3**

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-31-1.png)

# Data Table

          Participant 1 Participant 2 Participant 3
    Day 1 "A (8.997)"   "C (12.323)"  "B (8.193)"  
    Day 2 "B (10.043)"  "A (9.667)"   "C (8.547)"  
    Day 3 "C (14.547)"  "B (15.6)"    "A (9.997)"  

      Participant Day Caffeine Decrease
    1           1   1        A    8.997
    2           2   1        C   12.323
    3           3   1        B    8.193
    4           1   2        B   10.043
    5           2   2        A    9.667
    6           3   2        C    8.547
    7           1   3        C   14.547
    8           2   3        B   15.600
    9           3   3        A    9.997

# Analysis of Variance \[ANOVA\]

## Linear Model for Latin Square Design

The linear model for our Latin Square Design is as follows:

*y*<sub>*i**j**k*</sub> = *η* + *α*<sub>*i*</sub> + *β*<sub>*j*</sub> + *τ*<sub>*k*</sub> + *ϵ*<sub>*i**j**k*</sub>

where:

-   *η* is the grand mean.

-   *α*<sub>*i*</sub> is the i-th row effect \[`Day`\]

-   *β*<sub>*j*</sub> is the j-th column effect \[`Participant`\]

-   *τ*<sub>*k*</sub> is the k-th treatment effect of the letters
    (*A*, *B*, *C*) \[`Caffeine`\]

-   *ϵ*<sub>*i**j**k*</sub> are independent *N*(0,*σ*<sup>2</sup>).

There are no interaction terms as they cannot be estimated in an
un-replicated experiment.

Using the zero-sum constraints, we have that:

*y*<sub>*i**j**k*</sub> = *η̂* + *α̂*<sub>*i*</sub> + *β̂*<sub>*j*</sub> + *τ̂*<sub>*k*</sub> + *r*<sub>*i**j**k*</sub>

where:

-   *η̂* = *ȳ*<sub>....</sub>

-   *α̂*<sub>*i*</sub> = (*ȳ*<sub>*i*..</sub>−*ȳ*<sub>...</sub>)

-   *β̂*<sub>*j*</sub> = (*ȳ*<sub>.*j*.</sub>−*ȳ*<sub>...</sub>)

-   *τ̂*<sub>*k*</sub> = (*ȳ*<sub>..*k*</sub>−*ȳ*<sub>...</sub>)

-   *r̂*<sub>*i**j**k*</sub> = (*y*<sub>*i**j**k*</sub>−*ȳ*<sub>*i*..</sub>−*ȳ*<sub>.*j*.</sub>−*ȳ*<sub>..*k*</sub>+2*ȳ*<sub>...</sub>)

Then, subtracting *ȳ*<sub>...</sub>, squaring both sides, and summing
over all observations, we have that:

∑<sub>(*i*,*j*,*k*) ∈ *S*</sub>(*y*<sub>*i**j**k*</sub>−*ȳ*<sub>...</sub>)<sup>2</sup> = ∑<sub>*i* ∈ {1, 2, 3}</sub>3(*ȳ*<sub>*i*..</sub>−*ȳ*<sub>...</sub>)<sup>2</sup> + ∑<sub>*j* ∈ {1, 2, 3}</sub>3(*ȳ*<sub>.*j*.</sub>−*ȳ*<sub>...</sub>)<sup>2</sup> + ∑<sub>*k* ∈ {*A*, *B*, *C*}</sub>3(*ȳ*<sub>..*k*</sub>−*ȳ*<sub>...</sub>)<sup>2</sup> + ∑<sub>(*i*,*j*,*k*) ∈ *S*</sub>(*y*<sub>*i**j**k*</sub>−*ȳ*<sub>*i*..</sub>−*ȳ*<sub>.*j*.</sub>−*ȳ*<sub>..*k*</sub>+2*ȳ*<sub>...</sub>)<sup>2</sup>

where the set of 3<sup>2</sup> values dictated by the particular Latin
square triplets (*i*,*j*,*k*) is denoted by *S*.

The above derivation tells us that the corrected total sum of squares on
the left equals the sum of the row sum of squares, column sum of
squares, treatment sum of squares, and residual sum of squares.

## Code for ANOVA Table Latin Square Design

``` r
## Degrees of Freedom
n = 3
df_row = n-1
df_col = n-1
df_treat = n-1
df_resid = (n-1)*(n-2)

## Grand mean
y_... = mean(data$Decrease)  

## Row Effects [Day]
y_i.. = c(mean(data[which(data$Participant == '1'), ]$Decrease), 
          mean(data[which(data$Participant == '2'), ]$Decrease), 
          mean(data[which(data$Participant == '3'), ]$Decrease))
SSE_row = n*sum((y_i.. - y_...)^2)
MSE_row = SSE_row/df_row

## Column Effects [Participant]
y_.j. = c(mean(data[which(data$Day == '1'), ]$Decrease), 
          mean(data[which(data$Day == '2'), ]$Decrease), 
          mean(data[which(data$Day == '3'), ]$Decrease))
SSE_col = n*sum((y_.j. - y_...)^2)
MSE_col = SSE_col/df_col

## Treatment Effects [Caffeine]
y_..k = c(mean(data[which(data$Caffeine == 'A'), ]$Decrease),
          mean(data[which(data$Caffeine == 'B'), ]$Decrease),
          mean(data[which(data$Caffeine == 'C'), ]$Decrease))
SSE_treat = n*sum((y_..k - y_...)^2)
MSE_treat = SSE_treat/df_treat

## Residuals
SSE_resid = sum((data$Decrease - y_...)^2) - SSE_row - SSE_col - SSE_treat
MSE_resid = SSE_resid/df_resid

## F-values
F_row = MSE_row/MSE_resid
F_col = MSE_col/MSE_resid
F_treat = MSE_treat/MSE_resid

## P-value
Pval_row = 1 - pf(F_row, 2, 2)
Pval_col = 1 - pf(F_col, 2, 2)
Pval_treat = 1 - pf(F_treat, 2, 2)
```

**ANOVA Table:**

    ##        Source Df    SSE    MSE       F  pval
    ## 1         Day  2 20.082 10.041 156.471 0.006
    ## 2 Participant  2 28.433 14.216 221.543 0.004
    ## 3    Caffeine  2  8.325  4.162  64.865 0.015
    ## 4   Residuals  2  0.128  0.064              
    ## 5      Totals  8 65.293 28.484

## Analysis of Latin Square Design ANOVA Table

The null hypothesis of our model is that there are no treatment effect
differences, i.e.,

*H*<sub>0</sub> : *τ*<sub>*i*</sub> = *τ*<sub>*j*</sub>  *f**o**r* *a**l**l* *i*, *j* ∈ {*A*, *B*, *C*}

The alternative hypothesis of our model is that there is at least one
treatment effect difference, i.e.,

*H*<sub>1</sub> : *τ*<sub>*i*</sub> ≠ *τ*<sub>*j*</sub>  *f**o**r* *s**o**m**e* *i*, *j* ∈ {*A*, *B*.*C*}

Given the degrees of freedom *n* − 1 = 3 − 1 = 2 and
(*n*−1)(*n*−2) = (2)(1) = 2, along with following F-values:

1.  F-statistic = 19 (coral)
2.  F-value \[`Day`\] = 156.471 (navyblue)
3.  F-value \[`Participant`\] = 221.453 (limegreen)
4.  F-value \[`Caffeine`\] = 64.865 (purple)

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-35-1.png)

We can see that both our blocking factors \[`Day` and `Participants`\]
are statistically significant, i.e., null hypothesis rejected as p-value
\< 0.05. This implies that even upon taking into account the effects of
Day and Participant on decrease in pulse rate after consuming caffeine
pill, those variables seem to have a significant effect on our analysis.

More importantly, we can see that the p-value of treatment factor
`Caffeine` is also lesser than 0.05, but greater than 0.01. This could
imply that among the three levels of the treatment factor, at least one
pair of group means is not significant. In order to study this, we
conduct a Tukey Multiple-Comparisons 95% family-wise confidence level
test.

## Tukey Multiple-Comparisons for ANOVA

``` r
require(multcomp)
Tukey_posthoc = confint(glht(lm(Decrease ~ Day + Participant + Caffeine, data), linfct = mcp(Caffeine = 'Tukey')))
Tukey_posthoc
```

    ## 
    ##   Simultaneous Confidence Intervals
    ## 
    ## Multiple Comparisons of Means: Tukey Contrasts
    ## 
    ## 
    ## Fit: lm(formula = Decrease ~ Day + Participant + Caffeine, data = data)
    ## 
    ## Quantile = 5.8868
    ## 95% family-wise confidence level
    ##  
    ## 
    ## Linear Hypotheses:
    ##            Estimate lwr     upr    
    ## B - A == 0  1.7250   0.5074  2.9426
    ## C - A == 0  2.2520   1.0344  3.4696
    ## C - B == 0  0.5270  -0.6906  1.7446

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-37-1.png)

We can see that the paired-groups B-A \[100 mg caffeine vs 50 mg
caffeine\] and groups C-A \[200 mg caffeine vs 50 mg caffeine\] are
statistically significant. However, the paired-group C-B \[200 mg vs 100
caffeine\] is not statistically significant. This could imply that the
effects of caffeine on pulse rate is most significant when taking over
50 mg, not when taking over 100 mg or 200 mg.

## Visual Interpretation of Inference

Given below is a summary table of our treatment factor group `Caffeine`
and its corresponding means and sd in relation to `Decrease`.

    ## # A tibble: 3 × 4
    ##   group count  mean    sd
    ##   <chr> <int> <dbl> <dbl>
    ## 1 A         3  9.55 0.510
    ## 2 B         3 11.3  3.85 
    ## 3 C         3 11.8  3.03

Given below is a 2d line plot where the x-axis is our treatment factor
`Caffeine` and y-axis is our response `Decrease`. This plot allows us to
see how the three levels of caffeine quantity affects response.

![](Caffeine_effect_on_pulse_rate_files/figure-markdown_github/unnamed-chunk-39-1.png)

# Conclusion

A 3-by-3 Latin Square Design was chosen to conduct this experiment with
factors: `Day`, `Participants`, `Caffeine`, and `Decrease`. The blockedc
nuisance factors were `Day` and `Participants`, the treatment factor to
be studied was `Caffeine` and the response variable was `Decrease`.
After randomizing the factors and setting up the design, pulse rate
measurements were taken before and after consumption of assigned
caffeine pill, and the difference in average pulse rates were recorded.
After 9 trials, wherein each of the three participant consumed each of
the three pills on each separate day, an ANOVA was conducted for Latin
Square Design using the Sum Squared and Mean Squared errors for each
factor group.

The ANOVA found that there is a statistical significance between the
quantity of caffeine consumed and the subsequent decrease in heart rate.
In particular, there seems to be a statistical significance between 50
mg - 100 mg caffeine group and 50 mg - 200 mg caffeine group. This can
also be confirmed visually as we can see that the mean of 50 mg caffeine
group is significantly lower than the mean of 100 mg and 200 mg caffeine
group. Additionally, the mean of 100 mg and 200 mg caffeine groups were
relatively the same, and no statistical significance was found between
them. It was also found that even after blocking, the variables `Day`
and `Participants` were both statistically significant. This would imply
that there are significant effects between the blocking variable and
response, however due to non-replication of the experiment, the
interaction effects could not be studied. Furthermore, The variance of
treatment group A is much lesser than the variance of treatment group B
and C, which suggests that variance between groups is constant. Both
these issues could be fixed with replication, unfortunately due to time
and cost constraints, no replication was conducted for this experiment.

Due to the nature of the design, only two nuisance factors could be
blocked: the day in which caffeine was consumed and the participant who
consumed the caffeine. My intuition for blocking these two variables
were that, tolerance would increase each day of caffeine consumption,
and the prior tolerances of each candidate could significantly affect
readings of pulse rate. That said, there were some very important
confounding variables that could not be blocked. For one, the time of
day at which the caffeine pill was consumed was a primary factor I
wished to block using a 3-by-3 Graeco-Squared design for the experiment,
but unfortunately no degrees of freedom were left after estimating
factorial effects. Additionally, the sex of the candidates could also
not be blocked as a Latin-Square design requires that the blocking
factors have the same levels as treatment factors, which is not the case
here. Lastly, the experiment could not be conducted in a controlled
setting. Although I had asked the participants to refrain from consuming
any caffeine for the three days the experiment had to be done, there was
no way of knowing if they truly adhered to the instructions.
Furthermore, I had to record their readings in stressful environments
like the library or a cafe, which could have further impeded the reading
as a result.

Although the results of the experiment were interesting (it might be
jarring to know that effect of caffeine pills on pulse rate is
significant for only 50+ mg pills, but not so much for 100+ and 200+
caffeine pills), it must be noted that there are significant effects
from other extraneous factors that randomization and blocking could not
negate. A good followup to this experiment would be to conduct one where
multiple factors could be blocked by the use of a 4-by-4 or 5-by-5
Hyper-Graeco Latin Square Design or a 3^k factorial design (or
fractional factorial depending on the resources available). Placebos can
also be incorporated in the study to take into account the effect of
caffeine perception on pulse-rate. Furthermore, many replicates of the
experiment could be conducted under these design, which could help
further negate the effects of blocking variables. The setting for the
experiments should also be more controlled, and incentives should be
provided to candidates so as to make sure they stick to the instructions
to allow for better quality of readings. Lastly, the health and
well-being of participants should be of utmost importance. Studies like
[Meredith SE et
al.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3777290/), [Sweeney et
al.](https://www.liebertpub.com/doi/10.1089/caff.2019.0020), and [Ali
Samaha](https://www.sciencedirect.com/science/article/pii/S2352340919312004)
have studied the effect of caffeine on physical and mental health in
great depth and have found that caffeine is not just an addictive
substance, but also has considerable negative impacts on stress and
heart-rate. An experiment involving caffeine must be conducted
carefully, with necessary precautions taken to ensure that the
participants physical and mental health are kept in check and unaffected
by caffeine pills.

# References

Ali Samaha and Ahmad (Al Tassi) and Najwa Yahfoufi and Maya Gebbawi and
Mohammad Rached and Mirna A. Fawaz. Data on the relationship between
caffeine addiction and stress among Lebanese medical students in
Lebanon. Data in Brief. Vol: 28. pp: 104845. doi:
<https://doi.org/10.1016/j.dib.2019.104845>.

Farag, Noha H. and Whitsett, Thomas L. and McKey, Barbara S. and Wilson,
Michael F. and Vincent, Andrea S. and Everson-Rose, Susan A. and
Lovallo, William R. Caffeine and Blood Pressure Response: Sex, Age, and
Hormonal Status. Journal of Women’s Health. Vol 19:6. pp: 1171-1176.
doi: 10.1089/jwh.2009.1664.

Gonzaga LA, Vanderlei LCM, Gomes RL, Valenti VE. Caffeine affects
autonomic control of heart rate and blood pressure recovery after
aerobic exercise in young adults: a crossover study. Sci Rep. 2017 Oct
26;7(1):14091. doi: 10.1038/s41598-017-14540-4. PMID: 29075019; PMCID:
PMC5658389.

Karapetian GK, Engels HJ, Gretebeck KA, Gretebeck RJ. Effect of caffeine
on LT, VT and HRVT. Int J Sports Med. 2012 Jul;33(7):507-13. doi:
10.1055/s-0032-1301904. Epub 2012 Apr 12. PMID: 22499570.

Meredith SE, Juliano LM, Hughes JR, Griffiths RR. Caffeine Use Disorder:
A Comprehensive Review and Research Agenda. J Caffeine Res. 2013
Sep;3(3):114-130. doi: 10.1089/jcr.2013.0016. PMID: 24761279; PMCID:
PMC3777290.

Sweeney, Mary M. and Weaver, Darian C. and Vincent, Kathryn B. and
Arria, Amelia M. and Griffiths, Roland R. Prevalence and Correlates of
Caffeine Use Disorder Symptoms Among a United States Sample. Journal of
Caffeine and Adenosine Research. Vol 10:1. pp: 4-11. doi:
10.1089/caff.2019.0020.

Valentina Rakic and Valerie Burke and Lawrence J. Beilin. Effects of
Coffee on Ambulatory Blood Pressure in Older Men and Women.
Hypertension. Vol 33:3. pp: 869-873. doi: 10.1161/01.HYP.33.3.869.
