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

BA: Baseline, FO: Follow-up, 3 variables

``` r
df = data.frame(Subject=rep(c("S1","S2","S3"), each=2),
                Measure=rep(c("BA","FO"), 3),
                Var1=rnorm(6), Var2=rnorm(6), Var3=rnorm(6))

kable(df)
```

| Subject | Measure |        Var1|        Var2|        Var3|
|:--------|:--------|-----------:|-----------:|-----------:|
| S1      | BA      |   0.3406745|   0.3007572|   0.4899697|
| S1      | FO      |   0.7593458|   0.5277682|  -1.0424745|
| S2      | BA      |   0.1173973|  -0.6114426|   1.6512998|
| S2      | FO      |   0.4802231|   0.1074516|   1.6534635|
| S3      | BA      |  -0.0029475|   1.4979166|   1.2368592|
| S3      | FO      |   2.0658115|  -0.0157289|   0.3173809|

``` r
df_ratio = df %>% 
  gather(Var, Value, Var1:Var3) %>%
  group_by(Subject, Var) %>%
  spread(Measure, Value) %>%
  mutate(Ratio=BA/FO)

kable(df_ratio)
```

| Subject | Var  |          BA|          FO|        Ratio|
|:--------|:-----|-----------:|-----------:|------------:|
| S1      | Var1 |   0.3406745|   0.7593458|    0.4486421|
| S1      | Var2 |   0.3007572|   0.5277682|    0.5698661|
| S1      | Var3 |   0.4899697|  -1.0424745|   -0.4700064|
| S2      | Var1 |   0.1173973|   0.4802231|    0.2444641|
| S2      | Var2 |  -0.6114426|   0.1074516|   -5.6903975|
| S2      | Var3 |   1.6512998|   1.6534635|    0.9986914|
| S3      | Var1 |  -0.0029475|   2.0658115|   -0.0014268|
| S3      | Var2 |   1.4979166|  -0.0157289|  -95.2333497|
| S3      | Var3 |   1.2368592|   0.3173809|    3.8970818|
