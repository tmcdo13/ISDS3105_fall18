lesson 9: Querying a MySQL DB
================

`dplyr` makes easy to translate R code into SQL code for querying
databases. To see how that works, first we connect to our online reviews
MySQL DB:

``` r
#' this WON'T work off-campus unless you use a client server
#' you need to add USN/PW to con.R
#' DON'T push con.R to GitHub -- use .gitinore
#source(here::here('conn.R'))
```

1.  Report all the authors and the hotels they reviewed. Report the
    author name, the hotel ID and hotel name. Order the output by author
    name

2.  Report the total number of reviews received by each hotel. Report a
    three columns table with `hotelId`, `hotelName` and total number of
    reviews. Make sure that you are including hotels with zero reviews
    as well. Note that some hotels have 0 reviews. If you decide to
    count the rows in each grouping level, make sure you you don’t count
    as 1 those who have zero reviews.

3.  Report how many chains established their headquarter in each
    country. Plot a barchart those frequencies by country and then add a
    title to your plot. Adjust your axes’ labels as needed (remember
    that non-data ink points are modified within `theme()`).

4.  For each review of stays during 2011, calculate the composite
    average score as the mean of Location, Room, Service, Value and
    Cleanliness. Then plot a histogram (using `geom_hist()`) of the
    differences between the average of those 5 attributes and
    ratingOverall.

5.  Report all data about brands that have minimum square footage
    requirement for rooms that exceeds the average minimum square
    footage of all brands by at least 50%.

*warning*: If you query the DB and then pipe the remote table into a
ggplot2 function, you might need to `collect()` the remote table before
passing it to `ggplot()`, because `ggplot()` expects a class
`data.frame` (and tibbles are also data.frame). However, if you pass a
different object (such as a connection) “it will be converted to one by
fortify()” (see the documentation `?ggplot()). Apparently, for some of
you`fortify()`does not convert the table to a local data.frame, and if
that is the case you need to`collect()\`.
