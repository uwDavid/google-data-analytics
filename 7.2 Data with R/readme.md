# Week 2 - Data Analysis with R

R Data Structures:

-   Vectors
-   Data frames
-   Matrices
-   Arrays

There are 2 types of vectors:

1. atomic vectors
2. lists

## Vectors

There are 6 primary types of atomic vectors:

1. logical
2. integer
3. double
4. character
5. complex
6. raw

### Creating Vectors

`c(x, y, z, ... )` to store data into a vector.
To create a vector with integers, we must place the letter "L" after each number:
`c(1L, 5L, 15L)`

### Vector Functions

`typeof(c("a","b"))` - to display vector type

```R
x <- c(33.5, 57.75, 120.05)
length(x)
```

Is functions: `is.logical(), is.double(), is.integer()`

### Naming Vectors

```R
x <- c(1,3,5)
names(x) <- c("a", "b", "c")
x
```

Will display 2 rows:
a b c
1 3 5

## Lists

Lists are different from atomic vectors because list elements can be of any type, and data types can be mixed.

Create a list using `list(x, y, z)`
To determine the structure of a list `str(list("a", 1L, 1.5, TRUE))`

### Naming List

```R
list("Chicago"=1, "New York"=2, "LA"=3)
$Chicago
```

## Dates and Times in R

Use the `lubridate` package to work with date and times.
Note `lubridate` is part of `tidyverse`

To convert strings to dates `ymd("2021-01-20)`
We can arrange ymd to suit the format of the text.

`ymd_hms("2021-10-20 20:11:59")`

## Other Data Structures

### Data Frames

Same as data frames in `pandas` package
`data.frame(x=c(1,2,3), y=c(1.5, 5.5, 7.5))`

### Files

`file.create("new_text_file.txt")` if the file creation was successful, R will return `true`
`file.copy("new_text_file.txt", "destination folder")`
`unlink("file.csv")` to delete files

### Matrix

`matrix()` takes 2 arguments:

1. a vector of values to be placed in the matrix
2. at least 1 matrix dimension, specified using `nrow=` or `ncol=`

## Logical Operators and Conditional Statements

### Logical Operators

-   AND (& or &&)
-   OR (| or || )
-   NOT (!)

### Conditionals

```R
if (condition) {
    expr
} else if (condition2) {
    expr2
} else {
    expr3
}
```

## Coding Conventions

-   names should using underscore
-   operators should be surrounded with space
-   always put space after comma
-   no space inside parethensis
-   use `<-` instead of `=` for assignments

## Pipes

Pipe is a tool in R for expressing a sequence of multiple operations, represented by `%>%`

```R
data('ToothGrowth')
View(ToothGrowth)

filtered_tg <- filter(ToothGrowth, dose==0.5)
View(filtered_tg)

arrange(filtered_tg, len)
# Nested Example
arrange(filter(ToothGrowth, dose==0.5), len)

#Pipe Example
#ctrl+shift+m shortcut
filtered_toothgrowth <- ToothGrowth%>%
    filter(dose==0.5) %>%
    arrange(len)
```

More pipe example

```R
filtered_toothgrowth <- ToothGrowth %>%
    filter(dose==0.5) %>%
    group_by(supp) %>%
    summarize(mean_len = mean(len, na.rm = T), .group = "drop")
```

type `filtered_toothgrowth` in console to view the results.
