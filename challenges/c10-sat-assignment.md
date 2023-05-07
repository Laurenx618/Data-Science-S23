SAT and College Grades
================
(Your name here)
2020-

- [Grading Rubric](#grading-rubric)
  - [Individual](#individual)
  - [Due Date](#due-date)
- [Obtain the Data](#obtain-the-data)
  - [**q1** Visit the SAT and College GPA case study page, scroll to the
    bottom, and click the `Open Data with Excel` button. This will allow
    you to download an `xls` file. Save the file to your `data` folder,
    load the data as `df_sat`, and perform your “first checks” against
    these data. Answer the questions
    below:](#q1-visit-the-sat-and-college-gpa-case-study-page-scroll-to-the-bottom-and-click-the-open-data-with-excel-button-this-will-allow-you-to-download-an-xls-file-save-the-file-to-your-data-folder-load-the-data-as-df_sat-and-perform-your-first-checks-against-these-data-answer-the-questions-below)
- [Analysis with Hypothesis Testing](#analysis-with-hypothesis-testing)
  - [View 1: Correlations](#view-1-correlations)
    - [**q2** Create a *single* plot that shows `univ_GPA` against
      *both* `high_GPA` and `both_SAT`. Visually compare the two
      trends.](#q2-create-a-single-plot-that-shows-univ_gpa-against-both-high_gpa-and-both_sat-visually-compare-the-two-trends)
    - [Hypothesis Testing with a Correlation
      Coefficient](#hypothesis-testing-with-a-correlation-coefficient)
    - [**q3** Plot histograms for `both_SAT, high_GPA, univ_GPA`.
      Which—if any—of the variables look approximately normally
      distributed.](#q3-plot-histograms-for-both_sat-high_gpa-univ_gpa-whichif-anyof-the-variables-look-approximately-normally-distributed)
    - [**q4** Use the function `cor.test()` to construct confidence
      intervals for `corr[high_GPA, univ_GPA` and
      `corr[both_SAT, univ_GPA]`. Answer the questions
      below.](#q4-use-the-function-cortest-to-construct-confidence-intervals-for-corrhigh_gpa-univ_gpa-and-corrboth_sat-univ_gpa-answer-the-questions-below)
    - [**q5** Use the bootstrap to approximate a confidence
      interval.](#q5-use-the-bootstrap-to-approximate-a-confidence-interval)
  - [View 2: Modeling](#view-2-modeling)
    - [Hypothesis Testing with a
      Model](#hypothesis-testing-with-a-model)
    - [**q6** Fit a linear model predicting `univ_GPA` with the
      predictor `both_SAT`. Assess the model to determine how effective
      a predictor `both_SAT` is for `univ_GPA`. Interpret the resulting
      confidence interval for the coefficient on
      `both_SAT`.](#q6-fit-a-linear-model-predicting-univ_gpa-with-the-predictor-both_sat-assess-the-model-to-determine-how-effective-a-predictor-both_sat-is-for-univ_gpa-interpret-the-resulting-confidence-interval-for-the-coefficient-on-both_sat)
    - [**q7** Fit a model predicting `univ_GPA` using both `high_GPA`
      and `both_SAT`. Compare the prediction accuracy and hypothesis
      test
      results.](#q7-fit-a-model-predicting-univ_gpa-using-both-high_gpa-and-both_sat-compare-the-prediction-accuracy-and-hypothesis-test-results)
  - [Synthesize](#synthesize)
    - [**q8** Using the results from all previous q’s, answer the
      following
      questions.](#q8-using-the-results-from-all-previous-qs-answer-the-following-questions)
- [End Notes](#end-notes)

*Purpose*: How do we apply hypothesis testing to investigating data? In
this challenge you’ll practice using hypothesis testing tools to make
sense of a dataset.

*Reading*: - [Harvard Study Says SATs Should Be Optional: Here’s
Why](https://www.csmonitor.com/USA/USA-Update/2016/0120/Harvard-study-says-SATs-should-be-optional.-Here-s-why)
(Optional); easy-to-read news article on colleges going SAT-free -
[Norm-Referenced Tests and Race-Blind
Admissions](https://cshe.berkeley.edu/publications/norm-referenced-tests-and-race-blind-admissions-case-eliminating-sat-and-act-university)
(Optional); technical report on relationship between the SAT/ACT and
non-academic factors

*Credit*: This is based on a [case
study](http://onlinestatbook.com/2/case_studies/sat.html) originally
prepared by Emily Zitek, with data collected through the research of
Thomas MacFarland.

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.2.3

    ## Warning: package 'ggplot2' was built under R version 4.2.3

    ## Warning: package 'stringr' was built under R version 4.2.3

    ## Warning: package 'forcats' was built under R version 4.2.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.0.9     ✔ readr     2.1.2
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.2     ✔ tibble    3.1.8
    ## ✔ lubridate 1.8.0     ✔ tidyr     1.2.0
    ## ✔ purrr     0.3.4     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the ]8;;http://conflicted.r-lib.org/conflicted package]8;; to force all conflicts to become errors

``` r
library(readxl)
library(broom)
```

    ## Warning: package 'broom' was built under R version 4.2.3

``` r
library(modelr)
```

    ## Warning: package 'modelr' was built under R version 4.2.3

    ## 
    ## Attaching package: 'modelr'
    ## 
    ## The following object is masked from 'package:broom':
    ## 
    ##     bootstrap

``` r
library(rsample)
```

<!-- include-rubric -->

# Grading Rubric

<!-- -------------------------------------------------- -->

Unlike exercises, **challenges will be graded**. The following rubrics
define how you will be graded, both on an individual and team basis.

## Individual

<!-- ------------------------- -->

| Category    | Needs Improvement                                                                                                | Satisfactory                                                                                                               |
|-------------|------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| Effort      | Some task **q**’s left unattempted                                                                               | All task **q**’s attempted                                                                                                 |
| Observed    | Did not document observations, or observations incorrect                                                         | Documented correct observations based on analysis                                                                          |
| Supported   | Some observations not clearly supported by analysis                                                              | All observations clearly supported by analysis (table, graph, etc.)                                                        |
| Assessed    | Observations include claims not supported by the data, or reflect a level of certainty not warranted by the data | Observations are appropriately qualified by the quality & relevance of the data and (in)conclusiveness of the support      |
| Specified   | Uses the phrase “more data are necessary” without clarification                                                  | Any statement that “more data are necessary” specifies which *specific* data are needed to answer what *specific* question |
| Code Styled | Violations of the [style guide](https://style.tidyverse.org/) hinder readability                                 | Code sufficiently close to the [style guide](https://style.tidyverse.org/)                                                 |

## Due Date

<!-- ------------------------- -->

All the deliverables stated in the rubrics above are due **at midnight**
before the day of the class discussion of the challenge. See the
[Syllabus](https://docs.google.com/document/d/1qeP6DUS8Djq_A0HMllMqsSqX3a9dbcx1/edit?usp=sharing&ouid=110386251748498665069&rtpof=true&sd=true)
for more information.

*Background*: Every year about 2 million students take the Scholastic
Aptitude Test (SAT). The exam is
[controversial](http://www.nea.org/home/73288.htm) but [extremely
consequential](https://www.csmonitor.com/2004/0518/p13s01-legn.html).
There are many claims about the SAT, but we’re going to look at just
one: Is the SAT predictive of scholastic performance in college? It
turns out this is a fairly complicated question to assess—we’ll get an
introduction to some of the complexities.

# Obtain the Data

<!-- -------------------------------------------------- -->

### **q1** Visit the [SAT and College GPA](http://onlinestatbook.com/2/case_studies/sat.html) case study page, scroll to the bottom, and click the `Open Data with Excel` button. This will allow you to download an `xls` file. Save the file to your `data` folder, load the data as `df_sat`, and perform your “first checks” against these data. Answer the questions below:

``` r
## TODO:
filename_sat <- "C:/Users/zxiong/Desktop/Olin/C-Data Science/data-science-curriculum-build/challenges/data/sat.xls"

df_sat <- 
  read_xls(filename_sat) %>%
  glimpse()
```

    ## Rows: 105
    ## Columns: 5
    ## $ high_GPA <dbl> 3.45, 2.78, 2.52, 3.67, 3.24, 2.10, 2.82, 2.36, 2.42, 3.51, 3…
    ## $ math_SAT <dbl> 643, 558, 583, 685, 592, 562, 573, 559, 552, 617, 684, 568, 6…
    ## $ verb_SAT <dbl> 589, 512, 503, 602, 538, 486, 548, 536, 583, 591, 649, 592, 5…
    ## $ comp_GPA <dbl> 3.76, 2.87, 2.54, 3.83, 3.29, 2.64, 2.86, 2.03, 2.81, 3.41, 3…
    ## $ univ_GPA <dbl> 3.52, 2.91, 2.40, 3.47, 3.47, 2.37, 2.40, 2.24, 3.02, 3.32, 3…

``` r
## TODO: Do your "first checks"
```

**Observations**:

- Fill in the following “data dictionary”

| Column     | Meaning                                |
|------------|----------------------------------------|
| `high_GPA` | High school grade point average        |
| `math_SAT` | Math SAT score                         |
| `verb_SAT` | Verbal SAT score                       |
| `comp_GPA` | Computer science grade point average   |
| `univ_GPA` | Overall university grade point average |

- What information do we have about these students?
  - Their general academic performances at high school, university as
    well as their SAT scores. In addition, we know their GPA for their
    computer science courses specifically.
- What kinds of information *do we not have* about these students?
  - Demographic information, their arts, science and humanity GPAs, the
    rigor of their course selections (if they were challenging
    themselves), extracurricular activity engagements, personal lives
    and challenges, etc.
- Based on these missing variables, what possible effects could be
  present in the data that we would have *no way of detecting*?
  - Their access to the quality resources that helps or would
    potentially help their academic performances, personal life
    struggles, etc.

# Analysis with Hypothesis Testing

<!-- ----------------------------------------------------------------------- -->

We’re going to use two complementary approaches to analyze the data, the
first based on hypothesis testing of correlation coefficients, and the
second based on fitting a regression model and interpreting the
regression coefficients.

To simplify the analysis, let’s look at a composite SAT score:

``` r
## NOTE: No need to edit this
df_composite <-
  df_sat %>%
  mutate(both_SAT = math_SAT + verb_SAT)
```

## View 1: Correlations

<!-- ----------------------------------------------------------------------- -->

### **q2** Create a *single* plot that shows `univ_GPA` against *both* `high_GPA` and `both_SAT`. Visually compare the two trends.

*Hint*: One way to do this is to first *pivot* `df_composite`.

``` r
## TODO:
df_q2 <- df_sat %>%
  mutate(both_SAT = math_SAT + verb_SAT)


coef <- 0.00251

df_q2 %>%
  ggplot(aes(y = univ_GPA)) + 
    geom_point(aes(x = both_SAT), color = "blue") +
    geom_point(aes(x = high_GPA/coef), color = "red") +
    
    # Custom the Y scales:
    scale_x_continuous(
      
      # Features of the first axis
      name = "Both SAT",
      
      # Add a second axis and specify its features
      sec.axis = sec_axis( trans = ~.* coef, name = "High school GPA")
    ) +
  theme(
    axis.title.x = element_text(color = "red", size=13),
    axis.title.x.bottom = element_text(color = "blue", size=13)
  ) 
```

![](c10-sat-assignment_files/figure-gfm/q2-task-1.png)<!-- -->

**Observations**:

- What relationship do `univ_GPA` and `both_SAT` exhibit?
  - `univ_GPA` increases as `both_SAT` increases. However, the points
    between `both_SAT = 1000` and `both_SAT = 1200` are generally
    aligned vertically, while the points between `both_SAT = 1200` and
    `both_SAT = 1400` are generally aligned horizontally.
- What relationship do `univ_GPA` and `high_GPA` exhibit?
  - `univ_GPA` increases as `high_SAT` increases. For a `high_GPA`
    ranged between 2.0 and 2.75, the trend is not sufficiently distinct.
    However, the relationship between `univ_GPA` and `both_SAT` tends to
    look much more linear with a positive slope when `both_SAT` is
    ranged from 2.75 to 4.0.

### Hypothesis Testing with a Correlation Coefficient

<!-- ------------------------- -->

We can use the idea of hypothesis testing with a correlation
coefficient. The idea is to set our null hypothesis to the case where
there is no correlation, and test to see if the data contradict that
perspective. Formally, the null (H0) and alternative (HA) hypotheses
relating to a correlation coefficient between two variables `X, Y` are:

$$\text{H0: } \text{Corr}[X, Y] = 0$$

$$\text{HA: } \text{Corr}[X, Y] \neq 0$$

The R function `cor.test` implements such a hypothesis test under the
assumption that `X, Y` are both normally distributed. First, let’s check
to see if this assumption looks reasonable for our data.

### **q3** Plot histograms for `both_SAT, high_GPA, univ_GPA`. Which—if any—of the variables look approximately normally distributed.

``` r
p1 <- ggplot(data = df_q2, aes(x = both_SAT)) +
    geom_histogram()

p2 <- ggplot(data = df_q2, aes(x = high_GPA)) +
    geom_histogram()

p3 <- ggplot(data = df_q2, aes(x = univ_GPA)) +
    geom_histogram()

library(patchwork)
p1 + p2 + p3
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](c10-sat-assignment_files/figure-gfm/q3-task-1.png)<!-- -->

**Observations**:

- To what extent does `both_SAT` look like a normal distribution?
  - It barely looks similar to a normal distribution, since there are
    missing data at the positions where it should be “peaks”. The entire
    data seems to be centered at 1150 but not quite.
- To what extent does `high_GPA` look like a normal distribution?
  - It barely looks similar to a normal distribution, since there are
    missing data at roughly `high_GPA = 3.0`. The entire data seems to
    have two centers at 2.75 and 3.5 respectively.
- To what extent does `univ_GPA` look like a normal distribution?
  - It barely looks similar to a normal distribution, since most of the
    data points seem to center at 3.5 while there are several spikes
    roughly located at `univ_GPA = 2.3` which differentiate the pattern
    further away from normal distribution.

Keep in mind your findings as you complete q4.

### **q4** Use the function `cor.test()` to construct confidence intervals for `corr[high_GPA, univ_GPA` and `corr[both_SAT, univ_GPA]`. Answer the questions below.

``` r
## TODO: Use the function cor.test() to test the correlations between
##       high_GPA and univ_GPA, as well as between
##       both_SAT and univ_GPA
corr_high_univ_GPA <- cor.test(df_q2$high_GPA, df_q2$univ_GPA)
corr_SAT_univ_GPA <- cor.test(df_q2$both_SAT, df_q2$univ_GPA)

corr_high_univ_GPA %>% tidy()
```

    ## # A tibble: 1 × 8
    ##   estimate statistic  p.value parameter conf.low conf.high method    alternative
    ##      <dbl>     <dbl>    <dbl>     <int>    <dbl>     <dbl> <chr>     <chr>      
    ## 1    0.780      12.6 1.18e-22       103    0.691     0.845 Pearson'… two.sided

``` r
corr_SAT_univ_GPA %>% tidy()
```

    ## # A tibble: 1 × 8
    ##   estimate statistic  p.value parameter conf.low conf.high method    alternative
    ##      <dbl>     <dbl>    <dbl>     <int>    <dbl>     <dbl> <chr>     <chr>      
    ## 1    0.685      9.53 8.05e-16       103    0.567     0.775 Pearson'… two.sided

**Observations**:

- Which correlations are significantly nonzero?
  - Both.
- Which of `high_GPA` and `both_SAT` seems to be more strongly
  correlated with `univ_GPA`?
  - high_GPA.
- How do the results here compare with the visual you created in q2?
  - This matches with the overlapping of the general shapes of high_GPA
    and univ_GPA in q2.
- Based on these results, what can we say about the predictive
  capabilities of both `high_GPA` and `both_SAT` to predict `univ_GPA`?
  - high_GPA has a better predictive capability compared to both_SAT.

Finally, let’s use the bootstrap to perform the same test using
*different* assumptions.

### **q5** Use the bootstrap to approximate a confidence interval.

Use the bootstrap to approximate a confidence interval for
`cor[high_GPA, univ_GPA]`. Compare your results—both the estimate and
confidence interval—to your results from q4.

*Hint 1*. The `cor(x, y)` function computes the correlation between two
variables `x` and `y`. You may find this more helpful than the
`cor.test()` function we used above.

*Hint 2*. You’ll find that the documentation for `int_pctl` has some
**really** useful examples for this task!

``` r
## TODO: Complete the following helper function to do a bootstrap analysis
corr_high_GPA <- function(split) {
  tibble(
    term = "cor",
    estimate = cor(analysis(split) %>% pull(high_GPA), 
                   analysis(split) %>% pull(univ_GPA)
    )
  )
}

# Use the bootstrap to approximate a CI
df_composite %>%
  bootstraps(times = 1000) %>%
  mutate(estimates = map(splits, corr_high_GPA)) %>%
  int_pctl(estimates)
```

    ## # A tibble: 1 × 6
    ##   term  .lower .estimate .upper .alpha .method   
    ##   <chr>  <dbl>     <dbl>  <dbl>  <dbl> <chr>     
    ## 1 cor    0.698     0.780  0.851   0.05 percentile

**Observations**:

- How does your estimate from q5 compare with your estimate from q4?
  - The estimate from q5 is 0.782, which is about 0.1 greater than the
    result from q4 (0.685).
- How does your CI from q5 compare with your CI from q4?
  - The CI from q5 is from 0.698 to 0.849, which is overall higher than
    the result from q4 (from 0.567 to 0.775).

*Aside*: When you use two different approximations to compute the same
quantity and get similar results, that’s an *encouraging sign*. Such an
outcome lends a bit more credibility to the results.

## View 2: Modeling

<!-- ------------------------- -->

Correlations are useful for relating two variables at a time. To study
the relationship among more variables we can instead use a fitted model.
Using a model, we can also help assess whether it is *worthwhile* to
measure a variable.

To begin, let’s first split the data into training and validation sets.

``` r
## NOTE: No need to edit
set.seed(101)

df_train <-
  df_composite %>%
  rowid_to_column() %>%
  slice_sample(n = 80)

df_validate <-
  df_composite %>%
  rowid_to_column() %>%
  anti_join(
    .,
    df_train,
    by = "rowid"
  )
```

### Hypothesis Testing with a Model

<!-- ------------------------- -->

We can combine the ideas of hypothesis testing with a model. Using a
model, we can express our hypotheses in terms of the model parameters.
For instance, if we were interested in whether $X$ has an affect on $Y$,
we might set up a model:

$$Y_i = \beta X_i + \epsilon_i$$

With the hypotheses:

$$\text{H0}: \beta = 0$$

$$\text{HA}: \beta \neq 0$$

In this case, we’re testing for whether $X$ has a significant effect on
$Y$. Let’s apply this idea to relating the variables `univ_GPA` and
`high_GPA`. Luckily R has built-in tools to construct a confidence
interval on the $\beta$’s in a regression \[1\]; we’ll simply use those
tools rather than do it by hand.

### **q6** Fit a linear model predicting `univ_GPA` with the predictor `both_SAT`. Assess the model to determine how effective a predictor `both_SAT` is for `univ_GPA`. Interpret the resulting confidence interval for the coefficient on `both_SAT`.

``` r
## TODO: Fit a model of univ_GPA on the predictor both_SAT
fit_basic <- 
  df_q2 %>%
  lm(
    data = .,
    formula = univ_GPA ~ both_SAT
  )

## NOTE: The following computes confidence intervals on regression coefficients
fit_basic %>%
  tidy(
    conf.int = TRUE,
    conf.level = 0.99
  )
```

    ## # A tibble: 2 × 7
    ##   term        estimate std.error statistic  p.value conf.low conf.high
    ##   <chr>          <dbl>     <dbl>     <dbl>    <dbl>    <dbl>     <dbl>
    ## 1 (Intercept) -0.172    0.352       -0.487 6.27e- 1 -1.10      0.753  
    ## 2 both_SAT     0.00274  0.000287     9.53  8.05e-16  0.00198   0.00349

``` r
rsquare(fit_basic, df_validate)
```

    ## [1] 0.5544037

**Observations**:

- What is the confidence interval on the coefficient of `both_SAT`? Is
  this coefficient significantly different from zero?
  - The CI on the coefficient of `both_SAT` is from 0.00198 to 0.00349,
    which doesn’t contain zero and the coefficient is significantly
    different from zero.
- By itself, how well does `both_SAT` predict `univ_GPA`?
  - `both_SAT` is a fair but not great predictor of `univ_GPA` with an
    rsquare value of 0.554.

Remember from `e-model03-interp-warnings` that there are challenges with
interpreting regression coefficients! Let’s investigate that idea
further.

### **q7** Fit a model predicting `univ_GPA` using both `high_GPA` and `both_SAT`. Compare the prediction accuracy and hypothesis test results.

``` r
## TODO: Fit and assess models with predictors both_SAT + high_GPA, and high_GPA alone
fit_both <-
  df_q2 %>%
  lm(
    data = .,
    formula = univ_GPA ~ both_SAT + high_GPA
  )

fit_both %>%
  tidy(
    conf.int = TRUE,
    conf.level = 0.99
  )
```

    ## # A tibble: 3 × 7
    ##   term        estimate std.error statistic       p.value  conf.low conf.high
    ##   <chr>          <dbl>     <dbl>     <dbl>         <dbl>     <dbl>     <dbl>
    ## 1 (Intercept) 0.540     0.318         1.70 0.0924        -0.294      1.37   
    ## 2 both_SAT    0.000792  0.000387      2.05 0.0432        -0.000224   0.00181
    ## 3 high_GPA    0.541     0.0837        6.47 0.00000000353  0.322      0.761

``` r
fit_high_GPA <-
  df_q2 %>%
  lm(
    data = .,
    formula = univ_GPA ~ high_GPA
  )

fit_high_GPA %>%
  tidy(
    conf.int = TRUE,
    conf.level = 0.99
  )
```

    ## # A tibble: 2 × 7
    ##   term        estimate std.error statistic  p.value conf.low conf.high
    ##   <chr>          <dbl>     <dbl>     <dbl>    <dbl>    <dbl>     <dbl>
    ## 1 (Intercept)    1.10     0.167       6.58 1.98e- 9    0.660     1.53 
    ## 2 high_GPA       0.675    0.0534     12.6  1.18e-22    0.535     0.815

``` r
rsquare(fit_both, df_validate)
```

    ## [1] 0.6918107

``` r
rsquare(fit_high_GPA, df_validate)
```

    ## [1] 0.6390909

``` r
univ_GPA_prediction <- cor.test(df_q2$both_SAT, df_q2$univ_GPA)
```

**Observations**:

- How well do these models perform, compared to the one you built in q6?
  - These models overall perform significantly better than the one in
    q6.
- What is the confidence interval on the coefficient of `both_SAT` when
  including `high_GPA` as a predictor?? Is this coefficient
  significantly different from zero?
  - The CI on the coefficient of `both_SAT` when including `high_GPA` is
    from -0.00022 to 0.00181, which contains zero and the coefficient is
    not significantly different from zero.
- How do the hypothesis test results compare with the results in q6?
  - The rsquare values are higher than the results in q6, indicating
    better hypothesis test results.

## Synthesize

<!-- ------------------------- -->

Before closing, let’s synthesize a bit from the analyses above.

### **q8** Using the results from all previous q’s, answer the following questions.

**Observations**:

- Between `both_SAT` and `high_GPA`, which single variable would you
  choose to predict `univ_GPA`? Why?
  - `high_GPA`, because it has a significantly higher correlation to the
    university GPA with a higher rsquare value than `both_SAT`.
- Is `both_SAT` an effective predictor of `univ_GPA`? What specific
  pieces of evidence do you have in favor of `both_SAT` being effective?
  What specific pieces of evidence do you have against?
  - `both_SAT` is a fair but not sufficiently effective predictor of
    `univ_GPA`. The lower bound of CI of `both_SAT` is above zero and
    the coefficient is different from zero, while that of the model
    fitted by both `both_SAT` and `high_GPA` has a CI lower bound that’s
    smaller than zero. This evidence is in favor of `both_SAT` being
    effective.
  - The rsquare values of `both_SAT` are lower than that of `high_GPA`
    or a combination of `high_GPA` and `both_SAT`, which proves against
    `both_SAT` being more effective than others.

# End Notes

<!-- ----------------------------------------------------------------------- -->

\[1\] There are also assumptions underlying this kind of testing, for
more information see this [Wiki
article](https://en.wikipedia.org/wiki/Linear_regression#Assumptions).
