---
title: "group2covidfoodproject"
author: “Mildred Hernandez, Brian Rezende, Margarita Ibarra, Byron Corado”
date: "2021-02-19"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---




```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.0.4     v dplyr   1.0.2
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(here)
```

```
## here() starts at C:/Users/mildr/OneDrive/Desktop/BIS15L-Group-2-Final-Project
```

```r
options(scipen=999) #disables scientific notation when printing
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

##Loading the Data


```r
fat_supply <- readr::read_csv("data/Fat_Supply_Quantity_Data.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   Country = col_character(),
##   Undernourished = col_character(),
##   `Unit (all except Population)` = col_character()
## )
## i Use `spec()` for the full column specifications.
```


```r
protein_supply <- readr::read_csv("data/Protein_Supply_Quantity_Data.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   Country = col_character(),
##   Undernourished = col_character(),
##   `Unit (all except Population)` = col_character()
## )
## i Use `spec()` for the full column specifications.
```

```r
food_supply <- readr::read_csv("data/Food_Supply_Quantity_kg_Data.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   Country = col_character(),
##   Undernourished = col_character(),
##   `Unit (all except Population)` = col_character()
## )
## i Use `spec()` for the full column specifications.
```


##Renaming the Data

```r
fat_supply_2 <- fat_supply %>% rename_all(paste0, "_f")
```


```r
fat_supply <- fat_supply_2 %>%
  rename(Country = Country_f)
fat_supply
```

```
## # A tibble: 170 x 32
##    Country `Alcoholic Beve~ `Animal Product~ `Animal fats_f` `Aquatic Produc~
##    <chr>              <dbl>            <dbl>           <dbl>            <dbl>
##  1 Afghan~                0             21.6           6.22                 0
##  2 Albania                0             32.0           3.42                 0
##  3 Algeria                0             14.4           0.897                0
##  4 Angola                 0             15.3           1.31                 0
##  5 Antigu~                0             27.7           4.67                 0
##  6 Argent~                0             30.4           3.31                 0
##  7 Armenia                0             29.7           6.26                 0
##  8 Austra~                0             24.1           4.60                 0
##  9 Austria                0             27.8          12.9                  0
## 10 Azerba~                0             32.1           7.80                 0
## # ... with 160 more rows, and 27 more variables: `Cereals - Excluding
## #   Beer_f` <dbl>, Eggs_f <dbl>, `Fish, Seafood_f` <dbl>, `Fruits - Excluding
## #   Wine_f` <dbl>, Meat_f <dbl>, Miscellaneous_f <dbl>, `Milk - Excluding
## #   Butter_f` <dbl>, Offals_f <dbl>, Oilcrops_f <dbl>, Pulses_f <dbl>,
## #   Spices_f <dbl>, `Starchy Roots_f` <dbl>, Stimulants_f <dbl>, `Sugar
## #   Crops_f` <dbl>, `Sugar & Sweeteners_f` <dbl>, Treenuts_f <dbl>, `Vegetal
## #   Products_f` <dbl>, `Vegetable Oils_f` <dbl>, Vegetables_f <dbl>,
## #   Obesity_f <dbl>, Undernourished_f <chr>, Confirmed_f <dbl>, Deaths_f <dbl>,
## #   Recovered_f <dbl>, Active_f <dbl>, Population_f <dbl>, `Unit (all except
## #   Population)_f` <chr>
```

```r
protein_supply_2 <- protein_supply %>% rename_all(paste0, "_p")
```


```r
protein_supply <- protein_supply_2 %>%
  rename(Country = Country_p)
protein_supply
```

```
## # A tibble: 170 x 32
##    Country `Alcoholic Beve~ `Animal Product~ `Animal fats_p` `Aquatic Produc~
##    <chr>              <dbl>            <dbl>           <dbl>            <dbl>
##  1 Afghan~           0                  9.75          0.0277           0     
##  2 Albania           0.184             27.7           0.0711           0     
##  3 Algeria           0.0323            13.8           0.0054           0     
##  4 Angola            0.628             15.2           0.0277           0     
##  5 Antigu~           0.154             33.2           0.129            0     
##  6 Argent~           0.170             32.0           0.0097           0     
##  7 Armenia           0.0411            22.9           0.144            0     
##  8 Austra~           0.291             33.0           0.074            0.0046
##  9 Austria           0.615             30.0           0.338            0     
## 10 Azerba~           0.346             16.3           0.0596           0     
## # ... with 160 more rows, and 27 more variables: `Cereals - Excluding
## #   Beer_p` <dbl>, Eggs_p <dbl>, `Fish, Seafood_p` <dbl>, `Fruits - Excluding
## #   Wine_p` <dbl>, Meat_p <dbl>, `Milk - Excluding Butter_p` <dbl>,
## #   Offals_p <dbl>, Oilcrops_p <dbl>, Pulses_p <dbl>, Spices_p <dbl>, `Starchy
## #   Roots_p` <dbl>, Stimulants_p <dbl>, `Sugar Crops_p` <dbl>, `Sugar &
## #   Sweeteners_p` <dbl>, Treenuts_p <dbl>, `Vegetal Products_p` <dbl>,
## #   `Vegetable Oils_p` <dbl>, Vegetables_p <dbl>, Miscellaneous_p <dbl>,
## #   Obesity_p <dbl>, Undernourished_p <chr>, Confirmed_p <dbl>, Deaths_p <dbl>,
## #   Recovered_p <dbl>, Active_p <dbl>, Population_p <dbl>, `Unit (all except
## #   Population)_p` <chr>
```

```r
food_supply_2 <- food_supply %>% 
  rename_all(paste0, "_x")
```


```r
food_supply <- food_supply_2 %>% 
  rename(Country = Country_x)
food_supply
```

```
## # A tibble: 170 x 32
##    Country `Alcoholic Beve~ `Animal fats_x` `Animal Product~ `Aquatic Produc~
##    <chr>              <dbl>           <dbl>            <dbl>            <dbl>
##  1 Afghan~           0.0014          0.197              9.43           0     
##  2 Albania           1.67            0.136             18.8            0     
##  3 Algeria           0.271           0.0282             9.63           0     
##  4 Angola            5.81            0.056              4.93           0     
##  5 Antigu~           3.58            0.0087            16.7            0     
##  6 Argent~           4.27            0.223             19.3            0     
##  7 Armenia           0.401           0.183             13.6            0     
##  8 Austra~           5.54            0.314             21.4            0.0033
##  9 Austria           7.02            0.856             19.6            0.0011
## 10 Azerba~           3.60            0.254             11.6            0     
## # ... with 160 more rows, and 27 more variables: `Cereals - Excluding
## #   Beer_x` <dbl>, Eggs_x <dbl>, `Fish, Seafood_x` <dbl>, `Fruits - Excluding
## #   Wine_x` <dbl>, Meat_x <dbl>, `Milk - Excluding Butter_x` <dbl>,
## #   Miscellaneous_x <dbl>, Offals_x <dbl>, Oilcrops_x <dbl>, Pulses_x <dbl>,
## #   Spices_x <dbl>, `Starchy Roots_x` <dbl>, Stimulants_x <dbl>, `Sugar &
## #   Sweeteners_x` <dbl>, `Sugar Crops_x` <dbl>, Treenuts_x <dbl>, `Vegetable
## #   Oils_x` <dbl>, Vegetables_x <dbl>, `Vegetal Products_x` <dbl>,
## #   Obesity_x <dbl>, Undernourished_x <chr>, Confirmed_x <dbl>, Deaths_x <dbl>,
## #   Recovered_x <dbl>, Active_x <dbl>, Population_x <dbl>, `Unit (all except
## #   Population)_x` <chr>
```

## Including Plots

You can also embed plots, for example:

![](Group_2_Project_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
