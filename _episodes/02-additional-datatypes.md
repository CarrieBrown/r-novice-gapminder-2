---
title: "Lists and Matrices"
teaching: 20
exercises: 10
questions:
- "How do I use and maneuver within other data classes available in R?"
- "How do I detect and manage missing and incorrect data?"
- "How can I create a class that contains multiple data types?"
Objectives:
- "Explore additional data types in R including Lists and Matrices'
- "Learn about missing data and other special values"
keypoints:
- "Missing data gets assigned as `NA`"
- "`Inf` is used to represent infinite values and `NaN` indicates undefined values."
- "A matrix is a three dimensional vector"
- "A list is a container that can contain objects of different data types."
---

### Missing Data

R supports missing data in vectors. They are represented as `NA` (Not Available)
and can be used for all the vector types covered in this lesson:


~~~
x <- c(0.5, NA, 0.7)
x <- c(TRUE, FALSE, NA)
x <- c("a", NA, "c", "d", "e")
x <- c(1+5i, 2-3i, NA)
~~~
{: .r}

The function `is.na()` indicates the elements of the vectors that represent
missing data, and the function `anyNA()` returns `TRUE` if the vector contains
any missing values:


~~~
x <- c("a", NA, "c", "d", NA)
y <- c("a", "b", "c", "d", "e")
is.na(x)
~~~
{: .r}

~~~
## [1] FALSE  TRUE FALSE FALSE  TRUE
~~~
{: .output}

~~~
is.na(y)
~~~
{: .r}

~~~
## [1] FALSE FALSE FALSE FALSE FALSE
~~~
{: .output}

~~~
anyNA(x)
~~~
{: .r}

~~~
## [1] TRUE
~~~
{: .output}

~~~
anyNA(y)
~~~
{: .r}

~~~
## [1] FALSE
~~~
{: .output}

### Other Special Values

`Inf` is infinity. You can have either positive or negative infinity.


~~~
1/0
~~~
{: .r}

~~~
## [1] Inf
~~~
{: .output}

`NaN` means Not a Number. It's an undefined value.


~~~
0/0
~~~
{: .r}

~~~
## [1] NaN
~~~
{: .output}

### Matrix

In R matrices are an extension of the numeric or character vectors. They are not
a separate type of object but simply an atomic vector with dimensions; the
number of rows and columns.


~~~
m <- matrix(nrow = 2, ncol = 2)
m
~~~
{: .r}

~~~
##      [,1] [,2]
## [1,]   NA   NA
## [2,]   NA   NA
~~~
{: .output}

~~~
dim(m)
~~~
{: .r}

~~~
## [1] 2 2
~~~
{: .output}

Matrices in R are filled column-wise.


~~~
m <- matrix(1:6, nrow = 2, ncol = 3)
~~~
{: .r}

Other ways to construct a matrix


~~~
m      <- 1:10
dim(m) <- c(2, 5)
~~~
{: .r}

This takes a vector and transform into a matrix with 2 rows and 5 columns.

Another way is to bind columns or rows using `cbind()` and `rbind()`.


~~~
x <- 1:3
y <- 10:12
cbind(x, y)
~~~
{: .r}

~~~
##      x  y
## [1,] 1 10
## [2,] 2 11
## [3,] 3 12
~~~
{: .output}

~~~
rbind(x, y)
~~~
{: .r}

~~~
##   [,1] [,2] [,3]
## x    1    2    3
## y   10   11   12
~~~
{: .output}

You can also use the `byrow` argument to specify how the matrix is filled. From R's own documentation:


~~~
mdat <- matrix(c(1,2,3, 11,12,13), nrow = 2, ncol = 3, byrow = TRUE)
mdat
~~~
{: .r}

~~~
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]   11   12   13
~~~
{: .output}

### List

In R lists act as containers. Unlike atomic vectors, the contents of a list are
not restricted to a single mode and can encompass any mixture of data
types. Lists are sometimes called generic vectors, because the elements of a
list can by of any type of R object, even lists containing further lists. This
property makes them fundamentally different from atomic vectors.

A list is a special type of vector. Each element can be a different type.

Create lists using `list()` or coerce other objects using `as.list()`. An empty
list of the required length can be created using `vector()`


~~~
x <- list(1, "a", TRUE, 1+4i)
x
~~~
{: .r}

~~~
## [[1]]
## [1] 1
## 
## [[2]]
## [1] "a"
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] 1+4i
~~~
{: .output}

~~~
x <- vector("list", length = 5) ## empty list
length(x)
~~~
{: .r}

~~~
## [1] 5
~~~
{: .output}

~~~
x[[1]]
~~~
{: .r}

~~~
## NULL
~~~
{: .output}

~~~
x <- 1:10
x <- as.list(x)
length(x)
~~~
{: .r}

~~~
## [1] 10
~~~
{: .output}

1. What is the class of `x[1]`?
2. What about `x[[1]]`?


~~~
xlist <- list(a = "Karthik Ram", b = 1:10, data = head(iris))
xlist
~~~
{: .r}

~~~
## $a
## [1] "Karthik Ram"
## 
## $b
##  [1]  1  2  3  4  5  6  7  8  9 10
## 
## $data
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
~~~
{: .output}

1. What is the length of this object? What about its structure?

Lists can be extremely useful inside functions. You can “staple” together lots
of different kinds of results into a single object that a function can return.

A list does not print to the console like a vector. Instead, each element of the
list starts on a new line.

Elements are indexed by double brackets. Single brackets will still return
a(nother) list.
