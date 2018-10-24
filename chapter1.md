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
#Term <- read.csv("CSVData\\term_life.csv", header = TRUE)
Term <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/efc64bc2d78cf6b48ad2c3f5e31800cb773de261/term_life.csv", header = TRUE)
Term1 <- subset(Term, subset = face > 0)
Term2 <- Term1[, c("education", "face", "income", "logface", "logincome", "numhh")]
```

`@sample_code`
```{r}
Term2$face <- exp(Term2$logface)/1000
Term2$income <- exp(Term2$logincome)/1000
Term_mlr1 <- lm(face ~ education + numhh + income, data = Term2)
summary(Term_mlr1)
```

`@solution`
```{r}
Term2$face <- exp(Term2$logface)/1000
Term2$income <- exp(Term2$logincome)/1000
Term_mlr1 <- lm(face ~ education + numhh + income, data = Term2)
summary(Term_mlr1)
```

`@sct`
```{r}
ex() %>% check_object("Term2") %>% {
  check_column(., "face") %>% check_equal()
  check_column(., "income") %>% check_equal()
 }
```
