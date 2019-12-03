Untitled
================

## R Markdown

Class 17 Part 2 Hands on Activity Run librarys necessary (in console)

``` r
library(RCy3)
library(igraph)
library(RColorBrewer)
```

Test that you are connected to cytoscape

``` r
cytoscapePing()
cytoscapeVersionInfo()
```

``` r
ge <- makeSimpleIgraph()
createNetworkFromIgraph(g,"myGraph")
```

This will save the image file from cytoscape.

``` r
fig <- exportImage(filename="demo", type="png", height=350)
```

``` r
knitr::include_graphics("./demo.png")
```

![](./demo.png)<!-- -->

Different Styles:

``` r
setVisualStyle("Marquee")
```

``` r
fig <- exportImage(filename="demo_marquee", type="png", height=350)
```

This is the image:

``` r
knitr::include_graphics("./demo_marquee.png")
```

![](./demo_marquee.png)<!-- -->

What other syles are there?

``` r
styles <- getVisualStyleNames()
styles
```

``` r
plot(ge)
```

``` r
## scripts for processing located in "inst/data-raw/"
prok_vir_cor <- read.delim("virus_prok_cor_abundant.tsv", stringsAsFactors = FALSE)

## Have a peak at the first 6 rows
head(prok_vir_cor)
```

    ##       Var1          Var2    weight
    ## 1  ph_1061 AACY020068177 0.8555342
    ## 2  ph_1258 AACY020207233 0.8055750
    ## 3  ph_3164 AACY020207233 0.8122517
    ## 4  ph_1033 AACY020255495 0.8487498
    ## 5 ph_10996 AACY020255495 0.8734617
    ## 6 ph_11038 AACY020255495 0.8740782

``` r
g <- graph.data.frame(prok_vir_cor, directed = FALSE)
```

``` r
class(g)
g
```

``` r
plot(g)
```

Make it look better

``` r
plot(g, vertex.label=NA)
```

Make the nodes/vertex smaller

``` r
plot(g, vertex.size=3, vertex.label=NA)
```

``` r
createNetworkFromIgraph(g,"myIgraph")
```

``` r
cb <- cluster_edge_betweenness(g)
```

``` r
cb
```

``` r
plot(cb, y=g, vertex.label=NA,  vertex.size=3)
```

``` r
head( membership(cb) )
```
