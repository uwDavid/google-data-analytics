# Week 5 - Documentation in R

R Markdown help with documentation of the steps in our analysis.
R Markdown can also be converted to other formats such as HTML and PDF.
Other notebooks have similar features: Jupyter, Kaggle, Google Colab.

```R
install.packages("rmarkdown")
library("rmarkdown")
```

Go to file and create a new rmarkdown file, it has a `.Rmd` extension.
Click the `knit` button to create HTML file.
All the codes will be automatically run to produce the output file.

## Differences with Markdown

Bullets are created using `*` instead of `-`
Embed image `![caption for image](url)`

## Code Chunks

ctrl+alt+i is shortcut to add a code chunk

You can add label to the code chunk delimiter:
\`\`\`{r loading packages}

We can also control the output of this code chunk in the notebook.

## Output Format

R's YAML meta data at the top can be changed to automatically determine the output file type.

Available document types:

-   pdf_document
-   word_document
-   odt_document
-   rtf_document
-   md_document
-   github_document

Presentation types:

-   beamer_presentation - pdf presentations with beamer
-   ioslides_presentation - html presentations with ioslides
-   slidy_presentation - for HTML presentations with Slidy
-   powerpoint_presentation - for ppt
-   revealjs::reavealjs_presentation - HTML presentation with reaveal.js

Other:
flexdashboard package allows you to publish a dashboard
shiny lets you build interactive web apps using R code
vitae is a CV template package in R
