Analytic plan
================
Associations between climate variation and anthropometric indicators of
under-5 nutritional status in Bangladesh, 1990-2006

  - [Summary](#summary)
  - [Background](#background)
  - [Hypothesis](#hypothesis)
  - [Data & Variables](#data-variables)
  - [Analyses](#analyses)
  - [Conclusion](#conclusion)
  - [References](#references)

       

-----

### Summary

Using Poisson regression models, we hope to estimate effects of various
climate exposures on childhood acute nutritional outcomes. We will
consider climate exposures at multiple timescales, including long-term
trends, seasonal patterns, and interannual variation.

-----

   

### Background

Climate variability has been shown to influence nutrition via several
pathways, including food and financial insecurity, gender-based
disempowerment, health services, and environment (Herforth et al, 2014).
However, research seldom differentiates nutritional vulnerabilities
resulting from climate variation at multiple timescales, e.g. seasonal
patterns versus short-term shocks (Füssel & Klein, 2006). This study
considers such climate-nutrition associations among children in
Bangladesh, a population and country disproportionately at-risk to
climate variability and nutritional shocks (Brouwer et al, 2007;
Stanberry et al, 2018).

   

### Hypothesis

Short-term variation in magnitude and timing of childhood wasting will
be explained by variation in magnitude and timing of regular climate
events.

   

### Data & Variables

Our climate and nutrition data for these analyses come from two
different datasets, with observations matched at the day-level by
subdistrict.

#### *Datasets*

1.  **Nutrition Surveillance Project** (NSP). Bangladesh, 1990-2006. N =
    796996 measurements of child anthropometry, health, and household
    characteristics.
2.  **ENACTS** climate data. Bangladesh, 1990-2006. N = 465000+ daily
    precipitation and temperature observations across 22 subdistricts.

#### *Exposures of interest*

Our climate-related exposures of interest here come from the ENACTS
dataset detailed above. They include:

1.  Daily-level precipitation, in millimeters
2.  Daily-level maximum temperature, in degrees Celsius
3.  Daily-level minimum temperature, in degrees Celsius

#### *Outcome of interest*

Our outcome of interest, broadly, is acute nutrition status in children
under age 5. This is operationalized using an anthropometric measure
known as weight-for-length, the ratio of a child’s weight to height (or
length). This measure is standardized into a Z-score using the WHO Child
Growth Standards (World Health Organization, 2006).

### Analyses

#### *Unadjusted Poisson Regression Models*

First, we will model our outcome - daily count of wasting, *Y\_i* - in
univariate models indcluding our three climate exposures separately.
These models will be stratified by subdistrict, across the timespan of
our study (1990-2006).

*Note:* Each of these Poisson regression models includes an offset term,
*n\_i*, which indicates the total sample out of which each daily wasting
count is measured (i.e., the denominator of the wasting proportion).

 

![Alt text](./images/eq1.gif)

 

![Alt text](./images/eq2.gif)

 

![Alt text](./images/eq3.gif)

##### *Mediational Analyses*

Next, we will test diarrheal disease as a potential mediator of each of
these relationships by adding a second term to each model:

![Alt text](./images/dia_term.gif)

We expect the addition of diarrhea to the model to bias each main effect
towards the null.    

##### *Sample weight adjustments*

Since our outcome of interest, child weight-for-length Z-score, was
sampled using a multistage cluster design, we will explore the use of
sampling weights to increase the precision of our inference. For now, we
will focus on the unadjusted and mediational analyses detailed above.

Use of the unadjusted analyses is justified by our belief that there is
likely no differential misclassification of exposure or outcome in our
sample. Assuming our sample collection was not biased at baseline and
representative at the subdistrict level, non-differential
misclassification of exposure and/or disease will only bias measures of
association towards the null - which, if anything, makes any observed
associations more robust.

##### *Other considerations for unadjusted models*

In these unadjusted models, we may also choose to operationalize climate
exposures as categories determined by percentile levels to aid in
interpretation. For example, on days when precipitation was in the upper
25th percentile for a given region, prevalence of wasting increased by X
compared to other days.

Adjusted models could also be constructed from the above that consider
region- and/or household-level socioeconomic status. However, these may
be better suited to analyses that consider seasonal and long-term trends
in exposure and outcome (below).

#### *Short-Term Effects Models*

##### Filtering out long-term and seasonal patterns

Both seasonal (Fig. 1) and long-term (Fig. 2) trends in child wasting
have been seen in previous analyses.

![Alt text](./images/area7_seasonal_notitle.jpg) *Figure 1: Multiyear
average seasonal wasting model, Shakhipur/Sreepur subdistricts*

 

![Alt text](./images/weekly_prev_plot.png) *Figure 2: Downward trend in
overall sample prevalence of wasting, 1990-2006*

 

These time-dependent patterns are important to consider, especially if
we desire a measure of association that is based on variation beyond
what is expected within the year and across time. Here, we would like to
observe the isolated effects of interannual variation in climate
exposures on our outcome of interest, child wasting.

We can “filter” the effects of seasonal patterns by including a
pre-fitted Fourier curve as a fixed effect in a Poisson regression model
(with count of child wasting as the outcome, as above). We can also
include a linear function of time to capture long-term trends.

From here, we can approach the question of isolated interannual
variability in at least two ways:

1.  Compare a crude Poisson regression model (with the only predictors
    being the Fourier term and the linear function) with a model
    including data on precipitation, minimum temperature, and/or maximum
    temperature.
2.  Extract the residuals from the crude Poisson regression model in
    \#1, and model these residuals using data on precipitation, minimum
    temperature, and/or maximum temperature.

Each of these methods would help us to answer the question: Apart from
knowing the day of the year (season) and year (long-term trend level),
does climate information help us predict childhood wasting?

### Conclusion

With the above analyses, we hope to address the effects of climate
exposures on childhood acute malnutrition (wasting) in Bangladesh.

### References

1.  Herforth A, Frongillo EA, Sassi F, et al. (2014). Toward an
    integrated approach to nutritional quality, environmental
    sustainability, and economic viability: research and measurement
    gaps. Annals of the New York Academy of Sciences, 1332(1):1-21.
    <https://doi.org/10.1111/nyas.12552>.

2.  Füssel, H.‐M. & R.J. Klein. (2006). Climate change vulnerability
    assessments: an evolution of conceptual thinking. Clim. Change,
    75:301–329. <https://doi.org/10.1007/s10584-006-0329-3>.

3.  Brouwer R., Akter S., Brander L. & Haque, E. (2007). Socioeconomic
    Vulnerability and Adaptation to Environmental Risk: A Case Study of
    Climate Change and Flooding in Bangladesh. Risk Analysis,
    27:313-326. <https://doi.org/10.1111/j.1539-6924.2007.00884.x>

4.  Stanberry LR, Thomson MC & James W. (2018). Prioritizing the needs
    of children in a changing climate. PLoS Medicine, 15(8):1-4.
    <https://doi.org/10.1371/journal.pmed.1002627>.

5.  Word Health Organization (2006). WHO Multicentre Growth Reference
    Study Group. WHO Child Growth Standards: Length/height-for-age,
    weight-for-age, weight-for-length, weight-for-height and body mass
    index-for-age: Methods and development. Geneva: World Health
    Organization.
    <https://www.who.int/childgrowth/standards/Technical_report.pdf?ua=1>.
