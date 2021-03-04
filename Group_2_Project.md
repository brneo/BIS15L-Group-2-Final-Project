---
title: "group2covidfoodproject"
author: “Mildred Hernandez, Brian Rezende, Margarita Ibarra, Byron Corado”
date: "2021-03-03"
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
## v tibble  3.0.6     v dplyr   1.0.4
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.1
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



```r
#fat_supply %>% rename_all(paste0, "_f", -"Country")
#fat_supply %>% rename_all(paste0, "_f", -Country)
#fat_supply %>% rename_all(paste0, "_f", -Country_f)
#fat_supply %>% rename_all(paste0, "_f", -"Country_f")
#fat_supply %>% rename_all(paste0, "_f")
#fat_supply
```



```r
#fat_supply_2 <- fat_supply %>% rename_all(paste0, "_f")
```



```r
#fat_supply <- fat_supply_2 %>%
#rename(Country = Country_f)
```



```r
#fat_supply$Country
```



```r
#fat_supply_2 <- fat_supply %>% rename_all(paste0, "_f")
```



```r
#fat_supply <- fat_supply_2 %>%
#rename(Country = Country_f)
#fat_supply
#fat_supply
#protein_supply_2 <- protein_supply %>% rename_all(paste0, "_p")
#protein_supply_2 <- protein_supply %>% rename_all(paste0, "_p")
#protein_supply <- protein_supply_2 %>%
#rename(Country = Country_p)
#protein_supply
#food_supply_2 <- food_supply %>%
#rename_all(paste0, "_x")
#food_supply <- food_supply_2 %>%
#rename(Country = Country_x)
##rename(Country = Country_x)
food_supply
```

```
## # A tibble: 170 x 32
##    Country    `Alcoholic Bever~ `Animal fats` `Animal Product~ `Aquatic Product~
##    <chr>                  <dbl>         <dbl>            <dbl>             <dbl>
##  1 Afghanist~            0.0014        0.197              9.43            0     
##  2 Albania               1.67          0.136             18.8             0     
##  3 Algeria               0.271         0.0282             9.63            0     
##  4 Angola                5.81          0.056              4.93            0     
##  5 Antigua a~            3.58          0.0087            16.7             0     
##  6 Argentina             4.27          0.223             19.3             0     
##  7 Armenia               0.401         0.183             13.6             0     
##  8 Australia             5.54          0.314             21.4             0.0033
##  9 Austria               7.02          0.856             19.6             0.0011
## 10 Azerbaijan            3.60          0.254             11.6             0     
## # ... with 160 more rows, and 27 more variables:
## #   Cereals - Excluding Beer <dbl>, Eggs <dbl>, Fish, Seafood <dbl>,
## #   Fruits - Excluding Wine <dbl>, Meat <dbl>, Milk - Excluding Butter <dbl>,
## #   Miscellaneous <dbl>, Offals <dbl>, Oilcrops <dbl>, Pulses <dbl>,
## #   Spices <dbl>, Starchy Roots <dbl>, Stimulants <dbl>,
## #   Sugar & Sweeteners <dbl>, Sugar Crops <dbl>, Treenuts <dbl>,
## #   Vegetable Oils <dbl>, Vegetables <dbl>, Vegetal Products <dbl>,
## #   Obesity <dbl>, Undernourished <chr>, Confirmed <dbl>, Deaths <dbl>,
## #   Recovered <dbl>, Active <dbl>, Population <dbl>,
## #   Unit (all except Population) <chr>
```

#Joining the Data

```r
#initial_join <- left_join(fat_supply_2, (protein_supply_2 %>% select(Country, food_division_p)), by="Country")
```


```r
#initial_join_2 <- left_join(initial_join, (food_supply_2 %>% select(Country, food_division_x)), by="Country")
```

```r
#food_intake[, c(colnames(food_intake))]
```

## Including Plots

You can also embed plots, for example:

![](Group_2_Project_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
