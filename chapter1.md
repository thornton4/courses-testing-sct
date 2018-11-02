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
meps$logexpend <- log(meps$expendop)
```

`@sample_code`
```{r}
n <- nrow(meps)
set.seed(12347)
shuffled_meps <- meps[sample(n), ]
train_indices <- 1:round(0.75 * n)
train_meps    <- shuffled_meps[train_indices, ]
test_indices  <- (round(0.25 * n) + 1):n
test_meps     <- shuffled_meps[test_indices, ]
meps_mlr1 <- lm(expendop ~ gender + age + race + region + educ + phstat + mpoor + anylimit + income + insure + usc + unemploy + managedcare, data = train_meps)
summary(meps_mlr1)
par(mfrow = c(2, 2))
plot(meps_mlr1)
```

`@solution`
```{r}
n <- nrow(meps)
set.seed(12347)
shuffled_meps <- meps[sample(n), ]
train_indices <- 1:round(0.75 * n)
train_meps    <- shuffled_meps[train_indices, ]
test_indices  <- (round(0.25 * n) + 1):n
test_meps     <- shuffled_meps[test_indices, ]
meps_mlr1 <- lm(expendop ~ gender + age + race + region + educ + phstat + mpoor + anylimit + income + insure + usc + unemploy + managedcare, data = train_meps)
summary(meps_mlr1)
par(mfrow = c(2, 2))
plot(meps_mlr1)
```

`@sct`
```{r}
ex() %>% check_function("plot") %>% check_result() %>% check_equal()
```
