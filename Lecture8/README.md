STAT406 - Lecture 8 notes
================
Matias Salibian-Barrera
2017-09-24

Lecture slides
--------------

The lecture slides are [here](STAT406-17-lecture-8-preliminary.pdf).

Non-parametric regression
=========================

Polynomial regression
---------------------

``` r
# help(lidar, package='SemiPar')

data(lidar, package='SemiPar')
plot(logratio~range, data=lidar, pch=19, col='gray', cex=1.5)

# Degree 4 polynomials
pm <- lm(logratio ~ poly(range, 4), data=lidar)
plot(logratio~range, data=lidar, pch=19, col='gray', cex=1.5)
lines(predict(pm)[order(range)] ~ sort(range), data=lidar, lwd=4, col='blue')

# Degree 10 polynomials
pm2 <- lm(logratio ~ poly(range, 10), data=lidar)
lines(predict(pm2)[order(range)]~sort(range), data=lidar, lwd=4, col='red')
```

![](README_files/figure-markdown_github-ascii_identifiers/nonparam-1.png)

``` r
# A more flexible basis: splines

# linear splines ``by hand''
# select the knots at 5 quantiles
kn <- as.numeric( quantile(lidar$range, (1:5)/6) )

# prepare the matrix of covariates / explanatory variables
x <- matrix(0, dim(lidar)[1], length(kn)+1)
for(j in 1:length(kn)) {
  x[,j] <- pmax(lidar$range-kn[j], 0)
}
x[, length(kn)+1] <- lidar$range

# Fit the regression model
ppm <- lm(lidar$logratio ~ x)
plot(logratio~range, data=lidar, pch=19, col='gray', cex=1.5)
lines(predict(ppm)[order(range)]~sort(range), data=lidar, lwd=4, col='green')

# a better way to obtain the same fit
library(splines)
ppm2 <- lm(logratio ~ bs(range, degree=1, knots=kn), data=lidar)
lines(predict(ppm)[order(range)]~sort(range), data=lidar, lwd=2, col='blue')
```

![](README_files/figure-markdown_github-ascii_identifiers/nonparam-2.png)

``` r
# quadratic splines?
plot(logratio~range, data=lidar, pch=19, col='gray', cex=1.5)
ppmq <- lm(logratio ~ bs(range, degree=2, knots=kn), data=lidar)
lines(predict(ppmq)[order(range)]~sort(range), data=lidar, lwd=4, col='steelblue')
```

![](README_files/figure-markdown_github-ascii_identifiers/nonparam-3.png)

``` r
# cubic splines
plot(logratio~range, data=lidar, pch=19, col='gray', cex=1.5)
ppmc <- lm(logratio ~ bs(range, degree=3, knots=kn), data=lidar)
lines(predict(ppmc)[order(range)]~sort(range), data=lidar, lwd=4, col='tomato3')
```

![](README_files/figure-markdown_github-ascii_identifiers/nonparam-4.png)
