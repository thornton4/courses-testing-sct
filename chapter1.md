---
title: 'Chapter Title Here'
description: 'Chapter description goes here.'
free_preview: true
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

```

`@sample_code`
```{r}
lm(hp~mpg, data=mtcars)
```

`@solution`
```{r}
lm(hp~mpg, data=mtcars)
```

`@sct`
```{r}
ex() %>% check_function("lm") %>% {
  check_arg(., "formula") %>% check_equal()
  check_arg(., "data") %>% check_equal()
}
success_msg="yaaas"
```
