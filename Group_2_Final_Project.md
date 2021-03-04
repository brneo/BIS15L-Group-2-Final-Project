---
title: "group2covidfoodproject"
author: “Mildred Hernandez, Brian Rezende, Margarita Ibarra, Byron Corado”
date: "2021-03-04"
output: 
  html_document: 
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

###Loading the Data

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
###Cleaning the Data

```r
food_supply_clean <- janitor::clean_names(food_supply)
food_supply_clean
```

```
## # A tibble: 170 x 32
##    country      alcoholic_bevera~ animal_fats animal_products aquatic_products_~
##    <chr>                    <dbl>       <dbl>           <dbl>              <dbl>
##  1 Afghanistan             0.0014      0.197             9.43             0     
##  2 Albania                 1.67        0.136            18.8              0     
##  3 Algeria                 0.271       0.0282            9.63             0     
##  4 Angola                  5.81        0.056             4.93             0     
##  5 Antigua and~            3.58        0.0087           16.7              0     
##  6 Argentina               4.27        0.223            19.3              0     
##  7 Armenia                 0.401       0.183            13.6              0     
##  8 Australia               5.54        0.314            21.4              0.0033
##  9 Austria                 7.02        0.856            19.6              0.0011
## 10 Azerbaijan              3.60        0.254            11.6              0     
## # ... with 160 more rows, and 27 more variables: cereals_excluding_beer <dbl>,
## #   eggs <dbl>, fish_seafood <dbl>, fruits_excluding_wine <dbl>, meat <dbl>,
## #   milk_excluding_butter <dbl>, miscellaneous <dbl>, offals <dbl>,
## #   oilcrops <dbl>, pulses <dbl>, spices <dbl>, starchy_roots <dbl>,
## #   stimulants <dbl>, sugar_sweeteners <dbl>, sugar_crops <dbl>,
## #   treenuts <dbl>, vegetable_oils <dbl>, vegetables <dbl>,
## #   vegetal_products <dbl>, obesity <dbl>, undernourished <chr>,
## #   confirmed <dbl>, deaths <dbl>, recovered <dbl>, active <dbl>,
## #   population <dbl>, unit_all_except_population <chr>
```
###Viewing the Data

```r
glimpse(food_supply_clean)
```

```
## Rows: 170
## Columns: 32
## $ country                    <chr> "Afghanistan", "Albania", "Algeria", "Angol~
## $ alcoholic_beverages        <dbl> 0.0014, 1.6719, 0.2711, 5.8087, 3.5764, 4.2~
## $ animal_fats                <dbl> 0.1973, 0.1357, 0.0282, 0.0560, 0.0087, 0.2~
## $ animal_products            <dbl> 9.4341, 18.7684, 9.6334, 4.9278, 16.6613, 1~
## $ aquatic_products_other     <dbl> 0.0000, 0.0000, 0.0000, 0.0000, 0.0000, 0.0~
## $ cereals_excluding_beer     <dbl> 24.8097, 5.7817, 13.6816, 9.1085, 5.9960, 8~
## $ eggs                       <dbl> 0.2099, 0.5815, 0.5277, 0.0587, 0.2274, 0.9~
## $ fish_seafood               <dbl> 0.0350, 0.2126, 0.2416, 1.7707, 4.1489, 0.4~
## $ fruits_excluding_wine      <dbl> 5.3495, 6.7861, 6.3801, 6.0005, 10.7451, 6.~
## $ meat                       <dbl> 1.2020, 1.8845, 1.1305, 2.0571, 5.6888, 7.0~
## $ milk_excluding_butter      <dbl> 7.5828, 15.7213, 7.6189, 0.8311, 6.3663, 10~
## $ miscellaneous              <dbl> 0.0728, 0.1123, 0.1671, 0.1165, 0.7139, 0.0~
## $ offals                     <dbl> 0.2057, 0.2324, 0.0870, 0.1550, 0.2219, 0.3~
## $ oilcrops                   <dbl> 0.0700, 0.9377, 0.3493, 0.4186, 0.2172, 0.0~
## $ pulses                     <dbl> 0.2953, 0.2380, 0.4783, 0.6507, 0.1840, 0.0~
## $ spices                     <dbl> 0.0574, 0.0008, 0.0557, 0.0009, 0.1524, 0.0~
## $ starchy_roots              <dbl> 0.8802, 1.8096, 4.1340, 18.1102, 1.4522, 3.~
## $ stimulants                 <dbl> 0.3078, 0.1055, 0.2216, 0.0508, 0.1564, 0.4~
## $ sugar_sweeteners           <dbl> 1.3489, 1.5367, 1.8342, 1.8495, 3.8749, 3.0~
## $ sugar_crops                <dbl> 0.0000, 0.0000, 0.0000, 0.0000, 0.0000, 0.0~
## $ treenuts                   <dbl> 0.0770, 0.1515, 0.1152, 0.0061, 0.0253, 0.0~
## $ vegetable_oils             <dbl> 0.5345, 0.3261, 1.0310, 0.6463, 0.8102, 0.9~
## $ vegetables                 <dbl> 6.7642, 11.7753, 11.6484, 2.3041, 5.4495, 4~
## $ vegetal_products           <dbl> 40.5645, 31.2304, 40.3651, 45.0722, 33.3233~
## $ obesity                    <dbl> 4.5, 22.3, 26.6, 6.8, 19.1, 28.5, 20.9, 30.~
## $ undernourished             <chr> "29.8", "6.2", "3.9", "25", NA, "4.6", "4.3~
## $ confirmed                  <dbl> 0.142134196, 2.967300916, 0.244897085, 0.06~
## $ deaths                     <dbl> 0.0061857789, 0.0509513742, 0.0065581532, 0~
## $ recovered                  <dbl> 0.123373921, 1.792635659, 0.167572198, 0.05~
## $ active                     <dbl> 0.0125744965, 1.1237138830, 0.0707667335, 0~
## $ population                 <dbl> 38928000, 2838000, 44357000, 32522000, 9800~
## $ unit_all_except_population <chr> "%", "%", "%", "%", "%", "%", "%", "%", "%"~
```

```r
summary(food_supply_clean)
```

```
##    country          alcoholic_beverages  animal_fats      animal_products 
##  Length:170         Min.   : 0.0000     Min.   :0.00100   Min.   : 1.739  
##  Class :character   1st Qu.: 0.8956     1st Qu.:0.04022   1st Qu.: 7.237  
##  Mode  :character   Median : 2.8662     Median :0.11685   Median :12.098  
##                     Mean   : 3.0230     Mean   :0.22106   Mean   :12.182  
##                     3rd Qu.: 4.7110     3rd Qu.:0.25390   3rd Qu.:16.444  
##                     Max.   :15.3706     Max.   :1.35590   Max.   :26.887  
##                                                                           
##  aquatic_products_other cereals_excluding_beer      eggs       
##  Min.   :0.00000        Min.   : 3.401         Min.   :0.0239  
##  1st Qu.:0.00000        1st Qu.: 7.227         1st Qu.:0.1876  
##  Median :0.00000        Median :10.143         Median :0.4602  
##  Mean   :0.01399        Mean   :11.800         Mean   :0.4706  
##  3rd Qu.:0.00140        3rd Qu.:15.149         3rd Qu.:0.6442  
##  Max.   :1.67940        Max.   :29.805         Max.   :1.6960  
##                                                                
##   fish_seafood    fruits_excluding_wine      meat       milk_excluding_butter
##  Min.   :0.0342   Min.   : 0.6596       Min.   :0.356   Min.   : 0.0963      
##  1st Qu.:0.5571   1st Qu.: 3.5419       1st Qu.:1.891   1st Qu.: 2.1723      
##  Median :1.0292   Median : 5.0213       Median :3.425   Median : 5.3369      
##  Mean   :1.3872   Mean   : 5.6214       Mean   :3.376   Mean   : 6.5198      
##  3rd Qu.:1.8213   3rd Qu.: 6.8277       3rd Qu.:4.422   3rd Qu.:10.4071      
##  Max.   :8.7959   Max.   :19.3028       Max.   :8.170   Max.   :20.8378      
##                                                                              
##  miscellaneous         offals          oilcrops           pulses      
##  Min.   :0.00000   Min.   :0.0000   Min.   : 0.0098   Min.   :0.0000  
##  1st Qu.:0.03232   1st Qu.:0.1051   1st Qu.: 0.1341   1st Qu.:0.1296  
##  Median :0.19685   Median :0.1668   Median : 0.3266   Median :0.3008  
##  Mean   :0.44312   Mean   :0.1934   Mean   : 0.8181   Mean   :0.5371  
##  3rd Qu.:0.58362   3rd Qu.:0.2286   3rd Qu.: 0.6917   3rd Qu.:0.7349  
##  Max.   :3.66340   Max.   :1.2256   Max.   :12.1763   Max.   :3.4838  
##                                                                       
##      spices        starchy_roots       stimulants      sugar_sweeteners
##  Min.   :0.00000   Min.   : 0.6796   Min.   :0.00420   Min.   :0.3666  
##  1st Qu.:0.01650   1st Qu.: 2.0238   1st Qu.:0.08332   1st Qu.:1.7210  
##  Median :0.04255   Median : 3.1086   Median :0.15945   Median :2.6016  
##  Mean   :0.09101   Mean   : 5.3354   Mean   :0.20195   Mean   :2.7991  
##  3rd Qu.:0.12315   3rd Qu.: 5.7459   3rd Qu.:0.26180   3rd Qu.:3.7822  
##  Max.   :0.66260   Max.   :27.7128   Max.   :1.28230   Max.   :9.7259  
##                                                                        
##   sugar_crops         treenuts       vegetable_oils     vegetables    
##  Min.   :0.00000   Min.   :0.00000   Min.   :0.0915   Min.   : 0.857  
##  1st Qu.:0.00000   1st Qu.:0.02075   1st Qu.:0.5077   1st Qu.: 3.616  
##  Median :0.00000   Median :0.07995   Median :0.7744   Median : 5.028  
##  Mean   :0.09585   Mean   :0.11747   Mean   :0.8516   Mean   : 6.086  
##  3rd Qu.:0.00000   3rd Qu.:0.14865   3rd Qu.:1.0709   3rd Qu.: 7.802  
##  Max.   :3.06770   Max.   :0.75690   Max.   :2.2026   Max.   :19.299  
##                                                                       
##  vegetal_products    obesity      undernourished       confirmed        
##  Min.   :23.11    Min.   : 2.10   Length:170         Min.   : 0.000312  
##  1st Qu.:33.55    1st Qu.: 8.50   Class :character   1st Qu.: 0.140976  
##  Median :37.90    Median :21.20   Mode  :character   Median : 1.011570  
##  Mean   :37.81    Mean   :18.71                      Mean   : 2.021972  
##  3rd Qu.:42.76    3rd Qu.:25.70                      3rd Qu.: 3.487069  
##  Max.   :48.26    Max.   :45.60                      Max.   :10.408199  
##                   NA's   :3                          NA's   :6          
##      deaths           recovered           active          population        
##  Min.   :0.000000   Min.   :0.00000   Min.   :0.00000   Min.   :     54000  
##  1st Qu.:0.002013   1st Qu.:0.09911   1st Qu.:0.01203   1st Qu.:   2816250  
##  Median :0.011998   Median :0.47540   Median :0.08104   Median :  10181500  
##  Mean   :0.039370   Mean   :1.45236   Mean   :0.53516   Mean   :  44523641  
##  3rd Qu.:0.069503   3rd Qu.:2.62287   3rd Qu.:0.35818   3rd Qu.:  32716250  
##  Max.   :0.185428   Max.   :9.03987   Max.   :8.01982   Max.   :1402385000  
##  NA's   :6          NA's   :6         NA's   :8                             
##  unit_all_except_population
##  Length:170                
##  Class :character          
##  Mode  :character          
##                            
##                            
##                            
## 
```


```r
food_supply_clean %>%
  naniar::miss_var_summary()
```

```
## # A tibble: 32 x 3
##    variable            n_miss pct_miss
##    <chr>                <int>    <dbl>
##  1 active                   8     4.71
##  2 undernourished           7     4.12
##  3 confirmed                6     3.53
##  4 deaths                   6     3.53
##  5 recovered                6     3.53
##  6 obesity                  3     1.76
##  7 country                  0     0   
##  8 alcoholic_beverages      0     0   
##  9 animal_fats              0     0   
## 10 animal_products          0     0   
## # ... with 22 more rows
```
###Analysis

```r
food_supply_clean %>%
  select(country, deaths) %>%
  arrange(desc(deaths))
```

```
## # A tibble: 170 x 2
##    country                  deaths
##    <chr>                     <dbl>
##  1 Belgium                   0.185
##  2 Slovenia                  0.172
##  3 United Kingdom            0.167
##  4 Czechia                   0.160
##  5 Italy                     0.151
##  6 Bosnia and Herzegovina    0.146
##  7 North Macedonia           0.140
##  8 United States of America  0.140
##  9 Portugal                  0.136
## 10 Bulgaria                  0.134
## # ... with 160 more rows
```

```r
food_supply_clean %>%
  select(country, deaths) %>%
  arrange(-desc(deaths))
```

```
## # A tibble: 170 x 2
##    country                             deaths
##    <chr>                                <dbl>
##  1 Cambodia                         0        
##  2 Dominica                         0        
##  3 Lao People's Democratic Republic 0        
##  4 Saint Kitts and Nevis            0        
##  5 Samoa                            0        
##  6 Solomon Islands                  0        
##  7 Timor-Leste                      0        
##  8 Vanuatu                          0        
##  9 United Republic of Tanzania      0.0000352
## 10 Vietnam                          0.0000364
## # ... with 160 more rows
```

***Total Protein Consumption by Country, Focusing on those with the Three HIGHEST Death Percentages**

```r
food_supply_clean %>%
  select(country, deaths) %>%
  filter(country=="Belgium"|country=="Slovenia"|country=="United Kingdom"|country=="United States of America")
```

```
## # A tibble: 4 x 2
##   country                  deaths
##   <chr>                     <dbl>
## 1 Belgium                   0.185
## 2 Slovenia                  0.172
## 3 United Kingdom            0.167
## 4 United States of America  0.140
```


```r
food_supply_clean %>%
  filter(country=="Belgium"| country=="Slovenia"| country=="United Kingdom") %>%
  group_by(country, deaths) %>%
  summarize(total_protein_consumption = sum(animal_fats, animal_products, aquatic_products_other, eggs, fish_seafood, meat, milk_excluding_butter, offals))%>%
  arrange(desc(total_protein_consumption))
```

```
## `summarise()` has grouped output by 'country'. You can override using the `.groups` argument.
```

```
## # A tibble: 3 x 3
## # Groups:   country [3]
##   country        deaths total_protein_consumption
##   <chr>           <dbl>                     <dbl>
## 1 Slovenia        0.172                      37.8
## 2 United Kingdom  0.167                      37.8
## 3 Belgium         0.185                      35.5
```

***Total Protein Consumption by Country, Focusing on those with the Three LOWEST Death Percentages**

```r
food_supply_clean %>%
  select(country, deaths) %>%
  filter(country=="Cambodia"|country=="Dominica"|country=="Lao People's Democratic Republic")
```

```
## # A tibble: 3 x 2
##   country                          deaths
##   <chr>                             <dbl>
## 1 Cambodia                              0
## 2 Dominica                              0
## 3 Lao People's Democratic Republic      0
```


```r
food_supply_clean %>%
  filter(country=="Cambodia"| country=="Dominica"| country=="Lao People's Democratic Republic") %>%
  group_by(country, deaths) %>%
  summarize(total_protein_consumption = sum(animal_fats, animal_products, aquatic_products_other, eggs, fish_seafood, meat, milk_excluding_butter, offals)) %>%
  arrange(-desc(total_protein_consumption))
```

```
## `summarise()` has grouped output by 'country'. You can override using the `.groups` argument.
```

```
## # A tibble: 3 x 3
## # Groups:   country [3]
##   country                          deaths total_protein_consumption
##   <chr>                             <dbl>                     <dbl>
## 1 Lao People's Democratic Republic      0                      7.32
## 2 Cambodia                              0                     12.2 
## 3 Dominica                              0                     17.8
```


```r
food_supply_clean %>%
  filter(country=="United States of America") %>%
  group_by(country) %>%
  summarize(total_protein_consumption = sum(animal_fats, animal_products, aquatic_products_other, eggs, fish_seafood, meat, milk_excluding_butter, offals))
```

```
## # A tibble: 1 x 2
##   country                  total_protein_consumption
## * <chr>                                        <dbl>
## 1 United States of America                      42.5
```


```r
food_supply_clean %>%
  filter(country=="Belgium"| country=="Slovenia"| country=="United Kingdom"|country=="Cambodia"| country=="Dominica"| country=="Lao People's Democratic Republic"|country=="United States of America") %>%
  group_by(country) %>%
  summarize(total_protein_consumption = sum(animal_fats, animal_products, aquatic_products_other, eggs, fish_seafood, meat, milk_excluding_butter, offals)) %>%
  ggplot(aes(x=country, y=total_protein_consumption))+
  geom_col()+
  labs(title = "Total Protein Consumption by Country (%)",
       x="Country",
       y="Protein Consumption")+
  coord_flip()+
  theme(plot.title=element_text(hjust=0.5), axis.text.x = element_text(angle = 45, hjust=1))
```

![](Group_2_Final_Project_files/figure-html/unnamed-chunk-14-1.png)<!-- -->

higher protein because it's a bigger country...
## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


## Including Plots

You can also embed plots, for example:

![](Group_2_Final_Project_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
