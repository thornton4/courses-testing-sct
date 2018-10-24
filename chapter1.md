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
Term4 <- Term1[,c("numhh", "education", "logincome", "marstat", "logface")]
Term4$single <- 1*(Term4$marstat == 0)
```

`@sample_code`
```{r}
round(cor(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```

`@solution`
```{r}
round(cor(Term4[,c("numhh", "education", "logincome", "single", "logface")]), digits = 3)
Term_mlr3 <- lm(logface ~ education + numhh + logincome + single, data = Term4)
summary(Term_mlr3)
Term_mlr4 <- lm(logface ~ education + numhh + logincome + single + single*logincome, data = Term4)
summary(Term_mlr4)
```

`@sct`
```{r}
ex() %>% check_function("round") %>% check_result() %>% check_equal()
ex() %>% check_object("Term_mlr3") %>% check_equal()
ex() %>% check_function("lm",index=1) %>% {
  check_arg(., "formula") %>% check_equal()
  check_arg(., "data") %>% check_equal()
}
ex() %>% check_function("summary",index=1) %>% check_result() %>% check_equal()
ex() %>% check_object("Term_mlr4") %>% check_equal()
ex() %>% check_function("lm",index=2) %>% {
  check_arg(., "formula") %>% check_equal()
  check_arg(., "data") %>% check_equal()
}
ex() %>% check_function("summary",index=2) %>% check_result() %>% check_equal()
```
