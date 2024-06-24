# Activity Objective

The goal of this graphics activity is to improve your familiarity with
manipulating tabular data and formatting it using a library called
[`gt`](https://gt.rstudio.com/index.html). The `gt` package is used to
create publish quality tables using R code.

The table you will attempt to recreate is the following. ![Activity Two
Table](imgs/Graphics_Activity_Two.png)

# Helpful Tips

## Resources

For this activity, the documentation of the
[`gt`](https://gt.rstudio.com/reference/index.html) package will be
extremely helpful. If you are unsure of what any functions do, running
`?function_name` will open the documentation menu in RStudio. For
example, to understand what the `tab_style` function does, we could run
`?tab_style`.

Reading the [Get Started](https://gt.rstudio.com/articles/gt.html) page
of the function should give you a good idea of how the workflow of the
package is meant to work.

## Required Packages

Install the following packages if you don't have them.

``` r
install.packages("dplyr")
install.packages("gt")
install.packages("stringr")
```

Load all libraries

``` r
library(dplyr)
library(gt)
library(stringr)
```

## Data and Additional Variables

This is the data set you will use to make the table

``` r
# Load the data set from dplyr as storms_df
attitude_df <- attitude
attitude_df
```

These are some additional variables/formatting you will need

``` r
# The list of department names to use as row names
department_names <- c(
  "Human_Resources", "Finance", "Marketing", "Sales", "IT",
  "Customer_Service", "Research_and_Development", "Logistics",
  "Operations", "Legal", "Purchasing", "Quality_Assurance",
  "Public_Relations", "Product_Management", "Training",
  "Project_Management", "Compliance", "Administration",
  "Security", "Engineering", "Technical_Support", "Accounting",
  "Business_Development", "Corporate_Strategy", "Investor_Relations",
  "Facilities", "Health_and_Safety", "Procurement", "Data_Analysis", "Innovation"
)

# You will need to format both the row names and colnames using stringr functions
```

## Formatting Notes

The following are all of the functions used to format the table. Check
the documentation online for each to understand how they work

-   `dplyr::filter()`: Select specific rows based on department names.
-   `dplyr::arrange()`: Sort rows by 'Rating' in descending order.
-   `gt()`: Convert the data frame to a gt table.
-   `tab_header()`: Add title and subtitle to the table.
-   `tab_stubhead()`: Label the row names (stub).
-   `tab_spanner()`: Create grouped column headers.
-   `tab_style()`: Apply custom styles to specific parts of the table.
-   `opt_stylize()`: Apply a predefined table style.
-   `opt_table_font()`: Set a custom font for the table.
-   `fmt_percent()`: Format columns as percentages.
-   `tab_footnote()`: Add footnotes to column labels.
-   `tab_source_note()`: Add a source note at the bottom.
-   `data_color()`: Apply color gradients to a column.
-   `grand_summary_rows()`: Add summary rows with averages.
-   `cols_align()`: Center-align all columns.
-   `tab_style()`: Center-align text in the stubhead and grand summary
    cells.

Some additional notes on specific styling values.

-   Formatting on text is done using inline markdown syntax with `md()`,
    you can alternatively use `html()`.
    -   In Markdown, `*text*` is italics and `**text**` is bold.
-   The table has a style added to it using `opt_stylize()` where style
    is 4 and color is cyan.
-   The column with the gradient coloring uses the `data_color()`
    function with a custom palette.
    -   These are the colors
        `palette = c("black", "white", "darkgreen")`
-   The stubhead and the title also have the following formatting.
    -   They are both `v_align = "center"` and `align = "center"`.
    -   They both have the bottom border removed.

Feel free to ask any questions on any item on the table if you are
unsure.

## Submission

The submission will be the code used to generate the graphic and the
image itself. You can save the graphic using the following code.
Remember to add metadata to the top of your submission file.

``` r
gtsave(df_table, filename = "imgs/Graphics_Activity_Two.png", expand=10)
```

### Troubleshooting `gtsave()`

The way that `gtsave()` and a number of other table and graphics
libraries save images as `.png` files is by rendering them first into
html and then taking a screenshot of the render. The `gt` library uses
the `chromote` package for this. The package executes a chromium based
web browser to render the html and to save, if the executive file is not
directed, the saving may not work.

Here's how to fix the issue.

-   Run `chromote::find_chrome()`. If this returns `NULL` it means that
    the path to a browser is not set.
-   Run `usethis::edit_r_environ()` and add a variable called
    `CHROMOTE_CHROME = "path to browser executable\chrome.exe"`.
    -   Adjust the path to the directory of `chrome.exe` or `msedge.exe`
        on your device. If you don't have any chromium based web browser
        you will need to download one.
-   Save the `.Renviron` file Restart your R session.
-   Verify that `chromote::find_chrome()` now returns your executable
    file.
-   Run `gtsave()` again.
