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

```

`@sample_code`
```{r}
x=c(10,11,13,16)
x[2:4]-x[1:3]
```

`@solution`
```{r}
x=c(10,11,13,16)
x[2:4]-x[1:3]
```

`@sct`
```{r}
ex() %>% check_output_expr(x[2:4]-x[1:3]) %>% check_equal()
```
