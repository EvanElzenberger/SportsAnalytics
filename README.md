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
