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
You can extract the residuals from a regression object with the function [residuals()].

`@pre_exercise_code`
```{r}
#Lot <- read.csv("CSVData\\Wisc_lottery.csv", header = TRUE)
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```

`@sample_code`
```{r}
model_blr <-lm(sales ~ pop, data = Lot)
summary(model_blr)
model_Kenosha <- lm(sales ~ pop, data = Lot, subset = -c(9))
summary(model_Kenosha)

plot(Lot$pop, Lot$sales, xlab = "population", ylab = "sales")
text(5000, 24000, "Kenosha")
abline(model_blr, col="blue")
abline(model_Kenosha, col="red")

par(mfrow = c(1, 2))
qqnorm(residuals(model_blr), main = "")
qqline(residuals(model_blr))
qqnorm(residuals(model_Kenosha), main = "")
qqline(residuals(model_Kenosha))
```

`@solution`
```{r}
model_blr <-lm(sales ~ pop, data = Lot)
summary(model_blr)
model_Kenosha <- lm(sales ~ pop, data = Lot, subset = -c(9))
summary(model_Kenosha)

plot(Lot$pop, Lot$sales, xlab = "population", ylab = "sales")
text(5000, 24000, "Kenosha")
abline(reg=model_blr, col="blue")
abline(reg=model_Kenosha, col="red")

par(mfrow = c(1, 2))
qqnorm(residuals(model_blr), main = "")
qqline(residuals(model_blr))
qqnorm(residuals(model_Kenosha), main = "")
qqline(residuals(model_Kenosha))
```

`@sct`
```{r}
ex() %>% check_object("model_blr",undefined_msg="Make sure to name the first regression model `model_blr`.") %>% check_equal(incorrect_msg="This has already been done for you, please don’t change it. ")
ex() %>% check_function("lm",index=1,not_called_msg="Use `lm` to create the linear model for `model_blr`.") %>% {
  check_arg(., "formula") %>% check_equal(incorrect_msg="Make sure to model `sales` based on `pop`.")
  check_arg(., "data") %>% check_equal(incorrect_msg="Make sure to specify the dataframe we are using, `Lot`.")
}
ex() %>% check_function("summary", index=1,not_called_msg="run `summary` on `model_blr`.") %>% check_arg(., "object") %>% check_equal(incorrect_msg="Make sure to specify that we want the summary of `model_blr`.")
ex() %>% check_function("summary", index=1) %>% check_result() %>% check_equal()
ex() %>% check_object("model_Kenosha", undefined_msg="Name the result of a `lm` excluding Kenosha `model_Kenosha`.") %>% check_equal(incorrect_msg="Make sure to exclude observation 9. ")
ex() %>% check_function("lm", index=2,not_called_msg="Create a linear model excluding the Kenosha observation. ") %>% {
  check_arg(., "formula") %>% check_equal(incorrect_msg="Make sure to specify that we want to base `sales` on `pop`.")
  check_arg(., "data") %>% check_equal(incorrect_msg="Make sure to specify that our data is from the dataframe `Lot`.")
  check_arg(., "subset") %>% check_equal(incorrect_msg="Make sure to remove the Kenosha observation from the data. Kenosha is observation 9. ")
}
ex() %>% check_function("summary", index=2,not_called_msg="Look at the summary stats of `model_Kenosha` using `summary`.") %>% check_arg(., "object") %>% check_equal(incorrect_msg="Make sure to specify we want summary stats of `model_Kenosha`." )
ex() %>% check_function("summary", index=2) %>% check_result() %>% check_equal()
ex() %>% check_function("plot", not_called_msg="Create a plot of population vs sales from the full data. ") %>% {
  check_arg(., "x") %>% check_equal(incorrect_msg="The x variable should be all of the population observations. ")
  check_arg(., "y") %>% check_equal(incorrect_msg="They y variable should be all of the sales observations. ")
}
ex() %>% check_function("abline",index=1,not_called_msg="plot the regression of `model_blr` using `abline`.") %>% check_arg(., "reg") %>% check_equal(incorrect_msg="The first line should be for `model_blr`.")
ex() %>% check_function("abline",index=2,not_called_msg="plot the regression of `model_Kenosha` using `abline`.") %>% check_arg(., "reg") %>% check_equal(incorrect_msg="The second line should be for `model_Kenosha`.")
ex() %>% check_function("par",not_called_msg="Set up the plotting window so it has 2 graphs using `par`.") %>% check_arg(., "mfrow") %>% check_equal(incorrect_msg="Make sure to create 2 side-by-side graphs! ")
ex() %>% check_function("qqnorm",index=1,not_called_msg="Create a qq-plot for `model_blr` using `qqnorm`.") %>% check_arg(., "y") %>% check_equal(incorrect_msg="The first graph should be for `model_blr`.")
ex() %>% check_function("qqline",index=1,not_called_msg="Add a qq-line to the graph for `model_blr`.") %>% check_arg(., "y") %>% check_equal(incorrect_msg="The first line should be for `model_blr`.")
ex() %>% check_function("qqnorm",index=2,not_called_msg="Create a qq-plot for `model_Kenosha` using `qqnorm`.") %>% check_arg(., "y") %>% check_equal(incorrect_msg="The second graph should be for `model_Kenosha`.")
ex() %>% check_function("qqline",index=2, not_called_msg="Add a qq-line to the graph for `model_Kenosha`.") %>% check_arg(., "y") %>% check_equal(incorrect_msg="The second line should be for `model_Kenosha`.")
success_msg("Congratulations! Just because an observation is unusual does not make it bad or noninformative. Kenosha is close to the Illinois border; residents from Illinois probably participate in the Wisconsin lottery thus effectively increasing the potential pool of sales in Kenosha. Although unusual, there is interesting information to be learned from this observation.")
```
