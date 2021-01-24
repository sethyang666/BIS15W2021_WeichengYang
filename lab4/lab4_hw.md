---
title: "Lab 4 Homework"
author: "Please Add Your Name Here"
date: "2021-01-24"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

```r
homerange <- readr::read_csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

```
## Parsed with column specification:
## cols(
##   .default = col_character(),
##   mean.mass.g = col_double(),
##   log10.mass = col_double(),
##   mean.hra.m2 = col_double(),
##   log10.hra = col_double(),
##   preymass = col_double(),
##   log10.preymass = col_double(),
##   PPMR = col_double()
## )
```

```
## See spec(...) for full column specifications.
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

```r
glimpse(homerange)
```

```
## Observations: 569
## Variables: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fish…
## $ common.name                <chr> "american eel", "blacktail redhorse", "cen…
## $ class                      <chr> "actinopterygii", "actinopterygii", "actin…
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprin…
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae…
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cl…
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fund…
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recap…
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2",…
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00…
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600…
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, …
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437…
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home rang…
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic"…
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ec…
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimm…
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "ca…
## $ dimension                  <chr> "3D", "2D", "2D", "2D", "2D", "2D", "2D", …
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, …
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA,…
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, N…
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 2…
```

```r
str(homerange)
```

```
## Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':	569 obs. of  24 variables:
##  $ taxon                     : chr  "lake fishes" "river fishes" "river fishes" "river fishes" ...
##  $ common.name               : chr  "american eel" "blacktail redhorse" "central stoneroller" "rosyside dace" ...
##  $ class                     : chr  "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii" ...
##  $ order                     : chr  "anguilliformes" "cypriniformes" "cypriniformes" "cypriniformes" ...
##  $ family                    : chr  "anguillidae" "catostomidae" "cyprinidae" "cyprinidae" ...
##  $ genus                     : chr  "anguilla" "moxostoma" "campostoma" "clinostomus" ...
##  $ species                   : chr  "rostrata" "poecilura" "anomalum" "funduloides" ...
##  $ primarymethod             : chr  "telemetry" "mark-recapture" "mark-recapture" "mark-recapture" ...
##  $ N                         : chr  "16" NA "20" "26" ...
##  $ mean.mass.g               : num  887 562 34 4 4 ...
##  $ log10.mass                : num  2.948 2.75 1.531 0.602 0.602 ...
##  $ alternative.mass.reference: chr  NA NA NA NA ...
##  $ mean.hra.m2               : num  282750 282.1 116.1 125.5 87.1 ...
##  $ log10.hra                 : num  5.45 2.45 2.06 2.1 1.94 ...
##  $ hra.reference             : chr  "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 ...
##  $ realm                     : chr  "aquatic" "aquatic" "aquatic" "aquatic" ...
##  $ thermoregulation          : chr  "ectotherm" "ectotherm" "ectotherm" "ectotherm" ...
##  $ locomotion                : chr  "swimming" "swimming" "swimming" "swimming" ...
##  $ trophic.guild             : chr  "carnivore" "carnivore" "carnivore" "carnivore" ...
##  $ dimension                 : chr  "3D" "2D" "2D" "2D" ...
##  $ preymass                  : num  NA NA NA NA NA NA 1.39 NA NA NA ...
##  $ log10.preymass            : num  NA NA NA NA NA ...
##  $ PPMR                      : num  NA NA NA NA NA NA 530 NA NA NA ...
##  $ prey.size.reference       : chr  NA NA NA NA ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   taxon = col_character(),
##   ..   common.name = col_character(),
##   ..   class = col_character(),
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   genus = col_character(),
##   ..   species = col_character(),
##   ..   primarymethod = col_character(),
##   ..   N = col_character(),
##   ..   mean.mass.g = col_double(),
##   ..   log10.mass = col_double(),
##   ..   alternative.mass.reference = col_character(),
##   ..   mean.hra.m2 = col_double(),
##   ..   log10.hra = col_double(),
##   ..   hra.reference = col_character(),
##   ..   realm = col_character(),
##   ..   thermoregulation = col_character(),
##   ..   locomotion = col_character(),
##   ..   trophic.guild = col_character(),
##   ..   dimension = col_character(),
##   ..   preymass = col_double(),
##   ..   log10.preymass = col_double(),
##   ..   PPMR = col_double(),
##   ..   prey.size.reference = col_character()
##   .. )
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```



**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

```r
taxon <- as.factor(homerange$taxon)
order <- as.factor(homerange$order)
levels(taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(order)
```

```
##  [1] "accipitriformes"    "afrosoricida"       "anguilliformes"    
##  [4] "anseriformes"       "apterygiformes"     "artiodactyla"      
##  [7] "caprimulgiformes"   "carnivora"          "charadriiformes"   
## [10] "columbidormes"      "columbiformes"      "coraciiformes"     
## [13] "cuculiformes"       "cypriniformes"      "dasyuromorpha"     
## [16] "dasyuromorpia"      "didelphimorphia"    "diprodontia"       
## [19] "diprotodontia"      "erinaceomorpha"     "esociformes"       
## [22] "falconiformes"      "gadiformes"         "galliformes"       
## [25] "gruiformes"         "lagomorpha"         "macroscelidea"     
## [28] "monotrematae"       "passeriformes"      "pelecaniformes"    
## [31] "peramelemorphia"    "perciformes"        "perissodactyla"    
## [34] "piciformes"         "pilosa"             "proboscidea"       
## [37] "psittaciformes"     "rheiformes"         "roden"             
## [40] "rodentia"           "salmoniformes"      "scorpaeniformes"   
## [43] "siluriformes"       "soricomorpha"       "squamata"          
## [46] "strigiformes"       "struthioniformes"   "syngnathiformes"   
## [49] "testudines"         "tetraodontiformes\xa0" "tinamiformes"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  

```r
taxa <- select(homerange,"taxon","common.name","class","order","family","genus","species")
taxa
```

```
## # A tibble: 569 x 7
##    taxon     common.name       class      order     family    genus    species  
##    <chr>     <chr>             <chr>      <chr>     <chr>     <chr>    <chr>    
##  1 lake fis… american eel      actinopte… anguilli… anguilli… anguilla rostrata 
##  2 river fi… blacktail redhor… actinopte… cyprinif… catostom… moxosto… poecilura
##  3 river fi… central stonerol… actinopte… cyprinif… cyprinid… campost… anomalum 
##  4 river fi… rosyside dace     actinopte… cyprinif… cyprinid… clinost… funduloi…
##  5 river fi… longnose dace     actinopte… cyprinif… cyprinid… rhinich… cataract…
##  6 river fi… muskellunge       actinopte… esocifor… esocidae  esox     masquino…
##  7 marine f… pollack           actinopte… gadiform… gadidae   pollach… pollachi…
##  8 marine f… saithe            actinopte… gadiform… gadidae   pollach… virens   
##  9 marine f… lined surgeonfish actinopte… percifor… acanthur… acanthu… lineatus 
## 10 marine f… orangespine unic… actinopte… percifor… acanthur… naso     lituratus
## # … with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

```r
table(taxon)
```

```
## taxon
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  

```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

```r
carnivores <- filter(homerange, trophic.guild=="carnivore")
herbivores <- filter(homerange,trophic.guild=="herbivores")
carnivores
```

```
## # A tibble: 342 x 24
##    taxon common.name class order family genus species primarymethod N    
##    <chr> <chr>       <chr> <chr> <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake… american e… acti… angu… angui… angu… rostra… telemetry     16   
##  2 rive… blacktail … acti… cypr… catos… moxo… poecil… mark-recaptu… <NA> 
##  3 rive… central st… acti… cypr… cypri… camp… anomal… mark-recaptu… 20   
##  4 rive… rosyside d… acti… cypr… cypri… clin… fundul… mark-recaptu… 26   
##  5 rive… longnose d… acti… cypr… cypri… rhin… catara… mark-recaptu… 17   
##  6 rive… muskellunge acti… esoc… esoci… esox  masqui… telemetry     5    
##  7 mari… pollack     acti… gadi… gadid… poll… pollac… telemetry     2    
##  8 mari… saithe      acti… gadi… gadid… poll… virens  telemetry     2    
##  9 mari… giant trev… acti… perc… caran… cara… ignobi… telemetry     4    
## 10 lake… rock bass   acti… perc… centr… ambl… rupest… mark-recaptu… 16   
## # … with 332 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <chr>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

```r
herbivores
```

```
## # A tibble: 0 x 24
## # … with 24 variables: taxon <chr>, common.name <chr>, class <chr>,
## #   order <chr>, family <chr>, genus <chr>, species <chr>, primarymethod <chr>,
## #   N <chr>, mean.mass.g <dbl>, log10.mass <dbl>,
## #   alternative.mass.reference <chr>, mean.hra.m2 <dbl>, log10.hra <dbl>,
## #   hra.reference <chr>, realm <chr>, thermoregulation <chr>, locomotion <chr>,
## #   trophic.guild <chr>, dimension <chr>, preymass <dbl>, log10.preymass <dbl>,
## #   PPMR <dbl>, prey.size.reference <chr>
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  

```r
carnivores_mean <- colMeans(carnivores[ ,13], na.rm=TRUE)
herbivores_mean <- colMeans(herbivores[,13], na.rm=TRUE)
carnivores_mean
```

```
## mean.hra.m2 
##    13039918
```

```r
herbivores_mean
```

```
## mean.hra.m2 
##         NaN
```


**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  

```r
deer <- select(homerange,"mean.mass.g","log10.mass","family","genus","species","common.name")
deer <- filter(deer,family=="cervidae")
deer
```

```
## # A tibble: 12 x 6
##    mean.mass.g log10.mass family   genus      species     common.name      
##          <dbl>      <dbl> <chr>    <chr>      <chr>       <chr>            
##  1     307227.       5.49 cervidae alces      alces       moose            
##  2      62823.       4.80 cervidae axis       axis        chital           
##  3      24050.       4.38 cervidae capreolus  capreolus   roe deer         
##  4     234758.       5.37 cervidae cervus     elaphus     red deer         
##  5      29450.       4.47 cervidae cervus     nippon      sika deer        
##  6      71450.       4.85 cervidae dama       dama        fallow deer      
##  7      13500.       4.13 cervidae muntiacus  reevesi     Reeves's muntjac 
##  8      53864.       4.73 cervidae odocoileus hemionus    mule deer        
##  9      87884.       4.94 cervidae odocoileus virginianus white-tailed deer
## 10      35000.       4.54 cervidae ozotoceros bezoarticus pampas deer      
## 11       7500.       3.88 cervidae pudu       puda        pudu             
## 12     102059.       5.01 cervidae rangifer   tarandus    reindeer
```

```r
arrange(deer, 'mean.hra.m2')
```

```
## # A tibble: 12 x 6
##    mean.mass.g log10.mass family   genus      species     common.name      
##          <dbl>      <dbl> <chr>    <chr>      <chr>       <chr>            
##  1     307227.       5.49 cervidae alces      alces       moose            
##  2      62823.       4.80 cervidae axis       axis        chital           
##  3      24050.       4.38 cervidae capreolus  capreolus   roe deer         
##  4     234758.       5.37 cervidae cervus     elaphus     red deer         
##  5      29450.       4.47 cervidae cervus     nippon      sika deer        
##  6      71450.       4.85 cervidae dama       dama        fallow deer      
##  7      13500.       4.13 cervidae muntiacus  reevesi     Reeves's muntjac 
##  8      53864.       4.73 cervidae odocoileus hemionus    mule deer        
##  9      87884.       4.94 cervidae odocoileus virginianus white-tailed deer
## 10      35000.       4.54 cervidae ozotoceros bezoarticus pampas deer      
## 11       7500.       3.88 cervidae pudu       puda        pudu             
## 12     102059.       5.01 cervidae rangifer   tarandus    reindeer
```

#	largest:alces	common.name:moose

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
snake <- filter(homerange,taxon=="snakes")
snake <- select(snake,"common.name","mean.hra.m2")
min(snake$mean.hra.m2)
```

```
## [1] 200
```

```r
smallest <- subset(snake, mean.hra.m2==200)
smallest
```

```
## # A tibble: 1 x 2
##   common.name         mean.hra.m2
##   <chr>                     <dbl>
## 1 namaqua dwarf adder         200
```
# "Common names: Namaqua dwarf adder, spotted dwarf adder, Schneider's adder. Bitis schneideri is a species of venomous snake in the subfamily Viperinae of the family Viperidae." --Wikipedia


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
