Assignment 7: Iteration (for loops) and functions
================

### **Instructions: please read through this before you begin**

  - This homework is due by **10pm on Monday 11/09/20.**

  - Please **reproduce this markdown template.** Pay attention to all
    the formatting in this file, including bullet points, bolded
    characters, inserted code chuncks, headings, text colors, blank
    lines, and etc.

  - When a verbal response is needed, answer by editing the part in the
    R markdown template where it says “Write your response here”.

  - Have all your code embedded within the R markdown file, and show
    both your code and plots in the knitted markdown file.

  - Use R Markdown functionalities to **hide messages and warnings when
    needed**. (Suggestion:messages and warnings can often be informative
    and important, so please examine them carefully and only turn them
    off when you finish the exercise).

  - Please name your R markdown file `assignment_7.Rmd` and the knitted
    markdown file `assignment_7.md`. Please upload both files using your
    personal GitHub repository for this class.

**Acknowledgments:** Exercise 1 has been adapted (with permission) from
the **[Data Carpentry for Biologists semester
course](https://datacarpentry.org/semester-biology/exercises/Functions-use-and-modify-Python/)**
and exercises 2 and 3 are adapted (with permission) from lain
Carmichael’s course **[STOR 390:Introduction Data
Science](https://idc9.github.io/stor390/#course_material).**

To start, first load all the required packages with the following code.
Install them if they are not installed yet.

``` r
library(tidyverse)
```

### **Exercise 1: Body mass estimation using vectorization vs. for loop**

There are two major types of approaches to perform multiple operations
in
R:**[vectorization](https://swcarpentry.github.io/r-novice-gapminder/09-vectorization/)**
and for loops. As a simple to calculate the sum of two vectors, `x` and
`y`, the syntax for vectorization is simply `z <- x + y`. With this, the
computer will be able to perform the same operation to each element of x
and y vector **simultaneously.**

The for loop approach to achieve the same task (create a new vector z
that is the sum of vectors x and y), on the other hand, takes the
following form:

``` r
z[i] <- NULL

for (i in 1:length(x)){
  
  z[i] <- x[i] +y[i]
  
  }
```

In this case, the computer loops through each element of x and y and
performs the operation **sequentially**, resulting in a significantly
longer runtime. Let’s now try to quantify this difference in runtime in
this exercise.

**1.1**

The length of an organism is typically strongly correlated with its body
mass. This is useful because it allows us to estimate the mass of an
organism even if we only know its length. This relationship generally
takes the form: `mass = a * length ^ b`, where the parameters `a` and
`b` vary among groups. This allometric approach is regularly used to
estimate the mass of dinosaurs since we cannot weigh something that is
only preserved as bones.

*Spinosaurus* is a predator that is bigger, and therefore, by
definition, cooler, than that stupid *Tyrannosaurus* that everyone likes
so much. It has an estimated `a` of `0.73` and `b` of `3.63.` What is
the estimated mass of a *Spinosaurus* that is `16` m long based `16` m
long based on its reassembled skeleton?

``` r
##[1] 17150.56
```

**1.2**

The following vectors contain the `length`s of 40 dinosaurs and their
respective `a` and `b` values. Estimate their `mass` first using a
vectorization approach and then using a for and then using a for loop
approach.

``` r
dinosaur_lengths <- c(17.8013631070471, 20.3764452071665, 14.0743486294308, 25.65782386974, 26.0952008049675, 20.3111541103134, 17.5663244372533, 11.2563431277577, 20.081903202614, 18.6071626441984, 18.0991894513166, 23.0659685685892, 20.5798853467837, 25.6179254233558, 24.3714331573996, 26.2847248252537, 25.4753783544473, 20.4642089867304, 16.0738256364701, 20.3494171706583, 19.854399305869, 17.7889814608919, 14.8016421998303, 19.6840911485379, 19.4685885050906, 24.4807784966691, 13.3359960054899, 21.5065994598917, 18.4640304608411, 19.5861532398676, 27.084751999756, 18.9609366301798, 22.4829168046521, 11.7325716149514, 18.3758846100456, 15.537504851634, 13.4848751773738, 7.68561192214935, 25.5963348603783, 16.588285389794)

a_values <- c(0.759, 0.751, 0.74, 0.746, 0.759, 0.751, 0.749, 0.751, 0.738, 0.768, 0.736, 0.749, 0.746, 0.744, 0.749, 0.751, 0.744, 0.754, 0.774, 0.751, 0.763, 0.749, 0.741, 0.754, 0.746, 0.755, 0.764, 0.758, 0.76, 0.748, 0.745, 0.756, 0.739, 0.733, 0.757, 0.747, 0.741, 0.752, 0.752, 0.748)

b_values <- c(3.627, 3.633, 3.626, 3.633, 3.627, 3.629, 3.632, 3.628, 3.633, 3.627, 3.621, 3.63, 3.631, 3.632, 3.628, 3.626, 3.639, 3.626, 3.635, 3.629, 3.642, 3.632, 3.633, 3.629, 3.62, 3.619, 3.638, 3.627, 3.621, 3.628, 3.628, 3.635, 3.624, 3.621, 3.621, 3.632, 3.627, 3.624, 3.634, 3.621)

a_values*dinosaur_lengths^b_values
```

  - with vectorization:

<!-- end list -->

``` r
##[1]  26039.686  42825.603  10800.224  98273.049 104257.481  41822.386  24840.644   4899.022  39915.948
#[10]  30937.922  26354.908  66384.865  43837.944  97141.451  80553.856 105556.405  97374.660  42760.136
##[19]  18749.274  42109.012  40674.182  26003.425  13229.824  37472.789  34684.033  80187.272   9460.977
##[28]  51630.571  29253.772  36399.306 117511.962  33384.288  58581.226   5462.316  28637.745  15864.172
##[37]   9284.810   1218.755  98522.609  19534.524
```
