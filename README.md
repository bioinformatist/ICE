
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ICE

<!-- badges: start -->

<!-- badges: end -->

ICE (**I**mpute **C**ircRNA **E**xpression) is designed for imputing
circRNA expression using PCGs (protein-coding genes).

## Installation

> Currently bundled example data may be huge in size. One could try use
> proxy and pull it first.

``` r
remotes::install_github("bioinformatist/ICE")
```

## Quick start

### `library()` package and load example data

``` r
library(ICE)
data("mionco.circ")
data("mionco.pcg")
```

### Perform cross-validation analysis to determine the expected accuracy of imputing a circRNA of interest using the training datasets

``` r
(cv.circ <- ICE_cv(train.pcg = mionco.pcg, train.circ = mionco.circ, gene.index="hsa_circ_0000801"))
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#>             PCC      P-Value      RMSE
#>  [1,] 0.3593281 7.884782e-04  8.729384
#>  [2,] 0.3264386 2.441395e-03 12.647389
#>  [3,] 0.5119432 6.444677e-07  9.898483
#>  [4,] 0.4611714 1.010764e-05 11.491493
#>  [5,] 0.4698115 6.523424e-06  8.570688
#>  [6,] 0.2335763 3.248762e-02  6.581966
#>  [7,] 0.4055682 1.295863e-04  5.622876
#>  [8,] 0.4702542 6.376640e-06  9.019864
#>  [9,] 0.3617744 7.213418e-04  9.110699
#> [10,] 0.4553113 1.351237e-05  7.014257
```

### Perform cross-validation analysis to determine the expected imputation accuracy of entire circRNA dataset

``` r
# Use a small part of example circRNA expression data
sample.sub <- sample(rownames(mionco.pcg), size = 100)
cv.full <- ICE_cv_entire(train.pcg = mionco.pcg[sample.sub, ], train.circ = mionco.circ[sample.sub, 1:300])
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 1
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 2
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 3
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 4
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 5
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 6
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 7
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 8
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 9
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 10
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 11
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 12
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 13
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 14
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 15
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 16
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 17
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 18
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 19
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 20
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 21
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 22
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 23
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 24
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 25
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 26
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 27
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 28
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 29
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 30
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 31
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 32
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 33
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 34
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 35
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 36
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 37
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 38
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 39
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 40
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 41
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 42
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 43
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 44
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 45
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 46
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 47
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 48
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 49
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 50
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 51
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 52
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 53
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 54
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 55
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 56
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 57
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 58
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 59
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 60
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 61
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 62
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 63
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 64
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 65
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 66
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 67
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 68
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 69
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 70
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 71
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 72
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 73
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 74
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 75
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 76
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 77
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 78
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 79
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 80
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 81
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 82
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 83
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 84
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 85
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 86
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 87
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 88
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 89
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 90
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 91
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 92
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 93
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 94
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 95
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 96
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 97
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 98
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 99
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 100
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 101
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 102
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 103
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 104
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 105
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 106
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 107
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 108
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 109
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 110
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 111
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 112
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 113
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 114
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 115
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 116
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 117
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 118
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 119
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 120
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 121
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 122
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 123
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 124
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 125
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 126
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 127
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 128
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 129
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 130
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 131
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 132
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 133
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 134
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 135
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 136
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 137
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 138
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 139
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 140
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 141
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 142
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 143
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 144
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 145
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 146
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 147
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 148
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 149
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 150
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 151
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 152
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 153
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 154
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 155
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 156
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 157
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 158
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 159
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 160
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 161
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 162
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 163
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 164
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 165
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 166
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 167
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 168
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 169
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 170
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 171
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 172
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 173
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 174
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 175
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 176
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 177
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 178
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 179
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 180
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 181
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 182
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 183
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 184
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 185
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 186
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 187
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 188
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 189
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 190
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 191
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 192
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 193
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 194
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 195
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 196
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 197
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 198
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 199
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 200
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 201
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 202
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 203
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 204
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 205
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 206
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 207
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 208
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 209
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 210
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 211
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 212
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 213
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 214
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 215
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 216
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 217
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 218
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 219
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 220
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 221
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 222
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 223
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 224
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 225
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 226
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 227
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 228
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 229
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 230
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 231
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 232
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 233
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 234
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 235
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 236
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 237
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 238
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 239
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 240
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 241
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 242
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 243
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 244
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 245
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 246
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 247
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 248
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 249
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 250
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 251
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 252
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 253
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 254
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 255
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 256
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 257
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 258
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 259
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 260
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 261
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 262
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 263
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 264
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 265
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 266
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 267
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 268
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 269
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 270
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 271
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 272
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 273
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 274
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 275
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 276
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 277
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 278
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 279
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 280
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 281
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 282
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 283
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 284
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 285
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 286
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 287
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 288
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 289
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 290
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 291
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 292
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 293
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 294
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 295
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 296
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 297
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 298
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 299
#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero

#> Warning in cor(train.pcg, train.circ[, gene.index]): the standard deviation is
#> zero
#> 
#> Running 10-folds cross-validation...
#> Iteration 1
#> Iteration 2
#> Iteration 3
#> Iteration 4
#> Iteration 5
#> Iteration 6
#> Iteration 7
#> Iteration 8
#> Iteration 9
#> Iteration 10
#> Cross-validation complete
#> [1] 300
plot(cv.full[,1], -log10(cv.full[,2]), xlab = "Spearman R", ylab = "P-value (-log10)", pch = 16, main = "Cross-validation accuracy")
abline(h = -log10(0.05), lty = 3)
```

<img src="man/figures/README-unnamed-chunk-4-1.png" width="100%" />

``` r
# Find out which miRNAs were imputed with better accuracy 
colnames(mionco.circ)[which(cv.full[,1] > 0.5)]
#> character(0)
colnames(mionco.circ)[which(cv.full[,2] < 0.05)]
#> character(0)
```

### Impute expression of certain circRNA(s) of interest with new dataset

> I use the same dataset as *new* dataset for a temporary show, as it
> will be replaced once we have another pair of
data.

``` r
(pred.circ <- ICE(train.pcg = mionco.pcg, train.circ = mionco.circ, new.pcg = mionco.pcg, gene.index = "hsa_circ_0000801"))
#>   [1] 19.04 18.26 18.32 15.16 18.80 18.72 10.24 20.22 16.94 19.24 18.14 18.24
#>  [13] 17.34 19.22 19.02 18.86 18.08 17.86 19.38 18.68 19.04 20.62 18.88 18.38
#>  [25] 20.96 19.26 18.52 17.36 18.84 18.96 19.20 21.26 19.10 17.76 16.20 21.04
#>  [37] 16.90 20.18 18.02 19.44 16.46 18.16 19.00 19.98 18.44 19.30 19.60 17.54
#>  [49] 16.12 18.36 17.98 19.34 16.78 17.12 18.12 19.78 19.42 19.64 19.44 21.16
#>  [61] 21.00 18.36 20.58 18.84 19.74 16.66 18.84 19.86 18.64 20.00 15.00 17.86
#>  [73] 19.40 20.14 19.02 19.30 19.62 18.10 17.44 15.36 18.30 19.36 18.30 20.38
#>  [85] 22.20 16.60 19.58 15.38 18.98 18.88 18.72 19.06 19.50 19.46 18.92 18.48
#>  [97] 19.20 20.70 17.60 17.46 15.74 19.72 17.94 19.28 22.24 21.24 16.38 15.74
#> [109] 18.38 15.32 19.54 17.88 18.86 18.80 13.50 17.60 18.66 14.92 20.78 17.56
#> [121] 17.60 20.62 19.42 20.14 15.88 19.08 20.54 20.02 17.58 16.58 20.58 17.24
#> [133] 18.72 17.06 20.86 18.42 20.84 16.78 18.54 15.24 17.26 18.88 19.06 19.42
#> [145] 18.08 19.06 18.36 18.90 17.94 14.90 21.20 19.96 19.90 18.92 20.26 17.14
#> [157] 20.22 17.50 17.02 19.58 20.62 18.74 18.74 21.06 21.06 18.08 15.42 15.42
#> [169] 20.78 20.72 19.16 17.70 18.10 17.90 18.16 16.80 21.30 21.16 21.16 17.84
#> [181] 19.46 19.30 19.30 19.36 19.00 18.08 17.04 15.40 20.14 18.28 16.80 15.98
#> [193] 19.98 20.40 20.62 18.88 19.04 20.16 17.00 17.60 20.46 20.46 18.54 17.20
#> [205] 19.98 17.74 16.46 17.96 19.04 19.58 20.94 18.92 19.02 18.64 18.82 21.08
#> [217] 20.50 18.72 19.22 20.92 19.16 18.44 19.34 19.46 17.02 19.14 14.88 18.90
#> [229] 18.20 18.08 19.50 18.62 22.46 17.78 20.98 18.46 19.62 19.52 17.72 20.90
#> [241] 18.22 17.42 17.14 18.60 18.84 19.02 17.74 17.18 18.24 18.54 17.46 20.30
#> [253] 18.90 21.24 17.88 17.80 19.20 18.88 19.30 18.86 19.28 20.48 17.94 18.06
#> [265] 19.16 19.08 17.76 16.10 18.76 17.86 17.76 19.14 18.64 16.08 18.86 19.14
#> [277] 19.16 19.20 17.96 18.70 18.96 21.10 17.12 19.36 19.12 19.62 18.16 16.64
#> [289] 16.98 17.98 18.08 18.26 20.52 20.52 21.00 21.00 19.24 19.56 16.96 19.98
#> [301] 20.74 19.38 16.20 17.66 18.86 18.94 20.24 19.98 19.64 19.58 18.72 17.94
#> [313] 22.78 19.38 17.98 19.66 19.36 17.16 22.28 21.26 15.48 16.44 18.82 17.50
#> [325] 17.32 20.00 19.74 18.68 18.94 18.64 17.10 21.68 17.02 17.02 18.00 19.26
#> [337] 19.42 17.90 20.54 16.90 20.54 16.66 16.22 17.92 19.68 18.98 18.06 17.16
#> [349] 19.66 20.96 20.48 19.08 19.94 20.18 17.20 15.98 18.80 19.56 19.16 17.50
#> [361] 17.52 18.20 16.96 16.88 20.44 17.54 20.10 18.68 19.34 20.38 19.98 17.88
#> [373] 19.08 19.08 21.42 18.88 18.20 18.90 16.92 19.74 18.90 18.88 19.38 18.32
#> [385] 19.02 18.42 17.02 18.18 18.62 20.48 19.52 19.62 17.66 19.98 19.88 19.14
#> [397] 19.18 17.98 19.62 17.92 20.96 18.48 19.48 18.32 16.98 17.56 16.80 17.40
#> [409] 16.78 16.62 18.12 19.24 20.12 21.44 17.60 18.86 18.72 19.72 18.70 19.38
#> [421] 17.50 17.76 19.32 19.06 17.80 18.66 20.02 18.64 19.76 18.98 18.36 20.16
#> [433] 19.90 17.70 18.32 20.00 19.04 16.46 18.80 21.72 17.66 17.12 19.90 19.48
#> [445] 16.68 18.28 18.34 18.96 19.18 18.78 20.88 15.96 21.38 21.28 18.36 18.34
#> [457] 13.84 19.04 18.54 19.66 20.16 19.06 20.54 16.78 20.86 19.68 18.54 21.52
#> [469] 20.68 19.86 20.42 18.90 19.92 20.00 17.52 19.26 18.82 20.56 20.12 21.28
#> [481] 19.00 19.26 17.62 18.32 14.14 20.70 19.44 20.42 19.22 21.26 20.92 19.06
#> [493] 19.64 19.80 19.56 20.54 19.76 18.06 14.48 19.22 20.76 15.58 21.30 20.60
#> [505] 17.78 18.74 19.46 19.54 15.50 19.18 18.80 21.16 19.64 17.54 16.78 19.90
#> [517] 21.10 21.24 21.60 17.72 17.64 18.56 21.04 19.38 19.34 17.06 18.70 18.34
#> [529] 18.34 18.66 19.18 19.10 16.10 19.76 20.36 13.40 19.72 18.44 18.44 20.52
#> [541] 20.86 15.90 18.80 18.46 20.32 20.32 19.82 16.04 18.50 17.02 18.12 19.50
#> [553] 18.18 23.24 21.32 19.92 21.08 17.88 19.62 22.58 15.36 17.18 16.98 19.34
#> [565] 14.18 18.52 18.38 18.94 19.60 13.80 14.70 20.88 20.82 19.42 18.12 20.96
#> [577] 21.40 20.64 15.58 18.84 17.80 22.62 22.50 18.54 20.92 21.48 20.28 18.62
#> [589] 20.06 18.24 18.36 19.08 19.06 21.30 18.14 16.24 17.38 19.28 19.42 19.38
#> [601] 18.50 20.34 19.38 20.02 19.22 19.30 20.30 18.08 18.78 20.68 21.20 19.20
#> [613] 17.98 16.64 16.70 17.60 17.44 17.66 17.42 18.44 17.88 20.54 16.32 18.92
#> [625] 19.20 18.08 17.86 18.02 21.06 19.10 21.46 18.76 15.36 18.40 18.32 14.54
#> [637] 18.74 17.54 21.52 17.90 18.98 18.94 18.92 17.52 19.70 18.22 18.60 17.98
#> [649] 19.04 18.54 21.32 16.58 17.98 19.32 19.52 19.02 18.34 19.26 19.36 20.78
#> [661] 19.12 19.46 19.18 19.80 19.06 17.98 18.46 20.44 19.98 19.30 20.12 20.82
#> [673] 19.86 19.34 17.10 20.24 18.72 20.12 18.58 17.92 17.62 18.42 17.88 16.70
#> [685] 17.90 15.64 19.78 19.32 20.94 21.50 17.78 17.18 20.62 19.48 17.68 18.32
#> [697] 19.90 16.48 17.80 18.66 18.64 19.98 17.84 17.70 18.18 18.22 18.90 18.48
#> [709] 19.82 19.94 20.04 19.62 18.78 17.88 17.88 18.52 18.32 21.28 18.86 18.22
#> [721] 20.16 19.50 21.54 21.06 17.94 17.62 19.60 17.94 19.28 21.32 17.96 18.40
#> [733] 19.04 21.30 18.90 19.68 17.56 19.78 18.76 19.08 19.72 20.66 18.68 19.40
#> [745] 19.20 16.74 16.66 20.96 20.00 18.88 19.64 18.26 18.74 20.22 20.22 18.72
#> [757] 19.28 19.02 18.78 18.86 19.78 20.68 21.14 19.68 18.16 19.66 20.52 19.48
#> [769] 17.78 17.62 18.32 18.08 18.08 18.82 18.66 17.50 18.90 17.62 18.08 18.84
#> [781] 17.60 18.72 17.22 18.92 18.60 18.64 18.94 18.62 18.84 19.06 16.58 18.84
#> [793] 16.62 18.10 19.20 19.06 18.50 18.78 19.48 19.24 15.38 18.82 18.38 18.64
#> [805] 19.10 19.36 19.06 18.62 18.36 18.38 18.42 18.30 19.16 18.82 18.26 18.68
#> [817] 18.42 18.90 19.00 18.72 19.36 15.80 18.84 18.46 18.26 19.16 19.00 18.74
#> [829] 19.00 17.70 16.52 13.66 18.52 18.40 18.58 19.64 20.84 20.84 20.36 18.40
#> [841] 17.74 18.18
plot(pred.circ, mionco.circ[, "hsa_circ_0000801"], xlab = "Predicted", ylab = "Measured", main = "hsa_circ_0000801 imputation performance", pch = 16)
abline(lm(mionco.circ[, "hsa_circ_0000801"] ~ pred.circ), lty = 3)
```

<img src="man/figures/README-unnamed-chunk-5-1.png" width="100%" />

### Impute expression of all circRNAs available in the training dataset (*To be finished*)

## Example dataset (*To be finished*)

To perform further analysis on circRNAs, we need to convert genome
region (**Chromosome**:**Start**-**End**) to circRNA identifiers
according to [circBase](http://www.circbase.org) records. Besides,
genome assemblies currently used in circBase are hg19 for H. sapiens. To
convert the data between assemblies, one can use liftOver tool at
[UCSC’s web interface](http://genome.ucsc.edu/cgi-bin/hgLiftOver).

One pair of circRNA and PCGs matrices is from paper [*The Landscape of
Circular RNA in
Cancer*](https://www.sciencedirect.com/science/article/pii/S0092867418316350).

circRNA expression matrix was downloaded from [this
website](https://mioncocirc.github.io/download/), and pre-processed by
below code:

``` r
library(data.table)
mionco.circ <- fread('v0.1.release.txt')
bed <- fread('hglft_genome_5d4de_3493b0.bed')
bed <- bed[, 1:4]
setnames(bed, c('chr', 'start', 'end', 'ID'))
mionco.circ <- na.omit(mionco.circ[bed, on = .(chr == chr, start > start, end < end), allow.cartesian=TRUE])
mionco.circ <- dcast(mionco.circ, formula = sample ~ ID, value.var = 'reads', fun.aggregate = max)
mionco.circ <- as.matrix(mionco.circ, rownames = 'sample')

mionco.pcg <- fread('fpkm_matrix.csv', drop = 1)
mionco.pcg[, Row.names := tstrsplit(Row.names, '\\.')[[1]]]
mionco.pcg[, V2 := NULL]
mionco.pcg <- as.matrix(mionco.pcg, rownames = 'Row.names')
mionco.pcg <- t(mionco.pcg)

sample.used <- intersect(rownames(mionco.circ), rownames(mionco.pcg))
mionco.circ <- mionco.circ[sample.used, ]
mionco.pcg <- mionco.pcg[sample.used, ]
```

## TODO list

  - \[ \] Add: new test datasets (also make adjustment for gene IDs)
  - \[ \] Subset: we do **NOT** need such a big training dataset
  - \[ \] Refactor: rewrite cv process with `caret`?
  - \[ \] Refactor: rewrite type check for satisfying the Bioc’s?
  - \[ \] Fix: warning `In cor(train.pcg, train.circ[, gene.index]) :
    the standard deviation is zero`
  - \[ \] Vignette: replace plots with `ggplot2` and add other examples
  - \[ \] Application: on TCGA datasets? Artificial datasets? Others?
