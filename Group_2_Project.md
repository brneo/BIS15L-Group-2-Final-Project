---
title: "group2covidfoodproject"
author: “Mildred Hernandez, Brian Rezende, Margarita Ibarra, Byron Corado”
date: "2021-02-28"
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
fat_supply_2 <- fat_supply %>%
  select(Country:Vegetables) %>%
  pivot_longer(-Country,
               names_to = "food_division",
               values_to = "food_division_f")
fat_supply_2
```

```
## # A tibble: 3,910 x 3
##    Country     food_division            food_division_f
##    <chr>       <chr>                              <dbl>
##  1 Afghanistan Alcoholic Beverages               0     
##  2 Afghanistan Animal Products                  21.6   
##  3 Afghanistan Animal fats                       6.22  
##  4 Afghanistan Aquatic Products, Other           0     
##  5 Afghanistan Cereals - Excluding Beer          8.04  
##  6 Afghanistan Eggs                              0.686 
##  7 Afghanistan Fish, Seafood                     0.0327
##  8 Afghanistan Fruits - Excluding Wine           0.425 
##  9 Afghanistan Meat                              6.12  
## 10 Afghanistan Miscellaneous                     0.0163
## # ... with 3,900 more rows
```


```r
fat_supply_covid <- fat_supply %>% 
  select(Country, Confirmed:Population) %>% 
  pivot_longer(-Country, 
               names_to = "covid_status",
               values_to = "covid_stats")
fat_supply_covid
```

```
## # A tibble: 850 x 3
##    Country     covid_status covid_stats
##    <chr>       <chr>              <dbl>
##  1 Afghanistan Confirmed        1.42e-1
##  2 Afghanistan Deaths           6.19e-3
##  3 Afghanistan Recovered        1.23e-1
##  4 Afghanistan Active           1.26e-2
##  5 Afghanistan Population       3.89e+7
##  6 Albania     Confirmed        2.97e+0
##  7 Albania     Deaths           5.10e-2
##  8 Albania     Recovered        1.79e+0
##  9 Albania     Active           1.12e+0
## 10 Albania     Population       2.84e+6
## # ... with 840 more rows
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
protein_supply_2 <- protein_supply%>% 
  select(Country:Vegetables) %>% 
  pivot_longer(-Country,
               names_to = "food_division",
               values_to = "food_division_p")
protein_supply_2
```

```
## # A tibble: 3,740 x 3
##    Country     food_division            food_division_p
##    <chr>       <chr>                              <dbl>
##  1 Afghanistan Alcoholic Beverages               0     
##  2 Afghanistan Animal Products                   9.75  
##  3 Afghanistan Animal fats                       0.0277
##  4 Afghanistan Aquatic Products, Other           0     
##  5 Afghanistan Cereals - Excluding Beer         36.0   
##  6 Afghanistan Eggs                              0.407 
##  7 Afghanistan Fish, Seafood                     0.0647
##  8 Afghanistan Fruits - Excluding Wine           0.582 
##  9 Afghanistan Meat                              3.13  
## 10 Afghanistan Milk - Excluding Butter           5.53  
## # ... with 3,730 more rows
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
food_supply_2 <- food_supply%>% 
  select(Country:Vegetables) %>% 
  pivot_longer(-Country,
               names_to = "food_division",
               values_to = "food_division_x")
food_supply_2
```

```
## # A tibble: 3,740 x 3
##    Country     food_division            food_division_x
##    <chr>       <chr>                              <dbl>
##  1 Afghanistan Alcoholic Beverages               0.0014
##  2 Afghanistan Animal fats                       0.197 
##  3 Afghanistan Animal Products                   9.43  
##  4 Afghanistan Aquatic Products, Other           0     
##  5 Afghanistan Cereals - Excluding Beer         24.8   
##  6 Afghanistan Eggs                              0.210 
##  7 Afghanistan Fish, Seafood                     0.035 
##  8 Afghanistan Fruits - Excluding Wine           5.35  
##  9 Afghanistan Meat                              1.20  
## 10 Afghanistan Milk - Excluding Butter           7.58  
## # ... with 3,730 more rows
```

#Joining the Data

```r
initial_join <- full_join(fat_supply_2, (protein_supply_2 %>% select(Country, food_division_p)), by="Country")
initial_join
```

```
## # A tibble: 86,020 x 4
##    Country     food_division       food_division_f food_division_p
##    <chr>       <chr>                         <dbl>           <dbl>
##  1 Afghanistan Alcoholic Beverages               0          0     
##  2 Afghanistan Alcoholic Beverages               0          9.75  
##  3 Afghanistan Alcoholic Beverages               0          0.0277
##  4 Afghanistan Alcoholic Beverages               0          0     
##  5 Afghanistan Alcoholic Beverages               0         36.0   
##  6 Afghanistan Alcoholic Beverages               0          0.407 
##  7 Afghanistan Alcoholic Beverages               0          0.0647
##  8 Afghanistan Alcoholic Beverages               0          0.582 
##  9 Afghanistan Alcoholic Beverages               0          3.13  
## 10 Afghanistan Alcoholic Beverages               0          5.53  
## # ... with 86,010 more rows
```

```r
initial_join_2 <- full_join(initial_join, (food_supply_2 %>% select(Country, food_division_x)), by="Country")
initial_join_2
```

```
## # A tibble: 1,892,440 x 5
##    Country     food_division     food_division_f food_division_p food_division_x
##    <chr>       <chr>                       <dbl>           <dbl>           <dbl>
##  1 Afghanistan Alcoholic Bevera~               0               0          0.0014
##  2 Afghanistan Alcoholic Bevera~               0               0          0.197 
##  3 Afghanistan Alcoholic Bevera~               0               0          9.43  
##  4 Afghanistan Alcoholic Bevera~               0               0          0     
##  5 Afghanistan Alcoholic Bevera~               0               0         24.8   
##  6 Afghanistan Alcoholic Bevera~               0               0          0.210 
##  7 Afghanistan Alcoholic Bevera~               0               0          0.035 
##  8 Afghanistan Alcoholic Bevera~               0               0          5.35  
##  9 Afghanistan Alcoholic Bevera~               0               0          1.20  
## 10 Afghanistan Alcoholic Bevera~               0               0          7.58  
## # ... with 1,892,430 more rows
```



## Including Plots

You can also embed plots, for example:

![](Group_2_Project_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
