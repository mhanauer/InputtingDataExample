# InputtingDataExample
---
title: "Imputting Missing Example"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Below we have an example of how to input missing data using the k nearest neighbors methods with the iris data set.

First we need to create a data with some missing values.  Because the package we are using in caret only works with metric data, we are only using the first four, metric, variables in the iris data set.  We use the prodNA function to produce 10% missing data for the first four variables in the iris dataset.
```{r}
data(iris)
iris.mis <- prodNA(iris[1:4], noNA = 0.1); iris.mis
```
Then we set the seed for reproduciability and library the caret package.  The caret package.  The specific package we are using the caret package in knnInpute, which uses the k nearest neighbors algorithm. is The k nearest neighbors using data from other variables with similar nonmissing values in the dataset to predict missing values.  The caret package automatically standardizes the values, because the creators state that standardization almost always preoduces more accurate results.

To create the model of the missing values that will be used to predict the missing values, we use the preProcess function, which takes the data and the function that we want to run the data through, which in this case is "knnImpute".
```{r}
set.seed(12345)
library(caret)
iris.mis.model = preProcess(iris.mis, "knnImpute")
```
Finally, we use the predict function to predict the missing values from the model.  
```{r}
iris.mis.pred = predict(iris.mis.model, iris.mis); iris.mis.pred
```

