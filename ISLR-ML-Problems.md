ISLR ML Problems
================
Robbie Mc Guinness
12/11/2021

# Chapter 2: Statistical Learning

### Question 8

``` r
library(ISLR)
summary(College)
```

    ##  Private        Apps           Accept          Enroll       Top10perc    
    ##  No :212   Min.   :   81   Min.   :   72   Min.   :  35   Min.   : 1.00  
    ##  Yes:565   1st Qu.:  776   1st Qu.:  604   1st Qu.: 242   1st Qu.:15.00  
    ##            Median : 1558   Median : 1110   Median : 434   Median :23.00  
    ##            Mean   : 3002   Mean   : 2019   Mean   : 780   Mean   :27.56  
    ##            3rd Qu.: 3624   3rd Qu.: 2424   3rd Qu.: 902   3rd Qu.:35.00  
    ##            Max.   :48094   Max.   :26330   Max.   :6392   Max.   :96.00  
    ##    Top25perc      F.Undergrad     P.Undergrad         Outstate    
    ##  Min.   :  9.0   Min.   :  139   Min.   :    1.0   Min.   : 2340  
    ##  1st Qu.: 41.0   1st Qu.:  992   1st Qu.:   95.0   1st Qu.: 7320  
    ##  Median : 54.0   Median : 1707   Median :  353.0   Median : 9990  
    ##  Mean   : 55.8   Mean   : 3700   Mean   :  855.3   Mean   :10441  
    ##  3rd Qu.: 69.0   3rd Qu.: 4005   3rd Qu.:  967.0   3rd Qu.:12925  
    ##  Max.   :100.0   Max.   :31643   Max.   :21836.0   Max.   :21700  
    ##    Room.Board       Books           Personal         PhD        
    ##  Min.   :1780   Min.   :  96.0   Min.   : 250   Min.   :  8.00  
    ##  1st Qu.:3597   1st Qu.: 470.0   1st Qu.: 850   1st Qu.: 62.00  
    ##  Median :4200   Median : 500.0   Median :1200   Median : 75.00  
    ##  Mean   :4358   Mean   : 549.4   Mean   :1341   Mean   : 72.66  
    ##  3rd Qu.:5050   3rd Qu.: 600.0   3rd Qu.:1700   3rd Qu.: 85.00  
    ##  Max.   :8124   Max.   :2340.0   Max.   :6800   Max.   :103.00  
    ##     Terminal       S.F.Ratio      perc.alumni        Expend     
    ##  Min.   : 24.0   Min.   : 2.50   Min.   : 0.00   Min.   : 3186  
    ##  1st Qu.: 71.0   1st Qu.:11.50   1st Qu.:13.00   1st Qu.: 6751  
    ##  Median : 82.0   Median :13.60   Median :21.00   Median : 8377  
    ##  Mean   : 79.7   Mean   :14.09   Mean   :22.74   Mean   : 9660  
    ##  3rd Qu.: 92.0   3rd Qu.:16.50   3rd Qu.:31.00   3rd Qu.:10830  
    ##  Max.   :100.0   Max.   :39.80   Max.   :64.00   Max.   :56233  
    ##    Grad.Rate     
    ##  Min.   : 10.00  
    ##  1st Qu.: 53.00  
    ##  Median : 65.00  
    ##  Mean   : 65.46  
    ##  3rd Qu.: 78.00  
    ##  Max.   :118.00

``` r
pairs(College[,2:6])
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
boxplot(College$Outstate~College$Private)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->

``` r
Elite<-rep("No",nrow(College))
Elite[College$Top10perc>50]<-"Yes"
Elite<-as.factor(Elite)
College<-data.frame(College,Elite)
summary(College$Elite)
```

    ##  No Yes 
    ## 699  78

``` r
boxplot(College$Outstate~College$Elite)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-1-3.png)<!-- -->

``` r
par(mfrow=c(2,2))
hist(College$Room.Board,breaks=25)
hist(College$Books,breaks=15)
hist(College$Apps,breaks=50)
hist(College$PhD,breaks=12)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-1-4.png)<!-- -->

### Question 9

The variables Name and Origin are qualitative and the rest are
quantitative.

``` r
for (i in 1:7)
{cat("The range of", names(Auto)[i],"is",range(Auto[,i]),"\n")}
```

    ## The range of mpg is 9 46.6 
    ## The range of cylinders is 3 8 
    ## The range of displacement is 68 455 
    ## The range of horsepower is 46 230 
    ## The range of weight is 1613 5140 
    ## The range of acceleration is 8 24.8 
    ## The range of year is 70 82

``` r
for (i in 1:7)
{cat("The mean and standard deviation of",names(Auto)[i],"are",mean(Auto[,i]),"and",sd(Auto[,i]),"\n")}
```

    ## The mean and standard deviation of mpg are 23.44592 and 7.805007 
    ## The mean and standard deviation of cylinders are 5.471939 and 1.705783 
    ## The mean and standard deviation of displacement are 194.412 and 104.644 
    ## The mean and standard deviation of horsepower are 104.4694 and 38.49116 
    ## The mean and standard deviation of weight are 2977.584 and 849.4026 
    ## The mean and standard deviation of acceleration are 15.54133 and 2.758864 
    ## The mean and standard deviation of year are 75.97959 and 3.683737

``` r
Auto2<-Auto[-c(10:85),]
for (i in 1:7)
{cat("Having removed the 10th through 85th rows; the range of", names(Auto2)[i],"is",range(Auto2[,i]),"\n and the mean and standard deviation of",names(Auto2)[i],"are",mean(Auto2[,i]),"and",sd(Auto2[,i]),".\n")}
```

    ## Having removed the 10th through 85th rows; the range of mpg is 11 46.6 
    ##  and the mean and standard deviation of mpg are 24.40443 and 7.867283 .
    ## Having removed the 10th through 85th rows; the range of cylinders is 3 8 
    ##  and the mean and standard deviation of cylinders are 5.373418 and 1.654179 .
    ## Having removed the 10th through 85th rows; the range of displacement is 68 455 
    ##  and the mean and standard deviation of displacement are 187.2405 and 99.67837 .
    ## Having removed the 10th through 85th rows; the range of horsepower is 46 230 
    ##  and the mean and standard deviation of horsepower are 100.7215 and 35.70885 .
    ## Having removed the 10th through 85th rows; the range of weight is 1649 4997 
    ##  and the mean and standard deviation of weight are 2935.972 and 811.3002 .
    ## Having removed the 10th through 85th rows; the range of acceleration is 8.5 24.8 
    ##  and the mean and standard deviation of acceleration are 15.7269 and 2.693721 .
    ## Having removed the 10th through 85th rows; the range of year is 70 82 
    ##  and the mean and standard deviation of year are 77.14557 and 3.106217 .

``` r
pairs(Auto[,1:7])
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

There appears to be strong positive linear relationships between
horsepower and weight. Similarly, there is a positive approximately
linear relationship between horsepower and displacement and between
weight and displacement.

The predictors displacement, weight and horsepower seem to be the ones
with the most obvious relationship to mpg. Each exhibits a decreasing
weakly non-linear relationship with mpg.

### Question 10

``` r
library(ISLR2)
```

    ## 
    ## Attaching package: 'ISLR2'

    ## The following object is masked _by_ '.GlobalEnv':
    ## 
    ##     College

    ## The following objects are masked from 'package:ISLR':
    ## 
    ##     Auto, Credit

``` r
cat("The number of rows in the Boston dataset is",nrow(Boston),".")
```

    ## The number of rows in the Boston dataset is 506 .

``` r
cat("The number of columns in the Boston dataset is",ncol(Boston),".")
```

    ## The number of columns in the Boston dataset is 13 .

The rows represent different suburbs of Boston and the columns represent
various housing and area statistics for each suburb.

``` r
pairs(Boston[,1:6])
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
pairs(Boston[,7:13])
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
par(mfrow=c(3,4))
for (i in 2:13)
{plot(Boston$crim,Boston[,i],ylab=names(Boston)[i])}
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

None of the predictors seem to have a correlation with the per capita
crime rate

``` r
par(mfrow=c(3,1))
hist(Boston$crim,breaks=30)
hist(Boston$tax,breaks=30)
hist(Boston$ptratio,breaks=30)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

From the histograms it is clear to see that there is a small number of
outliers that have very large crime rates. Similarly, there are a number
of suburbs where property tax is appreacibly above all other suburbs.
The pupil teacher ratio is reasonably uniform apart from one large peak
just above 20.

``` r
cat("The number of suburbs bordering the Charles river is",sum(Boston$chas),"\n")
```

    ## The number of suburbs bordering the Charles river is 35

``` r
cat("The median pupil teacher ratio is",median(Boston$ptratio))
```

    ## The median pupil teacher ratio is 19.05

``` r
cat("The minimum median value of owner occupied homes is",min(Boston$medv),"and it occurs in the",which.min(Boston$medv),"suburb.\n")
```

    ## The minimum median value of owner occupied homes is 5 and it occurs in the 399 suburb.

``` r
medians<-rep(0,ncol(Boston))
for (i in 1:ncol(Boston))
{if (median(Boston[,i])==0)
     {medians[i]=mean(Boston[,i])}
else
{medians[i]=median(Boston[,i])}
cat("The",names(Boston)[i], "predictor value at this location is",round(Boston[which.min(Boston$medv),i]/medians[i],3),"times the median value of that predictor. \n")}
```

    ## The crim predictor value at this location is 149.514 times the median value of that predictor. 
    ## The zn predictor value at this location is 0 times the median value of that predictor. 
    ## The indus predictor value at this location is 1.868 times the median value of that predictor. 
    ## The chas predictor value at this location is 0 times the median value of that predictor. 
    ## The nox predictor value at this location is 1.288 times the median value of that predictor. 
    ## The rm predictor value at this location is 0.878 times the median value of that predictor. 
    ## The age predictor value at this location is 1.29 times the median value of that predictor. 
    ## The dis predictor value at this location is 0.464 times the median value of that predictor. 
    ## The rad predictor value at this location is 4.8 times the median value of that predictor. 
    ## The tax predictor value at this location is 2.018 times the median value of that predictor. 
    ## The ptratio predictor value at this location is 1.06 times the median value of that predictor. 
    ## The lstat predictor value at this location is 2.693 times the median value of that predictor. 
    ## The medv predictor value at this location is 0.236 times the median value of that predictor.

``` r
room7<-rep(0,nrow(Boston))
room7[Boston$rm>7]=1
cat("The number of suburbs that average more than 7 rooms per house is",sum(room7)," representing",round(sum(room7)/length(room7),3),"of suburbs  \n")
```

    ## The number of suburbs that average more than 7 rooms per house is 64  representing 0.126 of suburbs

``` r
room8<-rep(0,nrow(Boston))
room8[Boston$rm>8]=1
cat("The number of suburbs that average more than 8 rooms per house is",sum(room8)," representing",round(sum(room8)/length(room8),3),"of suburbs  \n")
```

    ## The number of suburbs that average more than 8 rooms per house is 13  representing 0.026 of suburbs

# Chapter 3: Linear Regression

## Question 8

``` r
Auto.fit1<-lm(mpg~horsepower,data=Auto)
summary(Auto.fit1)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ horsepower, data = Auto)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -13.5710  -3.2592  -0.3435   2.7630  16.9240 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 39.935861   0.717499   55.66   <2e-16 ***
    ## horsepower  -0.157845   0.006446  -24.49   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 4.906 on 390 degrees of freedom
    ## Multiple R-squared:  0.6059, Adjusted R-squared:  0.6049 
    ## F-statistic: 599.7 on 1 and 390 DF,  p-value: < 2.2e-16

``` r
predict(Auto.fit1,data.frame(horsepower=(98)),interval="confidence")
```

    ##        fit      lwr      upr
    ## 1 24.46708 23.97308 24.96108

``` r
predict(Auto.fit1,data.frame(horsepower=(98)),interval="prediction")
```

    ##        fit     lwr      upr
    ## 1 24.46708 14.8094 34.12476

There is a negative relationship between mpg and horsepower. For each
unit increase in horsepower the mpg decreases by `coef(Auto.fit1)[2]`.
The confidence and prediction intervals for a horsepower of 98 are as
given above.

``` r
plot(Auto$horsepower,Auto$mpg)
abline(Auto.fit1)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
par(mfrow=c(2,2))
plot(Auto.fit1)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-12-2.png)<!-- -->

\#\#Question 9

``` r
cor(Auto[,1:8])
```

    ##                     mpg  cylinders displacement horsepower     weight
    ## mpg           1.0000000 -0.7776175   -0.8051269 -0.7784268 -0.8322442
    ## cylinders    -0.7776175  1.0000000    0.9508233  0.8429834  0.8975273
    ## displacement -0.8051269  0.9508233    1.0000000  0.8972570  0.9329944
    ## horsepower   -0.7784268  0.8429834    0.8972570  1.0000000  0.8645377
    ## weight       -0.8322442  0.8975273    0.9329944  0.8645377  1.0000000
    ## acceleration  0.4233285 -0.5046834   -0.5438005 -0.6891955 -0.4168392
    ## year          0.5805410 -0.3456474   -0.3698552 -0.4163615 -0.3091199
    ## origin        0.5652088 -0.5689316   -0.6145351 -0.4551715 -0.5850054
    ##              acceleration       year     origin
    ## mpg             0.4233285  0.5805410  0.5652088
    ## cylinders      -0.5046834 -0.3456474 -0.5689316
    ## displacement   -0.5438005 -0.3698552 -0.6145351
    ## horsepower     -0.6891955 -0.4163615 -0.4551715
    ## weight         -0.4168392 -0.3091199 -0.5850054
    ## acceleration    1.0000000  0.2903161  0.2127458
    ## year            0.2903161  1.0000000  0.1815277
    ## origin          0.2127458  0.1815277  1.0000000

``` r
Auto.fit2<-lm(mpg~.-name,data=Auto)
summary(Auto.fit2)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ . - name, data = Auto)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -9.5903 -2.1565 -0.1169  1.8690 13.0604 
    ## 
    ## Coefficients:
    ##                Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  -17.218435   4.644294  -3.707  0.00024 ***
    ## cylinders     -0.493376   0.323282  -1.526  0.12780    
    ## displacement   0.019896   0.007515   2.647  0.00844 ** 
    ## horsepower    -0.016951   0.013787  -1.230  0.21963    
    ## weight        -0.006474   0.000652  -9.929  < 2e-16 ***
    ## acceleration   0.080576   0.098845   0.815  0.41548    
    ## year           0.750773   0.050973  14.729  < 2e-16 ***
    ## origin         1.426141   0.278136   5.127 4.67e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.328 on 384 degrees of freedom
    ## Multiple R-squared:  0.8215, Adjusted R-squared:  0.8182 
    ## F-statistic: 252.4 on 7 and 384 DF,  p-value: < 2.2e-16

``` r
par(mfrow=c(2,2))
plot(Auto.fit2)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
Auto.fit3<-lm(mpg~year+origin+year:origin,data=Auto)
summary(Auto.fit3)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ year + origin + year:origin, data = Auto)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -11.3141  -3.7120  -0.6513   3.3621  15.5859 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -83.3809    12.0000  -6.948 1.57e-11 ***
    ## year          1.3089     0.1576   8.305 1.68e-15 ***
    ## origin       17.3752     6.8325   2.543   0.0114 *  
    ## year:origin  -0.1663     0.0889  -1.871   0.0621 .  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 5.199 on 388 degrees of freedom
    ## Multiple R-squared:  0.5596, Adjusted R-squared:  0.5562 
    ## F-statistic: 164.4 on 3 and 388 DF,  p-value: < 2.2e-16

``` r
Auto.fit4<-lm(mpg~year*weight,data=Auto)
summary(Auto.fit4)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ year * weight, data = Auto)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -8.0397 -1.9956 -0.0983  1.6525 12.9896 
    ## 
    ## Coefficients:
    ##               Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) -1.105e+02  1.295e+01  -8.531 3.30e-16 ***
    ## year         2.040e+00  1.718e-01  11.876  < 2e-16 ***
    ## weight       2.755e-02  4.413e-03   6.242 1.14e-09 ***
    ## year:weight -4.579e-04  5.907e-05  -7.752 8.02e-14 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 3.193 on 388 degrees of freedom
    ## Multiple R-squared:  0.8339, Adjusted R-squared:  0.8326 
    ## F-statistic: 649.3 on 3 and 388 DF,  p-value: < 2.2e-16

``` r
Auto.fit5<-lm(mpg~log(weight),data=Auto)
summary(Auto.fit5)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ log(weight), data = Auto)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.4315  -2.6752  -0.2888   1.9429  16.0136 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 209.9433     6.0002   34.99   <2e-16 ***
    ## log(weight) -23.4317     0.7534  -31.10   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 4.189 on 390 degrees of freedom
    ## Multiple R-squared:  0.7127, Adjusted R-squared:  0.7119 
    ## F-statistic: 967.3 on 1 and 390 DF,  p-value: < 2.2e-16

``` r
Auto.fit6<-lm(mpg~poly(weight,3),data=Auto)
summary(Auto.fit6)
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ poly(weight, 3), data = Auto)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -12.6259  -2.7080  -0.3552   1.8385  16.0816 
    ## 
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)        23.4459     0.2112 111.008  < 2e-16 ***
    ## poly(weight, 3)1 -128.4436     4.1817 -30.716  < 2e-16 ***
    ## poly(weight, 3)2   23.1589     4.1817   5.538 5.65e-08 ***
    ## poly(weight, 3)3    0.2204     4.1817   0.053    0.958    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 4.182 on 388 degrees of freedom
    ## Multiple R-squared:  0.7151, Adjusted R-squared:  0.7129 
    ## F-statistic: 324.7 on 3 and 388 DF,  p-value: < 2.2e-16

There is a relationship between the predictors and the response
evidenced by the p-value of the F-statistic. The predictors year,
origin, weight and displacement are statistically significant. For each
unit increase in year the miles per gallon increases by 0.75.

There appears to be a systematic trend to the residuals in the first
plot indicating a mild non-linearity. Values at 323 and 326 are
potentially outliers with standardised residuals close to 4 in absolute
magnitude. Observation 14 is a reasonably high leverage point.

I’ve fitted two additional models - one with year and origin including
an interaction and one with year and weight including an interaction.
For the former only the year predictor is significant while for the
latter both predictors and their interaction are significant.

There are also two non-linear regression models including weight; one
with log(weight) as a predictor and the second with a polynomial up to
third order. In the former the single predictor is significant while in
the latter the linear and quadratic terms are significant.

## Question 10

``` r
Carseats.fit1<-lm(Sales~Price+Urban+US,data=Carseats)
summary(Carseats.fit1)
```

    ## 
    ## Call:
    ## lm(formula = Sales ~ Price + Urban + US, data = Carseats)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.9206 -1.6220 -0.0564  1.5786  7.0581 
    ## 
    ## Coefficients:
    ##              Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 13.043469   0.651012  20.036  < 2e-16 ***
    ## Price       -0.054459   0.005242 -10.389  < 2e-16 ***
    ## UrbanYes    -0.021916   0.271650  -0.081    0.936    
    ## USYes        1.200573   0.259042   4.635 4.86e-06 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 2.472 on 396 degrees of freedom
    ## Multiple R-squared:  0.2393, Adjusted R-squared:  0.2335 
    ## F-statistic: 41.52 on 3 and 396 DF,  p-value: < 2.2e-16

``` r
Carseats.fit2<-lm(Sales~Price+US,data=Carseats)
summary(Carseats.fit2)
```

    ## 
    ## Call:
    ## lm(formula = Sales ~ Price + US, data = Carseats)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -6.9269 -1.6286 -0.0574  1.5766  7.0515 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 13.03079    0.63098  20.652  < 2e-16 ***
    ## Price       -0.05448    0.00523 -10.416  < 2e-16 ***
    ## USYes        1.19964    0.25846   4.641 4.71e-06 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 2.469 on 397 degrees of freedom
    ## Multiple R-squared:  0.2393, Adjusted R-squared:  0.2354 
    ## F-statistic: 62.43 on 2 and 397 DF,  p-value: < 2.2e-16

``` r
confint(Carseats.fit2)
```

    ##                   2.5 %      97.5 %
    ## (Intercept) 11.79032020 14.27126531
    ## Price       -0.06475984 -0.04419543
    ## USYes        0.69151957  1.70776632

``` r
par(mfrow=c(2,2))
plot(Carseats.fit2)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->
The price and whether the vendor is in the USA are statistically
significant predictors. A one unit increase in carseat price will result
in around 54 fewer sales. Vendors based in the USA can expect to sell
1200 extra units.

Removing Urban makes little change to the coefficient estimates and the
significance of the predictors. There does not appear to be any outliers
or points with high leverage.

# Chapter 4: Classification

## Question 13

``` r
summary(Weekly)
```

    ##       Year           Lag1               Lag2               Lag3         
    ##  Min.   :1990   Min.   :-18.1950   Min.   :-18.1950   Min.   :-18.1950  
    ##  1st Qu.:1995   1st Qu.: -1.1540   1st Qu.: -1.1540   1st Qu.: -1.1580  
    ##  Median :2000   Median :  0.2410   Median :  0.2410   Median :  0.2410  
    ##  Mean   :2000   Mean   :  0.1506   Mean   :  0.1511   Mean   :  0.1472  
    ##  3rd Qu.:2005   3rd Qu.:  1.4050   3rd Qu.:  1.4090   3rd Qu.:  1.4090  
    ##  Max.   :2010   Max.   : 12.0260   Max.   : 12.0260   Max.   : 12.0260  
    ##       Lag4               Lag5              Volume            Today         
    ##  Min.   :-18.1950   Min.   :-18.1950   Min.   :0.08747   Min.   :-18.1950  
    ##  1st Qu.: -1.1580   1st Qu.: -1.1660   1st Qu.:0.33202   1st Qu.: -1.1540  
    ##  Median :  0.2380   Median :  0.2340   Median :1.00268   Median :  0.2410  
    ##  Mean   :  0.1458   Mean   :  0.1399   Mean   :1.57462   Mean   :  0.1499  
    ##  3rd Qu.:  1.4090   3rd Qu.:  1.4050   3rd Qu.:2.05373   3rd Qu.:  1.4050  
    ##  Max.   : 12.0260   Max.   : 12.0260   Max.   :9.32821   Max.   : 12.0260  
    ##  Direction 
    ##  Down:484  
    ##  Up  :605  
    ##            
    ##            
    ##            
    ## 

``` r
pairs(Weekly[,-9])
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
weekly.fit<-glm(Direction~Lag1+Lag2+Lag3+Lag4+Lag5+Volume,data=Weekly,family=binomial)
summary(weekly.fit)
```

    ## 
    ## Call:
    ## glm(formula = Direction ~ Lag1 + Lag2 + Lag3 + Lag4 + Lag5 + 
    ##     Volume, family = binomial, data = Weekly)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.6949  -1.2565   0.9913   1.0849   1.4579  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)   
    ## (Intercept)  0.26686    0.08593   3.106   0.0019 **
    ## Lag1        -0.04127    0.02641  -1.563   0.1181   
    ## Lag2         0.05844    0.02686   2.175   0.0296 * 
    ## Lag3        -0.01606    0.02666  -0.602   0.5469   
    ## Lag4        -0.02779    0.02646  -1.050   0.2937   
    ## Lag5        -0.01447    0.02638  -0.549   0.5833   
    ## Volume      -0.02274    0.03690  -0.616   0.5377   
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 1496.2  on 1088  degrees of freedom
    ## Residual deviance: 1486.4  on 1082  degrees of freedom
    ## AIC: 1500.4
    ## 
    ## Number of Fisher Scoring iterations: 4

``` r
weekly.prob<-predict(weekly.fit,type="response")
weekly.pred<-rep("Down",dim(Weekly)[1])
weekly.pred[weekly.prob>0.5]="Up"
table(weekly.pred,Weekly$Direction)
```

    ##            
    ## weekly.pred Down  Up
    ##        Down   54  48
    ##        Up    430 557

``` r
weekly.train<-(Weekly$Year<2009)
Weekly.test<-Weekly[!weekly.train,]
Direction.test<-Weekly$Direction[!weekly.train]
weekly.fit2<-glm(Direction~Lag2,data=Weekly,family=binomial,subset=weekly.train)
weekly.prob2<-predict(weekly.fit2,Weekly.test,type="response")
weekly.pred2<-rep("Down",dim(Weekly.test)[1])
weekly.pred2[weekly.prob2>0.5]="Up"
table(weekly.pred2,Direction.test)
```

    ##             Direction.test
    ## weekly.pred2 Down Up
    ##         Down    9  5
    ##         Up     34 56

There appears to be a relationship between volume and year. In the
logistic regression the only predictor that is significant is Lag2. The
fraction of correct predictions on the test data using logistic
regression is (9+56)/104=0.625.

``` r
library(MASS)
```

    ## 
    ## Attaching package: 'MASS'

    ## The following object is masked from 'package:ISLR2':
    ## 
    ##     Boston

``` r
weekly.fit3<-lda(Direction~Lag2,data=Weekly,subset=weekly.train)
weekly.prob3<-predict(weekly.fit3,Weekly.test)
weekly.class<-weekly.prob3$class
table(weekly.class,Direction.test)
```

    ##             Direction.test
    ## weekly.class Down Up
    ##         Down    9  5
    ##         Up     34 56

Linear discriminant analysis also successfully predicts 0.625 of cases
correctly.

``` r
weekly.fit4<-qda(Direction~Lag2,data=Weekly,subset=weekly.train)
weekly.prob4<-predict(weekly.fit4,Weekly.test)
weekly.classqda<-weekly.prob4$class
table(weekly.classqda,Direction.test)
```

    ##                Direction.test
    ## weekly.classqda Down Up
    ##            Down    0  0
    ##            Up     43 61

Quadratic discriminant analysis correctly predicts 61/104 instances
representing 0.586 of cases.

``` r
library(class)
train.knnx<-data.frame(Weekly$Lag2[weekly.train])
test.knnx<-data.frame(Weekly$Lag2[!weekly.train])
train.Direction<-Weekly$Direction[weekly.train]
set.seed(1)
knnweekly<-knn(train.knnx,test.knnx,train.Direction,k=1)
table(knnweekly,Direction.test)
```

    ##          Direction.test
    ## knnweekly Down Up
    ##      Down   21 30
    ##      Up     22 31

K nearest neighbours with k=1 correctly predicts 52/104=0.5 of the test
instances.

``` r
library(e1071)
nb.fit<-naiveBayes(Direction~Lag2,data=Weekly,subset=weekly.train)
nb.class<-predict(nb.fit,Weekly.test)
table(nb.class,Direction.test)
```

    ##         Direction.test
    ## nb.class Down Up
    ##     Down    0  0
    ##     Up     43 61

The naive Bayes classifier correctly identifies 61/104=0.586 instances
in the test set.

The linear regression and linear discriminant analysis classifier
perform best on the test data set.

## Question 14

``` r
mpg01<-rep(0,dim(Auto)[1])
mpg01[Auto$mpg>median(Auto$mpg)]=1
Auto01<-data.frame(Auto,mpg01)
par(mfrow=c(2,2))
for (i in 2:8)
{boxplot(Auto01[,i]~mpg01,ylab=names(Auto01)[i])}
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
Auto01.train<-(Auto01$year<80)
Auto01.test<-Auto01[!Auto01.train,]
mpg01.test<-Auto01$mpg01[!Auto01.train]
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-20-2.png)<!-- -->
Weight, horsepower and displacement seem to be the most important
predictors for mpg01.

``` r
ldaauto.fit<-lda(mpg01~weight+horsepower+displacement,data=Auto01,subset=Auto01.train)
ldaauto.fit.pred<-predict(ldaauto.fit,Auto01.test)$class
table(ldaauto.fit.pred,mpg01.test)
```

    ##                 mpg01.test
    ## ldaauto.fit.pred  0  1
    ##                0  5  9
    ##                1  0 71

A linear discriminant analysis classifier based on weight, horsepower
and displacement correctly classified 76/85=0.894 of test data instances
meaning the error rate was 0.106.

``` r
qdaauto.fit<-qda(mpg01~weight+horsepower+displacement,data=Auto01,subset=Auto01.train)
qdaauto.fit.pred<-predict(qdaauto.fit,Auto01.test)$class
table(qdaauto.fit.pred,mpg01.test)
```

    ##                 mpg01.test
    ## qdaauto.fit.pred  0  1
    ##                0  5 11
    ##                1  0 69

A quadratic discriminant analysis classifier based on weight, horsepower
and displacement correctly classified 74/85=0.870 of test data instances
meaning the error rate was 0.130.

``` r
lrauto.fit<-glm(mpg01~weight+horsepower+displacement,data=Auto01,family="binomial",subset=Auto01.train)
lrauto.prob<-predict(lrauto.fit,Auto01.test,type="response")
lrauto.pred<-rep(0,length(lrauto.prob))
lrauto.pred[lrauto.prob>0.5]=1
table(lrauto.pred,mpg01.test)
```

    ##            mpg01.test
    ## lrauto.pred  0  1
    ##           0  5 15
    ##           1  0 65

Logistic regression correctly identifies 70/85=0.823 test instances
meaning the error rate is 0.177.

``` r
nbauto.fit<-naiveBayes(mpg01~weight+horsepower+displacement,data=Auto01,subset=Auto01.train)
nbauto.pred<-predict(nbauto.fit,Auto01.test)
table(nbauto.pred,mpg01.test)
```

    ##            mpg01.test
    ## nbauto.pred  0  1
    ##           0  5  7
    ##           1  0 73

Naive Bayes correctly identifies 78/85=0.918 instances of the test data
set meaning the error rate is 0.812.

``` r
knnauto.train<-cbind(Auto01$weight,Auto01$horsepower,Auto01$displacement)[Auto01.train,]
knnauto.test<-cbind(Auto01$weight,Auto01$horsepower,Auto01$displacement)[!Auto01.train,]
set.seed(1)
knnauto.fit1<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=1)
table(knnauto.fit1,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit1  0  1
    ##            0  5 17
    ##            1  0 63

``` r
knnauto.fit2<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=2)
table(knnauto.fit2,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit2  0  1
    ##            0  5 19
    ##            1  0 61

``` r
knnauto.fit3<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=3)
table(knnauto.fit3,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit3  0  1
    ##            0  5 22
    ##            1  0 58

``` r
knnauto.fit4<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=4)
table(knnauto.fit4,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit4  0  1
    ##            0  5 22
    ##            1  0 58

``` r
knnauto.fit5<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=5)
table(knnauto.fit5,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit5  0  1
    ##            0  5 19
    ##            1  0 61

``` r
knnauto.fit6<-knn(knnauto.train,knnauto.test,mpg01[Auto01.train],k=6)
table(knnauto.fit6,mpg01.test)
```

    ##             mpg01.test
    ## knnauto.fit6  0  1
    ##            0  5 20
    ##            1  0 60

K nearest neighbours with k=1 correctly identifies 68/85=0.8 instances
in the test data set meaningt the error rate is 0.2. K=1 performs best
out of all possibilities between 1 and 6.

# Chapter 5: Resampling Methods

## Question 5

``` r
lr.fit3<-glm(default~income+balance,data=Default,family="binomial")
summary(lr.fit3)
```

    ## 
    ## Call:
    ## glm(formula = default ~ income + balance, family = "binomial", 
    ##     data = Default)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -2.4725  -0.1444  -0.0574  -0.0211   3.7245  
    ## 
    ## Coefficients:
    ##               Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept) -1.154e+01  4.348e-01 -26.545  < 2e-16 ***
    ## income       2.081e-05  4.985e-06   4.174 2.99e-05 ***
    ## balance      5.647e-03  2.274e-04  24.836  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 2920.6  on 9999  degrees of freedom
    ## Residual deviance: 1579.0  on 9997  degrees of freedom
    ## AIC: 1585
    ## 
    ## Number of Fisher Scoring iterations: 8

``` r
vs.error<-rep(0,4)
for (i in 1:4)
{set.seed(i)
Default.train<-sample(10000,5000)
lr.fitdef<-glm(default~income+balance,data=Default,family="binomial",subset=Default.train)
lr.def.prob<-predict(lr.fitdef,Default[-Default.train,],type="response")
lr.def.pred<-rep("No",5000)
lr.def.pred[lr.def.prob>0.5]="Yes"
tbl<-table(lr.def.pred,Default$default[-Default.train])
vs.error[i]=(tbl[2]+tbl[3])/5000}
vs.error
```

    ## [1] 0.0254 0.0238 0.0264 0.0256

``` r
set.seed(5)
Default.train<-sample(10000,5000)
lr.fit4<-glm(default~income+balance+student,data=Default,family="binomial",subset=Default.train)
lr.def.prob4<-predict(lr.fit4,Default[-Default.train,],type="response")
lr.def.pred4<-rep("No",5000)
lr.def.pred4[lr.def.prob4>0.5]="Yes"
tbl2<-table(lr.def.pred4,Default$default[-Default.train])
vs.error2=(tbl2[2]+tbl2[3])/5000
vs.error2
```

    ## [1] 0.029

## Question 6

``` r
summary(lr.fit3)$coef
```

    ##                  Estimate   Std. Error    z value      Pr(>|z|)
    ## (Intercept) -1.154047e+01 4.347564e-01 -26.544680 2.958355e-155
    ## income       2.080898e-05 4.985167e-06   4.174178  2.990638e-05
    ## balance      5.647103e-03 2.273731e-04  24.836280 3.638120e-136

The standard error associated with the coefficient estimates are
4.985e-6 for the income coefficient and 2.274e-4 for the balance
coefficient.

``` r
library(boot)
set.seed(3)
boot.fn<-function(data,index){
  coef(glm(default~income+balance,data = data,subset = index,family="binomial"))}
boot(Default,boot.fn,100)
```

    ## 
    ## ORDINARY NONPARAMETRIC BOOTSTRAP
    ## 
    ## 
    ## Call:
    ## boot(data = Default, statistic = boot.fn, R = 100)
    ## 
    ## 
    ## Bootstrap Statistics :
    ##          original        bias     std. error
    ## t1* -1.154047e+01 -2.494434e-02 4.570045e-01
    ## t2*  2.080898e-05 -2.500829e-07 4.785038e-06
    ## t3*  5.647103e-03  2.363975e-05 2.554328e-04

The standard error estimate using the bootstrap method is 4.785e-6 for
the income coefficient and 2.554e-4 for the balance coefficient. These
estimates are both quite comparable with the linear regression
estimates.

## Question 7

``` r
lr.week<-glm(Direction~Lag1+Lag2,data=Weekly,family="binomial")
lr.weekl<-glm(Direction~Lag1+Lag2,data=Weekly[-1,],family="binomial")
lr.weekl.prob<-predict(lr.weekl,Weekly[1,],type="response")
if (lr.weekl.prob>0.5)
{lr.weekl.pred<-1} else 
{lr.weekl.pred<-0}
contrasts(Weekly$Direction)
```

    ##      Up
    ## Down  0
    ## Up    1

``` r
lr.weekl.pred
```

    ## [1] 1

``` r
Weekly$Direction[1]
```

    ## [1] Down
    ## Levels: Down Up

``` r
error<-rep(0,dim(Weekly)[1])
for (i in 1:1089)
{lr.weekl<-glm(Direction~Lag1+Lag2,data=Weekly[-i,],family="binomial")
lr.weeekl.prob<-predict(lr.weekl,Weekly[i,],type="response")
if (lr.weekl.prob>0.5)
{lr.weekl.pred<-1} else 
{lr.weekl.pred<-0}
if (lr.weekl.pred==1&&Weekly$Direction[i]=="Down")
{error[i]=1} else if (lr.weekl.pred==0&&Weekly$Direction[i]=="Up")
{error[i]=1} else
{error[i]=0}
}
cat("The leave-one-out-cross-validation estimate for the test error is", sum(error)/dim(Weekly)[1])
```

    ## The leave-one-out-cross-validation estimate for the test error is 0.4444444

# Chapter 6: Linear Model Selection and Regularisation

## Question 8

``` r
library("leaps")
x<-rnorm(100)
eps<-rnorm(100,mean=0,sd=0.1)
b0=0.5
b1=0.2
b2=-0.05
b3=0.01
y<-b0+b1*x+b2*x^2+b3*x^3+eps
SData<-data.frame(x,y)
regfit.sdata<-regsubsets(y~poly(x,10),data=SData)
sumregfit.sdata<-summary(regfit.sdata)
sumregfit.sdata
```

    ## Subset selection object
    ## Call: regsubsets.formula(y ~ poly(x, 10), data = SData)
    ## 10 Variables  (and intercept)
    ##               Forced in Forced out
    ## poly(x, 10)1      FALSE      FALSE
    ## poly(x, 10)2      FALSE      FALSE
    ## poly(x, 10)3      FALSE      FALSE
    ## poly(x, 10)4      FALSE      FALSE
    ## poly(x, 10)5      FALSE      FALSE
    ## poly(x, 10)6      FALSE      FALSE
    ## poly(x, 10)7      FALSE      FALSE
    ## poly(x, 10)8      FALSE      FALSE
    ## poly(x, 10)9      FALSE      FALSE
    ## poly(x, 10)10     FALSE      FALSE
    ## 1 subsets of each size up to 8
    ## Selection Algorithm: exhaustive
    ##          poly(x, 10)1 poly(x, 10)2 poly(x, 10)3 poly(x, 10)4 poly(x, 10)5
    ## 1  ( 1 ) "*"          " "          " "          " "          " "         
    ## 2  ( 1 ) "*"          "*"          " "          " "          " "         
    ## 3  ( 1 ) "*"          "*"          "*"          " "          " "         
    ## 4  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 5  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 6  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 7  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 8  ( 1 ) "*"          "*"          "*"          "*"          "*"         
    ##          poly(x, 10)6 poly(x, 10)7 poly(x, 10)8 poly(x, 10)9 poly(x, 10)10
    ## 1  ( 1 ) " "          " "          " "          " "          " "          
    ## 2  ( 1 ) " "          " "          " "          " "          " "          
    ## 3  ( 1 ) " "          " "          " "          " "          " "          
    ## 4  ( 1 ) " "          " "          " "          " "          " "          
    ## 5  ( 1 ) " "          " "          " "          "*"          " "          
    ## 6  ( 1 ) "*"          " "          " "          "*"          " "          
    ## 7  ( 1 ) "*"          " "          " "          "*"          "*"          
    ## 8  ( 1 ) "*"          " "          " "          "*"          "*"

``` r
par(mfrow=c(2,2))
plot(sumregfit.sdata$rss,xlab="Number of variables",ylab="Residual sum of squares",type="l")
plot(sumregfit.sdata$adjr2,xlab="Number of variables",ylab="Adjusted R-squared",type="l")
points(which.max(sumregfit.sdata$adjr2),sumregfit.sdata$adjr2[which.max(sumregfit.sdata$adjr2)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata$cp,xlab="Number of variables",ylab="Cp",type="l")
points(which.min(sumregfit.sdata$cp),sumregfit.sdata$cp[which.min(sumregfit.sdata$cp)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata$bic,xlab="Number of variables",ylab="BIC",type="l")
points(which.min(sumregfit.sdata$bic),sumregfit.sdata$bic[which.min(sumregfit.sdata$bic)],col = "red", cex = 2,pch = 20)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

Following best-subset selection, the adjusted R-squared statistic picks
a model with 8 variables. Cp selects a model with 5 variables and BIC
picks a model with 4 variables.

``` r
regfit.sdata.back<-regsubsets(y~poly(x,10),data=SData,method="backward")
sumregfit.sdata.back<-summary(regfit.sdata.back)
sumregfit.sdata.back
```

    ## Subset selection object
    ## Call: regsubsets.formula(y ~ poly(x, 10), data = SData, method = "backward")
    ## 10 Variables  (and intercept)
    ##               Forced in Forced out
    ## poly(x, 10)1      FALSE      FALSE
    ## poly(x, 10)2      FALSE      FALSE
    ## poly(x, 10)3      FALSE      FALSE
    ## poly(x, 10)4      FALSE      FALSE
    ## poly(x, 10)5      FALSE      FALSE
    ## poly(x, 10)6      FALSE      FALSE
    ## poly(x, 10)7      FALSE      FALSE
    ## poly(x, 10)8      FALSE      FALSE
    ## poly(x, 10)9      FALSE      FALSE
    ## poly(x, 10)10     FALSE      FALSE
    ## 1 subsets of each size up to 8
    ## Selection Algorithm: backward
    ##          poly(x, 10)1 poly(x, 10)2 poly(x, 10)3 poly(x, 10)4 poly(x, 10)5
    ## 1  ( 1 ) "*"          " "          " "          " "          " "         
    ## 2  ( 1 ) "*"          "*"          " "          " "          " "         
    ## 3  ( 1 ) "*"          "*"          "*"          " "          " "         
    ## 4  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 5  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 6  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 7  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 8  ( 1 ) "*"          "*"          "*"          "*"          "*"         
    ##          poly(x, 10)6 poly(x, 10)7 poly(x, 10)8 poly(x, 10)9 poly(x, 10)10
    ## 1  ( 1 ) " "          " "          " "          " "          " "          
    ## 2  ( 1 ) " "          " "          " "          " "          " "          
    ## 3  ( 1 ) " "          " "          " "          " "          " "          
    ## 4  ( 1 ) " "          " "          " "          " "          " "          
    ## 5  ( 1 ) " "          " "          " "          "*"          " "          
    ## 6  ( 1 ) "*"          " "          " "          "*"          " "          
    ## 7  ( 1 ) "*"          " "          " "          "*"          "*"          
    ## 8  ( 1 ) "*"          " "          " "          "*"          "*"

``` r
par(mfrow=c(2,2))
plot(sumregfit.sdata.back$rss,xlab="Number of variables",ylab="Residual sum of squares",type="l")
plot(sumregfit.sdata.back$adjr2,xlab="Number of variables",ylab="Adjusted R-squared",type="l")
points(which.max(sumregfit.sdata.back$adjr2),sumregfit.sdata.back$adjr2[which.max(sumregfit.sdata.back$adjr2)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata.back$cp,xlab="Number of variables",ylab="Cp",type="l")
points(which.min(sumregfit.sdata.back$cp),sumregfit.sdata.back$cp[which.min(sumregfit.sdata.back$cp)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata.back$bic,xlab="Number of variables",ylab="BIC",type="l")
points(which.min(sumregfit.sdata.back$bic),sumregfit.sdata.back$bic[which.min(sumregfit.sdata.back$bic)],col = "red", cex = 2,pch = 20)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->
Using backward selection the preferred models are 6 variables from
adjusted R-squared, 3 variables from Cp and 2 variables from BIC.

``` r
regfit.sdata.fwd<-regsubsets(y~poly(x,10),data=SData,method="forward")
sumregfit.sdata.fwd<-summary(regfit.sdata.fwd)
sumregfit.sdata.fwd
```

    ## Subset selection object
    ## Call: regsubsets.formula(y ~ poly(x, 10), data = SData, method = "forward")
    ## 10 Variables  (and intercept)
    ##               Forced in Forced out
    ## poly(x, 10)1      FALSE      FALSE
    ## poly(x, 10)2      FALSE      FALSE
    ## poly(x, 10)3      FALSE      FALSE
    ## poly(x, 10)4      FALSE      FALSE
    ## poly(x, 10)5      FALSE      FALSE
    ## poly(x, 10)6      FALSE      FALSE
    ## poly(x, 10)7      FALSE      FALSE
    ## poly(x, 10)8      FALSE      FALSE
    ## poly(x, 10)9      FALSE      FALSE
    ## poly(x, 10)10     FALSE      FALSE
    ## 1 subsets of each size up to 8
    ## Selection Algorithm: forward
    ##          poly(x, 10)1 poly(x, 10)2 poly(x, 10)3 poly(x, 10)4 poly(x, 10)5
    ## 1  ( 1 ) "*"          " "          " "          " "          " "         
    ## 2  ( 1 ) "*"          "*"          " "          " "          " "         
    ## 3  ( 1 ) "*"          "*"          "*"          " "          " "         
    ## 4  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 5  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 6  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 7  ( 1 ) "*"          "*"          "*"          " "          "*"         
    ## 8  ( 1 ) "*"          "*"          "*"          "*"          "*"         
    ##          poly(x, 10)6 poly(x, 10)7 poly(x, 10)8 poly(x, 10)9 poly(x, 10)10
    ## 1  ( 1 ) " "          " "          " "          " "          " "          
    ## 2  ( 1 ) " "          " "          " "          " "          " "          
    ## 3  ( 1 ) " "          " "          " "          " "          " "          
    ## 4  ( 1 ) " "          " "          " "          " "          " "          
    ## 5  ( 1 ) " "          " "          " "          "*"          " "          
    ## 6  ( 1 ) "*"          " "          " "          "*"          " "          
    ## 7  ( 1 ) "*"          " "          " "          "*"          "*"          
    ## 8  ( 1 ) "*"          " "          " "          "*"          "*"

``` r
par(mfrow=c(2,2))
plot(sumregfit.sdata.fwd$rss,xlab="Number of variables",ylab="Residual sum of squares",type="l")
plot(sumregfit.sdata.fwd$adjr2,xlab="Number of variables",ylab="Adjusted R-squared",type="l")
points(which.max(sumregfit.sdata.fwd$adjr2),sumregfit.sdata.fwd$adjr2[which.max(sumregfit.sdata.fwd$adjr2)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata.fwd$cp,xlab="Number of variables",ylab="Cp",type="l")
points(which.min(sumregfit.sdata.fwd$cp),sumregfit.sdata.fwd$cp[which.min(sumregfit.sdata.fwd$cp)],col = "red", cex = 2,pch = 20)
plot(sumregfit.sdata.fwd$bic,xlab="Number of variables",ylab="BIC",type="l")
points(which.min(sumregfit.sdata.fwd$bic),sumregfit.sdata.fwd$bic[which.min(sumregfit.sdata.fwd$bic)],col = "red", cex = 2,pch = 20)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->
Forward selection leads to a 6 variable model for adjusted R-squared, a
3 variable model for Cp and a 2 variable model for BIC.

``` r
library(glmnet)
```

    ## Loading required package: Matrix

    ## Loaded glmnet 4.1-3

``` r
grid<-10^seq(10,-2,length=100)
x.vars=matrix(rep(rep(0,100),10),nrow=100,ncol=10)
for (i in 1:10)
{x.vars[,i]=x^i}
lasso.fit<-glmnet(x.vars,y,alpha=1,lambda=grid)
par(mfrow=c(1,2))
plot(coef(lasso.fit)[,],ylab="Coefficient estimates")
plot(lasso.fit)
```

    ## Warning in regularize.values(x, y, ties, missing(ties), na.rm = na.rm):
    ## collapsing to unique 'x' values

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

``` r
set.seed(1)
train<-sample(1:length(x),length(x)/2)
test<-(-train)
y.test<-y[test]
lasso.fit2<-glmnet(x.vars[train,],y[train],alpha=1,lambda=grid)
cv.lasso.fit<-cv.glmnet(x.vars[train,],y[train],alpha=1,lambda=grid)
plot(cv.lasso.fit)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

``` r
bestlam<-cv.lasso.fit$lambda.min
bestlam
```

    ## [1] 0.01

``` r
lasso.pred<-predict(lasso.fit2,s=bestlam,newx=x.vars[test,])
mean (( lasso.pred - y.test)^2)
```

    ## [1] 0.007952033

## Question 9

``` r
set.seed(1)
train<-sample(1:777,666)
test<-(-train)
College.train<-College[train,]
apps.lm<-lm(Apps~.,data=College,subset = train)
apps.lm.pred<-predict(apps.lm,College[test,])
mse.lm<-mean((College$Apps[test]-apps.lm.pred)^2)
mse.lm
```

    ## [1] 1576016

``` r
library(glmnet)
x<-model.matrix(Apps~.,College)[,-1]
y<-College$Apps
grid<-10^seq(10,-2,length=100)
apps.ridge<-glmnet(x[train,],y[train],alpha=0,lambda=grid)
apps.ridge.cv<-cv.glmnet(x[train,],y[train], alpha=0,lambda=grid)
plot(apps.ridge.cv)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

``` r
bestlam<-apps.ridge.cv$lambda.min
apps.ridge.pred<-predict(apps.ridge,s=bestlam,newx=x[test,])
mse.ridge<-mean((y[test]-apps.ridge.pred)^2)
mse.ridge
```

    ## [1] 1575610

``` r
apps.lasso<-glmnet(x[train,],y[train],alpha=1,lambda=grid)
apps.lasso.cv<-cv.glmnet(x[train,],y[train], alpha=1,lambda=grid)
plot(apps.lasso.cv)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

``` r
bestlam<-apps.lasso.cv$lambda.min
apps.lasso.pred<-predict(apps.lasso,s=bestlam,newx=x[test,])
mse.lasso<-mean((y[test]-apps.lasso.pred)^2)
mse.lasso
```

    ## [1] 1574871

``` r
predict(apps.lasso , type = "coefficients",
s = bestlam)
```

    ## 19 x 1 sparse Matrix of class "dgCMatrix"
    ##                        s1
    ## (Intercept) -5.798614e+02
    ## PrivateYes  -3.887947e+02
    ## Accept       1.652106e+00
    ## Enroll      -1.083641e+00
    ## Top10perc    4.314037e+01
    ## Top25perc   -1.178371e+01
    ## F.Undergrad  7.205360e-02
    ## P.Undergrad  5.873815e-02
    ## Outstate    -7.853565e-02
    ## Room.Board   1.517184e-01
    ## Books        1.562724e-01
    ## Personal     6.613317e-03
    ## PhD         -9.027669e+00
    ## Terminal     1.489658e-01
    ## S.F.Ratio    1.484456e+01
    ## perc.alumni  1.351553e-01
    ## Expend       5.794693e-02
    ## Grad.Rate    6.545461e+00
    ## EliteYes     3.017161e+02

Cross-validation has chosen a low-value of lambda so the estimates are
close to the least-squares ones. As such all of the variables have
non-zero coefficients.

``` r
library(pls)
```

    ## 
    ## Attaching package: 'pls'

    ## The following object is masked from 'package:stats':
    ## 
    ##     loadings

``` r
apps.pcr<-pcr(Apps~.,data=College,scale=TRUE,subest=train,validation="CV")
validationplot(apps.pcr,val.type = "MSEP")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

``` r
apps.pcr.pred <- predict(apps.pcr , College[test,], ncomp = 5)
mse.pcr<-mean (( apps.pcr.pred - College$Apps[test])^2)
mse.pcr
```

    ## [1] 2319381

We selected the model with 5 principal components.

``` r
apps.pls<-plsr(Apps~.,data=College,scale=TRUE,subset=train,validation="CV")
validationplot(apps.pls,val.type = "MSEP")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

``` r
apps.pls.pred <- predict(apps.pls , College[test,], ncomp = 5)
mse.pls<-mean (( apps.pls.pred - College$Apps[test])^2)
mse.pls
```

    ## [1] 1632095

We selected the partial least squares model with 5 components.

# Chapter 7: Moving Beyond Linearity

## Question 6

``` r
set.seed(4)
cv.error<-rep(0,10)
for (i in 1:10)
{glm.fit<-glm(wage~poly(age,i),data=Wage)
cv.error[i]<-cv.glm(Wage,glm.fit,K=10)$delta[1]}
plot(cv.error)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

``` r
model<-glm(wage~poly(age,3),data=Wage)
ages<-seq(0,80,1)
plot(ages,coef(model)[1]+coef(model)[2]*ages++coef(model)[3]*ages^2+coef(model)[4]*ages^3,ylab="Wage")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-40-2.png)<!-- -->

A degree 3 polynomial was chosen which is consistent with the 3/4
variable choice from the ANOVA approach.

``` r
cv.error.cut <- rep (0,12)
for (i in 2:13){
  Wage$tmp <- cut(Wage$age,i)
  step.fit = glm(wage~tmp, data = Wage)
  cv.error.cut[i] <- cv.glm(Wage ,step.fit, K= 10)$delta [1]
}
plot(cv.error.cut)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->
\#\# Question 7

``` r
par(mfrow=c(2,3))
plot(Wage$maritl,Wage$wage,xlab="Marital Status",ylab="Wage")
plot(Wage$race,Wage$wage,xlab="Race",ylab="Wage")
plot(Wage$jobclass,Wage$wage,xlab="Job Class",ylab="Wage")
plot(Wage$health,Wage$wage,xlab="Health Status",ylab="Wage")
plot(Wage$health_ins,Wage$wage,xlab="Health Insurance",ylab="Wage")
plot(Wage$region,Wage$wage,xlab="Region",ylab="Wage")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->
There is potential evidence for health status, marital status, race and
whether the individual has health insurance being relevant to Wage.

``` r
library(splines)
polyfits1<-lm(wage~race+health_ins+health+maritl,data=Wage)
summary(polyfits1)
```

    ## 
    ## Call:
    ## lm(formula = wage ~ race + health_ins + health + maritl, data = Wage)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -96.786 -23.043  -5.508  15.187 223.242 
    ## 
    ## Coefficients:
    ##                      Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            95.317      2.022  47.151  < 2e-16 ***
    ## race2. Black           -6.420      2.365  -2.715  0.00667 ** 
    ## race3. Asian            7.482      2.869   2.608  0.00916 ** 
    ## race4. Other          -14.101      6.310  -2.235  0.02550 *  
    ## health_ins2. No       -25.170      1.520 -16.561  < 2e-16 ***
    ## health2. >=Very Good   11.232      1.545   7.270 4.56e-13 ***
    ## maritl2. Married       22.603      1.727  13.086  < 2e-16 ***
    ## maritl3. Widowed        5.057      8.856   0.571  0.56804    
    ## maritl4. Divorced       8.362      3.069   2.725  0.00647 ** 
    ## maritl5. Separated      8.760      5.344   1.639  0.10129    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 38.01 on 2990 degrees of freedom
    ## Multiple R-squared:  0.1726, Adjusted R-squared:  0.1701 
    ## F-statistic: 69.32 on 9 and 2990 DF,  p-value: < 2.2e-16

## Question 9

``` r
cub.fit<-lm(nox~poly(dis,3),data=Boston)
summary(cub.fit)
```

    ## 
    ## Call:
    ## lm(formula = nox ~ poly(dis, 3), data = Boston)
    ## 
    ## Residuals:
    ##       Min        1Q    Median        3Q       Max 
    ## -0.121130 -0.040619 -0.009738  0.023385  0.194904 
    ## 
    ## Coefficients:
    ##                Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)    0.554695   0.002759 201.021  < 2e-16 ***
    ## poly(dis, 3)1 -2.003096   0.062071 -32.271  < 2e-16 ***
    ## poly(dis, 3)2  0.856330   0.062071  13.796  < 2e-16 ***
    ## poly(dis, 3)3 -0.318049   0.062071  -5.124 4.27e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 0.06207 on 502 degrees of freedom
    ## Multiple R-squared:  0.7148, Adjusted R-squared:  0.7131 
    ## F-statistic: 419.3 on 3 and 502 DF,  p-value: < 2.2e-16

``` r
plot(Boston$dis,Boston$nox,ylab="NOx, pp10m",xlab="Distance to employment centre")
pred <- predict(cub.fit)
dissort <- sort(Boston$dis, index.return=T)$ix
lines(Boston$dis[dissort],pred[dissort],col="red",type="l")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

``` r
poly.rss<-rep(0,10)
for (i in 1:10)
{poly.fits<-lm(nox~poly(dis,i),data=Boston)
poly.rss[i]<-sum(poly.fits$residuals^2)}
poly.rss
```

    ##  [1] 2.768563 2.035262 1.934107 1.932981 1.915290 1.878257 1.849484 1.835630
    ##  [9] 1.833331 1.832171

``` r
poly.cv<-rep(0,10)
for (i in 1:10)
{poly.fits<-glm(nox~poly(dis,i),data=Boston)
cv.poly.fits<-cv.glm(Boston,poly.fits,K=10)
poly.cv[i]<-cv.poly.fits$delta[1]}
plot(poly.cv)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-44-2.png)<!-- -->
Cross-validation seems to support a model using up to cubic or quartic
terms.

``` r
dislims<-range(Boston$dis)
dis.grid<-seq(from=dislims[1],to=dislims[2])
spline.fit<-lm(nox~bs(dis,knots=median(dis)),data=Boston)
spline.pred <- predict(spline.fit , newdata = list(dis=dis.grid), se = T)
se.bands <- cbind(spline.pred$fit + 2 * spline.pred$se.fit ,
spline.pred$fit - 2 * spline.pred$se.fit)
plot(Boston$dis,Boston$nox)
lines(dis.grid,spline.pred$fit)
matlines(dis.grid , se.bands, lwd = 1, col = "blue", lty = 3)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

``` r
bs.rss<-rep(0,10)
for (i in 1:10)
{bs.fits<-lm(nox~bs(dis,df=4+i),data=Boston)
bs.rss[i]<-sum(bs.fits$residuals^2)}
bs.rss
```

    ##  [1] 1.840173 1.833966 1.829884 1.816995 1.825653 1.792535 1.796992 1.788999
    ##  [9] 1.782350 1.781838

``` r
set.seed(10)
bs.cv<-rep(0,10)
for (i in 1:10)
{bs.fits<-glm(nox~bs(dis,df=4+i),data=Boston)
bs.fits.cv<-cv.glm(Boston,bs.fits,K=10)
bs.cv[i]<-bs.fits.cv$delta[1]}
```

    ## Warning in bs(dis, degree = 3L, knots = c(`33.33333%` = 2.32486666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`33.33333%` = 2.32486666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`33.33333%` = 2.40296666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`33.33333%` = 2.40296666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`25%` = 2.10215, `50%` = 3.3175, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`25%` = 2.10215, `50%` = 3.3175, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`25%` = 2.09445, `50%` = 3.2157, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`25%` = 2.09445, `50%` = 3.2157, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`20%` = 1.9709, `40%` = 2.5975, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`20%` = 1.9709, `40%` = 2.5975, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`20%` = 1.9669, `40%` = 2.5975, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`20%` = 1.9669, `40%` = 2.5975, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`16.66667%` = 1.8208, `33.33333%` =
    ## 2.354, : some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`16.66667%` = 1.8208, `33.33333%` =
    ## 2.354, : some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`16.66667%` = 1.86636666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`16.66667%` = 1.86636666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`14.28571%` = 1.7936, `28.57143%`
    ## = 2.19385714285714, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`14.28571%` = 1.7936, `28.57143%`
    ## = 2.19385714285714, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`14.28571%` = 1.76467142857143, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`14.28571%` = 1.76467142857143, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`12.5%` = 1.7278, `25%` = 2.0771, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`12.5%` = 1.7278, `25%` = 2.0771, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`12.5%` = 1.748425, `25%` = 2.09445, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`12.5%` = 1.748425, `25%` = 2.09445, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`11.11111%` = 1.74766666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`11.11111%` = 1.74766666666667, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`11.11111%` = 1.65225555555556, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`11.11111%` = 1.65225555555556, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`10%` = 1.62008, `20%` = 1.94984, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`10%` = 1.62008, `20%` = 1.94984, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`10%` = 1.64325, `20%` = 1.9444, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`10%` = 1.64325, `20%` = 1.9444, :
    ## some 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`9.090909%` = 1.61066363636364, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`9.090909%` = 1.61066363636364, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`9.090909%` = 1.59734545454545, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`9.090909%` = 1.59734545454545, : some
    ## 'x' values beyond boundary knots may cause ill-conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`8.333333%` = 1.5893, `16.66667%`
    ## = 1.85586666666667, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`8.333333%` = 1.5893, `16.66667%`
    ## = 1.85586666666667, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`8.333333%` = 1.57935, `16.66667%`
    ## = 1.84476666666667, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

    ## Warning in bs(dis, degree = 3L, knots = c(`8.333333%` = 1.57935, `16.66667%`
    ## = 1.84476666666667, : some 'x' values beyond boundary knots may cause ill-
    ## conditioned bases

``` r
plot(5:14,bs.cv)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-45-2.png)<!-- -->
The regression splines approach supports a model with 4+2=6 degrees of
freedom equivalent.

# Chapter 8: Tree Based Methods

``` r
library(tree)
library(randomForest)
```

    ## randomForest 4.6-14

    ## Type rfNews() to see new features/changes/bug fixes.

``` r
library(gbm)
```

    ## Loaded gbm 2.1.8

``` r
library(BART)
```

    ## Loading required package: nlme

    ## Loading required package: nnet

    ## Loading required package: survival

    ## 
    ## Attaching package: 'survival'

    ## The following object is masked from 'package:boot':
    ## 
    ##     aml

``` r
set.seed(1)
train<-sample(1:nrow(Boston),nrow(Boston)/2)
test<-(-train)
medv.test<-Boston$medv[test]
error.bag<-matrix(rep(0,40),nrow=5,ncol=8)
jay<-c(3,4,6,8,12)
for (j in 1:5)
{for (i in 1:8)
{tree.bag<-randomForest(medv~.,data=Boston,subset=train,mtry=jay[j],ntrees=40*i)
predict.bag<-predict(tree.bag,newdata=Boston[test,])
error.bag[j,i]<-mean((medv.test-predict.bag)^2)}}
plot(seq(40,320,40),error.bag[1,],type="b",col=2, xlab="Number of trees",ylab="Mean test error",ylim=c(17,26))
lines(seq(40,320,40),error.bag[2,],type="b",col=3)
lines(seq(40,320,40),error.bag[3,],type="b",col=4)
lines(seq(40,320,40),error.bag[4,],type="b",col=5)
lines(seq(40,320,40),error.bag[5,],type="b",col=6)
legend(x="topright",legend=c("p=3","p=4","p=6","p=8","p=12"),fill=2:6)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

``` r
train<-sample(1:nrow(Carseats),nrow(Carseats)/2)
test<-(-train)
tree.cars<-tree(Sales~.,data=Carseats,subset=train)
plot(tree.cars)
text(tree.cars,pretty=0)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

``` r
tree.pred<-predict(tree.cars,newdata=Carseats[test,])
MSE<- mean((tree.pred-Carseats$Sales[test])^2)
MSE
```

    ## [1] 6.71382

``` r
set.seed (7)
cv.cars <- cv.tree(tree.cars)
plot(cv.cars$size,cv.cars$dev,type="b")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-47-2.png)<!-- -->

``` r
prune.tree.cars<-prune.tree(tree.cars,best=14)
plot(prune.tree.cars)
text(tree.cars,pretty=0)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-47-3.png)<!-- -->

``` r
prune.pred<-predict(prune.tree.cars,newdata=Carseats[test,])
pruneMSE<-mean((prune.pred-Carseats$Sales[test])^2)
pruneMSE
```

    ## [1] 6.83461

The test MSE has improved after puning.

``` r
carseats.bag<-randomForest(Sales~.,data=Carseats,subset=train,mtry=10,ntrees=200)
bag.pred<-predict(carseats.bag,newdat=Carseats[test,])
bag.MSE<-mean((Carseats$Sales[test]-bag.pred)^2)
bag.MSE
```

    ## [1] 3.420791

``` r
importance(carseats.bag)
```

    ##             IncNodePurity
    ## CompPrice      133.646154
    ## Income         121.137159
    ## Advertising    113.733270
    ## Population      58.081735
    ## Price          413.758959
    ## ShelveLoc      561.541644
    ## Age            159.248094
    ## Education       35.156421
    ## Urban           10.420532
    ## US               5.650582

``` r
rf=c(3,4,5,6,8)
rf.mse<-rep(0,5)
rf.imp<-rep(0,5)
for (i in 1:5)
{carseats.bag<-randomForest(Sales~.,data=Carseats,subset=train,mtry=rf[i],ntrees=200)
bag.pred<-predict(carseats.bag,newdat=Carseats[test,])
rf.mse[i]<-mean((Carseats$Sales[test]-bag.pred)^2)}
rf.mse
```

    ## [1] 3.192982 3.154478 2.991543 3.115854 3.335379

``` r
importance(carseats.bag)
```

    ##             IncNodePurity
    ## CompPrice       134.96261
    ## Income          128.17053
    ## Advertising     117.16751
    ## Population       62.01756
    ## Price           409.99100
    ## ShelveLoc       555.91460
    ## Age             158.58002
    ## Education        39.07113
    ## Urban            11.99109
    ## US                6.25472

The approaches closest to bagging perform the best with the lowest test
MSE.

``` r
x<-Carseats[,2:11]
y<-Carseats[,1]
xtrain<-x[train,]
ytrain<-y[train]
xtest<-x[test,]
ytest<-y[test]
set.seed (1)
bartfit <- gbart(xtrain , ytrain , x.test = xtest)
```

    ## *****Calling gbart: type=1
    ## *****Data:
    ## data:n,p,np: 200, 14, 200
    ## y1,yn: 3.895950, 3.955950
    ## x1,x[n*p]: 104.000000, 1.000000
    ## xp1,xp[np*p]: 111.000000, 1.000000
    ## *****Number of Trees: 200
    ## *****Number of Cut Points: 61 ... 1
    ## *****burn,nd,thin: 100,1000,1
    ## *****Prior:beta,alpha,tau,nu,lambda,offset: 2,0.95,0.276302,3,0.167686,7.58405
    ## *****sigma: 0.927819
    ## *****w (weights): 1.000000 ... 1.000000
    ## *****Dirichlet:sparse,theta,omega,a,b,rho,augment: 0,0,1,0.5,1,14,0
    ## *****printevery: 100
    ## 
    ## MCMC
    ## done 0 (out of 1100)
    ## done 100 (out of 1100)
    ## done 200 (out of 1100)
    ## done 300 (out of 1100)
    ## done 400 (out of 1100)
    ## done 500 (out of 1100)
    ## done 600 (out of 1100)
    ## done 700 (out of 1100)
    ## done 800 (out of 1100)
    ## done 900 (out of 1100)
    ## done 1000 (out of 1100)
    ## time: 9s
    ## trcnt,tecnt: 1000,1000

``` r
yhat.bart <- bartfit$yhat.test.mean
mean (( ytest - yhat.bart)^2)
```

    ## [1] 1.792869

The BART MSE is significantly lower than any of the other approaches.

\#\#Question 10

``` r
Hitters<-na.omit(Hitters)
Logsal<-log10(Hitters$Salary)
Hitters2<-data.frame(Hitters,Logsal)
set.seed(6)
train<-sample(1:nrow(Hitters2),200)
test<-(-train)
shrink<-10^seq(-3,-1,length=10)
trainMSE<-rep(0,10)
testMSE<-rep(0,10)
for (i in 1:10)
{boost.hit<-gbm(Logsal~.-Salary,data=Hitters2[train,],n.trees=1000,distribution="gaussian",interaction.depth = 3,shrinkage = shrink[i])
trainMSE[i]<-boost.hit$train.error[1000]
yhat.boost <- predict(boost.hit ,
newdata = Hitters2[-train , ], n.trees = 1000)
testMSE[i]=mean((yhat.boost-Hitters2$Logsal)^2)}
```

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

    ## Warning in yhat.boost - Hitters2$Logsal: longer object length is not a multiple
    ## of shorter object length

``` r
plot(shrink,trainMSE,col=1,type="b")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

``` r
plot(shrink,testMSE,col=2,type="b")
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-51-2.png)<!-- -->

``` r
summary(boost.hit)
```

![](ISLR-ML-Problems_files/figure-gfm/unnamed-chunk-51-3.png)<!-- -->

    ##                 var    rel.inf
    ## CAtBat       CAtBat 20.4759928
    ## CRuns         CRuns  9.2218717
    ## CRBI           CRBI  8.4575286
    ## Walks         Walks  8.0505881
    ## CWalks       CWalks  7.5439763
    ## PutOuts     PutOuts  6.0084521
    ## HmRun         HmRun  5.6067961
    ## CHmRun       CHmRun  4.9680662
    ## RBI             RBI  4.8880469
    ## Hits           Hits  3.7689581
    ## Assists     Assists  3.6709054
    ## CHits         CHits  3.6644251
    ## Runs           Runs  3.5490740
    ## Years         Years  3.2345321
    ## Errors       Errors  2.7458657
    ## AtBat         AtBat  2.6123688
    ## League       League  0.6351817
    ## Division   Division  0.4754083
    ## NewLeague NewLeague  0.4219621

# Chapter 9: Support Vector Machines

# Chapter 10: Deep Learning

# Chapter 11: Survival Analysis and Censored Data

# Chapter 12: Unsupervised Learning

# Chapter 13: Multiple Testing
