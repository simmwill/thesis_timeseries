Exploratory Data Analysis
================
Will Simmons
11/4/2019

``` r
library(tidyverse)
```

    ## -- Attaching packages ---------------------------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.2.1     v purrr   0.3.3
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   1.0.0     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## -- Conflicts ------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readxl)
```

#### Importing and cleaning data

``` r
nsp = read_excel('./data/nsp_subset_datechanged.xlsx') %>% 
  select(-rd, -thana, -union, -vill, -para, -match_quality, -year) %>% 
  mutate(dov = as.Date(dov), ## converting POSIXct to Date
         surv_area = as.ordered(surv_area), 
         area_name = as.factor(area_name),
         area_name = forcats::fct_reorder(area_name, as.numeric(surv_area)), ## area_name is factor ordered by surv_area
         zwfl = as.numeric(zwfl), ## NAs will be introduced by coercion
         zlen = as.numeric(zlen),
         zwei = as.numeric(zwei),
         ageindays = as.numeric(ageindays)
  ) 
```

#### Table of survey area number by area name

| surv\_area | area\_name                 |
| :--------- | :------------------------- |
| 1          | Dhaka slum                 |
| 2          | Khulna slum                |
| 3          | Chittagong slum            |
| 4          | Pirganj                    |
| 5          | Chilmari/Kaunia            |
| 6          | Santhia/Shahjadpur         |
| 7          | Shakhipur/Sreepur          |
| 8          | Saturia/Serajdikhan        |
| 9          | Morrelganj/Fakirhat        |
| 10         | Mirzaganj/Patuakhali sadar |
| 11         | Moheshkhali/Coxs Bazaar    |
| 12         | Manda/Naogaon Sadar        |
| 13         | Kamalganj/Sreemangal       |
| 14         | Jhikargachha/Kaliganj      |
| 15         | Daulatpur/Gangni           |
| 16         | Derai/Jamalganj            |
| 17         | Golapganj/Fenchuganj       |
| 18         | Sarail/Nabinagar           |
| 19         | Chouddagram                |
| 20         | Nakla/Jamalpur Sadar       |
| 21         | Rangunia/Hathazari         |
| 22         | Kendua/Atpara              |
| 23         | Pathargantha               |
| 24         | Charfassion/Lalmhan        |
| 25         | Shyamnagar/Debhata         |

#### Survey frequency by time and area

``` r
nsp %>% 
  ggplot(aes(x = dov, y = zwfl)) +
  geom_point(size = 0.01) +
  facet_wrap(. ~ area_name, ncol = 5) +
  xlim(as.Date("1990-01-01"), as.Date("2006-12-31"))
```

    ## Warning: Removed 14632 rows containing missing values (geom_point).

![](thesis_eda_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
plot_zwfl_timeseries = function(area) {
  
  nsp %>% 
    filter(area_name == area) %>% 
    ggplot(aes(x = dov, y = zwfl)) +
    geom_point(size = 0.01) +
    xlim(as.Date("1990-01-01"), as.Date("2006-12-31"))
  
}

area_names = 
  nsp %>% 
  group_by(area_name) %>% 
  select(area_name) %>% 
  unique() %>% 
  as.character()

# plot one area
plot_zwfl_timeseries("Shyamnagar/Debhata")
```

    ## Warning: Removed 376 rows containing missing values (geom_point).

![](thesis_eda_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
# figure out how to plot all 25 using map()
# 
# plot all
# plots = map(area_names, plot_zwfl_timeseries)
```

#### Reading in ENACTS data

``` r
enacts_read = read_excel('./data/ENACTS.xlsx') 

enacts =
  enacts_read %>% 
  mutate(date = matlab2POS_dhaka(pull(enacts_read, matlab_daynum)),
         surv_area = as.ordered(surv_area)) %>%  ## using MATLAB date conversion defined in beginning (hidden)
  select(surv_area, date, everything(), -matlab_daynum, -month, -year, -contains('runavg'), -hotday, -starts_with('movsum'), -daynum) %>% view
```

#### Preliminary ENACTS plots

``` r
enacts %>% 
  filter(surv_area == 4) %>% 
  mutate(month_timeseries = cut(date, breaks = "month"),
         month_timeseries = as.Date(month_timeseries)) %>% 
  group_by(month_timeseries) %>% 
  summarize(mean_tmax = mean(tmax),
            mean_tmin = mean(tmin), 
            mean_precip = mean(precip)) %>% 
  ggplot(aes(x = month_timeseries)) +
  geom_line(aes(y = mean_tmax, color = 'mean_tmax')) + 
  geom_line(aes(y = mean_tmin, color = 'mean_tmin')) +
  geom_line(aes(y = mean_precip/2, color = "mean_precip")) +
  scale_color_manual(breaks = c('mean_tmax', 'mean_tmin', 'mean_precip'),
                     values = c('#A44D51', '#EED596', '#06826A')
  ) %>% 
  labs(x = "Day",
       y = "Mean monthly temperature [°C]\n",
       title = "Mean monthly weather patterns across data, Area 4") +
  scale_y_continuous(sec.axis = sec_axis(~.*2, name = "Mean monthly precipitation [mm]\n")) +
  theme_light() +
  theme(legend.title = element_blank(),
        plot.title = element_text(hjust = 0.5))
```

![](thesis_eda_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->
