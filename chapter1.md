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
O=c(5,4,8,2,9,3,5)
E=c(4,6,8,4,8,1,7)
data.chisq=data.frame(O,E)
```

`@sample_code`
```{r}
data.chisq$O.E=data.chisq$O-data.chisq$E
data.chisq$sq=data.chisq$O.E^2
data.chisq$chisq=data.chisq$sq/data.chisq$E
```

`@solution`
```{r}
data.chisq$chisq=((data.chisq$O-data.chisq$E)^2)/data.chisq$E
```

`@sct`
```{r}
ex() %>% check_object("data.chisq") %>% check_column(., "chisq") %>% check_equal()
success_msg="yaaas"
```
