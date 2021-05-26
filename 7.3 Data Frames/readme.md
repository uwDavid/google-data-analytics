# Week 3 - Data Frames

A data frame is like a excel spreadsheet

-   columns should be named
-   each column should contain the same number of data items

## Create Data Frame

```R
id <- c(1:10)
name <- c("John", "Robert",...)
job_title<- c("Professional", "Software", ...)
employee <- data.frame(id, name, job_title)
```

Tibbles - are streamined data frames

-   never change data types
-   never change names of variables
-   never create row names
-   easier printing

## Creating Tibbles

```R
library(tidyverse)
data(diamonds)
View(diamonds)

# create a tibble
as_tibble(diamonds)
```

## Data Import

`data()` will display a list of preloaded datasets from the datasets package
To load a dataset `data(mtcars)`
The environment pane will show the names of the data objects
To view data type in console `mtcars` and press ctrl+enter

`readr` package is useful for reading rectangular data

-   `read_csv()`
-   `read_tsv()` - tab-separated files
-   `read_delim()` - general delimited files
-   `read_fwf()` - fixed-width files
-   `read_table()` - tabular files where columns are separated by white-space
-   `read_log()` - web log files

`readxl` package can help import excel files

## Clean Data

`here` `skimr` `janitor` are packages that help clean the data
To get data summaries:

-   `skim_without_charts()` - alot of info about the data
-   `glimpse()` - very quick summmary
-   `head()` - first few rows
-   `select()` - like SQL's select columns, we use pipe into select

```R
penguins %>%
    select(species)
```

To select the species column
To get every column except species column `select(-species)`

`rename()` to rename a column

```R
penguins %>%
    rename(island_new=island)
```

Also check out `rename_with(penguins, tolower)`

Janitor package has `clean_names()` automatically ensure column names are unique and consistent.
`clean_names(penguins)`

## R Operators

`%%` - modulo
`%/%` - integer division
`^` - exponent

`!=` - not equal

Element wise `&` and `|` examines all elements of a vector
While logical `&&` and `||` examine only the 1st element of a vector

## Organizing Data

`arrange()`
`group_by()`
`filter()`

```R
penguins %>%
    arrange(bill_length_mm)
```

To sort descending order, `arrange(-bill_length_mm)`
To save this as a data frame, we need to name it:

```R
penguins2 <- penguins %>%
    arrange(bill_length_mm)

View(penguins2)
```

### Group by, and Summarize

```R
penguins %>% group_by(island) %>%
    drop_na() %>%
    summarize(mean_bill_length_mm=mean(bill_length_mm))
```

```R
penguins %>% group_by(species, island) %>%
    drop_na() %>%
    summarize(mean_bill_length_mm=mean(bill_length_mm), mean_bl=mean(bill_length_mm))
```

### Filter

```R
penguins %>%
    filter(species=="Adelie")
```

## Transform Data

`separate(employee, name, into=c('first_name', 'last_name'), sep=' ')`
Converts the name column in employee data frame to `first_name` and `last_name`.

Opposite of separate is `unite()`
`unite(employee, 'name', first_name, last_name, sep=' ')`

Add columns with `mutate()`

```R
penguins %>%
    mutate(body_mass_kg=body_mass_g/1000)
```

Transform from wide to long format with `pivot_longer()`

## Bias Function

```R
install.packages('SimDesign')
library('SimDesign')

actual_temp <- c(68.3, 70, 72.4, 71, 67, 70)
predicted_temp <- c(67.9, 69, 71.5, 70, 67, 69)
bias(actual_temp, predicted_temp)
```

0 means likely not biased, higher number means biased.
