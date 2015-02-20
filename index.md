---
title       : Cars Prediction ShinyApp
subtitle    : Predicting weight from miles per gallon
author      : Shibdas Roy
job         : PhD Student
framework   : html5slides   # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

## Cars Prediction ShinyApp

- This app predicts the weight, given miles per gallon, for a car.
- Internally, the app first fits a linear regression model to the 
data from the mtcars dataset.
- It outputs the predicted value of weight, reactively to the 
user-input value of miles per gallon.
- It also prints a plot with the predicted value highlighted on 
the regression line.

---

## Regressor and Outcome

- The mtcars dataset:


```r
data(mtcars)
head(mtcars)
```

```
##                    mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1
```

- The regressor is the miles per gallon variable mpg.
- The outcome is the weight variable wt.

---

## Regression Model

- We fit a linear regression model as follows:


```r
fit <- lm(wt~mpg,data=mtcars)
fit
```

```
## 
## Call:
## lm(formula = wt ~ mpg, data = mtcars)
## 
## Coefficients:
## (Intercept)          mpg  
##      6.0473      -0.1409
```

---

## Prediction Result

- The user inputs a value between 1 and 40 for miles per gallon.
- The app predicts the weight using the model fit from the previous slide.
- For example, the app by default shows the predicted value of weight for 
the default value of 15 of miles per gallon:


```r
answer <- predict(fit,newdata=data.frame(mpg=15))
answer
```

```
##        1 
## 3.934325
```

---

## Model plot


```r
plot(mtcars$mpg,mtcars$wt,pch=19,xlab="Miles per gallon"
    ,ylab="Weight",xlim=c(1,40),ylim=c(0,6))
abline(fit); points(15,answer,col='red',pch=19)
```

![plot of chunk plot](assets/fig/plot-1.png) 
