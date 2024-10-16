# Project_1 R Tutorial

## Authors

Shihab K. Nihan
Beth Williams
Amma Boamah-Appiah

## Target Audience

Our target audience includes the following: Students in BIOL 204 (or any beginner R class at Bucknell), beginner researchers, and anyone with an interest in data analysis.

## Instructions

Hi, we hope you're ready to get a bit of an introduction for how to use RStudio! In this tutorial, beginner researchers, students at Bucknell University in any beginner R class, and anyone with an interest in data analysis will learn how to conceptualize what specific codes mean and how they are useful for hypothesis testing, data exploration, and data visualization. Specifically, the following objectives will be achieved upon completion of this tutorial:

-Explanation and demonstration of when/how to conduct which statistical tests depending on the data being used, along with how to interpret the results of these tests. 

-Understanding the structure of data, and determining if there is a normal distribution of the data.

-How to effectively visualize data based on the dataset.

Before beginning the tutorial, it is necessary to load in the necessary packages. These packages allow for the following functions to be done within RStudio.

```{r Load Libraries, include=FALSE}
# Load other packages here.
if (!require("tidyverse")) install.packages("tidyverse"); library(tidyverse)
if (!require("MASS")) install.packages("MASS"); library(MASS)
if (!require("cowplot")) install.packages("cowplot"); library(cowplot)
if (!require("multcomp")) install.packages("multcomp"); library(multcomp) # for more accurate p
if (!require("emmeans")) install.packages("emmeans"); library(emmeans) # for more accurate p
if (!require("conflicted")) install.packages("conflicted"); library(conflicted) # For dealing with conflicts
conflict_prefer_all("dplyr", quiet = TRUE)
if (!require(lmtest)) install.packages("lmtest"); library(lmtest)
```

In order to achieve our objectives, we are going to import a built in dataset within R called "esoph." R has multiple datasets that can be imported for investigation or practice coding. Our dataset includes variables related to smoking, drinking, and esophageal cancer (which are explained further below in the hypothesis testing section).

Below is the code used to load in the dataset, write it as a csv file (to be saved separately), and then name the dataset (using the read.csv function). Finally, the view function can be used to look into our data 

```{r - X}
#Reading in the built in dataset from R
(esoph)

#Writing a csv file, the use of "row.names= FALSE" just makes the data cleaner by not labeling the rows by number
write.csv(esoph, "Esoph.scancer.csv", row.names = FALSE)

#Reading the newly created csv file and giving the dataframe a name
Esoph_scancer <- read.csv("Esoph.scancer.csv")

#Viewing the Esoph_scancer file to see if there are any problems in the data
view(Esoph_scancer)
```
*Here, a table will be created showing the data.

When viewing the dataset, we can see that some cells within the alcohol per day column (alcgp) and the tobacco per day column (tobgp) include "g/day." This should be removed in order to make our data tidier and more uniform. The following function "gsub" can be used to designate what we'd like to replace (0-39g/day and 0-9g/day, respectively) and what we'd like to replace it with (0-39 and 0-9, respectively). 

```{r - gsub function}
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

We can now see that our data is tidier and has been cleaned up for uniformity. Next, we should convert the relevant variables to factors. By using the "as.factor" function, this 'tells' R that these variables should be treated as categories. For example, this makes it so that any cell in the alcohol column that is "0-39" will be grouped together during following analyses.

```{r - converting to factors}

Esoph_scancer$agegp<- as.factor(Esoph_scancer$agegp)
Esoph_scancer$alcgp<- as.factor(Esoph_scancer$alcgp)
Esoph_scancer$tobgp<- as.factor(Esoph_scancer$tobgp)
```

Since we've cleaned up our data and converted the relevant variables to factors, we can now proceed with hypothesis testing.

###Creating a hypothesis:
When creating a hypothesis, it is important to not look at the results first as this could lead to “harking” or formulating a “hypothesis after the results are known.” When first looking at our dataset (“esoph” from the built-in R datasets, holds data for the age of subjects, alcohol intake, tobacco intake, number of esophageal cancer cases, and number of controls), we looked at the variables without checking for normality of the data or graphing/testing our results. There were three variables that stood out to us: alcohol intake, tobacco intake, and number of esophageal cancer cases. This led us to formulating the following hypothesis:

Groups that smoke or drink more may have a higher risk of developing cancer. The number of cases may also increase with age. 

Variables:
Tobacco per day (g) - ordinal, categorical
Alcohol per day (g) - ordinal, categorical
Age (grouped into ranges of age) - ordinal, categorical
Number of cases (numerical values that can be counted) - discrete, quantitative

As a first look for comparisons, we can calculate the mean of each of the groups individually to determine which groups had the highest average number of cases. 

Before explaining this code, it is necessary to explain what the symbol  "|>" does. This is called a "pipe" and it is simply a way of connecting together multiple codes. It also helps to create a cleaner, more readable code.

In the following code, "mean_age_group" is denoted as the name of the result for the average cancer cases by age group. The backwards arrow denotes that this is being created from the Esoph_scancer dataset, and then the pipe function is used to connect this to the "group_by" function which 'tells' R to only look at the "agegp" column in association with the number of cancer cases. This is then again connected to the "summarize" function which allows us to find the mean number of cases in the group that was designated. The aspect of the code that reads "na.rm = TRUE" 'tells' R not to include the cells that read "N/A." FInally, retyping the name "mean_age_group" just displays the results of the average number of cancer cases below.

This exact process was followed for both "alcgp" and "agegp." The only difference was changing out the names.

```{r - Finding the mean number of cases for each individual group without looking into other variables}
mean_age_group <- Esoph_scancer |> 
  group_by(agegp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_age_group

mean_alc_group <- Esoph_scancer |> 
  group_by(alcgp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_alc_group

mean_tob_group <- Esoph_scancer |> 
  group_by(tobgp) |> 
  summarize(mean_value = mean(ncases, na.rm = TRUE))
mean_tob_group

```
*Here, a table will apear displaying the mean number of cases for each group.

Since the above code was all written in the same code chunk, the results are displayed in multiple tables that can be selected and read separately.

Another aspect of the beginning of hypothesis testing can be done by ordering the number of cases just to see which groups had the highest number of cases and which groups had the lowest number of cases. This can be done by using the "arrange" function. 

In the following code, "ranking" is denoted as the name of the ranked data. Then the "arrange" function 'tells' R to sort the number of cancer cases (ncases) by descending order (desc). 

```{r - ranking}
ranking <- Esoph_scancer |>
  arrange(desc(ncases), .by_group = TRUE) 
```

We can see the first and last five rows in the ordered dataset by using the "head" and "tail" functions with the previously made "ranking." The aspect of the function that reads "n = 5" 'tells' R to only include the first and last five rows. 
```{r - ranking 2}
head(ranking, n = 5)
tail(ranking, n = 5)
```

*Here, two tables will appear showing the first and last five groups according to most cases and least cases, respectively.

The above functions and results give us a first look into each variable or group separately, however, this doesn’t take into account all of the factors together, so the results of this would not be reliable enough to make any conclusions. 

###Creating a linear model:

Creating a linear model is valuable for analyzing this data because it allows us to look into each of the explanatory variables separately and at each of the variables' interactions with the others. 

This is a relatively complicated code, so it can be broken down into the following:

"name_of_linear_model" <- lm(response_variable ~ explanatory_variable * (explanatory_variable + explanatory_variable), data="name_of_dataframe")

The symbol "~" defines the formula the linear model is calculated from to determine their impacts on the response variable (number of cancer cases). Then, the "*" symbol after "agegp" showing multiplication by both "alcgp" and "tobgp" allows for the following: the significance (shown by p-value) on the impact of each of the variables separately on the number of cancer cases, along with interactions of the variables on the number of cancer cases (age by alcohol intake and age by tobacco intake).

```{r - linear model}
lm1<-lm(ncases ~ agegp * (alcgp + tobgp), data=Esoph_scancer) 
summary(lm1)
```

*Here, the results of the linear model will be shown.

While the results of this yield many p-values, the overall p-value for this linear model is extremely small. Smaller p-values indicate that the relationship between variables is statistically significant, and therefore this shows that there is a significant relationship between each of the variables and the interactions on the number of cases. 

###Assumptions of linear models

In order to use a linear model, there are a few assumptions that must be followed relating to the residuals. These include the following:
1) Independence of data points
2) Normally distributed residuals
3) Homoscedastic data

The following test (the Durbin-Watson test) can be used to determine autocorrelation (independence of data points). This is important because it ensures that there are no other statistical impacts that may be impacting the results. The null hypothesis for this test is that there IS a positive correlation in the residuals, so a high p-value is wanted as this would reject this (and therefore show that there is independence of the data points).

The test can be done simply by using the function "dwtest" and applying this to the linear model we made above. 

```{r - dwtest}
dwtest(lm1)
```

*Here, the results of the Durbin Watson test will be shown.

The results of this show a high p-value of 0.6399, and this means that we fail to reject the null hypothesis (which was that there is positive autocorrelation in the residuals). The Durbin-Watson statistic is also close enough to the ideal value of 2. Due to these results, we can conclude that the data points are independent enough to proceed with a linear model. 

Creating a histogram can be done to determine if the residuals are normally distributed. A histogram can be created using the "hist" function. A further broken down code is as follows:

hist("name_of_linear_model"$"residuals",
        main = "title"
        xlab = "name of x-axis", 
        col = "color of histogram bins"
        border = "color of bin border")

```{r - histogram residuals}
hist(lm1$residuals, 
     main = "Histogram of Residuals for Linear Model",  
     xlab = "Residuals", 
     col = "gray", 
     border = "black")
```

*Here, the histogram of residuals will be shown.

This histogram shows that the residuals are normally distributed enough for creating linear models.

A homoscedastic spread is when the variability of the residuals is constant, showing that the errors are consistent regardless of the explanatory variables. We can determine homoscedasticity by plotting the linear model; this can be done by simply applying the "plot" function to the linear model we created. We can then assess the qqplot created to check for homoscedasticity. If the majority of the points lie along the line on this plot, we can assume that the residuals are consistent.

```{r - plot}
plot(lm1)
```

*Here, the plots of residuals will be shown (most importantly the qqplot).

The qqplot is the second plot created in our results. Since the points mainly lie along the line of the qqplot, this tells us that it is homoscedastic. Due to all of the assumptions being met, we can consider a linear model an effective analysis. 

An anova test can be conducted on the linear model to determine the statistical significance of each group. Anova tests are effective in assessing if there are statistically significant differences in the means between three or more groups. Since our linear model has five groups, this is an effective test for comparing the mean number of cancer cases between each of these groups. 
```{r - anova}
anova(lm1)
```

*Here, the results of the anova test will be shown.

###Testing for normality of the data

```{r - testing for normality in the data}
library(ggplot2)
library(cowplot)
a <- ggplot(Esoph_scancer, aes(x=tobgp)) + geom_bar() + ggtitle("Tobacco Group")
b <- ggplot(Esoph_scancer, aes(x=alcgp)) + geom_bar() + ggtitle("Alcohol Group")
c <- ggplot(Esoph_scancer, aes(x=agegp)) + geom_bar() + ggtitle("Age Group")

# Display the plots in a grid
plot_grid(a, b, c, ncol = 2)
```

*Here, the bar plots will be shown in grid format. 

This R code is using ggplot2 library for data visualization. It creates bar and density plots for both discrete and continuous variables from the dataset we picked, “ Esoph_scancer”.

Before running this code, make sure the ggplot2 library is loaded. You can do this with: library(ggplot2)

The first part of the code creates two bar plots for the discrete variables tobgp and alcgp 
aes(x=tobgp) and aes(x=alcgp) specify the aesthetics for the x-axis, mapping to the categorical variables tobgp and alcgp.
geom_bar() tells ggplot2 to create bar plots, which count the frequency of each category.
ggtitle() adds a title to each plot.
Esoph_scancer is the dataset, and tobgp is the discrete variable (Tobacco Group).
geom_bar() generates a bar plot based on the count of each tobgp category.
ggtitle() adds the title "Tobacco Group - Bar Plot".
alcgp is the discrete variable (Alcohol Group) plotted on the x-axis.
 A density plot visualizes the distrubution of a continous variables.
aes(x=ncases) maps ncases (continuous variable) to the x-axis.
geom_density() creates a smooth curve representing the distribution of ncases.
This plot shows the density distribution of the ncases variable directly

This plot shows the distribution of ncases after applying a logarithmic transformation (log(ncases): usually done to make highly skewed data more normal or easier to interpret 

The plot_grid() function arranges the four plots (two bar plots and two density plots) in a 2x2 grid layout
ncol = 2 specifies 2 columns, and nrow = 2 specifies 2 rows. This creates a 2x2 grid of the plots.
All four plots are arranged in a 2x2 grid for easy comparison.


#Making a histogram of the orginal and log transformed data and making density plots of them
```{r - graphing}
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

*Here, both bar plots and density plots will be shown.

###Data Visualization
Data visualization is another important aspect of data analysis because it allows you to simplify the data in a way that is easily digestible but still keep the importance of the findings. Another important reason to visualize the data is that most times, you will be presenting your findings to other people. There's also a good chance that your audience isn't as familiar with looking at data like you are so visuals are the best way to showcase your work.

Depending on the type of variables you are using, the kind of plot you will want to use will be different. For example, if you are comparing a quantitative variable with a categorical one, the type of visuals you will wabt to use includes bar charts, boxplots, or pie charts. If you are comparing a quantitative variable to another quantitative variable, the type of graphs you will want to use includes a scatterplot or a line graph. Finally, in rare cases(such as this one) comparing two categorical variables you will want use a mosaic plot.

Our data set only uses categorical variables so we will be using a mosaic plot along with some bar charts we used above.

```{r - Data Visualization}
require(stats)
require(graphics) # for mosaicplot
summary(esoph)
## effects of alcohol, tobacco and interaction, age-adjusted
model1 <- glm(cbind(ncases, ncontrols) ~ agegp + tobgp * alcgp,
              data = esoph, family = binomial())
anova(model1)
## Try a linear effect of alcohol and tobacco
model2 <- glm(cbind(ncases, ncontrols) ~ agegp + unclass(tobgp)
                                         + unclass(alcgp),
              data = esoph, family = binomial())
summary(model2)
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
#This generates a mosaic plot based on the 3D array tt, displaying the relationships between age group, alcohol consumption, tobacco consumption, and cancer/control status.
```
*Here, the mosaic plot will be shown.

By making a mosaic plot we can see that there are more cancer cases in older age groups that consume bother tobacco and alcohol compared to the lower age group and the groups that consume either a very low amount of each substance or none at all. The ANOVA test we performed alongside it also tell us the signnificance of each of our groups.

Thank you for following along with the tutorial! We hope this provides you a batter understanding of how to use R to perform your data analysis.

## Objectives

General objectives as included in the instructions:

-Explanation and demonstration of when/how to conduct which statistical tests depending on the data being used, along with how to interpret the results of these tests. 

-Understanding the structure of data, and determining if there is a normal distribution of the data.

-How to effectively visualize data based on the dataset.

Specific objectives to our group:

One of our overarching objectives is to conceptualize what specific codes mean and how they are useful for data exploration, data visualization, and hypothesis testing. Our second objective is to explain what graphs and what specific statistical tests should be used for particular data. 

Specifically, Amma is going to be working with data exploration. She is going to explain and demonstrate how to understand the structure of data, and test for normal distribution.

Shihab is going to be explaining the section about data visualization. He is going to explain and demonstrate how to know which graphs to use based on the types of variables within the dataset.

Beth is going to focus on hypothesis testing. She is going to explain and demonstrate when to use which statistical tests depending on the data. She is also going to show how to conduct these tests and interpret them, and how linear models can be utilized during hypothesis testing. 