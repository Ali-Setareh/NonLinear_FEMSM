# 5-minute speaker notes

## Slide 1 - Title (20s)
My thesis compares two approaches for estimating causal effects with time-varying treatments when there is a stable unmeasured confounder. The focus is both conceptual - what assumptions each method makes - and empirical - how they behave in simulation.


## Slide 2 - Motivation (45s)
In longitudinal observational data, treatments are assigned repeatedly over time. Standard g-methods can adjust for measured time-varying confounders, but they require sequential ignorability. This is often unrealistic, because stable characteristics such as baseline severity, personality, or political leaning may affect both treatment decisions and outcomes. My thesis focuses on this time-invariant unmeasured confounding problem.

## Slide 3 - Baseline 
For the oral explanation, say something like: “This is the standard IPTW-MSM pipeline. First we estimate the probability of receiving each observed treatment given the past observed history. Then we weight individuals by the inverse of these probabilities, creating a pseudo-population where treatment is balanced with respect to measured confounders. Finally, we fit a weighted marginal structural model. The limitation is exactly the assumption on the previous slide: this only works if the observed history contains all relevant confounders.”

## Slide 4 - Target (50s)
The causal target is an average potential outcome under interventions on the last few treatment periods, leaving the earlier history as observed. This is the truncated treatment-regime target. In the simulation, the MSM has two parameters: the final-period treatment effect tau_F and the cumulative recent-treatment effect tau_C. The key idea of both methods is to condition on a unit-specific hidden factor, either a fixed effect or a latent substitute confounder.

## Slide 5 - Methods (55s)
FE-MSM puts a unit fixed effect directly into the treatment model used for propensity-score estimation. SeqGPLVM instead infers a latent variable from the whole treatment history using a conditional Markov structure and Gaussian-process latent variable model. After that, both methods use the same IPTW/MSM pipeline. So the comparison is mainly about how the missing stable factor is represented and estimated.

## Slide 6 - Simulation design (50s)
The simulation uses a known DGP based on Blackwell and Yamauchi. Treatment depends on the previous treatment, observed covariates, and the unobserved time-invariant factor U. The outcome depends on U, the final treatment, the sum of treatments in the previous three periods, and average covariates. This gives known true values: tau_F equals 1 and tau_C equals 0.3. I vary sample size, the ratio N over T, and the strength of unmeasured confounding.

## Slide 7 - Results (65s)
The main finding is that both methods improve over naive IPTW, especially when the treatment history is longer. FE-MSM generally has lower bias and lower standard error in this DGP, likely because its propensity model is correctly specified. SeqGPLVM is more flexible, but in finite samples it is less stable, especially when the treatment sequence is short and unmeasured confounding is strong. Coverage is not uniformly close to the nominal level, so the methods should not be viewed as automatic fixes.

## Slide 8 - Conclusion (55s)
The thesis contributes a unified presentation of the assumptions, a detailed SeqGPLVM loss-function derivation, a modular implementation, and a common simulation comparison. The main conclusion is that both methods are useful for understanding how one might address time-invariant unmeasured confounding, but both rely on strong assumptions. FE-MSM is simpler and more stable here, while SeqGPLVM is more flexible but depends on strong latent-identifiability assumptions and enough treatment history.
