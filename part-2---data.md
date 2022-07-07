test_7\_6_2022
================
Bridget Knapp

-   [Data](#data)
-   [Start here…](#start-here)

## Data

> Use a relative path to import the data. Subset the data to work on the
> data channel of interest.
>
> This section should be done by whoever can get to it first.

## Start here…

``` r
#this is the code I used to render this document before I committed changes to the repository
rmarkdown::render("part 2 - data.Rmd",
                  output_format = "github_document",
                  output_options = list(
                    toc = TRUE,
                    html_preview=FALSE) 
)
```

``` r
#In order to make one html output for each news channel, run this code in the console first
channel_list <- c("Lifestyle", "Entertainment", "Business", "Social_Media", "Tech", "World")
output_file <- paste0(channel_list,".html")
params <- lapply(channel_list, FUN = function(x){list(data_channel_is=x)})
reports <- tibble(output_file,params)

library(rmarkdown)
apply(reports, MARGIN = 1,
      FUN = function(x){
        render(input="C://Users//Bridget//OneDrive//R_Scripts//test_7_6_2022.Rmd",output_file = x[[1]], params = x[[2]])
      })
```

``` r
library(tidyverse)
library(readr)
data<-read_csv("../ST558-Project2/data/OnlineNewsPopularity.csv")
head(data)
```

    ## # A tibble: 6 × 61
    ##   url                timedelta n_tokens_title n_tokens_content n_unique_tokens n_non_stop_words n_non_stop_uniq… num_hrefs
    ##   <chr>                  <dbl>          <dbl>            <dbl>           <dbl>            <dbl>            <dbl>     <dbl>
    ## 1 http://mashable.c…       731             12              219           0.664             1.00            0.815         4
    ## 2 http://mashable.c…       731              9              255           0.605             1.00            0.792         3
    ## 3 http://mashable.c…       731              9              211           0.575             1.00            0.664         3
    ## 4 http://mashable.c…       731              9              531           0.504             1.00            0.666         9
    ## 5 http://mashable.c…       731             13             1072           0.416             1.00            0.541        19
    ## 6 http://mashable.c…       731             10              370           0.560             1.00            0.698         2
    ## # … with 53 more variables: num_self_hrefs <dbl>, num_imgs <dbl>, num_videos <dbl>, average_token_length <dbl>,
    ## #   num_keywords <dbl>, data_channel_is_lifestyle <dbl>, data_channel_is_entertainment <dbl>, data_channel_is_bus <dbl>,
    ## #   data_channel_is_socmed <dbl>, data_channel_is_tech <dbl>, data_channel_is_world <dbl>, kw_min_min <dbl>,
    ## #   kw_max_min <dbl>, kw_avg_min <dbl>, kw_min_max <dbl>, kw_max_max <dbl>, kw_avg_max <dbl>, kw_min_avg <dbl>,
    ## #   kw_max_avg <dbl>, kw_avg_avg <dbl>, self_reference_min_shares <dbl>, self_reference_max_shares <dbl>,
    ## #   self_reference_avg_sharess <dbl>, weekday_is_monday <dbl>, weekday_is_tuesday <dbl>, weekday_is_wednesday <dbl>,
    ## #   weekday_is_thursday <dbl>, weekday_is_friday <dbl>, weekday_is_saturday <dbl>, weekday_is_sunday <dbl>, …

Subset the data to work on the data channel of interest.

``` r
#This code processes the data. It removes excess data_channel_is_ columns and filters the column we want so that it only includes values of 1. For example, if you want the "Lifestyle" data, this function will remove the other data channel columns (Entertainment, Business, Social Media, Tech, and World) and filter it so that it only includes data where data_channel_is_lifestyle == 1.

library(tidyverse)
library(readr)
library(shiny)
data<-read_csv("C://Users//Bridget//OneDrive//R_Scripts//repos//ST558-Project2//data//OnlineNewsPopularity.csv")
```

    ## Rows: 39644 Columns: 61
    ## ── Column specification ──────────────────────────────────────────────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (1): url
    ## dbl (60): timedelta, n_tokens_title, n_tokens_content, n_unique_tokens, n_non_stop_words, n_non_stop_unique_tokens, nu...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(data)
```

    ## # A tibble: 6 × 61
    ##   url                timedelta n_tokens_title n_tokens_content n_unique_tokens n_non_stop_words n_non_stop_uniq… num_hrefs
    ##   <chr>                  <dbl>          <dbl>            <dbl>           <dbl>            <dbl>            <dbl>     <dbl>
    ## 1 http://mashable.c…       731             12              219           0.664             1.00            0.815         4
    ## 2 http://mashable.c…       731              9              255           0.605             1.00            0.792         3
    ## 3 http://mashable.c…       731              9              211           0.575             1.00            0.664         3
    ## 4 http://mashable.c…       731              9              531           0.504             1.00            0.666         9
    ## 5 http://mashable.c…       731             13             1072           0.416             1.00            0.541        19
    ## 6 http://mashable.c…       731             10              370           0.560             1.00            0.698         2
    ## # … with 53 more variables: num_self_hrefs <dbl>, num_imgs <dbl>, num_videos <dbl>, average_token_length <dbl>,
    ## #   num_keywords <dbl>, data_channel_is_lifestyle <dbl>, data_channel_is_entertainment <dbl>, data_channel_is_bus <dbl>,
    ## #   data_channel_is_socmed <dbl>, data_channel_is_tech <dbl>, data_channel_is_world <dbl>, kw_min_min <dbl>,
    ## #   kw_max_min <dbl>, kw_avg_min <dbl>, kw_min_max <dbl>, kw_max_max <dbl>, kw_avg_max <dbl>, kw_min_avg <dbl>,
    ## #   kw_max_avg <dbl>, kw_avg_avg <dbl>, self_reference_min_shares <dbl>, self_reference_max_shares <dbl>,
    ## #   self_reference_avg_sharess <dbl>, weekday_is_monday <dbl>, weekday_is_tuesday <dbl>, weekday_is_wednesday <dbl>,
    ## #   weekday_is_thursday <dbl>, weekday_is_friday <dbl>, weekday_is_saturday <dbl>, weekday_is_sunday <dbl>, …

``` r
channel <- params$data_channel_is
channel
```

    ## [1] "Lifestyle"

``` r
subset_data <- function(channel_of_interest){
  if(channel_of_interest=="Lifestyle"){
    new_data = subset(data, select = -c(data_channel_is_entertainment,data_channel_is_bus,data_channel_is_socmed,data_channel_is_tech,data_channel_is_world))
    new_data <- filter(new_data, data_channel_is_lifestyle == 1)
  }
  if(channel_of_interest=="Entertainment"){
    new_data = subset(data, select = -c(data_channel_is_lifestyle,data_channel_is_bus,data_channel_is_socmed,data_channel_is_tech,data_channel_is_world) )
    new_data <- filter(new_data, data_channel_is_entertainment == 1)
  }
   if(channel_of_interest=="Business"){
    new_data = subset(data, select = -c(data_channel_is_lifestyle,data_channel_is_entertainment,data_channel_is_socmed,data_channel_is_tech,data_channel_is_world) )
    new_data <- filter(new_data, data_channel_is_bus == 1)
   }
   if(channel_of_interest=="Social_Media"){
    new_data = subset(data, select = -c(data_channel_is_lifestyle,data_channel_is_entertainment,data_channel_is_bus,data_channel_is_tech,data_channel_is_world) )
    new_data <- filter(new_data, data_channel_is_socmed == 1)
   }
   if(channel_of_interest=="Tech"){
    new_data = subset(data, select = -c(data_channel_is_lifestyle,data_channel_is_entertainment,data_channel_is_bus,data_channel_is_socmed,data_channel_is_world) )
    new_data <- filter(new_data, data_channel_is_tech == 1)
   }
   if(channel_of_interest=="World"){
    new_data = subset(data, select = -c(data_channel_is_lifestyle,data_channel_is_entertainment,data_channel_is_bus,data_channel_is_socmed,data_channel_is_tech) )
    new_data <- filter(new_data, data_channel_is_world == 1)
  }
  return(new_data)
}

channel_data <- subset_data(channel)
head(channel_data)
```

    ## # A tibble: 6 × 56
    ##   url                timedelta n_tokens_title n_tokens_content n_unique_tokens n_non_stop_words n_non_stop_uniq… num_hrefs
    ##   <chr>                  <dbl>          <dbl>            <dbl>           <dbl>            <dbl>            <dbl>     <dbl>
    ## 1 http://mashable.c…       731              8              960           0.418             1.00            0.550        21
    ## 2 http://mashable.c…       731             10              187           0.667             1.00            0.800         7
    ## 3 http://mashable.c…       731             11              103           0.689             1.00            0.806         3
    ## 4 http://mashable.c…       731             10              243           0.619             1.00            0.824         1
    ## 5 http://mashable.c…       731              8              204           0.586             1.00            0.698         7
    ## 6 http://mashable.c…       731             11              315           0.551             1.00            0.702         4
    ## # … with 48 more variables: num_self_hrefs <dbl>, num_imgs <dbl>, num_videos <dbl>, average_token_length <dbl>,
    ## #   num_keywords <dbl>, data_channel_is_lifestyle <dbl>, kw_min_min <dbl>, kw_max_min <dbl>, kw_avg_min <dbl>,
    ## #   kw_min_max <dbl>, kw_max_max <dbl>, kw_avg_max <dbl>, kw_min_avg <dbl>, kw_max_avg <dbl>, kw_avg_avg <dbl>,
    ## #   self_reference_min_shares <dbl>, self_reference_max_shares <dbl>, self_reference_avg_sharess <dbl>,
    ## #   weekday_is_monday <dbl>, weekday_is_tuesday <dbl>, weekday_is_wednesday <dbl>, weekday_is_thursday <dbl>,
    ## #   weekday_is_friday <dbl>, weekday_is_saturday <dbl>, weekday_is_sunday <dbl>, is_weekend <dbl>, LDA_00 <dbl>,
    ## #   LDA_01 <dbl>, LDA_02 <dbl>, LDA_03 <dbl>, LDA_04 <dbl>, global_subjectivity <dbl>, global_sentiment_polarity <dbl>, …

``` r
# Lifestyle_data <- subset_data(channel_of_interest="Lifestyle")
# head(Lifestyle_data)
# dim(Lifestyle_data)
# 
# Entertainment_data <- subset_data(channel_of_interest="Entertainment")
# head(Entertainment_data)
# dim(Entertainment_data)
# 
# Business_data <- subset_data(channel_of_interest="Business")
# head(Business_data)
# dim(Business_data)
# 
# Social_Media_data <- subset_data(channel_of_interest="Social_Media")
# head(Social_Media_data)
# dim(Social_Media_data)
# 
# Tech_data <- subset_data(channel_of_interest="Tech")
# head(Tech_data)
# dim(Tech_data)
# 
# World_data <- subset_data(channel_of_interest="World")
# head(World_data)
# dim(World_data)
```
