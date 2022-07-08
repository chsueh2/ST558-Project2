ST558 Porject 1: Part 1
================
Bridget Knapp and Chien-Lan Hsueh
2022-07-06

-   [Introduction Section](#introduction-section)
-   [Start here…](#start-here)

## Introduction Section

> You should have an introduction section that briefly describes the
> data and the variables you have to work with (just discuss the ones
> you want to use). Your target variables is the shares variable. You
> should also mention the purpose of your analysis and the methods
> you’ll use to model the response. You’ll describe those in more detail
> later.
>
> This section should be done by the ‘second’ group member.

## Start here…

``` r
#this is the code I used to render this document before I committed changes to the repository
rmarkdown::render("part 1 - introduction.Rmd",
                  output_format = "github_document",
                  output_options = list(
                    toc = TRUE,
                    html_preview=FALSE) 
)
```

Let’s say you’re interested in entertainment news and you would like to
predict the number shares based on different criteria. Luckily, this
repository is here to help. This will help you learn about our data set,
make predictions, and create automated Markdown reports. First, let’s
look at the data:

We want to predict the number of `shares` a certain type of news
receives. The news type is described in the `data_channel_is_*` columns.
There are six types: Lifestyle, Entertainment, Business, Social Media,
Tech, and World. The data also includes columns for the day of the week
the article was published (`weekday_is_*`), the best, worst, and average
keywords based on number of shares (`kw_*`); and negative or positive
popularity (`*_polarity`).

To predict the number of ‘shares’, we will use a linear regression model
and an ensemble tree-based model. In a linear regression model, the
response for the *i<sup>th</sup>* observation (Y<sub>i</sub>) is
calculated by using an explanatory variable for the *i<sup>th</sup>*
observation (x<sub>i</sub>) to calculate the y-intercept
(B<sub>0</sub>), slope (B<sub>1</sub>), and error (E<sub>i</sub>):

Y<sub>i</sub> = B<sub>0</sub> + B<sub>1</sub> x<sub>i</sub> +
E<sub>i</sub>

An ensemble tree-based model takes the average across many trees. Here,
we’ll use a random forest model, which creates many trees from bootstrap
samples. Bootstrapping is the process of taking many samples from our
data, calulating a statistic for each sample, and then averaging the
results. We’ll also use a boosted tree model, which creates many trees
based on the residuals (observed-predicted) of the previous set (the
user specifies how many times this is repeated).
