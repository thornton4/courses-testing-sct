---
title: 'Chapter Title Here'
description: 'Chapter description goes here.'
---

## Example coding exercise

```yaml
type: NormalExercise
key: 2bafef99a3
lang: r
xp: 100
skills: 1
```

This is where I can breakdown a more complex SCT that I need to write

`@instructions`
write a successful SCT

`@hint`
I wish I knew what to tell you bud!

`@pre_exercise_code`
```{r}
injury <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/8cca19d0503fcf6e9d30d9cb912de5ba95ecb9c1/MassBI.csv", header = TRUE)
claims <- injury$claims
```

`@sample_code`
```{r}
tail(injury)
injury2 <- subset(injury, claims < 25000 )
summary(injury)
summary(injury2)
par(mfrow = c(1, 2))
hist(claims, freq = FALSE,  main = "Full Data")
hist(injury2$claims, freq = FALSE,  main = "Largest Claim Omitted")  
```

`@solution`
```{r}
tail(injury)
injury2 <- subset(injury, claims < 25000 )
summary(injury)
summary(injury2)
par(mfrow = c(1, 2))
hist(claims, freq = FALSE,  main = "Full Data")
hist(injury2$claims, freq = FALSE,  main = "Largest Claim Omitted") 
```

`@sct`
```{r}
ex() %>% check_function("tail",not_called_msg="Have you used `tail` to view the last 6 observations of the data?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which dataframe you would like to view?") %>% check_equal(incorrect_msg="Make sure to use tail to see the las 6 entries in `injury`.")
ex() %>% check_function("subset",not_called_msg="Have you called `subset` to create a subset of our original data?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified the original data you would like to take a subset from?") %>% check_equal(incorrect_msg="Make sure to create a subset of `injury`.")
ex() %>% check_object("injury2") %>% check_equal(incorrect_msg="Make sure that `injury2` is the same as `injury` but without the largest claim. Try and think of creative ways to remove that observation from the data!")
ex() %>% check_function("summary",index=1,not_called_msg="Have you called `summary` to view basic statistics about the data?") %>% check_arg(., "object",arg_not_specified_msg="Have you specified which data you would like a summary of?") %>% check_equal(incorrect_msg="Make sure to get summary statistics of `injury`.")
ex() %>% chec_function("summary",index=2,not_called_msg="Have you called `summary` to view basic statistics about the data?") %>% check_arg(., "object",arg_not_specified_msg="Have you specified which data you would like a summary of?") %>% check_equal(incorrect_msg="Make sure to get summary statistics of `injury2`.")
ex() %>% check_function("par",not_called_msg="Have you called `par` to change the graphical parameters?") %>% check_arg(., "mfrow", arg_not_specified_msg="Have you specified the number of rows/columns for your plot to have?") %>% check_equal(incorrect_msg="Please dont change this part. it should read `par(mfrow=c(2,1))`")
ex() %>% check_function("hist",index=1,not_called_msg="Have you called `hist` to create a histogram of the data?") %>% {
  check_arg(., "x",arg_not_specified_msg="Have you specified which data should be used to create a histogram?") %>% check_equal(incorrect_msg="Create the first histogram using all of the observed claims.")
  check_arg(., "freq",arg_not_specified_msg="Have you specified that we would like a density histogram?") %>% check_equal(incorrect_msg="Make sure to create a density histogram instead of a frequency histogram.")
}
ex() %>% check_function("hist",index=2,not_called_msg="Have you called `hist` to create a histogram of the data?") %>% {
  check_arg(., "x",arg_not_specified_msg="Have you specified which data should be used to create a histogram?") %>% check_equal(incorrect_msg="Make sure to create the second histogram based on claims with the largest one removed.")
  check_arg(., "freq",arg_not_specified_msg="Have you specified that we would like a density histogram?") %>% check_equal(incorrect_msg="Make sure to create a density histogram instead of a frequency histogram.")
}
success_msg("Congratulations! The goal of predictive modeling is to discover patterns in the data. However, sometimes seeming 'patterns' are the result of one or two unusual observations. Unusual observations may be due to incorrect data gathering procedures or just due to wild fluctuations in a process of interest but are common in predictive modeling.")
```
