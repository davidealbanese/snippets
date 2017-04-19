R Tidy
================

-   [Baseline/Follow-up ratio](#baselinefollow-up-ratio)
-   [Spread multiple columns](#spread-multiple-columns)
-   [Transpose](#transpose)
-   [Move a column to the first position](#move-a-column-to-the-first-position)

``` r
# Visualization
library(knitr) 

library(tidyr) # spread, gather
library(dplyr) # mutate, ...

set.seed(0)
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
| S1      | BA      |   1.2629543|  -0.9285670|  -1.1476570|
| S1      | FO      |  -0.3262334|  -0.2947204|  -0.2894616|
| S2      | BA      |   1.3297993|  -0.0057672|  -0.2992151|
| S2      | FO      |   1.2724293|   2.4046534|  -0.4115108|
| S3      | BA      |   0.4146414|   0.7635935|   0.2522234|
| S3      | FO      |  -1.5399500|  -0.7990092|  -0.8919211|

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
| S1      | Var1 |   1.2629543|  -0.3262334|  -3.8713217|
| S1      | Var2 |  -0.9285670|  -0.2947204|   3.1506706|
| S1      | Var3 |  -1.1476570|  -0.2894616|   3.9647992|
| S2      | Var1 |   1.3297993|   1.2724293|   1.0450869|
| S2      | Var2 |  -0.0057672|   2.4046534|  -0.0023983|
| S2      | Var3 |  -0.2992151|  -0.4115108|   0.7271136|
| S3      | Var1 |   0.4146414|  -1.5399500|  -0.2692564|
| S3      | Var2 |   0.7635935|  -0.7990092|  -0.9556754|
| S3      | Var3 |   0.2522234|  -0.8919211|  -0.2827867|

Spread multiple columns
-----------------------

``` r
df = data.frame(Subject=rep(c("S1","S2","S3"), each=2),
                Group=rep(c("G1", "G2"), 3),
                Var1=rnorm(6), Var2=rnorm(6), Var3=rnorm(6))
kable(df)
```

| Subject | Group |        Var1|        Var2|        Var3|
|:--------|:------|-----------:|-----------:|-----------:|
| S1      | G1    |   0.4356833|  -0.0571068|  -0.2357066|
| S1      | G2    |  -1.2375384|   0.5036080|  -0.5428883|
| S2      | G1    |  -0.2242679|   1.0857694|  -0.4333103|
| S2      | G2    |   0.3773956|  -0.6909538|  -0.6494716|
| S3      | G1    |   0.1333364|  -1.2845994|   0.7267507|
| S3      | G2    |   0.8041895|   0.0467262|   1.1519118|

``` r
df_spread = df %>% 
  gather(variable, value, -(Subject:Group)) %>%
  unite(temp, Group, variable, sep=".") %>%
  spread(temp, value)

kable(df_spread)
```

| Subject |     G1.Var1|     G1.Var2|     G1.Var3|     G2.Var1|     G2.Var2|     G2.Var3|
|:--------|-----------:|-----------:|-----------:|-----------:|-----------:|-----------:|
| S1      |   0.4356833|  -0.0571068|  -0.2357066|  -1.2375384|   0.5036080|  -0.5428883|
| S2      |  -0.2242679|   1.0857694|  -0.4333103|   0.3773956|  -0.6909538|  -0.6494716|
| S3      |   0.1333364|  -1.2845994|   0.7267507|   0.8041895|   0.0467262|   1.1519118|

Transpose
---------

``` r
df = data.frame(Subject=c("S1","S2","S3", "S4"),
                Var1=rnorm(4), Var2=rnorm(4), Var3=rnorm(4))

kable(df)
```

| Subject |        Var1|        Var2|       Var3|
|:--------|-----------:|-----------:|----------:|
| S1      |   0.9921604|   1.7579031|  -1.166570|
| S2      |  -0.4295131|   0.5607461|  -1.065591|
| S3      |   1.2383041|  -0.4527840|  -1.563782|
| S4      |  -0.2793463|  -0.8320433|   1.156537|

``` r
df_t = df %>% 
  gather(Var, Val, -Subject) %>% 
  spread(Subject, Val)

kable(df_t)
```

| Var  |          S1|          S2|         S3|          S4|
|:-----|-----------:|-----------:|----------:|-----------:|
| Var1 |   0.9921604|  -0.4295131|   1.238304|  -0.2793463|
| Var2 |   1.7579031|   0.5607461|  -0.452784|  -0.8320433|
| Var3 |  -1.1665705|  -1.0655906|  -1.563782|   1.1565370|

Move a column to the first position
-----------------------------------

``` r
df = data.frame(Var1=rnorm(4),  Var2=rnorm(4), Var3=rnorm(4))

kable(df)
```

|        Var1|        Var2|        Var3|
|-----------:|-----------:|-----------:|
|   0.8320471|   2.4413646|   0.6182433|
|  -0.2273287|  -0.7953391|  -0.1726235|
|   0.2661374|  -0.0548775|  -2.2239003|
|  -0.3767027|   0.2501413|  -1.2636144|

``` r
df_m = df %>% 
  select(Var2, everything())

kable(df_m)
```

|        Var2|        Var1|        Var3|
|-----------:|-----------:|-----------:|
|   2.4413646|   0.8320471|   0.6182433|
|  -0.7953391|  -0.2273287|  -0.1726235|
|  -0.0548775|   0.2661374|  -2.2239003|
|   0.2501413|  -0.3767027|  -1.2636144|
