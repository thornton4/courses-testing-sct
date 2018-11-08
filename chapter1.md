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
boxplot(claims)
q25 <- quantile(claims, probs = 0.25)
q25
qn25 <- qnorm(p = 0.25, mean = mean(claims), sd = sd(claims))
qn25
qqnorm(claims)
qqline(claims)   
```

`@solution`
```{r}
boxplot(claims)
q25 <- quantile(claims, probs = 0.25)
q25
qn25 <- qnorm(p = 0.25, mean = mean(claims), sd = sd(claims))
qn25
qqnorm(claims)
qqline(claims)   
```

`@sct`
```{r}
ex() %>% check_function("boxplot",not_called_msg="Make sure to use `boxplot` to create a visual representation of the data.") %>% check_arg(., "x", arg_not_specified_msg="Have you specified the data R should use to create the boxplot?") %>% check_equal(incorrect_msg="Please create a boxplot of `claims`.")
ex() %>% check_function("quantile",not_called_msg="Have you called `quantile` to find the empirical percentile?") %>% {
  check_arg("probs",arg_not_specified_msg="Have you specified what empirical percentile we would like to find?") %>% check_equal(incorrect_msg="If we want to find the Yth percentile, make sure to set probs equal to Y in decimal format.")
  check_arg(., "x",arg_not_specified_msg="Have you specified which data R should use to find the 25th empirical percentile?") %>% check_equal(incorrect_msg="Make sure to find the 25th empirical percentile of `claims`.")
ex() %>% check_object("q25",undefined_msg="Make sure to assign the 25th quantile to `q25") %>% check_equal(incorrect_msg="Make sure to find the 25th quantile of claims.")
ex() %>% check_object("qn25",undefined_msg="Make sure to assign the normal value associated with the 25th percentile to qn25") %>% check_equal(incorrect_msg="We can use a normal approximation to solve for qn25 using `qnorm`.")
ex() %>% check_function("qqnorm",not_called_msg="Have you called `qqnorm` to create a normal qq plot?") %>% check_arg(., "y",arg_not_specified_msg="Have you specified which data R should use to create the qq plot?") %>% check_equal(incorrect_msg="Make sure that you are creating a qq-plot for `claims`.")
ex() %>% check_function("qqline",not_called_msg="Have you called `qqline` to overlay a normal line on your qq plot?") %>% check_arg(., "y",arg_not_specified_msg="Have you specified which data R should use to create and plot the line?") %>% check_equal(incorrect_msg="Make sure that you are adding a qq-line for `claims`.")
success_msg("Congratulations on learning about box and qq plots. Although you are unlikely to show these plots to consumers of your analysis, you will find them useful tools as we explore multivariate aspects of data.")
 
```
