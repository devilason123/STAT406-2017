STAT406 - Lecture 4 notes
================
Matias Salibian-Barrera
2017-09-11

Lecture slides
--------------

The lecture slides are [here](STAT406-17-lecture-4-preliminary.pdf).

Estimating MSPE with CV when the model was built using the data
---------------------------------------------------------------

One needs to be careful.

"Direct" comparison of models -- AIC
------------------------------------

A different approach to comparing competing models is to assess how "close" they are from the actual stochastic process generating the data (here "stochastic process" refers to the random mechanism that generated the data). In order to do this one needs:

1.  a distance / metric (or at least a "quasimetric") between models; and
2.  a way of estimating this distance when the "true" model is unknown.

AIC provides an unbiased estimator of the Kullback-Leibler divergence between the estimated model and the "true" one.

Shrinkage methods / Ridge regression
------------------------------------

To manage correlated explanatory variables...

### Selecting the amount of shrinkage