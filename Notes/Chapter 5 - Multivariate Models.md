## Purpose
- Extends linear models to include **multiple predictors**.  
- Allows analysis of **conditional relationships** and helps detect **spurious correlations**. 
- The main goal is to separate genuine causal effects from associations caused by confounding.

## Model Form
$$
y_i \sim \text{Normal}(\mu_i, \sigma)
$$
$$
\mu_i = \alpha + \beta_1 x_{1i} + \beta_2 x_{2i} + \dots
$$

- Each predictor $x_j$ contributes additively to the expected mean $\mu_i$.
- The model remains linear because parameters appear to the first power.

## Intuition
- Each coefficient $\beta_j$ represents the expected change in $y$ for a one-unit increase in $x_j$, **holding all other predictors constant**.  
- Adding predictors changes the meaning of each $\beta_j$ — coefficients are always *conditional* on the other variables in the model.
- Interpretation depends on the causal story: statistical association ≠ causation.

## Correlation and Confounding
- **Collinearity:** predictors share information; their posteriors become correlated and wider.  
- **Spurious correlation:** arises when two variables are correlated through a third, un-modelled cause.  
- **Multicollinearity:** strong correlations between predictors lead to unstable coefficients and broad posterior distributions.

**Example:**  
If divorce rates correlate with both age structure and marriage rates, failing to include age structure creates a spurious link between divorce and marriage.

## Posterior Correlation Structure
- Joint posterior plots (elliptical clouds) show parameter trade-offs.  
- Tilted ellipses = correlated parameters; round ellipses = independent parameters.  
- Correlation among $\beta$'s means uncertainty in one coefficient depends on another.

## Practical Tools
- **Centring predictors:**  
  Keeps the intercept $\alpha$ interpretable as the mean outcome when all predictors are at their average values.

- **Standardising (z-scores):**  
  $x' = \dfrac{x - \bar{x}}{\text{SD}(x)}$  
  Allows direct comparison of effect sizes and improves computation.

- **Interactions:**  
  Add terms like $\beta_{1,2} x_1 x_2$ to model joint effects between predictors.

- **Model comparison:**  
  Evaluate alternative models using posterior predictive checks or information criteria (e.g. WAIC), not p-values.

## Posterior Predictive Simulation
- As before, generate replicated data:
  $$
  y_i^{\text{rep},(m)} \sim \text{Normal}(\alpha^{(m)} +
  \beta_1^{(m)}x_{1i} + \beta_2^{(m)}x_{2i},\, \sigma^{(m)})
  $$
- Compare simulated distributions to observed data to check model fit.
- Persistent misfit indicates missing structure (e.g. nonlinearity, interactions, or hierarchical effects).

## Causal Reasoning
- Adding or removing predictors corresponds to conditioning on different variables.  
- Always build models from a **causal story** rather than purely statistical convenience.  
- “Controlling for” a variable means estimating the effect of one variable while accounting for another.

## Key Takeaways
- Multiple regression describes **conditional relationships** — how $y$ changes with $x_j$ when other predictors are held constant.  
- Multicollinearity increases uncertainty but does not bias estimates.  
- Bayesian multivariate models automatically propagate uncertainty across correlated parameters.  
- Model selection should follow the causal logic of the system, not mechanical criteria.

##  Workflow
1. Specify the causal story.  
2. Choose predictors c
