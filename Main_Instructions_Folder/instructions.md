Group Project 1 Resubmission After Preliminary Grading
================
14 October 2024

Hi, we hope you’re ready to get a bit of an introduction for how to use
RStudio! In this tutorial, beginner researchers, students at Bucknell
University in any beginner R class, and anyone with an interest in data
analysis will learn how to conceptualize what specific codes mean and
how they are useful for hypothesis testing, data exploration, and data
visualization. Specifically, the following objectives will be achieved
upon completion of this tutorial:

-Explanation and demonstration of when/how to conduct which statistical
tests depending on the data being used, along with how to interpret the
results of these tests.

-Understanding the structure of data, and determining if there is a
normal distribution of the data.

-How to effectively visualize data based on the dataset.

Before beginning the tutorial, it is necessary to load in the necessary
packages. These packages allow for the following functions to be done
within RStudio.

In order to achieve our objectives, we are going to import a built in
dataset within R called “esoph.” R has multiple datasets that can be
imported for investigation or practice coding. Our dataset includes
variables related to smoking, drinking, and esophageal cancer (which are
explained further below in the hypothesis testing section).

Below is the code used to load in the dataset, write it as a csv file
(to be saved separately), and then name the dataset (using the read.csv
function). Finally, the view function can be used to look into our data

``` r
#Reading in the built in dataset from R
(esoph)
```

    ##    agegp     alcgp    tobgp ncases ncontrols
    ## 1  25-34 0-39g/day 0-9g/day      0        40
    ## 2  25-34 0-39g/day    10-19      0        10
    ## 3  25-34 0-39g/day    20-29      0         6
    ## 4  25-34 0-39g/day      30+      0         5
    ## 5  25-34     40-79 0-9g/day      0        27
    ## 6  25-34     40-79    10-19      0         7
    ## 7  25-34     40-79    20-29      0         4
    ## 8  25-34     40-79      30+      0         7
    ## 9  25-34    80-119 0-9g/day      0         2
    ## 10 25-34    80-119    10-19      0         1
    ## 11 25-34    80-119      30+      0         2
    ## 12 25-34      120+ 0-9g/day      0         1
    ## 13 25-34      120+    10-19      1         0
    ## 14 25-34      120+    20-29      0         1
    ## 15 25-34      120+      30+      0         2
    ## 16 35-44 0-39g/day 0-9g/day      0        60
    ## 17 35-44 0-39g/day    10-19      1        13
    ## 18 35-44 0-39g/day    20-29      0         7
    ## 19 35-44 0-39g/day      30+      0         8
    ## 20 35-44     40-79 0-9g/day      0        35
    ## 21 35-44     40-79    10-19      3        20
    ## 22 35-44     40-79    20-29      1        13
    ## 23 35-44     40-79      30+      0         8
    ## 24 35-44    80-119 0-9g/day      0        11
    ## 25 35-44    80-119    10-19      0         6
    ## 26 35-44    80-119    20-29      0         2
    ## 27 35-44    80-119      30+      0         1
    ## 28 35-44      120+ 0-9g/day      2         1
    ## 29 35-44      120+    10-19      0         3
    ## 30 35-44      120+    20-29      2         2
    ## 31 45-54 0-39g/day 0-9g/day      1        45
    ## 32 45-54 0-39g/day    10-19      0        18
    ## 33 45-54 0-39g/day    20-29      0        10
    ## 34 45-54 0-39g/day      30+      0         4
    ## 35 45-54     40-79 0-9g/day      6        32
    ## 36 45-54     40-79    10-19      4        17
    ## 37 45-54     40-79    20-29      5        10
    ## 38 45-54     40-79      30+      5         2
    ## 39 45-54    80-119 0-9g/day      3        13
    ## 40 45-54    80-119    10-19      6         8
    ## 41 45-54    80-119    20-29      1         4
    ## 42 45-54    80-119      30+      2         2
    ## 43 45-54      120+ 0-9g/day      4         0
    ## 44 45-54      120+    10-19      3         1
    ## 45 45-54      120+    20-29      2         1
    ## 46 45-54      120+      30+      4         0
    ## 47 55-64 0-39g/day 0-9g/day      2        47
    ## 48 55-64 0-39g/day    10-19      3        19
    ## 49 55-64 0-39g/day    20-29      3         9
    ## 50 55-64 0-39g/day      30+      4         2
    ## 51 55-64     40-79 0-9g/day      9        31
    ## 52 55-64     40-79    10-19      6        15
    ## 53 55-64     40-79    20-29      4        13
    ## 54 55-64     40-79      30+      3         3
    ## 55 55-64    80-119 0-9g/day      9         9
    ## 56 55-64    80-119    10-19      8         7
    ## 57 55-64    80-119    20-29      3         3
    ## 58 55-64    80-119      30+      4         0
    ## 59 55-64      120+ 0-9g/day      5         5
    ## 60 55-64      120+    10-19      6         1
    ## 61 55-64      120+    20-29      2         1
    ## 62 55-64      120+      30+      5         1
    ## 63 65-74 0-39g/day 0-9g/day      5        43
    ## 64 65-74 0-39g/day    10-19      4        10
    ## 65 65-74 0-39g/day    20-29      2         5
    ## 66 65-74 0-39g/day      30+      0         2
    ## 67 65-74     40-79 0-9g/day     17        17
    ## 68 65-74     40-79    10-19      3         7
    ## 69 65-74     40-79    20-29      5         4
    ## 70 65-74    80-119 0-9g/day      6         7
    ## 71 65-74    80-119    10-19      4         8
    ## 72 65-74    80-119    20-29      2         1
    ## 73 65-74    80-119      30+      1         0
    ## 74 65-74      120+ 0-9g/day      3         1
    ## 75 65-74      120+    10-19      1         1
    ## 76 65-74      120+    20-29      1         0
    ## 77 65-74      120+      30+      1         0
    ## 78   75+ 0-39g/day 0-9g/day      1        17
    ## 79   75+ 0-39g/day    10-19      2         4
    ## 80   75+ 0-39g/day      30+      1         2
    ## 81   75+     40-79 0-9g/day      2         3
    ## 82   75+     40-79    10-19      1         2
    ## 83   75+     40-79    20-29      0         3
    ## 84   75+     40-79      30+      1         0
    ## 85   75+    80-119 0-9g/day      1         0
    ## 86   75+    80-119    10-19      1         0
    ## 87   75+      120+ 0-9g/day      2         0
    ## 88   75+      120+    10-19      1         0

``` r
#Writing a csv file, the use of "row.names= FALSE" just makes the data cleaner by not labeling the rows by number
write.csv(esoph, "Esoph.scancer.csv", row.names = FALSE)

#Reading the newly created csv file and giving the dataframe a name
Esoph_scancer <- read.csv("Esoph.scancer.csv")

#Viewing the Esoph_scancer file to see if there are any problems in the data
view(Esoph_scancer)
```

When viewing the dataset, we can see that some cells within the alcohol
per day column (alcgp) and the tobacco per day column (tobgp) include
“g/day.” This should be removed in order to make our data tidier and
more uniform. The following function “gsub” can be used to designate
what we’d like to replace (0-39g/day and 0-9g/day, respectively) and
what we’d like to replace it with (0-39 and 0-9, respectively).

``` r
#The first part of the following code is just designating the following: data_name$column_name. The backwards facing arrows denote that we are changing (using the gsub function) cells within that column in that data. And the part of the code within the parentheses of the gsub function are coding what to change within which columns in the data.
Esoph_scancer$alcgp <- gsub("0-39g/day", "0-39", Esoph_scancer$alcgp)
Esoph_scancer$tobgp <- gsub("0-9g/day", "0-9", Esoph_scancer$tobgp)

#Re-writing the csv file. This new csv will not include the "g/day" that the first csv included. 
write.csv(Esoph_scancer, "Esoph.scancer.csv", row.names = FALSE)

#Reading the new csv file (with the changed cells for uniformity)
Esoph_scancer <- read.csv("Esoph.scancer.csv")

#Viewing the new dataset
view(Esoph_scancer)
```

We can now see that our data is tidier and has been cleaned up for
uniformity. Next, we should convert the relevant variables to factors.
By using the “as.factor” function, this ‘tells’ R that these variables
should be treated as categories. For example, this makes it so that any
cell in the alcohol column that is “0-39” will be grouped together
during following analyses.

``` r
Esoph_scancer$agegp<- as.factor(Esoph_scancer$agegp)
Esoph_scancer$alcgp<- as.factor(Esoph_scancer$alcgp)
Esoph_scancer$tobgp<- as.factor(Esoph_scancer$tobgp)
```

Since we’ve cleaned up our data and converted the relevant variables to
factors, we can now proceed with hypothesis testing.

\###Creating a hypothesis: When creating a hypothesis, it is important
to not look at the results first as this could lead to “harking” or
formulating a “hypothesis after the results are known.” When first
looking at our dataset (“esoph” from the built-in R datasets, holds data
for the age of subjects, alcohol intake, tobacco intake, number of
esophageal cancer cases, and number of controls), we looked at the
variables without checking for normality of the data or graphing/testing
our results. There were three variables that stood out to us: alcohol
intake, tobacco intake, and number of esophageal cancer cases. This led
us to formulating the following hypothesis:

Groups that smoke or drink more may have a higher risk of developing
cancer. The number of cases may also increase with age.

Variables: Tobacco per day (g) - ordinal, categorical Alcohol per day
(g) - ordinal, categorical Age (grouped into ranges of age) - ordinal,
categorical Number of cases (numerical values that can be counted) -
discrete, quantitative

As a first look for comparisons, we can calculate the mean of each of
the groups individually to determine which groups had the highest
average number of cases.

Before explaining this code, it is necessary to explain what the symbol
“\|\>” does. This is called a “pipe” and it is simply a way of
connecting together multiple codes. It also helps to create a cleaner,
more readable code.

In the following code, “mean_age_group” is denoted as the name of the
result for the average cancer cases by age group. The backwards arrow
denotes that this is being created from the Esoph_scancer dataset, and
then the pipe function is used to connect this to the “group_by”
function which ‘tells’ R to only look at the “agegp” column in
association with the number of cancer cases. This is then again
connected to the “summarize” function which allows us to find the mean
number of cases in the group that was designated. The aspect of the code
that reads “na.rm = TRUE” ‘tells’ R not to include the cells that read
“N/A.” FInally, retyping the name “mean_age_group” just displays the
results of the average number of cancer cases below.

This exact process was followed for both “alcgp” and “agegp.” The only
difference was changing out the names.

``` r
mean_age_group <- Esoph_scancer |> 
  group_by(agegp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_age_group
```

    ## # A tibble: 6 × 2
    ##   agegp mean_value
    ##   <fct>      <dbl>
    ## 1 25-34     0.0667
    ## 2 35-44     0.6   
    ## 3 45-54     2.88  
    ## 4 55-64     4.75  
    ## 5 65-74     3.67  
    ## 6 75+       1.18

``` r
mean_alc_group <- Esoph_scancer |> 
  group_by(alcgp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_alc_group
```

    ## # A tibble: 4 × 2
    ##   alcgp  mean_value
    ##   <fct>       <dbl>
    ## 1 0-39         1.26
    ## 2 120+         2.14
    ## 3 40-79        3.26
    ## 4 80-119       2.43

``` r
mean_tob_group <- Esoph_scancer |> 
  group_by(tobgp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_tob_group
```

    ## # A tibble: 4 × 2
    ##   tobgp mean_value
    ##   <fct>      <dbl>
    ## 1 0-9         3.25
    ## 2 10-19       2.42
    ## 3 20-29       1.65
    ## 4 30+         1.55

Since the above code was all written in the same code chunk, the results
are displayed in multiple tables that can be selected and read
separately.

Another aspect of the beginning of hypothesis testing can be done by
ordering the number of cases just to see which groups had the highest
number of cases and which groups had the lowest number of cases. This
can be done by using the “arrange” function.

In the following code, “ranking” is denoted as the name of the ranked
data. Then the “arrange” function ‘tells’ R to sort the number of cancer
cases (ncases) by descending order (desc).

``` r
ranking <- Esoph_scancer |>
  arrange(desc(ncases), .by_group = TRUE) 
```

We can see the first and last five rows in the ordered dataset by using
the “head” and “tail” functions with the previously made “ranking.” The
aspect of the function that reads “n = 5” ‘tells’ R to only include the
first and last five rows.

``` r
head(ranking, n = 5)
```

    ##   agegp  alcgp tobgp ncases ncontrols
    ## 1 65-74  40-79   0-9     17        17
    ## 2 55-64  40-79   0-9      9        31
    ## 3 55-64 80-119   0-9      9         9
    ## 4 55-64 80-119 10-19      8         7
    ## 5 45-54  40-79   0-9      6        32

``` r
tail(ranking, n = 5)
```

    ##    agegp alcgp tobgp ncases ncontrols
    ## 84 45-54  0-39 10-19      0        18
    ## 85 45-54  0-39 20-29      0        10
    ## 86 45-54  0-39   30+      0         4
    ## 87 65-74  0-39   30+      0         2
    ## 88   75+ 40-79 20-29      0         3

The above functions and results give us a first look into each variable
or group separately, however, this doesn’t take into account all of the
factors together, so the results of this would not be reliable enough to
make any conclusions.

\###Creating a linear model:

Creating a linear model is valuable for analyzing this data because it
allows us to look into each of the explanatory variables separately and
at each of the variables’ interactions with the others.

This is a relatively complicated code, so it can be broken down into the
following:

“name_of_linear_model” \<- lm(response_variable ~ explanatory_variable
\* (explanatory_variable + explanatory_variable),
data=“name_of_dataframe”)

The symbol “~” defines the formula the linear model is calculated from
to determine their impacts on the response variable (number of cancer
cases). Then, the “\*” symbol after “agegp” showing multiplication by
both “alcgp” and “tobgp” allows for the following: the significance
(shown by p-value) on the impact of each of the variables separately on
the number of cancer cases, along with interactions of the variables on
the number of cancer cases (age by alcohol intake and age by tobacco
intake).

``` r
lm1<-lm(ncases ~ agegp * (alcgp + tobgp), data=Esoph_scancer) 
summary(lm1)
```

    ## 
    ## Call:
    ## lm(formula = ncases ~ agegp * (alcgp + tobgp), data = Esoph_scancer)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -3.9167 -0.5937  0.0278  0.4375  5.3333 
    ## 
    ## Coefficients:
    ##                          Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)            -5.556e-02  1.083e+00  -0.051  0.95932    
    ## agegp35-44              1.944e-01  1.532e+00   0.127  0.89956    
    ## agegp45-54              9.306e-01  1.526e+00   0.610  0.54500    
    ## agegp55-64              4.556e+00  1.526e+00   2.985  0.00453 ** 
    ## agegp65-74              6.750e+00  1.532e+00   4.406 6.25e-05 ***
    ## agegp75+                1.681e+00  1.614e+00   1.041  0.30309    
    ## alcgp120+               2.500e-01  1.149e+00   0.218  0.82872    
    ## alcgp40-79              9.216e-15  1.149e+00   0.000  1.00000    
    ## alcgp80-119            -2.778e-02  1.270e+00  -0.022  0.98265    
    ## tobgp10-19              2.500e-01  1.149e+00   0.218  0.82872    
    ## tobgp20-29             -2.778e-02  1.270e+00  -0.022  0.98265    
    ## tobgp30+               -7.542e-15  1.149e+00   0.000  1.00000    
    ## agegp35-44:alcgp120+    6.944e-01  1.713e+00   0.405  0.68704    
    ## agegp45-54:alcgp120+    2.750e+00  1.625e+00   1.692  0.09734 .  
    ## agegp55-64:alcgp120+    1.250e+00  1.625e+00   0.769  0.44567    
    ## agegp65-74:alcgp120+   -1.500e+00  1.625e+00  -0.923  0.36076    
    ## agegp75+:alcgp120+     -2.500e-01  1.934e+00  -0.129  0.89771    
    ## agegp35-44:alcgp40-79   7.500e-01  1.625e+00   0.462  0.64657    
    ## agegp45-54:alcgp40-79   4.750e+00  1.625e+00   2.923  0.00536 ** 
    ## agegp55-64:alcgp40-79   2.500e+00  1.625e+00   1.539  0.13077    
    ## agegp65-74:alcgp40-79   4.972e+00  1.713e+00   2.903  0.00566 ** 
    ## agegp75+:alcgp40-79    -8.499e-15  1.755e+00   0.000  1.00000    
    ## agegp35-44:alcgp80-119 -2.222e-01  1.713e+00  -0.130  0.89734    
    ## agegp45-54:alcgp80-119  2.778e+00  1.713e+00   1.622  0.11169    
    ## agegp55-64:alcgp80-119  3.028e+00  1.713e+00   1.768  0.08374 .  
    ## agegp65-74:alcgp80-119  5.278e-01  1.713e+00   0.308  0.75937    
    ## agegp75+:alcgp80-119   -4.722e-01  2.008e+00  -0.235  0.81516    
    ## agegp35-44:tobgp10-19   2.500e-01  1.625e+00   0.154  0.87840    
    ## agegp45-54:tobgp10-19  -5.000e-01  1.625e+00  -0.308  0.75970    
    ## agegp55-64:tobgp10-19  -7.500e-01  1.625e+00  -0.462  0.64657    
    ## agegp65-74:tobgp10-19  -5.000e+00  1.625e+00  -3.077  0.00352 ** 
    ## agegp75+:tobgp10-19    -5.000e-01  1.625e+00  -0.308  0.75970    
    ## agegp35-44:tobgp20-29   2.778e-01  1.713e+00   0.162  0.87188    
    ## agegp45-54:tobgp20-29  -1.472e+00  1.713e+00  -0.860  0.39451    
    ## agegp55-64:tobgp20-29  -3.222e+00  1.713e+00  -1.881  0.06628 .  
    ## agegp65-74:tobgp20-29  -5.222e+00  1.713e+00  -3.049  0.00380 ** 
    ## agegp75+:tobgp20-29    -1.597e+00  2.384e+00  -0.670  0.50625    
    ## agegp35-44:tobgp30+    -3.056e-01  1.713e+00  -0.178  0.85920    
    ## agegp45-54:tobgp30+    -7.500e-01  1.625e+00  -0.462  0.64657    
    ## agegp55-64:tobgp30+    -2.250e+00  1.625e+00  -1.385  0.17283    
    ## agegp65-74:tobgp30+    -5.778e+00  1.713e+00  -3.373  0.00152 ** 
    ## agegp75+:tobgp30+      -6.250e-01  1.905e+00  -0.328  0.74439    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1.625 on 46 degrees of freedom
    ## Multiple R-squared:  0.8158, Adjusted R-squared:  0.6517 
    ## F-statistic:  4.97 on 41 and 46 DF,  p-value: 1.908e-07

While the results of this yield many p-values, the overall p-value for
this linear model is extremely small. Smaller p-values indicate that the
relationship between variables is statistically significant, and
therefore this shows that there is a significant relationship between
each of the variables and the interactions on the number of cases.

\###Assumptions of linear models

In order to use a linear model, there are a few assumptions that must be
followed relating to the residuals. These include the following: 1)
Independence of data points 2) Normally distributed residuals 3)
Homoscedastic data

The following test (the Durbin-Watson test) can be used to determine
autocorrelation (independence of data points). This is important because
it ensures that there are no other statistical impacts that may be
impacting the results. The null hypothesis for this test is that there
IS a positive correlation in the residuals, so a high p-value is wanted
as this would reject this (and therefore show that there is independence
of the data points).

The test can be done simply by using the function “dwtest” and applying
this to the linear model we made above.

``` r
dwtest(lm1)
```

    ## 
    ##  Durbin-Watson test
    ## 
    ## data:  lm1
    ## DW = 2.5508, p-value = 0.6399
    ## alternative hypothesis: true autocorrelation is greater than 0

The results of this show a high p-value of 0.6399, and this means that
we fail to reject the null hypothesis (which was that there is positive
autocorrelation in the residuals). The Durbin-Watson statistic is also
close enough to the ideal value of 2. Due to these results, we can
conclude that the data points are independent enough to proceed with a
linear model.

Creating a histogram can be done to determine if the residuals are
normally distributed. A histogram can be created using the “hist”
function. A further broken down code is as follows:

hist(“name_of_linear_model”\$“residuals”, main = “title” xlab = “name of
x-axis”, col = “color of histogram bins” border = “color of bin border”)

``` r
hist(lm1$residuals, 
     main = "Histogram of Residuals for Linear Model",  
     xlab = "Residuals", 
     col = "gray", 
     border = "black")
```

![](instructions_files/figure-gfm/-%20histogram%20residuals-1.png)<!-- -->
This histogram shows that the residuals are normally distributed enough
for creating linear models.

A homoscedastic spread is when the variability of the residuals is
constant, showing that the errors are consistent regardless of the
explanatory variables. We can determine homoscedasticity by plotting the
linear model; this can be done by simply applying the “plot” function to
the linear model we created. We can then assess the qqplot created to
check for homoscedasticity. If the majority of the points lie along the
line on this plot, we can assume that the residuals are consistent.

``` r
plot(lm1)
```

    ## Warning: not plotting observations with leverage one:
    ##   83

![](instructions_files/figure-gfm/-%20plot-1.png)<!-- -->![](instructions_files/figure-gfm/-%20plot-2.png)<!-- -->![](instructions_files/figure-gfm/-%20plot-3.png)<!-- -->![](instructions_files/figure-gfm/-%20plot-4.png)<!-- -->
The qqplot is the second plot created in our results. Since the points
mainly lie along the line of the qqplot, this tells us that it is
homoscedastic. Due to all of the assumptions being met, we can consider
a linear model an effective analysis.

An anova test can be conducted on the linear model to determine the
statistical significance of each group. Anova tests are effective in
assessing if there are statistically significant differences in the
means between three or more groups. Since our linear model has five
groups, this is an effective test for comparing the mean number of
cancer cases between each of these groups.

``` r
anova(lm1)
```

    ## Analysis of Variance Table
    ## 
    ## Response: ncases
    ##             Df  Sum Sq Mean Sq F value    Pr(>F)    
    ## agegp        5 261.202  52.240 19.7850 1.796e-10 ***
    ## alcgp        3  52.695  17.565  6.6524 0.0007955 ***
    ## tobgp        3  54.706  18.235  6.9063 0.0006179 ***
    ## agegp:alcgp 15 100.158   6.677  2.5289 0.0080789 ** 
    ## agegp:tobgp 15  69.235   4.616  1.7481 0.0742146 .  
    ## Residuals   46 121.458   2.640                      
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

This anova tests yields many results as it shows the significance of
each group. It shows that the results are significant (less than 0.05)
for all of the groups except for age group correlated with tobacco
group.

\###Testing for normality of the data

``` r
library(ggplot2)
library(cowplot)
a <- ggplot(Esoph_scancer, aes(x=tobgp)) + geom_bar() + ggtitle("Tobacco Group")
b <- ggplot(Esoph_scancer, aes(x=alcgp)) + geom_bar() + ggtitle("Alcohol Group")
c <- ggplot(Esoph_scancer, aes(x=agegp)) + geom_bar() + ggtitle("Age Group")

# Display the plots in a grid
plot_grid(a, b, c, ncol = 2)
```

![](instructions_files/figure-gfm/-%20testing%20for%20normality%20in%20the%20data-1.png)<!-- -->

This R code is using ggplot2 library for data visualization. It creates
bar and density plots for both discrete and continuous variables from
the dataset we picked, “ Esoph_scancer”.

Before running this code, make sure the ggplot2 library is loaded. You
can do this with: library(ggplot2)

The first part of the code creates two bar plots for the discrete
variables tobgp and alcgp aes(x=tobgp) and aes(x=alcgp) specify the
aesthetics for the x-axis, mapping to the categorical variables tobgp
and alcgp. geom_bar() tells ggplot2 to create bar plots, which count the
frequency of each category. ggtitle() adds a title to each plot.
Esoph_scancer is the dataset, and tobgp is the discrete variable
(Tobacco Group). geom_bar() generates a bar plot based on the count of
each tobgp category. ggtitle() adds the title “Tobacco Group - Bar
Plot”. alcgp is the discrete variable (Alcohol Group) plotted on the
x-axis. A density plot visualizes the distrubution of a continous
variables. aes(x=ncases) maps ncases (continuous variable) to the
x-axis. geom_density() creates a smooth curve representing the
distribution of ncases. This plot shows the density distribution of the
ncases variable directly

This plot shows the distribution of ncases after applying a logarithmic
transformation (log(ncases): usually done to make highly skewed data
more normal or easier to interpret

The plot_grid() function arranges the four plots (two bar plots and two
density plots) in a 2x2 grid layout ncol = 2 specifies 2 columns, and
nrow = 2 specifies 2 rows. This creates a 2x2 grid of the plots. All
four plots are arranged in a 2x2 grid for easy comparison.

\#Making a histogram of the orginal and log transformed data and making
density plots of them

``` r
# Create bar plots for discrete variables
a <- ggplot(Esoph_scancer, aes(x=tobgp)) + geom_bar() + ggtitle("Tobacco Group - Bar Plot")
b <- ggplot(Esoph_scancer, aes(x=alcgp)) + geom_bar() + ggtitle("Alcohol Group - Bar Plot")

# Create density plots using continuous data (if needed)
# Assuming there is a continuous variable, for example, ncases
# If not, density plots may not be applicable to this dataset

# For demonstration, let's assume a continuous variable ncases exists
c <- ggplot(Esoph_scancer, aes(x=ncases)) + geom_density() + ggtitle("Density Plot - ncases")
d <- ggplot(Esoph_scancer, aes(x=log(ncases))) + geom_density() + ggtitle("Density Plot - log(ncases)")

# Plot in a 2x2 grid
plot_grid(a, b, c, d, ncol = 2, nrow = 2)
```

    ## Warning: Removed 29 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](instructions_files/figure-gfm/-%20graphing-1.png)<!-- -->

\###Data Visualization Data visualization is another important aspect of
data analysis because it allows you to simplify the data in a way that
is easily digestible but still keep the importance of the findings.
Another important reason to visualize the data is that most times, you
will be presenting your findings to other people. There’s also a good
chance that your audience isn’t as familiar with looking at data like
you are so visuals are the best way to showcase your work.

Depending on the type of variables you are using, the kind of plot you
will want to use will be different. For example, if you are comparing a
quantitative variable with a categorical one, the type of visuals you
will wabt to use includes bar charts, boxplots, or pie charts. If you
are comparing a quantitative variable to another quantitative variable,
the type of graphs you will want to use includes a scatterplot or a line
graph. Finally, in rare cases(such as this one) comparing two
categorical variables you will want use a mosaic plot.

Our data set only uses categorical variables so we will be using a
mosaic plot along with some bar charts we used above.

``` r
require(stats)
require(graphics) # for mosaicplot
summary(esoph)
```

    ##    agegp          alcgp         tobgp        ncases         ncontrols     
    ##  25-34:15   0-39g/day:23   0-9g/day:24   Min.   : 0.000   Min.   : 0.000  
    ##  35-44:15   40-79    :23   10-19   :24   1st Qu.: 0.000   1st Qu.: 1.000  
    ##  45-54:16   80-119   :21   20-29   :20   Median : 1.000   Median : 4.000  
    ##  55-64:16   120+     :21   30+     :20   Mean   : 2.273   Mean   : 8.807  
    ##  65-74:15                                3rd Qu.: 4.000   3rd Qu.:10.000  
    ##  75+  :11                                Max.   :17.000   Max.   :60.000

``` r
## effects of alcohol, tobacco and interaction, age-adjusted
model1 <- glm(cbind(ncases, ncontrols) ~ agegp + tobgp * alcgp,
              data = esoph, family = binomial())
anova(model1)
```

    ## Analysis of Deviance Table
    ## 
    ## Model: binomial, link: logit
    ## 
    ## Response: cbind(ncases, ncontrols)
    ## 
    ## Terms added sequentially (first to last)
    ## 
    ## 
    ##             Df Deviance Resid. Df Resid. Dev  Pr(>Chi)    
    ## NULL                           87     367.95              
    ## agegp        5  121.045        82     246.91 < 2.2e-16 ***
    ## tobgp        3   36.639        79     210.27 5.485e-08 ***
    ## alcgp        3  127.933        76      82.34 < 2.2e-16 ***
    ## tobgp:alcgp  9    5.451        67      76.89    0.7934    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

``` r
## Try a linear effect of alcohol and tobacco
model2 <- glm(cbind(ncases, ncontrols) ~ agegp + unclass(tobgp)
                                         + unclass(alcgp),
              data = esoph, family = binomial())
summary(model2)
```

    ## 
    ## Call:
    ## glm(formula = cbind(ncases, ncontrols) ~ agegp + unclass(tobgp) + 
    ##     unclass(alcgp), family = binomial(), data = esoph)
    ## 
    ## Coefficients:
    ##                Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)    -4.92067    0.37344 -13.177  < 2e-16 ***
    ## agegp.L         3.81892    0.67862   5.627 1.83e-08 ***
    ## agegp.Q        -1.49473    0.60671  -2.464   0.0138 *  
    ## agegp.C         0.07923    0.46318   0.171   0.8642    
    ## agegp^4         0.12136    0.32203   0.377   0.7063    
    ## agegp^5        -0.24856    0.21153  -1.175   0.2400    
    ## unclass(tobgp)  0.43955    0.09623   4.568 4.93e-06 ***
    ## unclass(alcgp)  1.06766    0.10493  10.175  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 367.953  on 87  degrees of freedom
    ## Residual deviance:  91.121  on 80  degrees of freedom
    ## AIC: 222.18
    ## 
    ## Number of Fisher Scoring iterations: 6

``` r
## Re-arrange data for a mosaic plot
ttt <- table(esoph$agegp, esoph$alcgp, esoph$tobgp)
#Creates a table from our dataset esoph and counts the number of occurrences for each combination of age group, alcohol consumption group, and tobacco consumption group.
o <- with(esoph, order(tobgp, alcgp, agegp))
#This creates an ordered index based on the values of each group. The order() function returns the indices of the elements sorted by the values of the specified columns
ttt[ttt == 1] <- esoph$ncases[o]
#This line replaces all the 1s in the table with the corresponding values of ncases
tt1 <- table(esoph$agegp, esoph$alcgp, esoph$tobgp)
#A new table is created
tt1[tt1 == 1] <- esoph$ncontrols[o]
#This line replaces all the 1s in the table table with the corresponding values of ncontrols
tt <- array(c(ttt, tt1), c(dim(ttt),2),
            c(dimnames(ttt), list(c("Cancer", "control"))))
#An array is created by combining ttt (cancer cases) and tt1 (controls) into a 3D array.
mosaicplot(tt, main = "esoph data set", color = TRUE)
```

![](instructions_files/figure-gfm/-%20Data%20Visualization-1.png)<!-- -->

``` r
#This generates a mosaic plot based on the 3D array tt, displaying the relationships between age group, alcohol consumption, tobacco consumption, and cancer/control status.
```

By making a mosaic plot we can see that there are more cancer cases in
older age groups that consume bother tobacco and alcohol compared to the
lower age group and the groups that consume either a very low amount of
each substance or none at all. The ANOVA test we performed alongside it
also tell us the signnificance of each of our groups.

Thank you for following along with the tutorial! We hope this provides
you a batter understanding of how to use R to perform your data
analysis.
