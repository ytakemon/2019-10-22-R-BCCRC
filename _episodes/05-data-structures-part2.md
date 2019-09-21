---
title: "Exploring Data Frames"
teaching: 20
exercises: 10
questions:
- "How can I manipulate a data frame?"
objectives:
- "Be able to add and remove rows and columns."
- "Be able to remove rows with `NA` values."
- "Be able to append two data frames"
- "Be able to articulate what a `factor` is and how to convert between `factor` and `character`."
- "Be able to find basic properties of a data frames including size, class or type of the columns, names, and first few rows."
keypoints:
- "Use `cbind()` to add a new column to a data frame."
- "Use `rbind()` to add a new row to a data frame."
- "Remove rows from a data frame."
- "Use `na.omit()` to remove rows from a data frame with `NA` values."
- "Use `levels()` and `as.character()` to explore and manipulate factors"
- "Use `str()`, `nrow()`, `ncol()`, `dim()`, `colnames()`, `rownames()`, `head()` and `typeof()` to understand structure of the data frame"
- "Read in a csv file using `read.csv()`"
- "Understand `length()` of a data frame"
output: 
  html_document: 
    keep_md: yes
---




At this point, you've see it all - in the last lesson, we toured all the basic
data types and data structures in R. Everything you do will be a manipulation of
those tools. But a whole lot of the time, the star of the show is going to be
the data frame - that table that we started with that information from a CSV
gets dumped into when we load it. In this lesson, we'll learn a few more things
about working with data frame.

## Adding columns and rows in data frame

We learned last time that the columns in a data frame were vectors, so that our
data are consistent in type throughout the column. As such, if we want to add a
new column, we need to start by making a new vector:




~~~
age <- c(2,3,5,12)
cats
~~~
{: .language-r}



~~~
##     coat weight likes_string
## 1 calico    2.1         TRUE
## 2  black    5.0        FALSE
## 3  tabby    3.2         TRUE
~~~
{: .output}

We can then add this as a column via:


~~~
cats <- cbind(cats, age)
~~~
{: .language-r}



~~~
## Error in data.frame(..., check.names = FALSE): arguments imply differing number of rows: 3, 4
~~~
{: .error}

Why didn't this work? Of course, R wants to see one element in our new column
for every row in the table:


~~~
cats
~~~
{: .language-r}



~~~
##     coat weight likes_string
## 1 calico    2.1         TRUE
## 2  black    5.0        FALSE
## 3  tabby    3.2         TRUE
~~~
{: .output}



~~~
age <- c(4,5,8)
cats <- cbind(cats, age)
cats
~~~
{: .language-r}



~~~
##     coat weight likes_string age
## 1 calico    2.1         TRUE   4
## 2  black    5.0        FALSE   5
## 3  tabby    3.2         TRUE   8
~~~
{: .output}

Now how about adding rows - in this case, we saw last time that the rows of a
data frame are made of lists:


~~~
newRow <- list("tuxedo", 3.3, TRUE, 9)
cats <- rbind(cats, newRow)
~~~
{: .language-r}

## Factors

Another thing to look out for has emerged - when R creates a factor, it only
allows whatever is originally there when our data was first loaded, which was
'black', 'calico' and 'tabby' in our case. Anything new that doesn't fit into
one of these categories is rejected as nonsense (becomes NA).

The warning is telling us that we unsuccessfully added 'tuxedo' to our
*coat* factor, but 3.3 (a numeric), TRUE (a logical), and 9 (a numeric) were
successfully added to *weight*, *likes_string*, and *age*, respectfully, since
those values are not factors. To successfully add a cat with a
'tortoiseshell' *coat*, explicitly add 'tortoiseshell' as a *level* in the factor:


~~~
levels(cats$coat)
~~~
{: .language-r}



~~~
## NULL
~~~
{: .output}



~~~
levels(cats$coat) <- c(levels(cats$coat), "tuxedo")
cats <- rbind(cats, list("tuxedo", 3.3, TRUE, 9))
~~~
{: .language-r}



~~~
## Warning in `[<-.factor`(`*tmp*`, ri, value = structure(c("calico",
## "black", : invalid factor level, NA generated
~~~
{: .error}

Alternatively, we can change a factor column to a character vector; we lose the
handy categories of the factor, but can subsequently add any word we want to the
column without babysitting the factor levels:


~~~
str(cats)
~~~
{: .language-r}



~~~
## 'data.frame':	5 obs. of  4 variables:
##  $ coat        : Factor w/ 1 level "tuxedo": NA NA NA 1 1
##  $ weight      : num  2.1 5 3.2 3.3 3.3
##  $ likes_string: logi  TRUE FALSE TRUE TRUE TRUE
##  $ age         : num  4 5 8 9 9
~~~
{: .output}



~~~
cats$coat <- as.character(cats$coat)
str(cats)
~~~
{: .language-r}



~~~
## 'data.frame':	5 obs. of  4 variables:
##  $ coat        : chr  NA NA NA "tuxedo" ...
##  $ weight      : num  2.1 5 3.2 3.3 3.3
##  $ likes_string: logi  TRUE FALSE TRUE TRUE TRUE
##  $ age         : num  4 5 8 9 9
~~~
{: .output}

## Removing rows

We now know how to add rows and columns to our data frame in R - but in our
first attempt to add a 'tortoiseshell' cat to the data frame we've accidentally
added a garbage row:


~~~
cats
~~~
{: .language-r}



~~~
##     coat weight likes_string age
## 1   <NA>    2.1         TRUE   4
## 2   <NA>    5.0        FALSE   5
## 3   <NA>    3.2         TRUE   8
## 4 tuxedo    3.3         TRUE   9
## 5 tuxedo    3.3         TRUE   9
~~~
{: .output}

We can ask for a data frame minus this offending row:


~~~
cats[-4,]
~~~
{: .language-r}



~~~
##     coat weight likes_string age
## 1   <NA>    2.1         TRUE   4
## 2   <NA>    5.0        FALSE   5
## 3   <NA>    3.2         TRUE   8
## 5 tuxedo    3.3         TRUE   9
~~~
{: .output}

Notice the comma with nothing after it to indicate we want to drop the entire fourth row.

Note: We could also remove both new rows at once by putting the row numbers
inside of a vector: `cats[c(-4,-5),]`

Alternatively, we can drop all rows with `NA` values:


~~~
na.omit(cats)
~~~
{: .language-r}



~~~
##     coat weight likes_string age
## 4 tuxedo    3.3         TRUE   9
## 5 tuxedo    3.3         TRUE   9
~~~
{: .output}

Let's reassign the output to `cats`, so that our changes will be permanent:


~~~
cats <- na.omit(cats)
~~~
{: .language-r}
## StringsAsFactors argument

You can also by pass all factor related headaches by reading a dataframe and defining a new argument:


~~~
cats2 <- read.csv("data/feline-data.csv", stringsAsFactors = FALSE)
str(cats2)
~~~
{: .language-r}



~~~
## 'data.frame':	3 obs. of  3 variables:
##  $ coat        : chr  "calico" "black" "tabby"
##  $ weight      : num  2.1 5 3.2
##  $ likes_string: logi  TRUE FALSE TRUE
~~~
{: .output}

Now let's compare what happened to the factor column:

~~~
str(cats)
~~~
{: .language-r}



~~~
## 'data.frame':	2 obs. of  4 variables:
##  $ coat        : chr  "tuxedo" "tuxedo"
##  $ weight      : num  3.3 3.3
##  $ likes_string: logi  TRUE TRUE
##  $ age         : num  9 9
##  - attr(*, "na.action")= 'omit' Named int  1 2 3
##   ..- attr(*, "names")= chr  "1" "2" "3"
~~~
{: .output}



~~~
str(cats2)
~~~
{: .language-r}



~~~
## 'data.frame':	3 obs. of  3 variables:
##  $ coat        : chr  "calico" "black" "tabby"
##  $ weight      : num  2.1 5 3.2
##  $ likes_string: logi  TRUE FALSE TRUE
~~~
{: .output}

## Appending data frame

The key to remember when adding data to a data frame is that *columns are
vectors or factors, and rows are lists.* We can also glue two data frames
together with `rbind`:


~~~
cats <- rbind(cats, cats)
cats
~~~
{: .language-r}



~~~
##      coat weight likes_string age
## 4  tuxedo    3.3         TRUE   9
## 5  tuxedo    3.3         TRUE   9
## 41 tuxedo    3.3         TRUE   9
## 51 tuxedo    3.3         TRUE   9
~~~
{: .output}
But now the row names are unnecessarily complicated. We can remove the rownames,
and R will automatically re-name them sequentially:


~~~
rownames(cats) <- NULL
cats
~~~
{: .language-r}



~~~
##     coat weight likes_string age
## 1 tuxedo    3.3         TRUE   9
## 2 tuxedo    3.3         TRUE   9
## 3 tuxedo    3.3         TRUE   9
## 4 tuxedo    3.3         TRUE   9
~~~
{: .output}

> ## Challenge 1
>
> You can create a new data frame right from within R with the following syntax:
> 
> ~~~
> df <- data.frame(id = c('a', 'b', 'c'),
>                  x = 1:3,
>                  y = c(TRUE, TRUE, FALSE),
>                  stringsAsFactors = FALSE)
> ~~~
> {: .language-r}
> Make a data frame that holds the following information for yourself:
>
> - first name
> - last name
> - lucky number
>
> Then use `rbind` to add an entry for the people sitting beside you.
> Finally, use `cbind` to add a column with each person's answer to the question, "Is it time for coffee break?"
>
> > ## Solution to Challenge 1
> > 
> > ~~~
> > df <- data.frame(first = c('Grace'),
> >                  last = c('Hopper'),
> >                  lucky_number = c(0),
> >                  stringsAsFactors = FALSE)
> > df <- rbind(df, list('Marie', 'Curie', 238) )
> > df <- cbind(df, coffeetime = c(TRUE,TRUE))
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

## Realistic example
So far, you've seen the basics of manipulating data frames with our cat data;
now, let's use those skills to digest a more realistic dataset. Lets read in the
gapminder dataset that we downloaded previously:


~~~
gapminder <- read.csv("data/gapminder.csv")
~~~
{: .language-r}

> ## Miscellaneous Tips
>
> * Another type of file you might encounter are tab-separated value files (.tsv). To specify a tab as a separator, use `"\\t"` or `read.delim()`.
>
> * Files can also be downloaded directly from the Internet into a local
> folder of your choice onto your computer using the `download.file` function.
> The `read.csv` function can then be executed to read the downloaded file from the download location, for example,
> 
> ~~~
> download.file("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv", destfile = "data/gapminder-FiveYearData.csv")
> gapminder <- read.csv("data/gapminder-FiveYearData.csv")
> ~~~
> {: .language-r}
>
> * Alternatively, you can also read in files directly into R from the Internet by replacing the file paths with a web address in `read.csv`. One should note that in doing this no local copy of the csv file is first saved onto your computer. For example,
> 
> ~~~
> gapminder <- read.csv("https://raw.githubusercontent.com/swcarpentry/r-novice-gapminder/gh-pages/_episodes_rmd/data/gapminder-FiveYearData.csv")
> ~~~
> {: .language-r}
>
> * You can read directly from excel spreadsheets without
> converting them to plain text first by using the [readxl](https://cran.r-project.org/web/packages/readxl/index.html) package.
{: .callout}

The gapminder dataset was provided by the **Gapminder Foundation**, which is a non-profit organization that promotes sustainable global development of the UN Millenium Developmen Goals via incrased use and understanding of statistics and other information about social, economic, and environmental development at national and global levels. 

Let's investigate gapminder a bit; the first thing we should always do is check
out what the data looks like with `str`:


~~~
str(gapminder)
~~~
{: .language-r}



~~~
## 'data.frame':	1704 obs. of  6 variables:
##  $ country  : Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ continent: Factor w/ 5 levels "Africa","Americas",..: 3 3 3 3 3 3 3 3 3 3 ...
##  $ year     : int  1952 1957 1962 1967 1972 1977 1982 1987 1992 1997 ...
##  $ lifeExp  : num  28.8 30.3 32 34 36.1 ...
##  $ pop      : int  8425333 9240934 10267083 11537966 13079460 14880372 12881816 13867957 16317921 22227415 ...
##  $ gdpPercap: num  779 821 853 836 740 ...
~~~
{: .output}

We can also examine individual columns of the data frame with our `typeof` function:


~~~
typeof(gapminder$year)
~~~
{: .language-r}



~~~
## [1] "integer"
~~~
{: .output}



~~~
typeof(gapminder$country)
~~~
{: .language-r}



~~~
## [1] "integer"
~~~
{: .output}



~~~
str(gapminder$country)
~~~
{: .language-r}



~~~
##  Factor w/ 142 levels "Afghanistan",..: 1 1 1 1 1 1 1 1 1 1 ...
~~~
{: .output}

We can also interrogate the data frame for information about its dimensions;
remembering that `str(gapminder)` said there were 1704 observations of 6
variables in gapminder, what do you think the following will produce, and why?


~~~
length(gapminder)
~~~
{: .language-r}



~~~
## [1] 6
~~~
{: .output}

A fair guess would have been to say that the length of a data frame would be the
number of rows it has (1704), but this is not the case; remember, a data frame
is a *list of vectors and factors*:


~~~
typeof(gapminder)
~~~
{: .language-r}



~~~
## [1] "list"
~~~
{: .output}

When `length` gave us 6, it's because gapminder is built out of a list of 6
columns. To get the number of rows and columns in our dataset, try:


~~~
nrow(gapminder)
~~~
{: .language-r}



~~~
## [1] 1704
~~~
{: .output}



~~~
ncol(gapminder)
~~~
{: .language-r}



~~~
## [1] 6
~~~
{: .output}

Or, both at once:


~~~
dim(gapminder)
~~~
{: .language-r}



~~~
## [1] 1704    6
~~~
{: .output}

We'll also likely want to know what the titles of all the columns are, so we can
ask for them later:


~~~
colnames(gapminder)
~~~
{: .language-r}



~~~
## [1] "country"   "continent" "year"      "lifeExp"   "pop"       "gdpPercap"
~~~
{: .output}

At this stage, it's important to ask ourselves if the structure R is reporting
matches our intuition or expectations; do the basic data types reported for each
column make sense? If not, we need to sort any problems out now before they turn
into bad surprises down the road, using what we've learned about how R
interprets data, and the importance of *strict consistency* in how we record our
data.

Once we're happy that the data types and structures seem reasonable, it's time
to start digging into our data proper. Check out the first few lines:


~~~
head(gapminder)
~~~
{: .language-r}



~~~
##       country continent year lifeExp      pop gdpPercap
## 1 Afghanistan      Asia 1952  28.801  8425333  779.4453
## 2 Afghanistan      Asia 1957  30.332  9240934  820.8530
## 3 Afghanistan      Asia 1962  31.997 10267083  853.1007
## 4 Afghanistan      Asia 1967  34.020 11537966  836.1971
## 5 Afghanistan      Asia 1972  36.088 13079460  739.9811
## 6 Afghanistan      Asia 1977  38.438 14880372  786.1134
~~~
{: .output}

To make sure our analysis is reproducible, we should put the code
into a script file so we can come back to it later.

> ## Challenge 2
>
> Read the output of `str(gapminder)` again;
> this time, use what you've learned about factors, lists and vectors,
> as well as the output of functions like `colnames` and `dim`
> to explain what everything that `str` prints out for gapminder means.
> If there are any parts you can't interpret, discuss with your neighbors!
>
> > ## Solution to Challenge 2
> >
> > The object `gapminder` is a data frame with columns
> > - `country` and `continent` are factors.
> > - `year` is an integer vector.
> > - `pop`, `lifeExp`, and `gdpPercap` are numeric vectors.
> >
> {: .solution}
{: .challenge}
