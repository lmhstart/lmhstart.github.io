[mpg.html](https://github.com/user-attachments/files/22677446/mpg.html)
---
title: "MPG 分析报告"
output: html_document
date: "2025-10-03"
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
library(tidyverse)
```

## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r cars}
glimpse(mpg)
```

## Inclusion Plots 

```{r scatter_plot, echo=TRUE, message=TRUE, warning=TRUE}
ggplot(mpg,aes(x = cty,
               y = hwy,
               colour = class)) +
  geom_point() +
  scale_color_brewer(palette = "Dark2")

