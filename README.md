# google_trends
Few examples at pulling Google Trend data using the gtrends package in R


``` r
# ---- set up ----- 
library(gtrendsR)   # easy acces to google trends
library(tidyverse)  # data manipulation and plotting
library(gganimate)  # animating the plot

# ---- data ----
# data pull
g_trend <-  gtrends(
  keyword = c("jordan", "potato"), # key terms to compare
  geo = "US",                      # location 
  time = "today+5-y"               # time span
  )

# ----- interest over time
g_trend_df <- g_trend$interest_over_time

# plot
p <- ggplot(
    data = g_trend_df
  , aes(x = as.Date(date),y = hits, group = keyword, color = keyword)) + 
  geom_line(size = 1.5) + 
  expand_limits(y = c(0,100)) + 
  scale_y_continuous(breaks=seq(0, 100, by=20)) +
  scale_x_date(date_breaks = "1 year", date_labels = "%Y") + 
  theme_minimal() +
  theme(
    plot.title = element_text(size=16, face="bold"),
    axis.title = element_text(size=11, face="bold"),
    axis.title.x = element_blank(),
    axis.text.x = element_text( angle = 45, hjust = 1),
    axis.text = element_text(size=10, face = "bold"),
    legend.title = element_blank(),
    legend.key = element_rect(color = "grey50"),
    legend.key.width = unit(.55,"cm"),
    legend.key.height = unit(.55,"cm"),
    legend.position = "bottom",
    legend.text = element_text(face = "bold")
  ) + 
  labs(
    title = "Jordan vs Potato",
    y = "'Popularity'",
    x = "",
    caption = "*Data pulled from Google Trends"
  )

# printing plot
p
```

![GitHub Logo](/plots_gifs/popularity.png)

