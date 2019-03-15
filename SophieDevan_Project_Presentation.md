---
title: "National Park Visits"
output: 
  ioslides_presentation: 
    keep_md: yes
---

# Getting Started

## Load libraries

```r
library(tidyverse)
```

```
## ── Attaching packages ────────────────────────────────────────────────────────── tidyverse 1.2.1 ──
```

```
## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
## ✔ readr   1.3.1     ✔ forcats 0.3.0
```

```
## ── Conflicts ───────────────────────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(skimr)
library(paletteer)
```

## Get dataframe of palettes

```r
colors<-
  paletteer::palettes_d_names
```

## Set palette

```r
my_palette <-
  paletteer_d(package="ggsci", palette="category20_d3")
my_palette2 <-
  paletteer_d(package="ggsci", palette="category20_d3", 1)
```

## Read csv

```r
parks <- 
  readr::read_csv("National_Parks_Statistics.csv", skip=3, na=c("NA", "N/A", "#N/A"))
```

```
## Parsed with column specification:
## cols(
##   .default = col_number(),
##   ParkName = col_character(),
##   UnitCode = col_character(),
##   ParkType = col_character(),
##   Region = col_character(),
##   State = col_character(),
##   Year = col_double(),
##   Month = col_double(),
##   ConcessionerLodging = col_double(),
##   ConcessionerCamping = col_double(),
##   Backcountry = col_double(),
##   NonRecreationOvernightStays = col_double(),
##   ParkNameTotal = col_character(),
##   UnitCodeTotal = col_character(),
##   ParkTypeTotal = col_character(),
##   RegionTotal = col_character(),
##   StateTotal = col_character(),
##   YearTotal = col_double(),
##   ConcessionerLodgingTotal = col_double(),
##   NonRecreationOvernightStaysTotal = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

```
## Warning: 48461 parsing failures.
##  row         col               expected actual                            file
## 1503 Backcountry no trailing characters   ,615 'National_Parks_Statistics.csv'
## 1504 Backcountry no trailing characters   ,372 'National_Parks_Statistics.csv'
## 1505 Backcountry no trailing characters   ,780 'National_Parks_Statistics.csv'
## 1506 Backcountry no trailing characters   ,550 'National_Parks_Statistics.csv'
## 1507 Backcountry no trailing characters   ,457 'National_Parks_Statistics.csv'
## .... ........... ...................... ...... ...............................
## See problems(...) for more details.
```

## Get variable names

```r
names(parks)
```

```
##  [1] "ParkName"                         "UnitCode"                        
##  [3] "ParkType"                         "Region"                          
##  [5] "State"                            "Year"                            
##  [7] "Month"                            "RecreationVisits"                
##  [9] "NonRecreationVisits"              "RecreationHours"                 
## [11] "NonRecreationHours"               "ConcessionerLodging"             
## [13] "ConcessionerCamping"              "TentCampers"                     
## [15] "RVCampers"                        "Backcountry"                     
## [17] "NonRecreationOvernightStays"      "MiscellaneousOvernightStays"     
## [19] "ParkNameTotal"                    "UnitCodeTotal"                   
## [21] "ParkTypeTotal"                    "RegionTotal"                     
## [23] "StateTotal"                       "YearTotal"                       
## [25] "RecreationVisitsTotal"            "NonRecreationVisitsTotal"        
## [27] "RecreationHoursTotal"             "NonRecreationHoursTotal"         
## [29] "ConcessionerLodgingTotal"         "ConcessionerCampingTotal"        
## [31] "TentCampersTotal"                 "RVCampersTotal"                  
## [33] "BackcountryTotal"                 "NonRecreationOvernightStaysTotal"
## [35] "MiscellaneousOvernightStaysTotal"
```

## Summarize data

```r
glimpse(parks)
```

```
## Observations: 79,949
## Variables: 35
## $ ParkName                         <chr> "Acadia NP", "Acadia NP", "Acad…
## $ UnitCode                         <chr> "ACAD", "ACAD", "ACAD", "ACAD",…
## $ ParkType                         <chr> "National Park", "National Park…
## $ Region                           <chr> "Northeast", "Northeast", "Nort…
## $ State                            <chr> "ME", "ME", "ME", "ME", "ME", "…
## $ Year                             <dbl> 1979, 1979, 1979, 1979, 1979, 1…
## $ Month                            <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, …
## $ RecreationVisits                 <dbl> 6011, 5243, 11165, 219351, 3394…
## $ NonRecreationVisits              <dbl> 15252, 13776, 15252, 37657, 506…
## $ RecreationHours                  <dbl> 37446, 17661, 36051, 1334058, 2…
## $ NonRecreationHours               <dbl> 15252, 13776, 15252, 37657, 506…
## $ ConcessionerLodging              <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ ConcessionerCamping              <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ TentCampers                      <dbl> 102, 53, 176, 1037, 3193, 23821…
## $ RVCampers                        <dbl> 13, 8, 37, 459, 1148, 9819, 232…
## $ Backcountry                      <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ NonRecreationOvernightStays      <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ MiscellaneousOvernightStays      <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ ParkNameTotal                    <chr> "Acadia NP", "Acadia NP", "Acad…
## $ UnitCodeTotal                    <chr> "ACAD", "ACAD", "ACAD", "ACAD",…
## $ ParkTypeTotal                    <chr> "National Park", "National Park…
## $ RegionTotal                      <chr> "Northeast", "Northeast", "Nort…
## $ StateTotal                       <chr> "ME", "ME", "ME", "ME", "ME", "…
## $ YearTotal                        <dbl> 1979, 1979, 1979, 1979, 1979, 1…
## $ RecreationVisitsTotal            <dbl> 2787366, 2787366, 2787366, 2787…
## $ NonRecreationVisitsTotal         <dbl> 395913, 395913, 395913, 395913,…
## $ RecreationHoursTotal             <dbl> 17155530, 17155530, 17155530, 1…
## $ NonRecreationHoursTotal          <dbl> 198056, 198056, 198056, 198056,…
## $ ConcessionerLodgingTotal         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ ConcessionerCampingTotal         <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ TentCampersTotal                 <dbl> 139708, 139708, 139708, 139708,…
## $ RVCampersTotal                   <dbl> 74279, 74279, 74279, 74279, 742…
## $ BackcountryTotal                 <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ NonRecreationOvernightStaysTotal <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
## $ MiscellaneousOvernightStaysTotal <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0…
```

## Map na's

```r
parks %>%
  purrr::map_df(~ sum(is.na(.))) %>%
  tidyr::gather(variables, num_nas) %>% 
  arrange(desc(num_nas))
```

```
## # A tibble: 35 x 2
##    variables                        num_nas
##    <chr>                              <int>
##  1 ConcessionerLodgingTotal           19224
##  2 ConcessionerLodging                10376
##  3 Backcountry                         9875
##  4 NonRecreationOvernightStaysTotal    4499
##  5 ConcessionerCamping                 2880
##  6 NonRecreationOvernightStays         1607
##  7 ParkName                               0
##  8 UnitCode                               0
##  9 ParkType                               0
## 10 Region                                 0
## # … with 25 more rows
```

## Rename variables

```r
parks_renamed <- parks %>%
  dplyr::rename(
            park_name = ParkName,
            unit_code = UnitCode,                     
            park_type = ParkType,
               region = Region,                         
                state = State,
                year = Year,                           
                month = Month,   
            rec_visits = RecreationVisits,
        non_rec_vists = NonRecreationVisits,
            rec_hours = RecreationHours,
         non_rec_hours = NonRecreationHours,
          conc_lodging = ConcessionerLodging,            
          conc_camping = ConcessionerCamping,
          tent_campers = TentCampers,
            rv_campers = RVCampers,
            backcountry = Backcountry,               
non_rec_overnight_stays = NonRecreationOvernightStays,
  misc_overnight_stays = MiscellaneousOvernightStays,
      park_name_total = ParkNameTotal,
      unit_code_total = UnitCodeTotal,    
      park_type_total = ParkTypeTotal,            
        regional_total = RegionTotal,    
          state_total = StateTotal,
            year_total = YearTotal,
      rec_visits_total = RecreationVisitsTotal,
  non_rec_visits_total = NonRecreationVisitsTotal,
      rec_hours_total = RecreationHoursTotal,
  non_rec_hours_total = NonRecreationHoursTotal,   
    conc_lodging_total = ConcessionerLodgingTotal,
    conc_camping_total = ConcessionerCampingTotal,
    tent_campers_total = TentCampersTotal,
      rv_campers_total = RVCampersTotal,      
      backgrounty_total = BackcountryTotal,                
      non_rec_overnight = NonRecreationOvernightStaysTotal,
misc_overnight_stays_total = MiscellaneousOvernightStaysTotal
          )
```

## Get rid of scientific notation

```r
options(scipen=999)
```

# Preliminary Analysis

## What is the most popular park type? 
- GGNRA in 1987 had the highest average number of visits 
- NRAs seem to be the most popular park type, at least recreationally
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

## What is the most popular park?
- Kobuk Valley is least popular
- Great Smoky Mountains is most popular
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-11-1.png)<!-- -->



## What is the best season to go?
- July is the most popular month
- January is least popular
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

## What region is the most popular?

```r
parks_renamed %>%
  group_by(region) %>%
   summarize(mean_rec_visits = mean(rec_visits), 
              min_rec_visits = min(rec_visits),
              max_rec_visits = max(rec_visits),
              total = n()) %>%
  arrange(desc(mean_rec_visits))
```

```
## # A tibble: 7 x 5
##   region           mean_rec_visits min_rec_visits max_rec_visits total
##   <chr>                      <dbl>          <dbl>          <dbl> <int>
## 1 Northeast                159158.              0        3912215  7830
## 2 Pacific West             122492.              0        2787131 15719
## 3 Southeast                 95338.            -39        1761918 11280
## 4 Midwest                   53000.              0        1341013 11460
## 5 Intermountain             52355.              0        1009665 28224
## 6 Alaska                     7568.              0         222077  5412
## 7 National Capital            567.              0           2383    24
```

## What region is the most popular?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

## How do regions compare?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-16-1.png)<!-- -->

# Our question: How did the recessions of 1981 and 2008 affect rec visits in the 5 most popular National Parks?

## How did visits fare across the parks?

![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

## How did visits fare across the parks?
- visits have been going up going up over time
- peaked in late 80s then again in 2016 and onwards
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-18-1.png)<!-- -->

## How did visits fare in the Great Smoky Mountains?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-19-1.png)<!-- -->

## How did visits fare in the Grand Canyon?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-20-1.png)<!-- -->

## How did visits fare in Yosemite?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-21-1.png)<!-- -->

```
## List of 1
##  $ legend.position: chr "none"
##  - attr(*, "class")= chr [1:2] "theme" "gg"
##  - attr(*, "complete")= logi FALSE
##  - attr(*, "validate")= logi TRUE
```

## How did visits fare in Yellowstone?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-22-1.png)<!-- -->

## How did visits fare in Olympic?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-23-1.png)<!-- -->

## How do the graphs compare?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-24-1.png)<!-- -->

## How did visits fare in the least popular park, Kobuk Valley?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-25-1.png)<!-- -->

## How did visits fare in Gates of the Arctic?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-26-1.png)<!-- -->

## How did visits fare in Lake Clark?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-27-1.png)<!-- -->

## How did visits fare in Isle Royale?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-28-1.png)<!-- -->

## How did visits fare in Katmai?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-29-1.png)<!-- -->

## How do the graphs compare?
![](SophieDevan_Project_Presentation_files/figure-html/unnamed-chunk-30-1.png)<!-- -->
