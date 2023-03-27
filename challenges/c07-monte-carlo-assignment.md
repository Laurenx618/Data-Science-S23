Estimating Pi With a Shotgun
================
(Your name here)
2020-

- <a href="#grading-rubric" id="toc-grading-rubric">Grading Rubric</a>
  - <a href="#individual" id="toc-individual">Individual</a>
  - <a href="#due-date" id="toc-due-date">Due Date</a>
- <a href="#monte-carlo" id="toc-monte-carlo">Monte Carlo</a>
  - <a href="#theory" id="toc-theory">Theory</a>
  - <a href="#implementation" id="toc-implementation">Implementation</a>
    - <a
      href="#q1-pick-a-sample-size-n-and-generate-n-points-uniform-randomly-in-the-square-x-in-0-1-and-y-in-0-1-create-a-column-stat-whose-mean-will-converge-to-pi"
      id="toc-q1-pick-a-sample-size-n-and-generate-n-points-uniform-randomly-in-the-square-x-in-0-1-and-y-in-0-1-create-a-column-stat-whose-mean-will-converge-to-pi"><strong>q1</strong>
      Pick a sample size <img style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20n"
      alt="n" title="n" class="math inline" /> and generate <img
      style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20n"
      alt="n" title="n" class="math inline" /> points <em>uniform
      randomly</em> in the square <img style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20x%20%5Cin%20%5B0%2C%201%5D"
      alt="x \in [0, 1]" title="x \in [0, 1]" class="math inline" /> and <img
      style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20y%20%5Cin%20%5B0%2C%201%5D"
      alt="y \in [0, 1]" title="y \in [0, 1]" class="math inline" />. Create a
      column <code>stat</code> whose mean will converge to <img
      style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20%5Cpi"
      alt="\pi" title="\pi" class="math inline" />.</a>
    - <a href="#q2-using-your-data-in-df_q1-estimate-pi"
      id="toc-q2-using-your-data-in-df_q1-estimate-pi"><strong>q2</strong>
      Using your data in <code>df_q1</code>, estimate <img
      style="vertical-align:middle"
      src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20%5Cpi"
      alt="\pi" title="\pi" class="math inline" />.</a>
- <a href="#quantifying-uncertainty"
  id="toc-quantifying-uncertainty">Quantifying Uncertainty</a>
  - <a
    href="#q3-using-a-clt-approximation-produce-a-confidence-interval-for-your-estimate-of-pi-make-sure-you-specify-your-confidence-level-does-your-interval-include-the-true-value-of-pi-was-your-chosen-sample-size-sufficiently-large-so-as-to-produce-a-trustworthy-answer"
    id="toc-q3-using-a-clt-approximation-produce-a-confidence-interval-for-your-estimate-of-pi-make-sure-you-specify-your-confidence-level-does-your-interval-include-the-true-value-of-pi-was-your-chosen-sample-size-sufficiently-large-so-as-to-produce-a-trustworthy-answer"><strong>q3</strong>
    Using a CLT approximation, produce a confidence interval for your
    estimate of <img style="vertical-align:middle"
    src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20%5Cpi"
    alt="\pi" title="\pi" class="math inline" />. Make sure you specify your
    confidence level. Does your interval include the true value of <img
    style="vertical-align:middle"
    src="https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&amp;space;%5Cbg_white&amp;space;%5Ctextstyle%20%5Cpi"
    alt="\pi" title="\pi" class="math inline" />? Was your chosen sample
    size sufficiently large so as to produce a trustworthy answer?</a>
- <a href="#references" id="toc-references">References</a>

*Purpose*: Random sampling is extremely powerful. To build more
intuition for how we can use random sampling to solve problems, we’ll
tackle what—at first blush—doesn’t seem appropriate for a random
approach: estimating fundamental deterministic constants. In this
challenge you’ll work through an example of turning a deterministic
problem into a random sampling problem, and practice quantifying
uncertainty in your estimate.

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

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.8     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

*Background*: In 2014, some crazy Quebecois physicists estimated
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")
with a pump-action shotgun\[1,2\]. Their technique was based on the
*Monte Carlo method*, a general strategy for turning deterministic
problems into random sampling.

# Monte Carlo

<!-- -------------------------------------------------- -->

The [Monte Carlo
method](https://en.wikipedia.org/wiki/Monte_Carlo_method) is the use of
randomness to produce approximate answers to deterministic problems. Its
power lies in its simplicity: So long as we can take our deterministic
problem and express it in terms of random variables, we can use simple
random sampling to produce an approximate answer. Monte Carlo has an
[incredible
number](https://en.wikipedia.org/wiki/Monte_Carlo_method#Applications)
of applications; for instance Ken Perlin won an [Academy
Award](https://en.wikipedia.org/wiki/Perlin_noise) for developing a
particular flavor of Monte Carlo for generating artificial textures.

I remember when I first learned about Monte Carlo, I thought the whole
idea was pretty strange: If I have a deterministic problem, why wouldn’t
I just “do the math” and get the right answer? It turns out “doing the
math” is often hard—and in some cases an analytic solution is simply not
possible. Problems that are easy to do by hand can quickly become
intractable if you make a slight change to the problem formulation.
Monte Carlo is a *general* approach; so long as you can model your
problem in terms of random variables, you can apply the Monte Carlo
method. See Ref. \[3\] for many more details on using Monte Carlo.

In this challenge, we’ll tackle a deterministic problem (computing
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi"))
with the Monte Carlo method.

## Theory

<!-- ------------------------- -->

The idea behind estimating
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")
via Monte Carlo is to set up a probability estimation problem whose
solution is related to
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi").
Consider the following sets: a square with side length one
![St](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;St "St"),
and a quarter-circle
![Sc](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;Sc "Sc").

``` r
## NOTE: No need to edit; this visual helps explain the pi estimation scheme
tibble(x = seq(0, 1, length.out = 100)) %>%
  mutate(y = sqrt(1 - x^2)) %>%

  ggplot(aes(x, y)) +
  annotate(
    "rect",
    xmin = 0, ymin = 0, xmax = 1, ymax = 1,
    fill = "grey40",
    size = 1
  ) +
  geom_ribbon(aes(ymin = 0, ymax = y), fill = "coral") +
  geom_line() +
  annotate(
    "label",
    x = 0.5, y = 0.5, label = "Sc",
    size = 8
  ) +
  annotate(
    "label",
    x = 0.8, y = 0.8, label = "St",
    size = 8
  ) +
  scale_x_continuous(breaks = c(0, 1/2, 1)) +
  scale_y_continuous(breaks = c(0, 1/2, 1)) +
  theme_minimal() +
  coord_fixed()
```

![](c07-monte-carlo-assignment_files/figure-gfm/vis-areas-1.png)<!-- -->

The area of the set
![Sc](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;Sc "Sc")
is
![\pi/4](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi%2F4 "\pi/4"),
while the area of
![St](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;St "St")
is
![1](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;1 "1").
Thus the probability that a *uniform* random variable over the square
lands inside
![Sc](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;Sc "Sc")
is the ratio of the areas, that is

![\mathbb{P}\_{X}\[X \in Sc\] = (\pi / 4) / 1 = \frac{\pi}{4}.](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cmathbb%7BP%7D_%7BX%7D%5BX%20%5Cin%20Sc%5D%20%3D%20%28%5Cpi%20%2F%204%29%20%2F%201%20%3D%20%5Cfrac%7B%5Cpi%7D%7B4%7D. "\mathbb{P}_{X}[X \in Sc] = (\pi / 4) / 1 = \frac{\pi}{4}.")

This expression is our ticket to estimating
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")
with a source of randomness: If we estimate the probability above and
multiply by
![4](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;4 "4"),
we’ll be estimating
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi").

## Implementation

<!-- ------------------------- -->

Remember in `e-stat02-probability` we learned how to estimate
probabilities as the limit of frequencies. Use your knowledge from that
exercise to generate Monte Carlo data.

### **q1** Pick a sample size ![n](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;n "n") and generate ![n](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;n "n") points *uniform randomly* in the square ![x \in \[0, 1\]](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;x%20%5Cin%20%5B0%2C%201%5D "x \in [0, 1]") and ![y \in \[0, 1\]](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;y%20%5Cin%20%5B0%2C%201%5D "y \in [0, 1]"). Create a column `stat` whose mean will converge to ![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi").

*Hint*: Remember that the mean of an *indicator function* on your target
set will estimate the probability of points landing in that area (see
`e-stat02-probability`). Based on the expression above, you’ll need to
*modify* that indicator to produce an estimate of
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi").

``` r
## TASK: Choose a sample size and generate samples
n <- 500000 # Choose a sample size

df_q1 <- tibble(x = runif(n, min = 0, max = 1)) %>%
  mutate(y = runif(n, min = 0, max = 1), stat = (sqrt(x^2 + y^2) <= 1) * 4)
df_q1
```

    ## # A tibble: 500,000 × 3
    ##         x      y  stat
    ##     <dbl>  <dbl> <dbl>
    ##  1 0.697  0.847      0
    ##  2 0.717  0.823      0
    ##  3 0.899  0.0944     4
    ##  4 0.627  0.615      4
    ##  5 0.912  0.626      0
    ##  6 0.640  0.149      4
    ##  7 0.662  0.180      4
    ##  8 0.103  0.797      4
    ##  9 0.0475 0.516      4
    ## 10 0.252  0.526      4
    ## # … with 499,990 more rows
    ## # ℹ Use `print(n = ...)` to see more rows

``` r
# pi/4 = (x^2 + y^2) <= 1)
```

### **q2** Using your data in `df_q1`, estimate ![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi").

``` r
## TASK: Estimate pi using your data from q1
pi_est <- mean(df_q1$stat)
  
pi_est
```

    ## [1] 3.141064

# Quantifying Uncertainty

<!-- -------------------------------------------------- -->

You now have an estimate of
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi"),
but how trustworthy is that estimate? In `e-stat06-clt` we discussed
*confidence intervals* as a means to quantify the uncertainty in an
estimate. Now you’ll apply that knowledge to assess your
![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")
estimate.

### **q3** Using a CLT approximation, produce a confidence interval for your estimate of ![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi"). Make sure you specify your confidence level. Does your interval include the true value of ![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")? Was your chosen sample size sufficiently large so as to produce a trustworthy answer?

``` r
n <- 500000
q95 <- qnorm( 1 - (1 - 0.95) / 2 )
mean <- pi_est

df_q1 %>%
  mutate(
    sd = sd(stat),
    se = sd / sqrt(n),
    lo = mean - q95 * se,
    hi = mean + q95 * se,
    sample_size = n
  ) %>%
  ggplot(aes(x = sample_size)) +
  geom_hline(yintercept = pi, linetype = 2) +
  geom_errorbar(aes(
    ymin = lo,
    ymax = hi,
    color = (lo <= pi) & (mean <= pi)
  )) +
  geom_point(aes(x = sample_size, y = mean)) +
  facet_grid(1~.) +
  scale_color_discrete(name = "CI Contains True Mean") +
  theme(legend.position = "bottom") +
  labs(
    x = "Replication",
    y = "Estimated Mean"
  )
```

![](c07-monte-carlo-assignment_files/figure-gfm/q3-task-1.png)<!-- -->

**Observations**:

- Does your interval include the true value of
  ![\pi](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Cpi "\pi")?
  - Yes!
- What confidence level did you choose?
  - The confidence level that I chose was 0.95.
- Was your sample size
  ![n](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;n "n")
  large enough? Why do you say that?
  - My sample size (500,000) is large enough to produce a value which
    can be applied in most disciplines, because the entire confidence
    interval lies from roughly 3.1372 to 3.1462 with a accuracy to 2
    significant figures.

# References

<!-- -------------------------------------------------- -->

\[1\] Dumoulin and Thouin, “A Ballistic Monte Carlo Approximation of Pi”
(2014) ArXiv, [link](https://arxiv.org/abs/1404.1499)

\[2\] “How Mathematicians Used A Pump-Action Shotgun to Estimate Pi”,
[link](https://medium.com/the-physics-arxiv-blog/how-mathematicians-used-a-pump-action-shotgun-to-estimate-pi-c1eb776193ef)

\[3\] Art Owen “Monte Carlo”,
[link](https://statweb.stanford.edu/~owen/mc/)
