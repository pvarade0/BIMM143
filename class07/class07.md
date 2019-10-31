Class 7 R functions and packages
================
Pratik Varade
10/22/2019

## R functions revisited

Source my functions from last day

``` r
source("http://tinyurl.com/rescale-R")
```

``` r
rescale(1:10)
```

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

``` r
rescale(c(1,10,5,NA,6))
```

    ## [1] 0.0000000 1.0000000 0.4444444        NA 0.5555556

``` r
rescale2(c(1:10,"barry"))
```

``` r
rescale(c(1:10, "Barry"))
```

The error on the rescale 2 function is a lot more helpful than rescale.

\#\#Write a function to find NA in 2 vectors Write a function to find
where there are NA elements in two input vectors. First make some simple
input where I know the answers.

``` r
x <- c( 1, 2, NA, 3, NA)
y <- c(NA, 3, NA, 3, 4)
```

Looked online and found the **is.na()** function

``` r
is.na(x)
```

    ## [1] FALSE FALSE  TRUE FALSE  TRUE

and the **which()** function tells me where the TRUE values are

``` r
which(is.na(x))
```

    ## [1] 3 5

``` r
which(is.na(y))
```

    ## [1] 1 3

``` r
is.na(x)
```

    ## [1] FALSE FALSE  TRUE FALSE  TRUE

``` r
is.na(y)
```

    ## [1]  TRUE FALSE  TRUE FALSE FALSE

the AND function requires two input TRUE to give a TRUE output

``` r
is.na(x) & is.na(y)
```

    ## [1] FALSE FALSE  TRUE FALSE FALSE

Taking the **sum()** of TRUE FALSE vector will tell me how many TRUE
elements I have. Remember, TRUE = 1, FALSE = 0. So when sum = 1, that
means there is one pair of TRUES. This is my working **snippet**.

``` r
sum(is.na(x)& is.na(y))
```

    ## [1] 1

``` r
sum(c(T, T, F, T))
```

    ## [1] 3

Now turn that **snippet** into a function.

``` r
both_NA <- function(x, y) {
sum(is.na(x) & is.na(y))
}
```

Test

``` r
both_NA(x,y)
```

    ## [1] 1

Eejit Proofing, both\_NA(x,y2) is weird because one vector has 3
elements, while the other has 4. What happens is recycling. x is too
small, so it will recycle it, so in theory its NA, NA, NA, (original 3
NAs) NA, NA, NA(this is recycled x vector), but only the first 4 count
because the second vector is 4 elements.

``` r
x <- c(NA, NA, NA)
y1 <- c( 1, NA, NA)
y2 <- c( 1, NA, NA, NA)

both_NA(x,y1)
```

    ## [1] 2

``` r
both_NA(x,y2)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 3

``` r
x2<- c(NA,NA)
both_NA(x2,y2)
```

    ## [1] 3

Testing how recycling works.

``` r
x <-   c(1, NA, NA)
y3 <- c( 1, NA, NA, NA, NA, NA, NA)

both_NA(x,y3)
```

    ## Warning in is.na(x) & is.na(y): longer object length is not a multiple of
    ## shorter object length

    ## [1] 4

This is the same as the problem on top because of recycling.

``` r
x3<- c(1, NA,NA,1,NA,NA,1)
y3 <- c(1, NA, NA, NA,NA,NA, NA)
```

``` r
length(x)
```

    ## [1] 3

``` r
length(y3)
```

    ## [1] 7

Add a check for when inputs x and u are not the same lengths

``` r
both_NA2 <- function(x, y) {
if(length(x) != length(y)) {
stop(print("Inputs x and y should be the same length!"))
  }
  sum(is.na(x) & is.na(y))
}
```

Test

``` r
both_NA2(x,y3)
```

Make a function that will help Prof. Barry grade student work.

``` r
# student 1
student1 <- c(100, 100, 100, 100, 100, 100, 100, 90)
# student 2
student2 <- c(100, NA, 90, 90, 90, 90, 97, 80)
```

Student 1

``` r
mean(student1[-which.min(student1)])
```

    ## [1] 100

Student 2

``` r
which.min(student2)
```

    ## [1] 8

``` r
student2[-which.min(student2)]
```

    ## [1] 100  NA  90  90  90  90  97

``` r
mean(student2[-which.min(student2)], na.rm= TRUE)
```

    ## [1] 92.83333

any means if any of the vector is NA, it will say true. If all of them
are not NA, false.

``` r
is.na(student2)
```

    ## [1] FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
any(is.na(student2))
```

    ## [1] TRUE

``` r
any(is.na(student1))
```

    ## [1] FALSE

We have out working code now turn it into a first function

``` r
grade1 <- function(x) {
  if(any(is.na(x)))
    warning(print("This student is missing a homework"))
  mean(x[-which.min(x)], na.rm=TRUE)
}
```

We have out working code now turn it into a first function

``` r
grade2 <- function(x) {
  if(any(is.na(x)))
    warning(print("This student is missing a homework"))
  sum(x[-which.min(x)], na.rm=TRUE)/length(x)-1
}

grade(student1)
grade(student2)
```

``` r
s3<- c(100, NA,NA,NA,NA)
```

``` r
url <- "https://tinyurl.com/gradeinput"
read.csv(url)
```

    ##             X hw1 hw2 hw3 hw4 hw5
    ## 1   student-1 100  73 100  88  79
    ## 2   student-2  85  64  78  89  78
    ## 3   student-3  83  69  77 100  77
    ## 4   student-4  88  NA  73 100  76
    ## 5   student-5  88 100  75  86  79
    ## 6   student-6  89  78 100  89  77
    ## 7   student-7  89 100  74  87 100
    ## 8   student-8  89 100  76  86 100
    ## 9   student-9  86 100  77  88  77
    ## 10 student-10  89  72  79  NA  76
    ## 11 student-11  82  66  78  84 100
    ## 12 student-12 100  70  75  92 100
    ## 13 student-13  89 100  76 100  80
    ## 14 student-14  85 100  77  89  76
    ## 15 student-15  85  65  76  89  NA
    ## 16 student-16  92 100  74  89  77
    ## 17 student-17  88  63 100  86  78
    ## 18 student-18  91  NA 100  87 100
    ## 19 student-19  91  68  75  86  79
    ## 20 student-20  91  68  76  88  76

``` r
hw <- read.csv(url, row.names=1)
```

1 = rows, 2 = columns

``` r
apply(hw, 1, grade1)
```

    ## [1] "This student is missing a homework"

    ## Warning in FUN(newX[, i], ...): This student is missing a homework

    ## [1] "This student is missing a homework"

    ## Warning in FUN(newX[, i], ...): This student is missing a homework

    ## [1] "This student is missing a homework"

    ## Warning in FUN(newX[, i], ...): This student is missing a homework

    ## [1] "This student is missing a homework"

    ## Warning in FUN(newX[, i], ...): This student is missing a homework

    ##  student-1  student-2  student-3  student-4  student-5  student-6 
    ##   91.75000   82.50000   84.25000   88.00000   88.25000   89.00000 
    ##  student-7  student-8  student-9 student-10 student-11 student-12 
    ##   94.00000   93.75000   87.75000   81.33333   86.00000   91.75000 
    ## student-13 student-14 student-15 student-16 student-17 student-18 
    ##   92.25000   87.75000   83.33333   89.50000   88.00000   97.00000 
    ## student-19 student-20 
    ##   82.75000   82.75000

Datapasta

``` r
install.packages("datapasta")
```
