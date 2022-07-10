# ST558-Project2
Due Sunday, July 10, 2022, 11:59 PM

Group 2-5<br>
Bridget Knapp (brknapp@ncsu.edu)<br>
Chien-Lan Hsueh (chsueh2@ncsu.edu)

# Online News Popularity
This project is to study the [Online News Popularity data set]() and create model for the predictions of the number of shares on a new article.

## Links to reports

- [Introduction and Data Preparation]
- [Analysis on Entertainment News Channel]

## Automation of Report

The script used to automate the process of generating the reports can be found [here]("render markdown.R").

For the introduction and data preparation:
```
# render introduction and data prep
rmarkdown::render(
  here("_Rmd", "Introduction_and_Data.Rmd"), 
  output_format = github_document(html_preview = FALSE), 
  output_dir = here()
)
```

For the analysis reports on each news channel:
```
# render analysis reports for each news channel
for(i in unique(df_train$channel)[1:2]){
  filename <- "Analysis on " %&% str_to_title(i) %&% ".html"

  rmarkdown::render(
    here("_Rmd", "analysis.Rmd"), 
    output_format = github_document(html_preview = FALSE), 
    output_file = filename,
    output_dir = here(),
    params = list(channel = i, load_data = FALSE)
  )
}
```