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

    ##    Subject Visit        Var1       Var2        Var3
    ## 1       S1    V1  0.26871350 -1.2424315  0.32682211
    ## 2       S1    V2  0.71675706 -0.9117497 -1.47363838
    ## 3       S1    V3  1.28133831 -1.7747507  1.05527252
    ## 4       S1    V4 -1.54413980 -0.2206778 -1.02212856
    ## 5       S2    V1 -0.74829863  0.9037992 -1.47276268
    ## 6       S2    V2 -0.25905784 -0.3905982  2.01522145
    ## 7       S2    V3  0.30273730 -0.9263077 -0.14624132
    ## 8       S2    V4 -0.94426701  0.9424068  0.02192532
    ## 9       S3    V1 -0.76889561  1.3267765  0.37284774
    ## 10      S3    V2 -0.61085668  1.5058840  1.17254710
    ## 11      S3    V3 -0.09018097 -0.1987421 -0.14324245
    ## 12      S3    V4 -0.22204866  0.2152923  0.71098644

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code.

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd+Shift+Enter*.

``` r
plot(cars)
```

![](Rtidy_files/figure-markdown_github/unnamed-chunk-2-1.png)

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Cmd+Option+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Cmd+Shift+K* to preview the HTML file).
