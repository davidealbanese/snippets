R Tidy
================

Baseline/Follow-up ratio
------------------------

BA: Baseline, FO: Follow-up, 3 variables

``` r
library(tidyr)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
df = data.frame(Subject=rep(c("S1","S2","S3"), each=2),
                Measure=rep(c("BA","FO"), 3),
                Var1=rnorm(6), Var2=rnorm(6), Var3=rnorm(6))
df
```

    ##   Subject Measure         Var1        Var2        Var3
    ## 1      S1      BA  1.137617500 -1.22791121  0.52528676
    ## 2      S1      FO -0.504555189 -1.34075486 -1.40107216
    ## 3      S2      BA -1.938562329  0.01065907  0.14174794
    ## 4      S2      FO  0.040044364 -0.76444987 -0.33083560
    ## 5      S3      BA -0.001096032 -0.02881580 -1.54609337
    ## 6      S3      FO -1.381120306  0.35654772  0.03899373

``` r
df %>% gather(Var, Value, Var1:Var3) %>% group_by(Subject, Var) %>% spread(Measure, Value) %>% mutate(Ratio=BA/FO)
```

    ## Source: local data frame [9 x 5]
    ## Groups: Subject, Var [9]
    ## 
    ##   Subject   Var           BA          FO         Ratio
    ##    <fctr> <chr>        <dbl>       <dbl>         <dbl>
    ## 1      S1  Var1  1.137617500 -0.50455519 -2.254694e+00
    ## 2      S1  Var2 -1.227911214 -1.34075486  9.158357e-01
    ## 3      S1  Var3  0.525286758 -1.40107216 -3.749177e-01
    ## 4      S2  Var1 -1.938562329  0.04004436 -4.841037e+01
    ## 5      S2  Var2  0.010659066 -0.76444987 -1.394345e-02
    ## 6      S2  Var3  0.141747939 -0.33083560 -4.284543e-01
    ## 7      S3  Var1 -0.001096032 -1.38112031  7.935816e-04
    ## 8      S3  Var2 -0.028815795  0.35654772 -8.081890e-02
    ## 9      S3  Var3 -1.546093372  0.03899373 -3.964980e+01
