# InputtingDataExample
---
title: "Imputting Missing Example"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Below we have an example of how to input missing data using the k nearest neighbors methods.  The k nearest neighbors using data from other variables in the dataset to predict missing values.  This packages offers several options for measuring distance including  
```{r}
data(iris)
# Need to get rid of the last column, because won't predict categorical values
iris.mis <- prodNA(iris, noNA = 0.1); iris.mis
set.seed(12345)
iris.mis.model = preProcess(iris.mis, "knnImpute")
iris.mis.pred = predict(iris.mis.model, iris.mis); iris.mis.pred

```

