Lesson 3: Data frames and tibbles
================

``` r
if (!require(tidyverse)) {install.packages('tidyverse')}
library(tidyverse)
```

Data frame
==========

To create a data frame, use the function `data.frame`:

``` r
#data from https://www.statista.com/statistics/804398/us-iphone-sales-by-model/
iphoneSales <- data.frame(
                  time = c("Sep 2014", "Sep 2015", "Sep 2016", "Dec 2016", "Sep 2017", "Dec 2017", "Jun 2018"), 
                  iPhone4S = c(9, NA, NA, NA, NA, NA, NA), 
                  iPhone5C = c(15.5, 5, NA, NA, NA, NA, NA), 
                  iPhone5S = c(30, 19, NA, NA, NA, NA, NA), 
                  iPhoneSE = c(NA, NA, 9.5, 6, 11, 7, 8), 
                  iPhone6 = c(33, 33, 5, NA, NA, NA, NA), 
                  iPhone6Plus = c(12.5, 19, 7, NA, NA, NA, NA), 
                  iPhone6S = c(NA, 16, 19, 11, 10, 6, 8), 
                  iPhone6SPlus = c(NA, 8, 12.5, 10, 4.5, 2, 3), 
                  iPhone7 = c(NA, NA, 31, 40, 28.5, 13, 16), 
                  iPhone7Plus = c(NA, NA, 16, 32.1, 29.5, 11, 11), 
                  iPhone8 = c(NA, NA, NA, NA, 6, 24, 13), 
                  iPhone8Plus = c(NA, NA, NA, NA, 10.5, 17, 24), 
                  iPhoneX = c(NA, NA, NA, NA, NA, 20.1, 17))
#note how "time" becomes a factor-- more details at http://r4ds.had.co.nz/factors.html#creating-factors
```

Dataframes are a special case of a list, where each element is a vector of the same length but possibly different type. For instance:

``` r
str(iphoneSales)
## 'data.frame':    7 obs. of  14 variables:
##  $ time        : Factor w/ 7 levels "Dec 2016","Dec 2017",..: 4 5 6 1 7 2 3
##  $ iPhone4S    : num  9 NA NA NA NA NA NA
##  $ iPhone5C    : num  15.5 5 NA NA NA NA NA
##  $ iPhone5S    : num  30 19 NA NA NA NA NA
##  $ iPhoneSE    : num  NA NA 9.5 6 11 7 8
##  $ iPhone6     : num  33 33 5 NA NA NA NA
##  $ iPhone6Plus : num  12.5 19 7 NA NA NA NA
##  $ iPhone6S    : num  NA 16 19 11 10 6 8
##  $ iPhone6SPlus: num  NA 8 12.5 10 4.5 2 3
##  $ iPhone7     : num  NA NA 31 40 28.5 13 16
##  $ iPhone7Plus : num  NA NA 16 32.1 29.5 11 11
##  $ iPhone8     : num  NA NA NA NA 6 24 13
##  $ iPhone8Plus : num  NA NA NA NA 10.5 17 24
##  $ iPhoneX     : num  NA NA NA NA NA 20.1 17
class(iphoneSales)
## [1] "data.frame"
typeof(iphoneSales)
## [1] "list"
```

Indexing works similarly to vectors, but note the difference between *extracting* and *selecting*:

``` r
#selecting
iphoneSales['iPhone4S']
##   iPhone4S
## 1        9
## 2       NA
## 3       NA
## 4       NA
## 5       NA
## 6       NA
## 7       NA
iphoneSales[2]
##   iPhone4S
## 1        9
## 2       NA
## 3       NA
## 4       NA
## 5       NA
## 6       NA
## 7       NA
#extracting
iphoneSales[['iPhone4S']]
## [1]  9 NA NA NA NA NA NA
iphoneSales[['iPhone4S']][1]
## [1] 9
iphoneSales[,2]
## [1]  9 NA NA NA NA NA NA
iphoneSales$iPhone4S
## [1]  9 NA NA NA NA NA NA
```

``` r
#For readability, show the code but hide the output of this chucnk once you tested the solutions
# use dataframe[row,col] to

#extract the first two elements of column "IPhone6s"

#subset iphoneSales to a dataframe with only time, iPhone5C, IPhoneX

#keep only the rows where the sales for iPhoneSE are higher than 7 AND are not NA (AND = &, OR = |, NOT = !)

#Use %in% to keep only the rows for c("Sep 2014", "Sep 2015", "Sep 2018")

#calculate the mean() of the IPhone7 sold 

#use inline code to print the mean of the iphone sold in Jun 2018
```

However, the `tidyverse` is best suited for using rectangular data structures called `tibbles` instead of data frames. To convert a `data.frame` into a `tibble`:

``` r
as_tibble(iphoneSales)
## # A tibble: 7 x 14
##   time  iPhone4S iPhone5C iPhone5S iPhoneSE iPhone6 iPhone6Plus iPhone6S
##   <fct>    <dbl>    <dbl>    <dbl>    <dbl>   <dbl>       <dbl>    <dbl>
## 1 Sep …        9     15.5       30     NA        33        12.5       NA
## 2 Sep …       NA      5         19     NA        33        19         16
## 3 Sep …       NA     NA         NA      9.5       5         7         19
## 4 Dec …       NA     NA         NA      6        NA        NA         11
## 5 Sep …       NA     NA         NA     11        NA        NA         10
## 6 Dec …       NA     NA         NA      7        NA        NA          6
## 7 Jun …       NA     NA         NA      8        NA        NA          8
## # ... with 6 more variables: iPhone6SPlus <dbl>, iPhone7 <dbl>,
## #   iPhone7Plus <dbl>, iPhone8 <dbl>, iPhone8Plus <dbl>, iPhoneX <dbl>
class(as_tibble(iphoneSales))
## [1] "tbl_df"     "tbl"        "data.frame"
typeof(as_tibble(iphoneSales))
## [1] "list"
```

Because tibbles are also dataframes, you can use indexing as you would do on a `data.frame`. However, a crucial difference between tibbles and dataframe is that tibbles allow to have column-list elements while dataframes allow only column-vectors:

``` r
iphoneSales_tibble <- tibble(year = c(2017, 2018), 
                    iphones = list(
                      c(iphone7 = 13, iphone7plus = 11), 
                      c(iphone7 = 16, iphone7plus = 11))
                    )
iphoneSales_tibble
## # A tibble: 2 x 2
##    year iphones  
##   <dbl> <list>   
## 1  2017 <dbl [2]>
## 2  2018 <dbl [2]>

iphoneSales_df <- data.frame(year = c(2017, 2018), 
       iphones = list(list(iphone7 = 13, iphone7plus = 11), list(iphone7 = 16, iphone7plus = 11)))
iphoneSales_df
##   year iphones.iphone7 iphones.iphone7plus iphones.iphone7.1
## 1 2017              13                  11                16
## 2 2018              13                  11                16
##   iphones.iphone7plus.1
## 1                    11
## 2                    11
```

``` r
# from iphoneSales_tibble extract the *vector* with the amounts of iphone7/7plus sold in 2017
```

The pipe operator
-----------------

Before moving into tidyverse, we need to familiarize with the `%>%` (pipe), an operator that enables to chain functions rather than nesting them. That makes the code easier to process for humans rather than nesting multiple functions. For instance:

``` r
round(mean(c(1:10, NA), na.rm = T), 0)
## [1] 6
```

You can "pipe" the above functions using `%>%` (shortcut: shift+cmd/ctrl+I), which passes the output that preceeds `%>%` to the first argument of the subsequent function (or alternatively anywhere you place a `.`). For instance:

``` r
c(1:10, NA) %>% 
  mean(na.rm = T) %>% 
  round(0)
## [1] 6
```

Which is equivalent to

``` r
c(1:10, NA) %>% 
  mean(x = . , na.rm = T) %>% 
  round(x = ., digits = 0)
## [1] 6
#' the dot is just a pronoun for what precedes the pipe operator
#' sometimes you don't want to pipe into the first argument
c('hello', 'hi', 'bye', 'ciao') %>% 
  gsub('ciao', 'hello', .)
## [1] "hello" "hi"    "bye"   "hello"
```

``` r
# `$` is a function too. Can you pipe `iphoneSales` to `$` to extract the vectro `iPhoneX`? Then, calculate the mean removing NAs
```
