Data visualization
================

Data Visualization
==================

Base R offers comes with native plotting functions for data visualization, such as `plot()`, `barplot()`, `pie()`, etc. but we will not cover them. Instead, we focus on another graphic library called [ggplot2](http://ggplot2.org/), which is part of the tidyverse package suite. Despite plotting functions in base R came chronologically before ggplot2 (and are still widely used), [ggplot2](http://ggplot2.org/) ([cheatsheet](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)) is probably the most popular package for dataviz. Its rapid success is due both to the attractive design of its plots and to a more consistent syntax. Also, there are a number of [extensions](http://www.ggplot2-exts.org/) developed within the ggplot2 framework that make easier to add themes or create more sophisticated charts.

ggplot2
=======

References
----------

Check [Chapter 3](http://r4ds.had.co.nz/data-visualisation.html) on dataviz in ggplot2.

Installing ggplot2
------------------

Because you already installed the tidyverse, to use `ggplot2` you can just call `library(tidyverse)`. From now we will be using functions that are not part of base R, thus make you rerun `library(tidyverse)` every time you start a new R session, and to have a `library(tidyverse)` call before you use any ggplot2 function in your RMarkdown. If you get error messages saying that R `could not find function`, you probably have not loaded the package correctly.

``` r
library(tidyverse)
load(here::here('data', 'dataset.RData'))
```

Using ggplot2
-------------

ggplot2 builds on an underlying grammar, which entails seven fundamental elements:

| Element     | Visual attribute                      |
|-------------|---------------------------------------|
| data        | dataset with the variables of interst |
| aesthetics  | x-axis, y-axis, color, fill, alpha    |
| geometries  | bars, dots, lines                     |
| facets      | coloumns, rows                        |
| statistics  | bins, smooth, count                   |
| coordinates | polar, cartesian                      |
| themes      | non-data ink                          |

Each ggplot2 statement requires at least a dataset, a set of aesthetics that the variables are mapped to, and the geometrical shape to visualize the aesthetics into.

For instance, to plot a chart of million of twitter users per year:

``` r
ggplot() +
  geom_col(data =  twitter_users, aes(x = Year, y = millions))
```

<img src="README_files/figure-markdown_github/unnamed-chunk-2-1.png" alt="Millions of Twitter users" width="80%" />
<p class="caption">
Millions of Twitter users
</p>

The [concept of *mapping*](http://r4ds.had.co.nz/data-visualisation.html#aesthetic-mappings) is fundamental when learning ggplot2; although it might not be very intuitive at first, it ensures a high level of consistency when working in complex multivariate enviroment. *To map* means to assign a variable to an *aesthetic*, namely to a visual property such' height, fill color, border color, etc. In the previous example we mapped only to x-y coordinates; but you can call `?geom_col()` and scroll down in the help pane to the paragraph *Aesthetics* for a complete list of the attributes available. For instance, try to map Year to the fill too:

``` r
ggplot() +
  geom_col(data =  twitter_users, aes(x = Year, y = millions, ------ ))
```

Use `freqCasualties` to plot a barchart of casualties count by class and gender

``` r
#what chart/geom?
#what do we want to map to x and y? how do we map the third variable?
```

Using the same set of aesthetics and mapped variables, we can create different charts by using different `geom_*` functions. For instance,

``` r
#the dataset twitter_users
#the set of aesthetics we are using: aes(x = Year, y = millions )
#ggplot() +
  #use geom_line()
  #use geom_point()
```

Some times, you want to manually **set** a value for a certain aesthetic, rather than **mapping** a variable to it. In this case, the aesthetic is not usually interpretable, but it might be be helpful to make a chart clearer or more appealing. For instance, note the difference between the charts below:

``` r
ggplot() +
  geom_line(data =  twitter_users, aes(x = Year, y = millions, color ='blue' )) 
```

![](README_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
ggplot() +
geom_line(data =  twitter_users, aes(x = Year, y = millions), color ='blue') 
```

![](README_files/figure-markdown_github/unnamed-chunk-6-2.png)

To change color, you can use either [color names](http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf) (e.g., 'red'), hex codes (e.g., `#ff0000`) or rgb (e.g. `rgb(255, 0, 0)`).

So far, we specified aesthetics and datasets inside a specific geom, but usually we put them in the `ggplot()` function and let the `geom_` to inherit them from the `ggplot()` statement:

``` r
#use twitter_users to plot twitter users
#use sn_users to overlap FB users
```

If you ran `ggplot()` and `geom_` separately, you might notice that every `geom_` is nothing but a new layer added to the plane. This means that you can overlap multiple geoms in the same chart:

``` r
  #use geom_line AND geom_point
```

### Exercise:

-   use `beerDt` to create a linechart of beer consumption in US from 1903.
-   add a layer of points using `geom_point`

Suppose that you now want to color the point presenting your birthyear. We can do it in two steps:

    1. Use ifelse() to create a character column called 'myBirthYear' that takes value 'My birthyear' for your birth year, and NA for everything else.
    2. Map `myBirthYear` to the fill of `geom_point` to flag your birth year
    3. Use ggtitle to add a title to the chart
