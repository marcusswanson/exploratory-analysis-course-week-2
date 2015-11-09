# exploratory-analysis-course-week-2

## Notes from the course videos:

## Lattice plot functions:

 - xyplot - main function for creating scatterplots
 - bwplot - box-and-whiskers plots ("boxplots")
 - histogram - histograms
 - stripplot - like a boxplot but with actual points
 - dotplot - plot dots on "violin strings"
 - splom - scatterplot matrix; like pairs in base plotting system
 - levelplot, contourplot: for plotting "image" data
 
 Summary:
 
 xyplot(y ~ x | f * g, data)
 
 y = y-axis data
 x = x-axis data
 f and g are condition variables with * indicating an interaction between two variables

 e.g:

 ## Example 1
 
 library(lattice)
 library(datasets)
 xyplot(Ozone ~ Wind, data = airquality)

 ## Example 2

 airquality <- transform(airquality, Month = factor(Month))
 xyplot(Ozone ~ Wind | Month, data = airquality, layout = c(5,1))
 
 ## Multiple panels
 
 set.seed(10)
 x <- rnorm(100)
 f <- rep(0:1, each=50)
 y <- x + f - f * x + rnorm(100, sd=0.5)
 f <- factor(f, labels = c("Group 1", "Group 2"))
 xyplot(y ~ x | f, layout = c(2, 1))
 

 ## Custom panel function
 xyplot(y ~ x | f, panel = function(x,y,...){
 panel.xyplot(x, y, ...) ## First call the default panel function for 'xyplot'
 panel.abline(h = median(y), lty = 1) ## Add a horizontal line at the median
 })

 xyplot(y ~ x | f, panel = function(x,y,...){
 panel.xyplot(x, y, ...) ## First call the default panel function for 'xyplot'
 panel.lmline(x, y, col=2) ## Overlay a simple regression line
 })

 
