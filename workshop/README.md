
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Workshop

## Introducing spatial availability, a singly-constrained competitive-access accessibility measure

Antonio Paez (School of Earth, Environment and Society, McMaster
University, Canada)

<!-- badges: start -->
<!-- badges: end -->
<!--
ALL IMAGES WERE CREATED BY ANTONIO USING TAYASUI SKETCHES ON AN IPAD
-->

## Abstract

Accessibility measures are widely used in transportation, urban and
healthcare planning, among other applications. These measures are
weighted sums of the opportunities that can be reached given the cost of
movement and are interpreted to represent the potential for spatial
interaction. Though these measures are useful in understanding spatial
structure, their methodologies count available opportunities multiple
times. This leads to interpretability issues, as noted in recent
research on balanced floating catchment areas (BFCA) and competitive
measures of accessibility. In this paper, we respond to the limitations
of the accessibility measure by proposing a new measure of *spatial
availability* which is calculated by imposing a single constraint on the
conventional gravity-based accessibility. Similar to the gravity model
from which spatial availability is derived, a single constraint ensures
that the marginals at the destination are met and thus the number of
opportunities are preserved. Through examples, we detail the formulation
of the proposed measure. Further, we use data from the 2016
Transportation Tomorrow Survey of the Greater Golden Horseshoe area in
southern Ontario, Canada, to contrast how the conventional accessibility
measure tends to overestimate and underestimate the number of jobs
*available* to workers. We conclude with some discussion of the possible
uses of spatial availability and argue that, compared to conventional
measures of accessibility, it can offer a more meaningful and
interpretable measure of opportunity access. All data and code used in
this research are openly available.

## Materials

- Packages
  - [{accessibility}](https://github.com/paezha/accessibility) (We use
    the development version in `paezha/accessibility` which can be
    installed like this:

  <!-- -->

      remotes::install_github(paezha/accessibility)

  - [{dplyr}](https://dplyr.tidyverse.org/) (Install from CRAN).
  - [{ggplot}](https://ggplot2.tidyverse.org/) (Install from CRAN).
  - [{leaflet}](https://rstudio.github.io/leaflet/) (Install from CRAN).
  - [{patchwork}](https://patchwork.data-imaginist.com/articles/patchwork.html)
    (Install from CRAN).
  - [{sf}](https://r-spatial.github.io/sf/) (Install from CRAN).
- Data
  - [{TTS2016R}]() (Install from GitHub):

  <!-- -->

      remotes::install_github(soukhova/TTS2016R)

## Keywords

- Spatial availability
- Accessibility
- Gravity model
- Transportation
- TTS

## From accessibility to spatial availability

![](images/Image-01.png)

![](images/Image-02.png)

![](images/Image-03.png)

![](images/Image-04.png)

![](images/Image-05.png)

![](images/Image-06.png)

![](images/Image-07.png)

![](images/Image-08.png)

![](images/Image-09.png)

![](images/Image-10.png)

![](images/Image-11.png)

![](images/Image-12.png)

![](images/Image-13.png)

![](images/Image-14.png)

![](images/Image-15.png)

![](images/Image-16.png)

![](images/Image-17.png)

Formalizing this, we see that spatial availability $V_i$ is the
weighted, and *constrained*, sum of opportunities: $$
V_i = \sum_j^J O_j\frac{f(c_{ij})}{\sum_n^N f(c_{nj})}
$$

where:

- $N$ is the number of locations where population is
- $J$ is the number of locations where opportunities are

Compare to accessibility:

$$
S_i = \sum_j^JO_jf(c_{ij})
$$

Let us change the set up to illustrate a different point.

![](images/Image-18.png)

![](images/Image-19.png)

When we formalize this we see again that *spatial availability* is a
weighted sum of the opportunities, constrained to match the total:

$$
V_i = \sum_j O_j\frac{P_i}{\sum_n^N P_n}
$$

We have described two proportional allocation mechanisms:

1.  By the cost of interaction (through the impedance function)

2.  By the size of the population

These are consistent with the principles of spatial interaction (e.g.,
the gravity model):

1.  The friction of space

2.  The importance of size (mass)

We call these quantities *proportional allocation factors*:

$$
F^C_{ij} = \frac{f(c_{ij})}{\sum_n^N f(c_{nj})}
$$

and:

$$
F^P_i = \frac{P_i}{\sum_n^N P_m}
$$

The two factors are combined as follows:

$$
F_{ij}^T = \frac{F^C_{ij}F^P_i}{\sum_n^NF^C_{ij}F^P_i}
$$

to give the following expression for *spatial availability*:

$$
V_i = \sum_j^J O_jF^T_{ij}
$$

Compare again to accessibility:

$$
S_i = \sum_j^JO_jf(c_{ij})
$$

Spatial availability is a measure of the number of opportunities that
are available from a location. It is singly constrained measure of
accessibility.

- It constrains the sum of available opportunities to match the total
  number of opportunities in the region
- It is easier to interpret than accessibility
- It provides intuitive results
- It gives a natural baseline for equity analysis

## Exercise

This exercise is meant to be solved by hand. This is a great way to
develop a good feeling for the mechanics of the method. See the figure
below. It represents a tiny system with only two population centers ($a$
and $b$) and two employment centers ($A$ and $B$).

![](images/Exercise.png)

For the exercise use the following impedance function for $c_{ij}$,
where $c$ is trip duration in minutes:

$$
f(c_{ij}) = \begin{cases}
\frac{1}{c_{ij}^\beta} &\text{for } c_{ij}\le\delta\\
0 & \text{for } c_{ij}>\delta\\
\end{cases}
$$

Assume that the number of people and jobs at each location is as shown
below:

$$
\begin{array}{l}
P_{a} = 80 \\
P_{b} = 120 \\
O_{A} = 100 \\
O_{B} = 50 
\end{array}
$$

Further, the travel times in minutes between these locations are:

$$
\begin{array}{l}
c_{aA} = 15 \\
c_{Ab} = 20 \\
c_{bB} = 15 
\end{array}
$$

Use $\beta=1$ and $\delta=45$ min.

As a reminder, accessibility is:

$$
S_i = \sum_j O_jf(c_{ij})
$$

### Questions: Part 1

1.  What is the *global* jobs/population ratio in this system?
2.  What does $\delta=45$ min represent?
3.  Calculate the impedance for each population center-employment center
    pair.
4.  Calculate the accessibility.
5.  Tabulate $F^c_{ij}$ for each population center-employment center
    pair. what do these values represent?
6.  Tabulate $F^P_{i}$ for each population center. What do these values
    represent?
7.  Tabulate $F^T_{ij}$ for each population center-employment center
    pair. what do these values represent?
8.  Calculate the jobs available from each employment center to each
    population center (i.e., $V_ij$).
9.  Calculate the jobs available at each population center (i.e.,
    $V_i$).
10. Verify that $\sum_iV_i = \sum_jO_j$
11. Calculate the jobs per capita at each population center (i.e.,
    $v_i = \frac{V_i}{P_i}$)
12. Compare to the global jobs/population ratio.
13. In which of the two population centers is the risk of unemployment
    higher? Discuss.
14. What do you think would happen if $\beta$ was less than one or
    greater than one? Explain.

### Solution: Part 1

The spatial availability is as follows:

$$
\begin{array}{l}
V_{a} = 47.1 \text{ jobs}\\ 
V_{b} = 102.9 \text{ jobs}
\end{array}
$$

Next, suppose that there is an upgrade in the transportation system that
shortens the duration of trips between $a-A$, so the new travel times
are:

$$
\begin{array}{l}
c_{aA} = 5 \\
c_{Ab} = 20 \\
c_{bB} = 15 
\end{array}
$$

Continue to use $\beta =1$ and $\delta=45$ min.

### Questions: Part 2

1.  Does the accessibility of $b$ change? Discuss.
2.  Explain the changes to spatial availability $V_i$ and spatial
    availability per capita $v_i$ compared to those calculated using the
    earlier travel times.

### Solution: Part 2

The spatial availability is now as follows:

$$
\begin{array}{l}
V_{a} = 82.7 \text{ jobs}\\ 
V_{b} = 67.3 \text{ jobs}
\end{array}
$$

## Practical example

For this practical example we will use data from the 2016 edition of the
[Transportation Tomorrow
Survey](http://dmg.utoronto.ca/tts-introduction/) (TTS). This is a
comprehensive travel survey conducted in the Greater Toronto and
Hamilton Area every five years, and it includes rich information about
travel patterns and the socio-demographic composition of the population
in the region. For convenience, parts of the survey have been sourced in
[{TTS2016R}](https://soukhova.github.io/TTS2016R/), an [open data
product](https://rdcu.be/dn6yP). The data are augmented with other
information, such as travel time tables, and distributed as
analysis-ready data objects.

We will begin by loading the packages used in this example.

    library(accessibility) # Transport Accessibility Measures # Transport Accessibility Measures
    library(dplyr) # A Grammar of Data Manipulation # A Grammar of Data Manipulation
    library(ggplot2) # Create Elegant Data Visualisations Using the Grammar of Graphics # Create Elegant Data Visualisations Using the Grammar of Graphics
    library(leaflet) # Create Interactive Web Maps with the JavaScript 'Leaflet' Library # Create Interactive Web Maps with the JavaScript 'Leaflet' Library
    library(patchwork) # The Composer of Plots # The Composer of Plots
    library(sf) # Simple Features for R # Simple Features for R
    library(tidyr) # Tidy Messy Data # Tidy Messy Data
    library(TTS2016R) # An augmented 2016 Transportation Tomorrow Survey (TTS) data package: worker and place of employment counts, trips and estimated travel time to work in the Greater Golden Horsehoe area, Canada # An augmented 2016 Transportation Tomorrow Survey (TTS) data package: worker and place of employment counts, trips and estimated travel time to work in the Greater Golden Horsehoe area, Canada

We will use two objects from the data package, information aggregated at
the level of traffic analysis zones (TAZs) and an origin-destination
table:

``` r
data("ggh_taz") # Traffic analysis zones.
data("od") # Origin-destination table.
```

The data sets are documented, and you can check the help files like so:

    ?ggh_ttz
    ?od

For the exercise we will use a slice of the data, so we will extract the
parts of the data corresponding to the City of Toronto. According to the
TTS [Data
Guide](http://dmg.utoronto.ca/wp-content/uploads/2022/06/2016TTS_DataGuide.pdf)
of TTS (p. 29), the identifiers of the TAZs in Toronto are 1-625. We
will create a vector with those identifiers:

``` r
TO_taz <- c(1:625) |> 
  as.character()
```

Using the vector we just created we will filter the zones corresponding
to the City of Toronto, and then select the three variables that will be
used in the example, namely the zone identifier (using the GTA06 zoning
system), the number of workers in the zone (work age population), and
the number of jobs in the zone:

``` r
# Filter the traffic analysis zones in the City of Toronto.
lu <- ggh_taz |>
  filter(GTA06 %in% TO_taz) |>
  # Rename and select only the three variables needed for the example.
  transmute(id = GTA06,
            P = workers,
            O = jobs)
```

This selection somewhat simplifies a characteristic of the data set,
because not all the workers living in Toronto work there, and not all
jobs in Toronto are taken by people who live in Toronto. Given this
caveat, we can calculate the jobs/workers ratio in the region:

``` r
sum(lu$O)/sum(lu$P)
#> [1] 1.11989
```

A summary of the table shows that workers in Toronto tend to be more
dispersed than jobs. Some TAZs have zero workers (there is no housing in
the zone) and some have zero jobs (they are purely residential):

``` r
lu |> 
  # Drop the geometry before reporting the summary.
  st_drop_geometry() |>
  summary()
#>       id                  P              O        
#>  Length:625         Min.   :   0   Min.   :    0  
#>  Class :character   1st Qu.: 697   1st Qu.:  305  
#>  Mode  :character   Median :1471   Median :  643  
#>                     Mean   :1719   Mean   : 1925  
#>                     3rd Qu.:2442   3rd Qu.: 1704  
#>                     Max.   :8491   Max.   :41821
```

The overall jobs/workers ratio is probably a little bit optimistic
because Toronto tends to attract many commuting trips from beyond the
city boundaries. Since table `lu` is a simple features object with
geometry, we can map the variables in the form of choroplet maps. The
next two chunks of code are for workers and jobs:

``` r
Pi_plot <- ggplot() +
  geom_sf(data = lu,
          aes(fill = P)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Workers per TAZ")
```

``` r
Oi_plot <- ggplot() +
  geom_sf(data = lu,
          aes(fill = O)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Jobs per TAZ")
```

The two maps can be plotted side-by-side using the syntax of package
{patchwork}:

``` r
Pi_plot + Oi_plot
```

![](README_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

The maps show that jobs are highly concentrated in downtown Toronto. The
number of inhabitants downtown is not as high, and there are places in
the periphery of the core of the city and towards the edges with
relatively high populations.

Next, we will prepare the travel time matrix by filtering TAZ that are
in Toronto.

``` r
# Rename the table.
od_ggh <- od

# Filter the origin and destinations in the City of Toronto.
od <- od |>
  filter(Origin %in% lu$id, 
         Destination %in% lu$id) |>
  # Rename and select only the three variables needed for the example.
  transmute(from_id = Origin,
            to_id = Destination,
            travel_time)
```

Travel times in the table are in minutes. The longest travel time
between any origin and any destination is:

``` r
max(od$travel_time)
#> [1] 146
```

We will use an inverse power impedance function of the following form
for the example:

$$
f(c_{ij}) = c_{ij}^{\beta}
$$

We present the example with $\beta = 0.5$ (try this value first; you can
experiment with other values later if you wish). This is the shape of
the curve with the initial value of $\beta$:

``` r
# Parameter for inverse power impedance function.
beta <- 1

# Plot impedance function with {ggplot}
ggplot() +
  geom_function(fun = function(x) 1/(abs(x)^beta),
                xlim = c(1, max(od$travel_time))) +
  xlab("t (travel time in min)") +
  ylab("f(t)") +
  theme_minimal()
```

![](README_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

Package [{accessibility}](https://ipeagit.github.io/accessibility/)
includes functions to calculate both accessibility metrics and spatial
availability. The documentation can be consulted like so:

    ?accessibility

The inputs are a travel matrix (which in this example is our `od` table)
and a land use table (which in our example is the `lu` table containing
the opportunities and demand).

We calculate the accessibility first. The function to do this is
`accessibiliy::gravity()`. We need to specify the name of the columns
with the opportunities, the cost, as well as the impedance function
(here `accessibility::decay_power()`):

``` r
# Use table `od` with the travel time information for origin-destination pairs.
Si <- gravity(travel_matrix = od, 
              # Use table `lu` with the land use information.
              land_use_data = lu, 
              # Use column `O` for the opportunities; this column contains the number of jobs per zone.
              opportunity = "O", 
              # Use column `travel_time` as the cost variable.
              travel_cost = "travel_time", 
              # Use the power impedance function with parameter beta.
              decay_function = decay_power(beta)) |>
  # Rename the opportunities $S_i$ for accessibility.
  rename(Si = O)
```

Next, we calculate the spatial availability. The inputs are very
similar, with the addition of a variable for the demand (in our case the
population). You will recall that the population is needed to calculate
the proportional allocation factor. The spatial availability can be
reported in a detailed table that gives $V_{ij}$, that is, the number of
jobs available to each origin from each destination. The alternative
(`detailed_results = FALSE`) returns the spatial availability aggregated
by zone.

``` r
# Use table `od` with the travel time information for origin-destination pairs.
Vij <- spatial_availability(travel_matrix = od,
                            # Use table `lu` with the land use information.
                            land_use_data = lu, 
                            # Use column `O` for the opportunities; this column contains the number of jobs per zone.
                            opportunity = "O", 
                            # Use column `travel_time` as the cost variable.
                            travel_cost = "travel_time", 
                            # Use column `P` for the demand; this column contains the number of workers per zone.
                            demand = "P", 
                            # Use the power impedance function with parameter beta.
                            decay_function = decay_power(beta),
                            # Return the detailed results.
                            detailed_results = TRUE) |>
  # Rename the opportunities $V_i$ for spatial availability.
  rename(Vij = O)
```

If the detailed results are requested, the spatial availability by
origin can be computed as follows:

``` r
Vi <- Vij |>
  # Group by origin; this means that the operations in summarize() will be over the destinations.
  group_by(from_id) |>
  # Sum the opportunities available from every destination
  summarize(Vi = sum(Vij)) |>
  # Rename the column to `id`
  rename(id = from_id)
```

<!--
Compare results to our home-brewed function `spav()` above. The differences are rounding errors.
&#10;```r
junkij <- spav() |> select(-starts_with("geometry"))
junki <-  junkij |>
  st_drop_geometry() |>
  group_by(from_id) |>
  summarize(Vi = sum(Vij)) |>
  rename(id = from_id)
  &#10;junk_compare <- junki |> left_join(Vi, by = "id")  
  &#10;junk_compare |> mutate(diff = abs(Vi.x - Vi.y)/Vi.y) |> summarize(mean_diff = mean(diff))  
#> # A tibble: 1 × 1
#>   mean_diff
#>       <dbl>
#> 1   0.00186
```
-->

Join the results to the zoning system:

``` r
results <- lu |>
  left_join(Si,
            by = "id") |>
  left_join(Vi,
            by = "id")
```

Verify the total of jobs in the region, the jobs accessible, and the
jobs available:

``` r
# Sum of jobs in land use table,
sum(lu$O)
#> [1] 1202986
# Sum of jobs accessible.
sum(results$Si, na.rm = TRUE)
#> [1] 15421360
# Sum of jobs available.
sum(results$Vi, na.rm = TRUE)
#> [1] 1202843
```

We see that the jobs in the City of Toronto is preserved (with a small
difference caused by zones that cannot be reached). The sum of
accessibility in contrast is two orders of magnitude larger than the
number of jobs in the table. This complicates the interpretation of the
results. When we obtain a summary of these results we find that the
maximum accessibility for any one zone is several hundred thousands of
jobs, compared to less than sixteen thousand jobs according to spatial
availability (notice the 75 NA values; these are zones with a population
of zero). Recall that the maximum number of jobs in any one zone (check
the summary of the `lu` table above) is 41,821. Why are the values of
the accessibility so high?

``` r
results |> 
  st_drop_geometry() |>
  select(Si, Vi) |>
  summary()
#>        Si                  Vi           
#>  Min.   :    42.88   Min.   :    0.037  
#>  1st Qu.: 12475.44   1st Qu.:  579.082  
#>  Median : 21153.41   Median : 1370.369  
#>  Mean   : 28038.84   Mean   : 2186.987  
#>  3rd Qu.: 34883.20   3rd Qu.: 2575.955  
#>  Max.   :134653.00   Max.   :21152.968  
#>  NA's   :75          NA's   :75
```

Accessibility, in addition, has much greater range of variation, which
indicates that the high sum of accessibility is not the result of a few
extraordinary values. The [interquartile
range](https://en.wikipedia.org/wiki/Interquartile_range) (a measure of
dispersion) of $S_i$ is 22,407.76 but only 1,996.87 for $V_i$. The
latter value is more in line with the interquartile ranges of the
population (1,996.87) and jobs (1,399).

Maps of accessibility and spatial availability can be plotted using
package {ggplot2}. This code is for the map of accessibility:

``` r
Si_plot <- ggplot() +
  geom_sf(data = results,
          aes(fill = Si)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Accessibility")
```

This code is for the map of spatial availability:

``` r
Vi_plot <- ggplot() +
  geom_sf(data = results,
          aes(fill = Vi)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Spatial Availability")
```

The two maps can be plotted side-by-side using the syntax of package
{patchwork}:

``` r
Si_plot + Vi_plot
```

![](README_files/figure-gfm/applied-example-display-results-1.png)<!-- -->

As expected, the map of spatial availability in noticeably flatter with
its smaller interquartile range. High levels of accessibility in and
around Toronto downtown do not translate into high spatial availability.
Why is that? High accessibility creates a somewhat paradoxical effect:
the ease to reach destinations also means that there is more competition
for the same opportunities.

But, could it be that accessibility is just some sort of scaled-up
version of spatial availability? That somehow the two give similar
results but for some multiplicative constant? To answer this, we can
plot the ratio of accessibility to spatial availability. If the two
measures were similar but for the scale, we would expect that ratio to
be more or less constant. However, what we see is that the ratio of
$S_i$ to $V_i$ indicates that in some cases accessibility is tens,
hundreds, or even thousands of times biger than spatial availability.
This suggests that $S_i$ is not simply a scaled-up version of $V_i$ but
something different.

``` r
ggplot() +
  geom_sf(data = results,
          aes(fill = Si/Vi)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1, 
                       trans = "log10") +
  theme_void()
```

![](README_files/figure-gfm/applied-example-ratio-accessibility-to-availability-1.png)<!-- -->

Notice the resemblance between the population and spatial availability
maps. The correlation between these two variables is quite high:

``` r
cor(results$P, results$Vi, use = "pairwise.complete.obs")
#> [1] 0.933404
```

This should not be surprising, since the spatial availability depends
directly on the population: part of the proportional allocation
mechanism works to ensure that opportunities are proportionally
available by population. The global jobs-to-workers ratio provides a
useful reference; in the next figure, we plot the population vs the
spatial availability. The blue line passes through the origin and has a
slope of 1.1198902. If a zone had as many jobs available as the global
ratio it would be on the line; points below the line are zones with
*fewer* jobs available than what they would have, given their
population, if the jobs were equally distributed. In contrast, points
above the line are zones with populations with *more* jobs available
than their equal share.

``` r
ggplot(data = results |>
         drop_na(Vi), 
       # Plot P in the x axis and Vi in the y axis.
       aes(x = P, y = Vi)) + 
  # Plot the data as points, use alpha < 1 to control the transparency of the points.
  geom_point(alpha = 0.5) + 
  # Plot a line with a given intercept and slope.
  geom_abline(intercept = 0, 
              slope = sum(lu$O)/sum(lu$P),
              color = "orange",
              linewidth = 1.5) +
  theme_minimal()
```

![](README_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

<!--
&#10;Calculate values per capita:
&#10;```r
results <- results |>
  mutate(si = Si/P,
         vi = Vi/P)
```
&#10;Summary of values per capita:
&#10;```r
results |> 
  st_drop_geometry() |>
  select(si, vi) |>
  summary()
#>        si                 vi         
#>  Min.   :  0.1992   Min.   :0.00283  
#>  1st Qu.:  8.5324   1st Qu.:0.51484  
#>  Median : 12.4421   Median :0.79628  
#>  Mean   : 19.2023   Mean   :0.85798  
#>  3rd Qu.: 18.2990   3rd Qu.:1.11207  
#>  Max.   :735.8087   Max.   :2.66881  
#>  NA's   :75         NA's   :75
```
&#10;
```r
si_plot <- ggplot() +
  geom_sf(data = results,
          aes(fill = si)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Accessibility per capita")
```
&#10;
```r
vi_plot <- ggplot() +
  geom_sf(data = results,
          aes(fill = vi)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1) +
  theme_void() +
  ggtitle("Spatial Availability per capita")
```
&#10;Render:
&#10;```r
si_plot + vi_plot
```
&#10;![](README_files/figure-gfm/applied-example-display-per-capita-results-1.png)<!-- -->

The same is true of $s_i$: the ratio of $s_i$ to $v_i$ indicates it is
not simply a scaled-up version of $v_i$ but rather something different:

``` r
ggplot() +
  geom_sf(data = results,
          aes(fill = si/vi)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_viridis_c(direction = 1, trans = "log10") +
  theme_void()
```

![](README_files/figure-gfm/applied-example-ratio-accessibility-to-availability-per-capita-1.png)<!-- -->

The values of spatial availability per capita can be compared to the
overall jobs/workers ratio. In this plot we use a diverging gradient
with the mid-point set at that overall value. Shades of red indicate
that the spatial availability per capita is below the regional level,
and shades of blue indicate a value greater than the overall
jobs/workers ratio. This way we can explore deviations from equality:

``` r
ggplot() +
  geom_sf(data = results,
          aes(fill = vi)) +
  geom_sf(data = lu,
          fill = NA) +
  scale_fill_gradient2(midpoint = sum(lu$O)/sum(lu$P)) +
  theme_void() +
  ggtitle("Spatial Availability per capita")
```

![](README_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

The code in the next two chunks uses package {leaflet} to create
interactive maps to further explore the results. Some zones had high
accessibility, and yet relatively low availability. This could be caused
by the competition for opportunities in well-connected central parts of
Toronto.

Map to explore accessibility:

``` r

bins <- quantile(results$si, na.rm = TRUE) |> as.numeric()
pal <- colorBin("RdBu", domain = results$si, bins = bins)

labels <- sprintf(
  "<strong>%s</strong><br/>%g workers<br/>%g jobs accessible<br/>%g jobs / person",
  results$id, 
  results$P,
  results$Si,
  results$si
) %>% lapply(htmltools::HTML)

leaflet(data = results |> st_transform(crs = 4326 )) |> 
  addPolygons(
    fillColor = ~pal(si),
    weight = 2,
    opacity = 1,
    color = "white",
    dashArray = "3",
    fillOpacity = 0.7,
    highlightOptions = highlightOptions(
      weight = 5,
      color = "#666",
      dashArray = "",
      fillOpacity = 0.7,
      bringToFront = TRUE),
    label = labels,
    labelOptions = labelOptions(
      style = list("font-weight" = "normal", padding = "3px 8px"),
      textsize = "15px",
      direction = "auto"))
```

![](README_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Map to explore spatial availability:

``` r

bins <- quantile(results$vi, na.rm = TRUE) |> as.numeric()
pal <- colorBin("RdBu", domain = results$vi, bins = bins)

labels <- sprintf(
  "<strong>%s</strong><br/>%g workers<br/>%g jobs available<br/>%g jobs / person",
  results$id, 
  results$P,
  results$Vi,
  results$vi
) %>% lapply(htmltools::HTML)

leaflet(data = results |> st_transform(crs = 4326 )) |> 
  addPolygons(
    fillColor = ~pal(vi),
    weight = 2,
    opacity = 1,
    color = "white",
    dashArray = "3",
    fillOpacity = 0.7,
    highlightOptions = highlightOptions(
      weight = 5,
      color = "#666",
      dashArray = "",
      fillOpacity = 0.7,
      bringToFront = TRUE),
    label = labels,
    labelOptions = labelOptions(
      style = list("font-weight" = "normal", padding = "3px 8px"),
      textsize = "15px",
      direction = "auto"))
```

![](README_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->
