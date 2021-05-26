# Week 4 Visualization in R

## GGPLOT2

`ggplot2` is a popular library

### Four core concepts

1. Aesthetics - visual property of an object in the plot
2. Geoms - geometric object used to represent data
3. Facets - display smaller groups/subsets of data. Create separate plots for subsets
4. Labels and annotations - add texts to plot

### Example

```R
ggplot(data = penguins) +
    geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g))
```

`ggplot(data = penguins)` specifies that we are using the penguins dataset
`+` to add a new layer to plot, where we are adding a geom
`geom_point()` uses points to create scatter plots
`geom_popint()` takes a mapping argument, it defines how variables in your dataset are mapped to visual properties.
Mapping arugment is always paired with the `aes()` function. The x and y arguments specify which variables to map to x-axis and y-axis.

Linke to [cheatsheet](https://ggplot2.tidyverse.org/)

## Enhancing Aethestics

```R
ggplot(data = penguins) +
    geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g, color=species, shape=species))
```

Also checkout `alpha` attribute to introduce transparency to the points.

To set a specific color to the points:

```R
ggplot(data = penguins) +
    geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g), color="puple")
```

## Other Geoms

```R
ggplot(data = diamonds) +
    geom_bar(mapping=aes(x=cut, fill=cut))
```

To create stacked bar chart:

```R
ggplot(data = diamonds) +
    geom_bar(mapping=aes(x=cut, fill=clarity))
```

## Smoothing

Smoothing help detect trends in data points

```R
ggplot(data, aes(x=distance, y= dep_delay)) +
    geom_point() +
    geom_smooth()
```

Two types of smoothing:

1. loess smoothing - best for smoothing plots with <1000 points
2. gam smoothing

```R
ggplot(data, aes(x=, y=))+
    geom_point() +
    geom_smooth(method="loess")
```

## Facet

Facet function allow us to display a subset of a dataset
`facet_wrap()`

```R
ggplot(data=penguins) +
    geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species)) +
    facet_wrap(~species)
```

`facet_grid()`

```R
ggplot(data=penguins) +
    geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species)) +
    facet_grid(sex~species)
```

First variable = vertical grid
Second variable = horizontal grid
species x sex subsets

## Filtering Plots

Example code with `dplyr` filter():

```R
data %>%
    filter(variable1 == "DS") %>%
    ggplot(aes(x = weight, y = variable2, colour = variable1)) +
    geom_point(alpha = 0.3,  position = position_jitter()) + stat_smooth(method = "lm")
```

## Annotations

Example for title, subtitle, and caption.

```R
ggplot(data=penguins) +
    geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species)) +
    labs(title="Palmer Peguins: Body Mass vs. Flipper Length", subtitle="Sample of Three Penguin Species", caption="Data collected by")
```

To call out specific data point, use annotate

```R
ggplot(data=penguins) +
    geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species)) +
    labs(title="Palmer Peguins: Body Mass vs. Flipper Length", subtitle="Sample of Three Penguin Species", caption="Data collected by") +
    annotate("text", x=220, y=3500, label="The Gentoos are the largest", color="purple", fontface="bold", size=4.5, angle=25)
```

We can also store the plot as a variable and add annotations:

```R
p <- ggplot(data=penguins) +
    geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species)) +
    labs(title="Palmer Peguins: Body Mass vs. Flipper Length", subtitle="Sample of Three Penguin Species", caption="Data collected by")

p + annotate("text", x=200 ...)
# Rotate x-axis text
p + theme(axis.text.x= element_tex(angle=45))
```

Another Example

```R
ggplot(data = hotel_bookings) +
    geom_bar(mapping = aes(x=market_segment)) +
    face_wrap(~hotel) +
    theme(axis.text.x = element_text(angel=45)) +
    labs(title="Comparison of market segments",
        caption=paste0("Data from: ", mindate, " to " , maxdate),
        x="Market Segment",
        y="Number of Bookings")
ggsave('hotel_booking.png', width=25, height=25)
```

## Saving Plots

Can export as image and pdf files.
Can also use `ggsave()` saves the last plot.
`ggsave("Three penguin species.png")`

To save plots without using ggsave() R also have graphic devices `png()` and `pdf()`:

```R
# png example
png(file = "exampleplot.png", bg = "transparent")
plot(1:10)
rect(1, 5, 3, 7, col = "white")
dev.off()

# pdf example
pdf(file = "/Users/username/Desktop/example.pdf",
       width = 4,
       height = 4)
plot(x = 1:10,
        y = 1:10)
abline(v = 0)
text(x = 0, y = 1, labels = "Random text")
dev.off()
```
