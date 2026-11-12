# econ5200-lab12-instrumental-variables
# Instrumental Variables: Weak Instruments, Compliers and the Exclusion Restriction

## Objective

I set out to see how 2SLS behaves when its assumptions start to fail — when the instrument is weak, and when it has a small direct effect on the outcome — and to confirm I understand the estimator by building it myself.

## Methodology

- Simulated data from a model with a known true effect of 1.0, with endogeneity that biases OLS upward, and with an instrument weak enough that the median first-stage F was 0.5.
- Recorded the median OLS and median 2SLS estimates across the simulation draws, and looked separately at the 2SLS estimates that came out statistically significant.
- Replicated Card's (1995) college-proximity instrument for years of schooling, estimating the return to schooling by OLS and by 2SLS and reporting the first-stage F statistic.
- Added a small direct effect of the instrument on the outcome, violating the exclusion restriction, and measured how far that moved the 2SLS estimate.
- Wrote my own two-stage least squares function out of two OLS regressions, and checked its output against the `linearmodels` package.

## Key Findings

- With a median first-stage F of 0.5, 2SLS was no rescue. The median 2SLS estimate was 2.038, slightly worse than the median OLS estimate of 1.998, against a true effect of 1.0. A weak instrument pulls 2SLS toward the OLS bias rather than away from it.
- Statistical significance did not help. Among the 2SLS estimates that came back significant, most were still far from the true value of 1.0, so a significant result here is not evidence that the estimate is close to the truth.
- In the Card replication the instrument was much stronger, with a first-stage F of 16.7. The OLS return to schooling was 0.0740 and the 2SLS return was 0.1323 — 2SLS came in higher, not lower, which is the opposite of what simple ability bias in OLS would predict.
- Breaking the exclusion restriction by even a small amount shifted the 2SLS estimate, and there is nothing in the output that flags the violation. The assumption has to be argued, not tested.
- My hand-written two-stage function matched `linearmodels` on the point estimates, which confirmed that the estimator really is just two stacked OLS regressions. The standard errors are where the packaged version earns its keep.
