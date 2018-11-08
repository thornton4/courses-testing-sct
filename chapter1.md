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
par(mfrow = c(2, 2))
plot(density(claims))    
plot(density(claims^(0.5)))  
plot(density(log(claims)))  
plot(density(-claims^(-1)))  
```

`@solution`
```{r}
par(mfrow = c(2, 2))
plot(density(claims))    
plot(density(claims^(0.5)))  
plot(density(log(claims)))  
plot(density(-claims^(-1))) 
```

`@sct`
```{r}
ex() %>% check_function("par",not_called_msg="Have you called `par` to change the graphical parameters?") %>% check_arg(., "mfrow", arg_not_specified_msg="Have you specified the number of rows/columns for your plot to have?") %>% check_equal(incorrect_msg="Please dont change this part. it should read `par(mfrow=c(2,2))`")

ex() %>% check_function("plot",index=1,not_called_msg="Did you plot the density of claims?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which data should be plotted?") %>% check_equal(incorrect_msg="Make sure to create the first histogram using `claims`")

ex() %>% check_or(
check_function(.,"plot",index=2,not_called_msg="did you plot the square root of claims?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which data should be plotted?") %>% check_equal(incorrect_msg="Make sure to create the second histogram based on the square root of `claims`."),
  override_solution(.,"plot(density(sqrt(claims)))") %>% check_function("plot",not_called_msg="did you plot the square root of claims?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which data should be plotted?") %>% check_equal(incorrect_msg="Make sure to create the second histogram based on the square root of `claims`.")
)

ex() %>% check_function("plot",index=3,not_called_msg="Did you plot the density of logarithmic claims?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which data should be plotted?") %>% check_equal(incorrect_msg="Make sure to create the third histogram based on the natural log of `claims`.")

ex() %>% check_function("plot",index=4,not_called_msg="Did you plot the density of the negative reciprocal of claims?") %>% check_arg(., "x",arg_not_specified_msg="Have you specified which data should be plotted?") %>% check_equal(incorrect_msg="Make sure to create the fourth histogram based on the negative reciprocal () of `claims`.")

success_msg("Excellent! Transformations of data is a tool that incredibly expands potential applicability of (linear) regression techniques.")
```
