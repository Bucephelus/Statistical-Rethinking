

## Key Concepts
- **Posterior sampling:**  
  Draw parameter values from the posterior distribution rather than computing integrals.  
  Converts calculus problems into counting problems.

- Each posterior sample represents one plausible world consistent with the data.

## Posterior Summaries
- **Tail mass:**  
  $\Pr(\theta < c \mid \text{data})$ = fraction of posterior samples below $c$.

- **Percentile Interval (PI):**  
  The middle X% of samples (equal tails).  
  - Appropriate for symmetric posteriors.

- **Highest Posterior Density Interval (HPDI):**  
  The smallest interval containing X% of the probability mass.  
  - Always includes the most likely values.  
  - Better for skewed posteriors.

- **Point estimates:**  
  - Mean → minimizes squared error.  
  - Median → minimizes absolute error.  
  - Mode → minimizes 0–1 loss.

- **Compatibility interval:**  
  A more accurate term than “confidence interval.”  
  Indicates parameter values compatible with the model and data.

## Intuition
- The posterior is like a jar of marbles.  
- Sampling = drawing marbles.  
- Summaries describe the pile: averages, intervals, or tail probabilities.

## Posterior Predictive Simulation
- Bayesian models are **generative**: they can simulate new data using posterior samples.  
  $y^{\text{rep}} \sim p(y \mid \theta^{(m)})$

### Uses
- **Prior predictive check:** before data, to test priors.  
- **Model checking:** compare simulated vs. observed data.  
- **Software validation:** test recovery of known parameters.  
- **Research design:** assess identifiability or power.  
- **Forecasting:** generate predictions for new data.

## Key Takeaways
- Sampling converts integration into counting.  
- Posterior summaries describe what parameter values are compatible with data.  
- Bayesian models can generate and test “imaginary” datasets to evaluate model realism.

