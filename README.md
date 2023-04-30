# Sports Analytics

## Course Description:
This course serves as an introduction to sports analytics. Analytical topics will include, but are not limited to, regression (or
predictive) modeling, optimization, ranking methodologies, web scraping, among others. Sports topics will include topics from
most professional sports, gambling (daily fantasy sports), and business operations. In addition, the students will learn how to
communicate their results (business reports, dashboards, etc.) of the varioius modeling exercises and projects using RStudio
and the RMarkdown suite of tools.

## Learning Outcomes:
Performed statistical analysis and create various graphs to present findings.

## Software:
- [R](https://www.r-project.org/about.html)
- [R Studio](https://posit.co/products/open-source/rstudio/)
- R Packages Implimented 
  - **ggplot2**: ggplot2 is a popular data visualization package in R. It provides a powerful and flexible grammar of graphics for creating high-quality plots. The package allows users to create a wide range of visualizations, including scatter plots, bar charts, line graphs, and more. It is highly customizable and follows the layered approach to building plots. [Official website](https://ggplot2.tidyverse.org/)
  - **dplyr**: dplyr is a package for data manipulation and transformation in R. It provides a set of functions that simplify the process of filtering, selecting, arranging, summarizing, and joining data frames. With dplyr, users can perform common data manipulation tasks using intuitive and expressive syntax. It is widely used for data wrangling and exploratory data analysis. [Official website](https://dplyr.tidyverse.org/)
- **janitor**: janitor is a package that helps clean messy data sets. It provides functions to clean column names, remove empty rows or columns, convert data types, and handle missing values. janitor is particularly useful when dealing with data that has inconsistent naming conventions or formatting issues. It simplifies the process of tidying data and preparing it for further analysis. [Official website](https://sfirke.github.io/janitor/)
- **rvest**: rvest is an R package for web scraping. It allows users to extract data from HTML web pages by parsing the underlying structure of the page. With rvest, users can retrieve specific elements, such as tables or text, from web pages and convert them into usable data frames. It is a valuable tool for gathering data from websites for analysis or research purposes. [Official website](https://rvest.tidyverse.org/)
- **xml2**: xml2 is an R package for working with XML and HTML data. It provides functions for parsing XML and HTML documents, navigating their structure, and extracting information. xml2 allows users to access specific elements or attributes within XML/HTML files and manipulate the data as needed. It is commonly used for web scraping, data extraction, and processing XML-based data. [Official website](https://xml2.r-lib.org/)


## Final Exam Grade 98%


### Data Source:
NBA Provided by the professor, taken from [NBA.com](NBA.com/stats)
### Exam Highlights:
- Compute the average offensive rating by team for this data set
```r
nba_stats <- readRDS("nba_stats.rds")
average_team_offrating <- nba_stats %>%
dplyr::group_by(team_name)%>%
dplyr::mutate(off_rating = as.numeric(off_rating)) %>%
dplyr::summarize(mean(off_rating))
average_team_offrating
```

## Topic 2

### Data Source:

### Exam Highlights: 
-
