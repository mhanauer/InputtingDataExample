---
title: "Imputing missing data example"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Below we have an example of how to input missing data using the k nearest neighbors methods with the iris data set using the knnImpute function in the caret package.

First, I created a data set with some missing values.  Because the knnImpute function only works with metric data, we are only using the first four, metric, variables in the iris data set.  We then use the prodNA function to produce 10% missing data for the first four variables in the iris dataset.

```{r, message=FALSE, warning=FALSE}
#data(iris)
#iris.mis = prodNA(iris[1:4], noNA = 0.1); head(iris.mis)
#write.csv(iris.mis, "iris.mis.csv")
iris.mis = read.csv("iris.mis.csv", header = TRUE); head(iris.mis)
```
Then we set the seed for reproducibility and library the caret package. The specific package we are using the caret package is knnInpute, which uses the k nearest neighbors algorithm.  The k nearest neighbors function uses data from other variables with similar non-missing values in the dataset to predict missing values.  The caret package automatically standardizes the values, because the creators state that standardization almost always produces more accurate results.

To create the model of the missing values that will be used to predict the missing values, we use the preProcess function, which takes the data and the function that we want to run the data through, which in this case is "knnImpute".

```{r, message=FALSE, warning=FALSE}
set.seed(12345)
library(caret)
iris.mis.model = preProcess(iris.mis, "knnImpute")
```
Finally, we use the predict function to predict the missing values using the model we just developed.  

```{r, message=FALSE, warning=FALSE}
iris.mis.pred = predict(iris.mis.model, iris.mis); head(iris.mis.pred)
```
