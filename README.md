# ST558-Project2
Due Sunday, July 10, 2022, 11:59 PM

Group 2-5<br>
Bridget Knapp (brknapp@ncsu.edu)<br>
Chien-Lan Hsueh (chsueh2@ncsu.edu)

# Online News Popularity
This project is to study the [Online News Popularity data set](https://archive.ics.uci.edu/ml/datasets/Online+News+Popularity) and create model for the predictions of the number of shares on a new article.

## Links to Reports

- [Introduction and Data Preparation](./output/Introduction_and_Data.html)
- [Analysis on Entertainment News Channel](./output/Analysis_on_Entertainment.html)
- [Analysis on Businiss News Channel](./output/Analysis_on_Bus.html)
- [Analysis on Lifestyle News Channel](./output/Analysis_on_Lifestyle.html)
- [Analysis on Misc News Channel](./output/Analysis_on_Misc.html)
- [Analysis on Socmedia News Channel](./output/Analysis_on_Socmed.html)
- [Analysis on Technology News Channel](./output/Analysis_on_Tech.html)
- [Analysis on World News Channel](./output/Analysis_on_World.html)

## Automation of Report

The script used to automate the process of generating the reports: "render markdown.R"

### Introduction and Data
For the introduction and data preparation:
```
rmarkdown::render(
  here("_Rmd", "Introduction_and_Data.Rmd"), 
  output_format = github_document(html_preview = FALSE), 
  output_dir = here::here("output")
)
```


The body of Rmarkdown template for report "Introduction_and_Data.md":
````
```{r include=FALSE}
path <- here::here("images", "intro") %&% "/"
if(!file.exists(path)) dir.create(path)
knitr::opts_chunk$set(fig.path = path)
```

# Introduction
```{r, child="part 1 - introduction.Rmd"}
```

# Data
```{r, child="part 2 - data.Rmd"}
```

````


### Analysis Reports
For the analysis reports on each news channel:
```
# render analysis reports for each news channel
for(i in unique(df_train$channel)){
  filename <- "Analysis_on_" %&% str_to_title(i)

  rmarkdown::render(
    here("_Rmd", "Analysis.Rmd"), 
    output_format = github_document(html_preview = FALSE), 
    output_file = filename,
    output_dir = here::here("output"),
    params = list(channel = i, load_data = FALSE)
  )
}
```


The body of Rmarkdown template for report "Analysis_on_*.md":
````
```{r include=FALSE}
path <- here::here("images", params$channel) %&% "/"
if(!file.exists(path)) dir.create(path)

knitr::opts_chunk$set(fig.path = path)
```

This analysis report focuses on new channel: ``r params$channel``:
```{r}
# subset by channel
if(params$channel != "all"){
  df_train_x <- df_train %>% filter(channel == params$channel)
  df_test_x <- df_test %>% filter(channel == params$channel)
}
```

# Summarizations
```{r, child="part 3 - eda v2.Rmd"}
```

# Modeling
```{r, child="part 4 - model.Rmd"}
```
````