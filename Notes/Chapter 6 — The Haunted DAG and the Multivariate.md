## Overview
- Chapter 6 introduces **multiple regression** as a tool for understanding **causal structure**.
- The key idea: adding predictors can either **reveal** or **obscure** relationships.
- This chapter links **regression coefficients** to **DAGs.
- We learn when adding variables helps or harms inference.

---

## 1. Motivation
- In simple regression, one predictor might *stand in* for several hidden causes.
- Multiple regression lets us **control** for variables that might confound relationships.
- But adding predictors can also **open collider paths**, creating *spurious associations*.

---

## 2. General form of the model
A multiple linear regression with predictors $x_1, x_2, \dots, x_k$:

$$
y_i \sim \text{Normal}(\mu_i, \sigma)
$$

$$
\mu_i = \alpha + \beta_1 x_{i1} + \beta_2 x_{i2} + \dots + \beta_k x_{ik}
$$

- $\alpha$ = intercept (expected $y$ when all $x_j=0$)  
- $\beta_j$ = partial effect of predictor $j$ (holding others constant)  
- $\sigma$ = residual standard deviation  

---

## 3. The “Haunted DAG”
- A **DAG** encodes assumed causal directions.  
- A “haunted” DAG refers to missing arrows (unobserved causes) that still haunt the data.  
- Omitted variables can distort regression coefficients.

### Key concept:
When you **omit a common cause**, your regression absorbs its influence into the included variables.

---

## 4. Confounds and Colliders

### Confound (common cause)
A variable $U$ that causes both $X$ and $Y$.
- Omitting $U$ → spurious correlation between $X$ and $Y$.
- To block this back-door path, **include $U$ in the model**.

### Collider
A variable influenced by both $X$ and $Y$.
- Conditioning on a collider **creates** spurious correlation.
- Do **not** include colliders as predictors.

### Mediator
A variable that lies *on* the causal path from $X$ to $Y$.
- Including a mediator blocks part of the causal effect → changes the interpretation of $\beta_X$.

---

## 5. Simultaneous inference

In multivariate regression, $\beta_i$ represents the *partial* relationship:

$$
\beta_i = \text{change in } \mu_y \text{ per unit } x_i \text{, holding other } x_j \text{ constant.}
$$

Interpretation:
- If predictors are correlated, $\beta_i$ adjusts for their overlap.
- $\beta_i$ ≠ simple correlation with $y$; it’s the **unique contribution** of $x_i$.

---

## 6. Multicollinearity
- Occurs when predictors are strongly correlated.
- Leads to **wide posteriors** and **unstable signs** for coefficients.
- The model can still *predict* well, but individual $\beta$s are unreliable.

### Remedies
- Center or standardise predictors.
- Use **prior regularisation** (e.g. $\beta_j \sim \text{Normal}(0,1)$).
- Consider model comparison rather than raw coefficient interpretation.

---

## 7. Model comparison via information criteria
Use WAIC or PSIS-LOO to compare multivariate models.

- Adding predictors always improves fit but may hurt generalisation.
- Bayesian criteria reward **parsimony** by penalising unnecessary complexity.

---

## 8. Example: Marriage Rates and Age
McElreath’s motivating example:
- Predict marriage rate (`M`) using median age at marriage (`A`) and divorce rate (`D`).
- $M \sim \alpha + \beta_A A + \beta_D D$  
- Interpretation shifts once both predictors are included.

→ Demonstrates how controlling for a confound can **reveal true direction**, but adding a collider can **reverse signs**.

---

## 9. DAG logic in practice
### Rules of thumb
1. **Include** confounders (common causes of both outcome and predictor).  
2. **Do not include** colliders (common effects of both).  
3. **Decide carefully** about mediators — depends on causal question.  

This ensures regression reflects causal paths you intend to estimate.

---

## 10. Posterior interpretation
After fitting a multivariate model:
- Summarize with posterior means, intervals (`precis()`).
- Examine **correlations among parameters** (posterior covariance).
- Use **simulated predictions** (`link()`/`predict()`) to check model implications.

---

## 11. Regularization and Shrinkage
- With correlated predictors, regularising priors prevent overfitting.
- Example:
  $$
  \beta_j \sim \text{Normal}(0,\,1)
  $$
- This gently pulls extreme slopes toward 0, improving out-of-sample stability.

---

## 12. Summary Concepts

| Term | Meaning | Include? |
|------|----------|-----------|
| Confound | Common cause of both X and Y | ✅ Yes |
| Mediator | Intermediate on causal path | ⚠️ Maybe |
| Collider | Common effect of X and Y | 🚫 No |

**Goal:** adjust for confounding, avoid conditioning on colliders.

---

## 13. Key takeaways
- Regression is not automatically causal; it’s causal only under the **right DAG assumptions**.
- Coefficients describe **partial relationships**, not isolated effects.
- “Control for everything” is *not* good advice — only control for **common causes**.
- Use DAGs to design models before fitting them.
- Always inspect **posterior correlations** and **predictive performance**.

---

## 14. Rethinking Functions (Julia equivalents)
| Concept | Rethinking Function | Julia Equivalent |
|----------|--------------------|------------------|
| Posterior summary | `precis()` | `precis()` from `StatisticalRethinking.jl` or custom |
| Posterior prediction | `link()` / `sim()` | `predict()` in Turing |
| Model comparison | `compare()` | `waic()` / `loo()` |
| DAG reasoning | `dagitty` (R) | `DAGitty.jl` or manual sketch |

---

### Key Equations
1. **General model**
   $$
   y_i \sim \text{Normal}(\alpha + \sum_j \beta_j x_{ij}, \sigma)
   $$
2. **Partial coefficient meaning**
   $$
   \beta_j = \frac{\partial \mu_y}{\partial x_j}\bigg|_{x_{-j}}
   $$
3. **Model comparison metric**
   $$
   \text{WAIC} = -2(\text{lppd} - p_{WAIC})
   $$

---

###  Phrase:
> *“Multiple regression is a statistical mirror of causal structure.  
> If your DAG is wrong, your coefficients are ghosts.”*

