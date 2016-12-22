R Tidy
================

------------------------------------------------------------------------

First
-----

``` r
df = data.frame(Subject=rep(c("S1","S2","S3"), each=4),
                Visit=rep(c("V1","V2","V3","V4"), 3),
                Var1=rnorm(12), Var2=rnorm(12), Var3=rnorm(12))
df
```

    ##    Subject Visit        Var1        Var2         Var3
    ## 1       S1    V1 -0.53886487 -1.02736359  0.682867112
    ## 2       S1    V2  0.14052654 -0.77901161  0.702452725
    ## 3       S1    V3  0.53359077 -1.02113011  0.330857849
    ## 4       S1    V4  0.33738668  0.89358073 -0.008926675
    ## 5       S2    V1  0.81231913  0.01633745  1.078144197
    ## 6       S2    V2 -0.95610247 -0.40946979 -0.587069283
    ## 7       S2    V3  0.02660058  0.28236985 -0.081689573
    ## 8       S2    V4 -0.69593551  0.91503188  1.450663386
    ## 9       S3    V1 -1.72789830 -1.44949262  0.819033727
    ## 10      S3    V2 -0.21923432 -1.05637851  0.063365085
    ## 11      S3    V3  0.79848136 -0.93643869  0.027093678
    ## 12      S3    V4  0.28922510  0.59128271  0.688932568

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code.

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd+Shift+Enter*.

``` r
plot(cars)
```

![](Rtidy_files/figure-markdown_github/unnamed-chunk-2-1.png)

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Cmd+Option+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Cmd+Shift+K* to preview the HTML file).
