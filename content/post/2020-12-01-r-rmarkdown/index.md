---
title: "First R Markdown"
author: "Martin Fernandez Figarola"
date: "2020-12-01T21:13:14-05:00"
categories: R
tags:
- R Markdown
- plot
- regression
---



# R Markdown

The data give the speed of cars and the distances taken to stop. Note that the data were recorded in the 1920s.

Format
A data frame with 50 observations on 2 variables.

[,1]	speed	numeric	Speed (mph)
[,2]	dist	numeric	Stopping distance (ft)


```r
summary(cars)
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
fit <- lm(dist ~ speed, data = cars)
fit
## 
## Call:
## lm(formula = dist ~ speed, data = cars)
## 
## Coefficients:
## (Intercept)        speed  
##     -17.579        3.932
require(stats); require(graphics)
plot(cars, xlab = "Speed (mph)", ylab = "Stopping distance (ft)",
     las = 1)
lines(lowess(cars$speed, cars$dist, f = 2/3, iter = 3), col = "red")
title(main = "cars data")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/cars-1.png" width="672" />

```r
plot(cars, xlab = "Speed (mph)", ylab = "Stopping distance (ft)",
     las = 1, log = "xy")
title(main = "cars data (logarithmic scales)")
lines(lowess(cars$speed, cars$dist, f = 2/3, iter = 3), col = "red")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/cars-2.png" width="672" />

```r
summary(fm1 <- lm(log(dist) ~ log(speed), data = cars))
## 
## Call:
## lm(formula = log(dist) ~ log(speed), data = cars)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -1.00215 -0.24578 -0.02898  0.20717  0.88289 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  -0.7297     0.3758  -1.941   0.0581 .  
## log(speed)    1.6024     0.1395  11.484 2.26e-15 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 0.4053 on 48 degrees of freedom
## Multiple R-squared:  0.7331,	Adjusted R-squared:  0.7276 
## F-statistic: 131.9 on 1 and 48 DF,  p-value: 2.259e-15
opar <- par(mfrow = c(2, 2), oma = c(0, 0, 1.1, 0),
            mar = c(4.1, 4.1, 2.1, 1.1))
plot(fm1)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/cars-3.png" width="672" />

```r
par(opar)
```

