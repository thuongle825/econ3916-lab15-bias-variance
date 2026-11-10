# econ3916-lab15-bias-variance
# The Bias-Variance Tradeoff: Choosing How Flexible a Model Should Be

## Objective
I fit polynomials of increasing degree to simulated data with a known true curve to see how bias and variance trade off, and to choose a degree by cross-validation instead of by training error.

## Methodology
- Simulated a world with a known true curve plus noise, and drew one training sample of 60 points.
- Split the error of polynomial fits into bias squared and variance, using 200 fresh samples at each of six degrees.
- Compared training error with error on 2,000 new points for degrees 1 to 15, and found the degree where the held-out error was lowest.
- Chose a degree by 5-fold cross-validation, and looked at how much the error varied from fold to fold.
- Used nested cross-validation to check whether the smallest CV error is a fair estimate of the error on new data.
- Wrote a small function, `kfold_mse()`, that gives the k-fold CV error for any degree and number of folds, and checked it with 10 folds.

## Key Findings
- Bias squared fell to near zero by degree 5, while variance rose from 0.0180 at degree 5 to 0.0994 at degree 15. Past degree 5, extra flexibility only followed the noise.
- Training error fell at every degree, so it could not tell me where to stop. Held-out error on the 2,000 new points was lowest at degree 5.
- 5-fold CV chose degree 4, with a CV MSE of 0.1401. Degrees 4 and 5 were close, and both had a much smaller spread across folds than the other degrees.
- The nested CV estimate was 0.2070, well above 0.1401. Choosing a degree and scoring it with the same folds made the smallest CV error look better than it was.
- With 10 folds, my function gave a CV MSE of 0.1409 for degree 4 and 0.1457 for degree 5. Degree 4 stayed lowest, but the gap between the two got smaller.
