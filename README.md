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
  - **SportyR**: sportyR is an R package that provides various functions and datasets for sports analytics. It offers tools for collecting, cleaning, analyzing, and visualizing sports data. [Offical website](https://github.com/sportsdataverse/sportyR)
  - nhlapi is an R package that provides functions to access data from the NHL API. It allows users to retrieve various types of data related to NHL games, teams, players, and statistics.
  - **Purrr**: purrr is an R package that enhances functional programming and iteration in R. It provides a consistent and intuitive toolkit for working with functions and vectors. It is particularly useful for working with lists and applying functions to multiple elements.
  -  **Plotly**: plotly is an R package that provides an interface to the Plotly JavaScript graphing library. It allows users to create interactive and dynamic visualizations in R, including scatter plots, bar charts, line graphs, and more.
  -  **MGCV**: mgcv is an R package that provides tools for fitting generalized additive models (GAMs) and generalized additive mixed models (GAMMs). It extends the functionality of the base R package gam and offers additional features for modeling and visualizing smooth nonlinear relationships.


## Final Project Grade 100%

### Data Source: 
NHL data was scraped using the NHL api

### Exam Highlights: 
- I wanted to create a heat map for the Avalanche goals scored. 
```r
##Scrape Data
games <- nhlapi::nhl_schedule_seasons(seasons = 2021, teamIds = 21)[[1]]$dates
##Mutate Data
game_ids <- dplyr::bind_rows(games$games) %>% 
  dplyr::pull(gamePk)
all_game_feeds <- lapply(game_ids, nhlapi::nhl_games_feed)
plays <- purrr::map_df(all_game_feeds,
                       function(x){
                         return(x[[1]][["liveData"]][["plays"]][["allPlays"]])
                       }) %>%
        dplyr::filter(., result.event %in% c("Shot", "Missed Shot", "Blocked Shot", "Goal"))%>%
        dplyr::mutate(., goal = ifelse(result.event == "Goal", T, F)) %>%
        dplyr::mutate(., x.coordinate = -abs(coordinates.x))

##Run Gam Model
goals_gam <- gam(goal ~ s(x.coordinate) + s(coordinates.y),
family = binomial,
data = plays)

##Create Graph
y <- seq(-42,42, length = 50)
x <- seq(-98, 0, length = 50)

plays_predict_data <- expand.grid(x.coordinate = x,
                                  coordinates.y = y)
goal_prob <- predict(goals_gam, plays_predict_data, type = "response")
plays_predict_data <- mutate(plays_predict_data, goal_prob = goal_prob)

p <- geom_hockey('nhl', display_range = "offense")
p + geom_tile(data = plays_predict_data,
aes(x = x.coordinate , y = coordinates.y, fill = goal_prob), alpha = .5) +
scale_fill_distiller("prob", palette = "Spectral",
direction = -1,
limit = c(0,.125)) +
coord_fixed() +
labs(
title = "Goals")
```
![HeatmapAvsGoals](https://user-images.githubusercontent.com/121822843/235511735-7a576c71-ffe0-41a1-bbf7-9564b575f788.png)

## Final Exam Grade 98%


### Data Source:
NBA Provided by the professor, taken from [NBA.com](NBA.com/stats)

### Exam Highlights:

- Basketball
  - Compute the average offensive rating by team for this data set
```r
nba_stats <- readRDS("nba_stats.rds")
average_team_offrating <- nba_stats %>%
dplyr::group_by(team_name)%>%
dplyr::mutate(off_rating = as.numeric(off_rating)) %>%
dplyr::summarize(mean(off_rating))
average_team_offrating
```
- Football
  - Construct a desnisty plot showing the starting field position distribution for all plays immediately after a kickoff. What value appears to be the mode of this distribution?
 ``` r
kickoffs <- which(nfl_stats$play_type == "kickoff")
kickoff_df <- nfl_stats[kickoffs + 1, ]
p <- ggplot(data = kickoff_df,
            aes(x = yardline_100))
p+ geom_density()
```
- Hockey
  - Create a player link and scape NHL stats
 ```r
 scrape_nhl_player_stats <- function(player_link, 
                                    type = "basic", 
                                    career = FALSE){
  ...
}
MacKinnon_stats <- scrape_nhl_player_stats(MacKinnon_url, type = "advanced", career = FALSE)
McDavid_stats <- scrape_nhl_player_stats(McDavid_url, type = "advanced", career = FALSE)
df_advanced <- bind_rows(MacKinnon_stats, McDavid_stats)
```
  - Plot the player trajectory curves for each player showing Corsi percentage as a function of age. Overlay these curves on the same figure
```r
p <- ggplot(data = df_advanced,
            aes(x = as.numeric(age), y = as.numeric(cf_percent),
            col = team))
p + geom_smooth() +
  scale_color_brewer("", palette = "Set1") +
  labs(x = "age",
       y = "Corsi Percentage")
```
