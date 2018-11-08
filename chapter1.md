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
#heights <- read.csv("CSVData\\galton_height.csv",header = TRUE)
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
```

`@sample_code`
```{r}
hist(ht_child, freq = FALSE)
x <- seq(60, 80,by = 0.1)
lines(x, dnorm(x, mean = mchild, sd = sdchild), col = "blue")
prob <- 1 - pnorm(72, mean = mchild , sd = sdchild)
prob
```

`@solution`
```{r}
hist(ht_child, freq = FALSE)
x <- seq(60, 80,by = 0.1)
lines(x, dnorm(x, mean = mchild, sd = sdchild), col = "blue")
prob <- 1 - pnorm(72, mean = mchild , sd = sdchild)
prob
```

`@sct`
```{r}
ex() %>% check_function("hist",not_called_msg="Use the hist command to create a histogram of the children's heights.") %>% {
  check_arg(., "x",arg_not_specified_msg="Have you specified what data to make a histogram from?") %>% check_equal(incorrect_msg="Make sure to create a histogram of the children's heights.")
  check_arg(., "freq",arg_not_specified_msg="Have you specified that you would like a density histogram?") %>% check_equal(incorrect_msg="Make sure to create a density histogram instead of a frequency histogram.")
}
ex() %>% check_function("lines",not_called_msg="Please use the lines function to overlay a normal curve on your histogram") %>% {
  check_arg(., "x",arg_not_specified_msg="Have you specified the independant variable correctly?") %>% check_equal(incorrect_msg="Remeber that we are interested in how probability changes as our value of x changes!")
  check_Arg(., "y",arg_not_specified_msg="Have you specified the dependant variable correctly?") %>% check_equal(incorrect_msg="Remeber that we are interested in how probability changes as our value of x changes!")
}
ex() %>% check_object("prob", undefined_msg="Make sure to assign the probability of a child's height being greater than 72 inches to prob.") %>% check_equal(incorrect_msg="Make sure to find the probability of a child's height being GREATER than 72 inches.")
success_msg("Excellent! Visualizing a distribution, especially with reference to a normal, is important for communicating results of your analysis.")

```
