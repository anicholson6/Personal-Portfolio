

# Evaluating Job Training Impact via Propensity Score Matching

## Pseudo Business Problem: Is the NSW Program Working?

A 1974 government-funded job training program was launched to help marginalized individuals increase their earning potential. However, comparing the average earnings between the participants and control group suggested the program was a failure. **Participants were earning $635 less than non-participants three years later.**

The data science team suspected **Selection Bias** could be an issue because the program specifically targeted disadvantaged individuals (younger, less educated, mostly black). It would be unfair to do a direct comparison to the control which leaned older and whiter. To find the true impact, we used **Propensity Score Matching (PSM)** to create a balances comparison without confounding variables.

## Methodology: Correcting Selection Bias

I implemented a causal inference analysis to match the propensities between teh control and treatment.:

1. **Propensity Score Estimation:** Used **Logistic Regression**  to predict the probability of a person joining the program based on their background.
2. **Nearest Neighbor Matching:** For every program participant, I identified a match in the control group with the closest propensity score.
3. **Balance Validation:** Then used a **Love Plot** to ensure that after matching, the groups were balanced (aiming for a Standardized Mean Difference < 0.1).


![images](images/lalonde_love_plot.png)

## Business Impact

* **Initial Conclusion:** A simple A/B test suggested a **-$635** loss in earnings, which could have led to the program's cancellation.
* **New Causal Conclusion:** After matching, I see an average lift of **$1,376** in annual earnings per participant.
* **Statistical Conclusion:** However, the analysis yielded a p-value of **0.057**. While slightly above the 0.05 threshold, the $1,376 lift gives me pause to firmly say the program "isn't working".


## Summary & Recommendations

The program is effective for its target demographic, providing over $1,300 in incremental annual value per person. I highly recommend extending the pilot for longer to capture a larger sample size. 

Age seemed to still be the biggest factor in earnings, so we should also choose a control group with similar age ranges as participants. If we cannot get a firmer conclusion on effectiveness after more samples, then we can give a "yes or no".

## Notebook Work
[Lalonde Propensity Score Model](propensity_score_match.ipynb)