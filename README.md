# Multivariate OLS — What "Controlling For" Actually Does

## Objective
I used simulated wage data to see what adding or leaving out a control variable does to a regression estimate, and when controlling for something helps or hurts.

## Methodology
- I simulated wages that depend on education, experience, union status, and an unobserved ability term, with a true return to education of 2,500.
- I ran the wage regression twice, once leaving ability out and once putting it in, and compared each education coefficient to the true value.
- I calculated the bias predicted by the omitted-variable-bias formula (the effect of ability on wages times the slope from regressing ability on education) and compared it to the actual bias in my short regression.
- I checked the Frisch-Waugh-Lovell theorem. I took the residuals from regressing wages on ability and the residuals from regressing education on ability, then regressed the first set on the second.
- I added a collider, a variable caused by both the outcome and the treatment, to a model where the true effect was zero, and recorded the estimate and its p-value.
- I created a strongly correlated pair of regressors and compared standard errors and coefficient estimates with and without the correlation.
- I fitted an interaction between experience and union membership to get a separate experience slope for each group.
- I asked an AI to write a function that builds a specification table, revised my prompt once, and checked its coefficients against regressions I ran myself.

## Key Findings
- **Omitted ability biases the estimate.** Leaving ability out gave a return to education of 5,126 against a true 2,500, roughly double. Putting ability in brought it down to 2,546.
- **The bias formula works.** It predicted a bias of 2,629, and the actual bias was 2,626.
- **"Controlling for" means partialling out.** Regressing the part of wages that ability does not explain on the part of education that ability does not explain gave the same coefficient as the full regression. Adding a control amounts to using only the variation in education that the control cannot account for.
- **Some controls make things worse.** Controlling for a collider turned a true effect of zero into an estimate of -0.596, with a p-value that printed as 0.000. The p-value was rounded for display, not exactly zero. A tiny p-value showed that the estimate was precise. It did not show that the estimate was right.
- **Multicollinearity hurts precision, not accuracy.** Standard errors were about 12 times larger, but the estimates were still centered on the true values.
- **Effects can differ by group.** A year of experience was worth 903 to non-union workers and 504 to union members.
- **AI code needs checking.** I revised my prompt once, and I only trusted the specification-table function after its coefficients matched my own regressions.
