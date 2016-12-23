R Tidy
================

``` r
# Visualization
library(knitr) 

library(tidyr) # spread, gather
library(dplyr) # mutate, ...
```

Baseline/Follow-up ratio
------------------------

For each sample and variable we want to compute the baseline-follow-up ratio. BA: Baseline, FO: Follow-up, 3 variables.

``` r
df = data.frame(Subject=rep(c("S1","S2","S3"), each=2),
                Measure=rep(c("BA","FO"), 3),
                Var1=rnorm(6), Var2=rnorm(6), Var3=rnorm(6))

kable(df)
```

| Subject | Measure |        Var1|        Var2|        Var3|
|:--------|:--------|-----------:|-----------:|-----------:|
| S1      | BA      |  -0.2941902|  -0.8326408|  -1.0972273|
| S1      | FO      |  -0.8966106|  -0.3239683|   0.4066597|
| S2      | BA      |  -1.2355577|  -0.6397466|  -0.1466336|
| S2      | FO      |   0.5895973|  -0.2795851|   1.3623025|
| S3      | BA      |   1.3407078|  -0.2855879|  -0.7201147|
| S3      | FO      |   0.1769922|   0.3156139|  -0.0827527|

``` r
df_ratio = df %>% 
  gather(Var, Value, Var1:Var3) %>%
  group_by(Subject, Var) %>%
  spread(Measure, Value) %>%
  mutate(Ratio=BA/FO)

kable(df_ratio)
```

| Subject | Var  |          BA|          FO|       Ratio|
|:--------|:-----|-----------:|-----------:|-----------:|
| S1      | Var1 |  -0.2941902|  -0.8966106|   0.3281136|
| S1      | Var2 |  -0.8326408|  -0.3239683|   2.5701303|
| S1      | Var3 |  -1.0972273|   0.4066597|  -2.6981460|
| S2      | Var1 |  -1.2355577|   0.5895973|  -2.0955962|
| S2      | Var2 |  -0.6397466|  -0.2795851|   2.2882000|
| S2      | Var3 |  -0.1466336|   1.3623025|  -0.1076366|
| S3      | Var1 |   1.3407078|   0.1769922|   7.5749529|
| S3      | Var2 |  -0.2855879|   0.3156139|  -0.9048649|
| S3      | Var3 |  -0.7201147|  -0.0827527|   8.7020107|
