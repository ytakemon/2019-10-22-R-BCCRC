---
title: Writing Data
teaching: 10
exercises: 10
questions:
- "How can I save plots and data created in R?"
objectives:
- "To be able to write out plots and data from R."
keypoints:
- "Save plots from RStudio using the 'Export' button."
- "Use `write.table` to save tabular data."
output: 
  html_document: 
    keep_md: yes
---



## Saving plots
You can save a plot from within RStudio using the 'Export' button
in the 'Plot' window. This will give you the option of saving as a
.pdf or as .png, .jpg or other image formats.

Sometimes you will want to save plots without creating them in the
'Plot' window first. Perhaps you want to make a pdf document with
multiple pages: each one a different plot, for example. Or perhaps
you're looping through multiple subsets of a file, plotting data from
each subset, and you want to save each plot, but obviously can't stop
the loop to click 'Export' for each one.

In this case you can use a more flexible approach. The function
`pdf` creates a new pdf device. You can control the size and resolution
using the arguments to this function.


~~~
pdf("Hclust_corplot_mtcars.pdf", width=5, height=5)
corrplot(cor_mtcars, order = "hclust", addrect = 3)

# You then have to make sure to turn off the pdf device!
dev.off()
~~~
{: .language-r}

Open up this document and have a look.

The commands `jpeg`, `png` etc. are used similarly to produce
documents in different formats.

## Writing data

At some point, you'll also want to write out data from R.

We can use the `write.table` function for this, which is
very similar to `read.table` from before.

Let's create a data-cleaning script, for this analysis, we
only want to focus on the gapminder data for Australia:


~~~
aust_subset <- gapminder[gapminder$country == "Australia",]

write.table(aust_subset,
  file="gapminder-aus.csv",
  sep=",",
  row.names = FALSE,
  quote = FALSE
)
~~~
{: .language-r}

or directly as a .csv file


~~~
aust_subset <- gapminder[gapminder$country == "Australia",]

write.csv(aust_subset,
  file="gapminder-aus.csv",
  row.names = FALSE,
  quote = FALSE
)
~~~
{: .language-r}
