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
#Lot <- read.csv("CSVData\\Wisc_lottery.csv", header = TRUE)
Lot <- read.csv("https://assets.datacamp.com/production/repositories/2610/datasets/a792b30fb32b0896dd6894501cbab32b5d48df51/Wisc_lottery.csv", header = TRUE)
```

`@sample_code`
```{r}
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
summary(Lot)
plot(Lot$pop_1000, Lot$sales_1000)
cor(Lot$pop_1000, Lot$sales_1000)
```

`@solution`
```{r}
Lot$pop_1000 <- Lot$pop/1000
Lot$sales_1000 <- Lot$sales/1000
summary(Lot)
plot(Lot$pop_1000, Lot$sales_1000)
cor(Lot$pop_1000, Lot$sales_1000)
```

`@sct`
```{r}
ex() %>% check_object("Lot") %>% {
  check_column(., "pop_1000") %>% check_equal()
  check_column(., "sales_1000") %>% check_equal()
}
ex() %>% check_function("summary") %>% check_result() %>% check_equal()
ex() %>% check_function("plot") %>%{
  check_arg(., "x") %>% check_equal()
  check_arg(., "y") %>% check_equal()
}
ex() %>% check_function("cor") %>% check_result() %>% check_equal()
success_msg("Congratulations! We will rescale data using 'linear' transformations regularly. In part we do this for communicating our analysis to others. Also in part, this is for our own convenience as it can allow us to see patterns more readily.")
```
