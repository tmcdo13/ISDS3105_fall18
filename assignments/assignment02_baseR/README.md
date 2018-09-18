Assignment 2
================
Your name

The goal of this practice is to improve your understanding of vectors and how to manipulate them. The data we use are the prices of the [2017 Big Mac Index](http://www.economist.com/content/big-mac-index).

For each question, please create a new chunck with your reponse. Use narratives to comment the output whenever the question requires to do so.

1.  Edit the code below to assign country names to the vector `countries` and prices to the vector `prices`. Hide the code below when you knit (check the Rmarkdown cheatsheet to find the appropriate chunk option to hide code).

2.  Use `typeof()` to report the type of both vectors.

``` r
typeof(countries)
```

    ## [1] "character"

``` r
typeof(prices)
```

    ## [1] "double"

1.  Use `names()` to name the `prices` using `countries`. Show the first 5 values of your new vector

``` r
names(prices) <- countries
prices[c(1:5)]
```

    ## Argentina Australia    Brazil   Britain    Canada 
    ##  4.125534  4.527955  5.101568  4.111432  4.655697

1.  Use `round()` to round the prices at the 3rd decimal. Overwrite `prices` with the rounded prices.

``` r
prices <- round(prices,3)
```

1.  Use indexing to report the prices for Canada, United States, Mexico

``` r
prices['Canada']
```

    ## Canada 
    ##  4.656

``` r
prices['United States']
```

    ## United States 
    ##           5.3

``` r
prices['Mexico']
```

    ## Mexico 
    ##  2.754

1.  Use inline code and the function `length()` to display the following sentence:

"The are x observations in the Big-Mac Index"

The are 56 observations in the Big-Mac Index

1.  Convert the prices from Dollar to Euro (1 Dollar = .83 Euro). In the narrative, comment about the property which allows you to combine a vector of length 1 (the exchange rate) with a vector of length 56 (the prices).

``` r
# r automatically allows you to combine two vectors based on theit   type and since both parameters were vectors, 

#euro <- c(.83)
euro <- rep(.83,45)
toEuros <- function(prices,euro) {
  return (euro * prices[1:56])
}
toEuros(prices,euro)
```

    ## Warning in euro * prices[1:56]: longer object length is not a multiple of
    ## shorter object length

    ##      Argentina      Australia         Brazil        Britain         Canada 
    ##        3.42458        3.75824        4.23466        3.41213        3.86448 
    ##          Chile          China       Colombia     Costa Rica Czech Republic 
    ##        3.19052        2.42111        2.69252        3.32000        2.72323 
    ##        Denmark          Egypt      Euro area      Hong Kong        Hungary 
    ##        3.82298        1.45582        3.70595        2.04014        2.66347 
    ##          India      Indonesia         Israel          Japan       Malaysia 
    ##        2.28831        1.99449        3.96159        2.78963        1.66249 
    ##         Mexico    New Zealand         Norway       Pakistan           Peru 
    ##        2.28582        3.67856        4.90862        2.95978        2.68007 
    ##    Philippines         Poland         Russia   Saudi Arabia      Singapore 
    ##        2.19867        2.26009        1.89074        2.65600        3.37395 
    ##   South Africa    South Korea      Sri Lanka         Sweden    Switzerland 
    ##        1.87663        3.19052        3.13159        4.82977        5.59586 
    ##         Taiwan       Thailand         Turkey            UAE        Ukraine 
    ##        1.87912        2.90168        2.49498        3.16396        1.40934 
    ##  United States        Uruguay      Venezuela        Vietnam        Austria 
    ##        4.39900        3.75907        3.36648        2.19037        3.22289 
    ##        Belgium        Estonia        Finland         France        Germany 
    ##        3.83875        2.98551        4.32181        3.88606        3.69682 
    ##         Greece        Ireland          Italy    Netherlands       Portugal 
    ##        3.17558        3.85784        3.98068        3.42126        3.08013 
    ##          Spain 
    ##        3.60137

-   Could you use the vector `rep(.83, 28)` to do the same? Yes, this works since 28 is a factor of 56
-   Could you use the vector `rep(.83, 112)` to do the same? No, this doesn't work because 112 is larger than 56 and thus the result would be a vector of length 112
-   Would `rep(.83, 45)` also work? Why? Yes, this would work because 45 is less than 56, but it does give you a warning because 45 is not a factor of 56

1.  In your narrative, mention that we are going to drop the 46th element. Use dynamic code to report the country that will drop.

``` r
# This chunk of code drops the 46th element
prices[46]
```

    ## Belgium 
    ##   4.625

1.  Overwrite the vector of prices with a new vector without observation 46. Use `length()` to make sure you have one observation less.

``` r
prices <- prices[c(1:45,47:56)]
length(prices)
```

    ## [1] 55

1.  Knit, commit and push to your GitHub repo `assignment`. Then submit the link to the *assignment folder* on Moodle.
