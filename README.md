# STA302-Project
---
title: "STA302"
output: html_document
date: "2024-10-03"
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Loading Data
```{r}
#install.packages('tidyverse')
library(tidyverse)

data <- read_csv("dating_data.csv")

names(data) <- gsub(" ", "_", names(data)) #Changes Spaces to Underlines: 

```

## Add Full names
```{r}

# Adds a new column with the full country name using case_when
data <- data %>%
  mutate(country_full = case_when(
    country == "CH" ~ "Switzerland",
    country == "CA" ~ "Canada",
    country == "DE" ~ "Germany",
    country == "FR" ~ "France",
    country == "US" ~ "United States of America",
    country == "AT" ~ "Austria",
    country == "CZ" ~ "Czech Republic",
    country == "JM" ~ "Jamaica",
    country == "SC" ~ "Seychelles",
    country == "LR" ~ "Liberia",
    country == "BA" ~ "Bosnia and Herzegovina",
    country == "IT" ~ "Italy",
    country == "LI" ~ "Liechtenstein",
    country == "ES" ~ "Spain",
    country == "NL" ~ "Netherlands",
    country == "LU" ~ "Luxembourg",
    country == "AU" ~ "Australia",
    country == "BR" ~ "Brazil",
    country == "RU" ~ "Russia",
    country == "ID" ~ "Indonesia",
    country == "TR" ~ "Turkey",
    country == "GB" ~ "United Kingdom",
    country == "BE" ~ "Belgium",
    country == "ET" ~ "Ethiopia",
    country == "HU" ~ "Hungary",
    country == "AR" ~ "Argentina",
    country == "PE" ~ "Peru",
    country == "UA" ~ "Ukraine",
    country == "IN" ~ "India",
    country == "RO" ~ "Romania",
    country == "PH" ~ "Philippines",
    country == "CF" ~ "Central African Republic",
    TRUE ~ NA_character_  # For any unmatched values, set to NA
  ))

# Print the updated dataset to check
print(data)


```

## Add population
```{r}

# Adds a new column with the population of each country
data <- data %>%
  mutate(country_pop = case_when(
    country == "CH" ~ 8849850,
    country == "CA" ~ 40097760,
    country == "DE" ~ 84482270,
    country == "FR" ~ 68170230,
    country == "US" ~ 334914900,
    country == "AT" ~ 9132380,
    country == "CZ" ~ 10873690,
    country == "JM" ~ 2825540,
    country == "SC" ~ 119770,
    country == "LR" ~ 5418380,
    country == "BA" ~ 3210850,
    country == "IT" ~ 58761150,
    country == "LI" ~ 39580,
    country == "ES" ~ 48373340,
    country == "NL" ~ 17879490,
    country == "LU" ~ 668610,
    country == "AU" ~ 26638540,
    country == "BR" ~ 216422450,
    country == "RU" ~ 143826130,
    country == "ID" ~ 277534120,
    country == "TR" ~ 85326000,
    country == "GB" ~ 68350000,
    country == "BE" ~ 11822590,
    country == "ET" ~ 126527060,
    country == "HU" ~ 9589870,
    country == "AR" ~ 46654580,
    country == "PE" ~ 34352720,
    country == "UA" ~ 37000000,
    country == "IN" ~ 1428627660,
    country == "RO" ~ 19056120,
    country == "PH" ~ 117337370,
    country == "CF" ~ 5742310,
    TRUE ~ NA_real_  # For any unmatched values, set to NA
  ))


names(data) #Provides names of variables

# Print the updated dataset to check
print(data)
```

## Regression Model 1
```{r}

names(data)

# Inital Model with the given predictors
model <- lm(counts_kisses ~ age + counts_pictures + counts_profileVisits + country_pop + genderLooking, data = data)

# Residual vs Fitted plot
x1 = fitted(model)
y1 = resid(model)
plot(x = x1, y = y1, xlab = "Fitted", ylab = "Residual")

# Response Histogram
hist(
  data$counts_kisses, 
  breaks = 100, 
  main = "Reponse Histogram", 
  xlim = c(0, 2000), 
  xlab = "Number of Likes", 
  col = "lightblue"
  )

```


