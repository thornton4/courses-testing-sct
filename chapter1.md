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
#heights <- read.csv("CSVData\\galton_height.csv",header = TRUE)
heights <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/c85ede6c205d22049e766bd08956b225c576255b/galton_height.csv", header = TRUE)
```

`@sample_code`
```{r}
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
pr=pnorm(72, mean = mchild, sd = sdchild
```

`@solution`
```{r}
ht_child <- heights$child_ht
mchild <- mean(ht_child)
sdchild <- sd(ht_child)
pr=pnorm(72, mean = mchild, sd = sdchild
```

`@sct`
```{r}
ex() %>% check_object("ht_child",undefined_msg="Make sure you assign the children's hight to ht_child") %>% check_equal(incorrect_msg="Remember that in order to call a specific column from a dataframe, use the $ operator")
ex() %>% check_object("mchild")  %>% check_equal()
ex() %>% check_object("sdchild") %>% check_equal()
ex() %>% check_object("pr") %>% check_equal()
success_msg("Excellent! With this procedure, you can now calculate probabilities for any distribution using a normal curve approximation.")


```
