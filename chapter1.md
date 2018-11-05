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
#meps <- read.csv("CSVData\\HealthMeps.csv", header = TRUE)
meps <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/7b7dab6d0c528e4cd2f8d0e0fc7824a254429bf8/HealthMeps.csv", header = TRUE)
```

`@sample_code`
```{r}
str(meps)
summary(meps)
table(meps$race)
par(mfrow = c(1, 2))
hist(meps$expendop, main = "", xlab = "outpatient expenditures")
hist(log(meps$expendop), main = "", xlab = "log expenditures")
par(mfrow = c(1, 1))
meps$logexpend <- log(meps$expendop)
boxplot(logexpend ~ phstat, data = meps, main = "boxplot of log expend")
plot(meps$age,meps$logexpend, xlab = "age", ylab = "log expend")
lines(lowess(meps$age, meps$logexpend), col="red")
```

`@solution`
```{r}
str(meps)
summary(meps)
table(meps$race)
par(mfrow = c(1, 2))
hist(meps$expendop, main = "", xlab = "outpatient expenditures")
hist(log(meps$expendop), main = "", xlab = "log expenditures")
par(mfrow = c(1, 1))
meps$logexpend <- log(meps$expendop)
boxplot(logexpend ~ phstat, data = meps, main = "boxplot of log expend")
plot(meps$age,meps$logexpend, xlab = "age", ylab = "log expend")
lines(lowess(meps$age, meps$logexpend), col="red")
```

`@sct`
```{r}
ex() %>% check_function("str") %>% check_arg(., "object") %>% check_equal()
ex() %>% check_function("summary") %>% check_arg(., "object") %>% check_equal()
ex() %>% check_function("table") %>% check_result() %>% check_equal()
ex() %>% check_function("par",index=1) %>% check_arg(., "mfrow") %>% check_equal()
ex() %>% check_function("hist",index=1) %>% check_arg(., "x") %>% check_equal()
ex() %>% check_function("hist",index=2) %>% check_arg(., "x") %>% check_equal()
ex() %>% check_function("par",index=2) %>% check_arg(., "mfrow") %>% check_equal()
ex() %>% check_object("meps") %>% check_column("logexpend") %>% check_equal()
ex() %>% check_function("boxplot") %>% {
  check_arg(., "formula") %>% check_equal()
  check_arg(., "data") %>% check_equal()
}
ex() %>% check_function("plot") %>% {
  check_arg(., "x") %>% check_equal()
  check_arg(., "y") %>% check_equal()
}
ex() %>% check_function("lines") 
ex() %>% check_function("lowess") %>% {
  check_arg(., "x") %>% check_equal()
  check_arg(., "y") %>% check_equal()
}
success_msg("Excellent! Summarizing data, without reference to a model, is probably the most time-consuming part of any predictive modeling exercise. Summary statistics are also a key part of any report as they illustrate features of the data that are accessible to a broad audience.")

```
