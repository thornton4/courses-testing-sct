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
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
```

`@sample_code`
```{r}
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(model_blr1)
sqrt(anova(model_blr1)$Mean[2])
summary(model_blr1)$r.squared
model_blr2 <- lm(sales_1000  ~ pop_1000 , data = Lot)
anova(model_blr2)
sqrt(anova(model_blr2)$Mean[2])
summary(model_blr2)$r.squared
```

`@solution`
```{r}
model_blr1 <- lm(sales_1000  ~ pop, data = Lot)
anova(model_blr1)
sqrt(anova(model_blr1)$Mean[2])
summary(model_blr1)$r.squared
model_blr2 <- lm(sales_1000  ~ pop_1000 , data = Lot)
anova(model_blr2)
sqrt(anova(model_blr2)$Mean[2])
summary(model_blr2)$r.squared
```

`@sct`
```{r}
ex() %>% check_object("model_blr1",undefined_msg="Please name the first regression model `model_blr1`.") %>% check_equal(incorrect_msg="please don’t change this step, it should read: ` model_blr1 <- lm(sales_1000  ~ pop, data = Lot)`.")
ex() %>% check_function("anova",index=1,not_called_msg="Use `anova` to summarize the fit of `model_blr1`." ) %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify that we want to run `anova` on `model_blr1`.")
ex() %>% check_function("sqrt",index=1,not_called_msg="Make sure to take the square root in order to find `s`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure that you are taking the square root of the second argument of the mean found using `anova`.")
ex() %>% check_function("anova",index=2,not_called_msg="make sure to run `anova` on `model_blr1`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify that we would like to run `anova` on `model_blr1`.")
ex() %>% check_function("summary",index=1, not_called_msg="Use `summary` to find the summary stats on `model_blr1`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify we want the r-squared value from our model.")
ex() %>% check_object("model_blr2", "undefined_msg=”Please name the first regression model `model_blr2`.") %>% check_equal(incorrect_msg="Make sure to create `model_blr2` such that `sales_1000` is based on `pop_1000`.")
ex() %>% check_function("lm",index=2,not_called_msg="make sure to use `lm` to create a regression model.") %>% {
  check_arg(., "formula") %>% check_equal(incorrect_msg="make sure to specify we would like `sales_1000` to be based on `pop_1000`.")
  check_arg(., "data") %>% check_equal(incorrect_msg="make sure to specify that our data is from the dataframe `Lot`.")
}
ex() %>% check_function("anova",index=3,not_called_msg="Use `anova` to summarize the fit of `model_blr2`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify that we want to run `anova` on `model_blr2`.")
ex() %>% check_function("sqrt",index=2,not_called_msg="Make sure to take the square root in order to find `s`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure that you are taking the square root of the second argument of the mean found using `anova`.")
ex() %>% check_function("anova",index=4, not_called_msg="make sure to run `anova` on `model_blr2`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify that we would like to run `anova` on `model_blr2`.")
ex() %>% check_function("summary",index=2, not_called_msg="Use `summary` to find the summary stats on `model_blr2`.") %>% check_result() %>% check_equal(incorrect_msg="Make sure to specify we want the r-squared value from our model.")
success_msg("Congratulations! In this exercise, you have seen that rescaling does not affect our measures of goodness of fit in any meaningful way. For example, coeffcient of determinations are completely unaffected. This is helpful because we will rescale variables extensively in our search for patterns in the data.")
```
