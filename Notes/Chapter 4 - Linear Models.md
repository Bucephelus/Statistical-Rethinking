## Core Idea
- Linear models are **stories about averages**.  
- The basic model is:

  $$
  y_i \sim \text{Normal}(\mu_i, \sigma), \quad \mu_i = \alpha + \beta x_i
  $$

- Predictors shift the *mean* of $y$, while $\sigma$ captures residual scatter.

## Parameter Interpretation
- $\alpha$: baseline mean when $x = 0$.  
  - Often centre $x$ so that $\alpha$ represents the mean at an average value.  
- $\beta$: expected change in $y$ per one-unit increase in $x$.  
- $\sigma$: residual variation around the regression line (how noisy the data are).

## Generative View
1. Draw parameters from priors.  
2. Compute $\mu_i = \alpha + \beta x_i$.  
3. Generate fake outcomes $y_i \sim \text{Normal}(\mu_i, \sigma)$.  

If the simulated data look unrealistic, the priors are unrealistic.

## Typical Priors
$$
\alpha \sim \text{Normal}(0, 10), \quad
\beta \sim \text{Normal}(0, 1), \quad
\sigma \sim \text{Exponential}(1)
$$

These are examples, not fixed rules. Always check that the priors generate plausible simulated data.

## Techniques
- **Centring and scaling predictors:**  
  Improves interpretation and numerical stability.  
  - Center: $x' = x - \bar{x}$  
  - Scale: $x'' = (x - \bar{x}) / \text{SD}(x)$  

- **Prior predictive check:** simulate data before fitting to test priors.  
- **Posterior predictive check:** simulate after fitting to assess model fit.  
- **Linear in parameters:**  
  Can include transformations of $x$ (e.g. $x^2$, $\log x$) if coefficients enter linearly.

## Fitting and Posterior
After observing data:

$$
p(\alpha, \beta, \sigma \mid \text{data})
\propto p(\text{data} \mid \alpha, \beta, \sigma)
\, p(\alpha)\, p(\beta)\, p(\sigma)
$$

Posterior samples replace analytic solutions.  
Summaries and predictions are computed directly from these samples.

## Workflow
1. Define causal story.  
2. Write the model $y_i \sim \text{Normal}(\alpha + \beta x_i, \sigma)$.  
3. Choose priors.  
4. Perform prior predictive simulation.  
5. Fit model → obtain posterior samples.  
6. Conduct posterior predictive simulation.  
7. Revise model if misfit remains.

## What "Linear" Really Means
- “Linear” refers to parameters appearing linearly, not necessarily variables.  
  Example:  $$
  \mu_i = \alpha + \beta_1 x_i + \beta_2 x_i^2
  $$
  is still a linear model because $\alpha, \beta_1, \beta_2$ appear to the first power.

## Key Takeaways
- Linear models describe how **means** vary with predictors, not individual data points.  
- Priors regularise and make the model realistic.  
- Simulation (both prior and posterior predictive) is essential for understanding model behaviour.  
- Bayesian regression is a **generative model**: it predicts new data as well as describing existing data.
