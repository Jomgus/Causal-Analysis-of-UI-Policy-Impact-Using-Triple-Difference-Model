The analysis relies on CPS file stored externally : https://drive.google.com/file/d/1QQ9AD1ozgE56n1smAfVc4Vl-ml1inrUf/view?usp=sharing

# Triple-Difference Analysis of UI Policy's Differential Impact on Job-Finding
### Context

This capstone project is a quasi-experimental causal analysis of a major 2021 US labor policy: the early termination of pandemic unemployment benefits. In mid-2021, 26 states prematurely cut these federal benefits, while 24 states continued them until the national expiration in September. This created a large-scale natural experiment.


This project investigates the causal impact of this policy on job-finding rates, specifically testing the hypothesis that low-wage workers were affected differently than other-wage workers. Building on the methodology of Holzer et al. (2021) , this analysis moves from a simple baseline DiD on aggregate state-level data (from Opportunity Insights ) to a more robust Triple-Difference (DDD) model using CPS microdata.

### Key Findings

Our analysis reveals a significant differential impact of the policy, proving that low-wage workers were resilient to this specific policy change.

Other-Wage Workers (Significant Effect): For the "Other-Wage" group, terminating benefits worked as expected. It caused a 4.7 percentage point increase in their job-finding (U-to-E) rate (p=0.052).

Low-Wage Workers (No Effect): For our target "Low-Wage" group (defined as Leisure & Hospitality + Retail.source[82-85]`]), the policy had no statistically significant effect on their job-finding rate (p=0.470).

The Causal "Gap" (Significant DDD): Our main Triple-Difference model, which directly compares these two effects, confirms that this gap is statistically significant. The TreatState*Post*LowWage interaction coefficient was -0.080 (p=0.035), providing robust evidence that the policy's impact on low-wage workers was statistically different from its impact on everyone else.
