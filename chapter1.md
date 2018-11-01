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
Term1$marstat <- as.factor(Term1$marstat)

crossvalfct <- function(explvars){
  cvdata   <- shuffled_Term1[, c("logface", explvars)]
  crossval <- 0
  k <- 5
  for (i in 1:k) {
    indices <- (((i-1) * round((1/k)*nrow(cvdata))) + 1):((i*round((1/k) * nrow(cvdata))))
    # Exclude them from the train set
    train_mlr <- lm(logface ~ ., data = cvdata[-indices,])
    # Include them in the test set
    test  <- data.frame(cvdata[indices, explvars])
    names(test)  <- explvars
    predict_test <- exp(predict(train_mlr, test))
    # Compare predicted to held-out and summarize
    predict_err  <- exp(cvdata[indices, "logface"]) - predict_test
    crossval <- crossval + sum(abs(predict_err))
  }
  crossval/1000000
}
```

`@sample_code`
```{r}
# Randomly re-order data - "shuffle it"
n <- nrow(Term1)
set.seed(12347)
shuffled_Term1 <- Term1[sample(n), ]
# Cross - Validation
explvars.1 <- c("logincome")
crossvalfct(explvars.1)
explvars.2 <- c("education", "numhh", "logincome")
crossvalfct(explvars.2)
explvars.3 <- c("education", "numhh", "logincome", "marstat")
crossvalfct(explvars.3)
```

`@solution`
```{r}
# Randomly re-order data - "shuffle it"
n <- nrow(Term1)
set.seed(12347)
shuffled_Term1 <- Term1[sample(n), ]
# Cross - Validation
explvars.1 <- c("logincome")
crossvalfct(explvars.1)
explvars.2 <- c("education", "numhh", "logincome")
crossvalfct(explvars.2)
explvars.3 <- c("education", "numhh", "logincome", "marstat")
crossvalfct(explvars.3)
```

`@sct`
```{r}
ex() %>% check_object("explvars.1") %>% check_equal()
ex() %>% check_fuction("crossvalfct",index=1) %>% check_arg(., "explvars") %>% check_equal()
ex() %>% check_object("explvars.1") %>% check_equal()  
success_msg("Excellent! This exercises demonstrates the use of cross-validation, a very important technique in model selection. The exercise builds the procedure from the ground up so that you can see all the steps involved. Further, it illustrates how you can develop your own functions to automate procedures and save steps.")
```
