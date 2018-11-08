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
logclaims <- log(claims)
hist(logclaims , breaks = 40,freq = FALSE)
box()
plot(density(logclaims))
plot(density(logclaims, bw = 0.03))
```

`@solution`
```{r}
logclaims <- log(claims)
hist(logclaims , breaks = 40,freq = FALSE)
box()
plot(density(logclaims))
plot(density(logclaims, bw = 0.03))
```

`@sct`
```{r}
ex() %>% check_object("logclaims",undefined_msg="Make sure to assign the log of the claims data to `logclaims`.") %>% check_equal(incorrect_msg = "You made an error in the definition of the logarithmic claims. Check out the definition of the log() function.")
ex() %>% check_function("hist",not_called_msg="Make sure to use `hist` to create a histogram.") %>% {
  check_arg(., "x",arg_not_specified_msg="Did you assign x to be the log of our claims data?") %>% check_equal(incorrect_msg="Please create a histogram of logclaims.")
  check_arg(., "freq",arg_not_specified_msg="Did you specify that we would like a density histogram?") %>% check_equal(incorrect_msg="Please create a density histogram instead of a frequency histogram.")
  check_arg(., "breaks",arg_not_specified_msg="Did you specify the number of breaks we would like in our histogram?") %>% check_equal(incorrect_msg="Make sure to set breaks equal to 40!")
}
ex() %>% check_function("box",not_called_msg="Make sure to call `box` in order to create a decorative box around our histogram!")
ex() %>% check_function("plot",index=1,not_called_msg="Have you plotted the density of the log of claims?") %>% check_arg("x",arg_not_specified_msg="Have you specified the data we should use to create the plot?") %>% check_equal(incorrect_msg="Use the density function to plot the density of logclaims.")
ex() %>% check_function("plot",index=2,not_called_msg="Create another plot using `plot` that displays the density of logarithmic claims with a binwidtch of 0.03.") %>% {
  check_arg(., "x",arg_not_specified_msg="Have you specified the data we should use to create the plot?") %>% check_equal(incorrect_msg="Use the density function to plot the density of logclaims.")
  check_arg(., "bw",arg_not_specified_msg="Have you specified that our new binwidth?") %>% check_equal(incorrect_msg="While any value of binwidth is fine, please use a binwidth of 0.03 to see the imapct!")
success_msg("Excellent! Visualizing the distribution is important and smoothing techniques allow viewers to see important patterns without being distracted by random fluctations.")

```
