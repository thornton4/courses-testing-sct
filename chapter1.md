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
sum(c(1, 2, 3, 4, NA), na.rm = TRUE)
```

`@solution`
```{r}
sum(c(1, 2, 3, 4, NA), na.rm = TRUE)
```

`@sct`
```{r}
ex() %>% check_output_expr("10", missing_msg = "Did you correctly print out the sum?")
```
