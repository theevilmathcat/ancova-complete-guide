# ANCOVA Exercise: Weightlifting Data

The following is an ANCOVA exercise to explain how this works.

The idea here is: experienced and inexperienced athletes with different bodyweights and total deadlifts they did (in kg).

1. Open the attached `ancova_weightlifting_file.mpx`

### Model Components Summary

| Item                  | What it is                                           | Details from your data                          |
|-----------------------|------------------------------------------------------|-------------------------------------------------|
| Response variable (Y) | The outcome we are trying to explain/predict         | Deadlift_kg (in kg)                             |
| Covariate             | Continuous variable we control for (adjust for)      | Bodyweight_kg (in kg)                           |
| Categorical factor    | The grouping variable we want to compare             | Group (2 levels: Experienced vs. Inexperienced) |
| Model type            | ANCOVA with interaction                              | Deadlift_kg ~ Bodyweight_kg + Group + Bodyweight_kg × Group |

2. Then do the ANCOVA  
   Stat → Regression → General Linear Model → Fit General Linear Model  
   A. Response: Select Deadlift_kg → click Response.  
   B. Model (Predictors)  
      Under Factors, add Group.  
      Under Covariates, add Bodyweight_kg.  
   C. Add the interaction term: Click Model. Highlight Bodyweight_kg and Group. Add → Choose Interaction  
   D. Click ok to Return and Run.

3. Then if you want to know if the covariate slope is for instance significantly different from 2.8  
   the procedure is:  
   Data > Subset Worksheet  
   -> Column: Group  
   -> Values: Experienced  
   then do:  
   Stat > Regression > Regression > Fit Regression Model  
   under the coefficients, you are going to get 2.43 Bodyweight_kg and 0.0363 SE Coef. and because we are comparing to 2.8 you do:  
   t = (2.43 - 2.8) / 0.0363 = -10.1928  

   Then do the same for inexperienced athletes.  
   Data > Subset Worksheet  
   -> Column: Group  
   -> Values: Inexperienced  
   then do:  
   Stat > Regression > Regression > Fit Regression Model  
   under the coefficients, you are going to get 2.7066 Bodyweight_kg and 0.0786 SE Coef. and because we are comparing to 2.8 you do:  
   t = (2.7066 - 2.8) / 0.0786 = -1.1883  

   Now we need the critical value to check against our test statistics.  
   at DF = n-2 = 25-2 = 23 and a two-tailed test of 5% so 2.5%, (page 47 of the cambridge statistical tables)  
   a CV of 2.069.  

   so:  
   - Inexperienced lifters: |10.193| is > than 2.069 so we reject the null and conclude the slope is significantly different than 2.8 at 5% significance level  
   - Experienced lifters: |-1.1883| is < than 2.069 so we fail to reject the null and conclude the slope is not significantly different than 2.8 at 5% significance level  

### Group Comparison Against Target Slope (2.8)

| Group         | Estimated Slope | SE of Slope | t = (Slope − 2.8) / SE | df | p-value | Conclusion (at α = 0.05)                                      |
|---------------|-----------------|-------------|-------------------------|----|---------|--------------------------------------------------------------|
| Inexperienced | 2.430           | 0.0363      | -10.193                 | 23 | 0.0000  | p < 0.05 → Significantly different from 2.8 (lower than 2.8) |

| Experienced   | 2.7066          | 0.0786      | -1.188                  | 23 | 0.247   | p > 0.05 → Not significantly different from 2.8              |
