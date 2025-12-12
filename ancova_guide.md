# ANCOVA Guide for Weightlifting Example

## 1. What is ANCOVA

ANCOVA = **AN**alysis of **CO**variance\
It combines: - **ANOVA** (comparing group means)\
- **Regression** (using a numerical predictor)

Formally:\
**ANCOVA = ANOVA + a regression line adjustment.**

------------------------------------------------------------------------

## 2. The Role of the Covariate

A **covariate** is a numerical variable included to account for
differences between individuals that are *not part of your main
experimental groups*. It reduces unexplained error, adjusts group means,
and increases power.

### In the weightlifting example

-   **Response (Y):** Max squat (kg)\
-   **Factor:** Training program (A/B/C)\
-   **Covariate:** Body weight (kg)

You include body weight to **control for it**, not study it.

------------------------------------------------------------------------

## 3. Why Use a Covariate?

Without body weight: - Programs might look different due to athletes'
sizes.

With the covariate: - Squat scores are adjusted "as if" all athletes had
the same body weight.

This creates a fair comparison.

------------------------------------------------------------------------

## 4. ANCOVA as Regression

ANCOVA is **multiple regression** with a categorical + numerical
predictor.

\`\`\` Squat = β0 + β1(Program) + β2(BodyWeight) \`\`\`

This is why exercises often involve both ANCOVA and regression---they
are the same model written differently.

------------------------------------------------------------------------

## 5. Example With 8 Athletes

  Athlete   Program   Body_weight   Max_Squat
  1         A         70                 150
  2         A         82                 180
  3         B         77                 172
  4         B         85                 190
  5         C         68                 145
  6         C         79                 170
  7         A         90                 200
  8         B         72                 160

ANCOVA adjusts for weight before comparing programs.

------------------------------------------------------------------------

## 6. Running ANCOVA in Minitab

**Stat → ANOVA → General Linear Model**

-   **Response:** Max Squat\
-   **Model:** Program Weight\
-   Program = categorical\
-   Weight = covariate

Key outputs: - Covariate slope\
- Adjusted program means\
- p-value for Program (after adjusting)

------------------------------------------------------------------------

## 7. Interpretation

### If Weight is significant:

Heavier athletes squat more.

### If Program is significant:

Programs differ even after controlling for weight.

### Adjusted means:

Fair comparison of programs.

------------------------------------------------------------------------

## 8. Covariate Confusion Fix

Think of the covariate as a **fairness correction variable**.

------------------------------------------------------------------------

## Summary

  Term              Meaning
  ----------------- ------------------------------------------------
  Response          max squat
  Factor            training program
  Covariate         body weight
  ANCOVA            compares programs while adjusting for weight
  Regression link   ANCOVA = regression with categorical variables

## About regression
ANCOVA is related to regression. So you might encounter questions in your examinations about this. for instance: 

⭐ QUESTION 1: Is the slope of the covariate (Weight) significantly different from 0 at α = 0.05?
✔️ Step 1 — Go to:
Stat → ANOVA → General Linear Model → Fit General Linear Model
✔️ Step 2 — Fill in the fields:
Response: Squat
Model: Program Weight

✔️ Decision rule:
If
p-value for Weight < 0.05 → slope is significantly different from 0
If
p-value > 0.05 → slope is NOT significant
✔️ Interpretation:
There is (or is not) a significant linear relationship between body weight and max squat at the 5% level.

⭐ QUESTION 2: Does Program A have a different slope than other programs? (meaning: Are the slopes different between groups?)
This tests the homogeneity of regression slopes assumption.

✔️ Step 1 — Same menu:
Stat → ANOVA → General Linear Model → Fit General Linear Model

✔️ Step 2 — Add an interaction to the model
In the Model box, click:
Program
Weight
Then click “Add interaction”

✔️ Step 3 — Run the model
✔️ Decision rule:
If P < 0.05 → slopes DO differ between programs
(meaning Program A may have a different slope)

If P > 0.05 → slopes do NOT differ
(you can run standard ANCOVA and compare adjusted means)

✔️ Interpretation:
The Program × Weight interaction is (or is not) significant at the 5% level,
indicating that the relationship between weight and squat does / does not differ among training programs.

🎯 1. What is a slope in ANCOVA?

In ANCOVA, the slope is the relationship between the covariate and the response.

Here:

Covariate = Weight

Response = Max Squat

So the slope answers:

“For each extra kilogram of body weight, how many extra kg can someone squat?”

Example:
If the slope is +1.5, this means:

Every +1 kg of body weight → expected squat +1.5 kg

That’s it. The slope is just the regression coefficient for Weight.

🧩 2. Why do slopes matter in ANCOVA? Two reasons.
A. First reason: is the covariate useful at all?

You test whether the slope is different from zero.

If slope ≠ 0 → body weight really affects squat → useful covariate

If slope = 0 → body weight has no relationship with squat → useless covariate

This is the Weight p-value in Minitab.

This is the question you were originally thinking of.

B. Second reason: do different groups have different slopes?

This is the confusing part for most students.

This question checks whether the relationship between Weight and Squat is the same for each training program (A, B, C).

This is what you test by adding Program * Weight (the interaction).

What does “slopes differ” actually mean?

Example:

Program	Slope (effect of weight on squat)
A	1.0
B	1.0
C	1.0

→ Slopes are equal
→ Standard ANCOVA is valid
→ You can compare adjusted means

versus

Program	Slope
A	3.0
B	1.0
C	1.0

→ Slopes are NOT equal
→ Program A’s athletes gain much more squat per kg of body weight
→ This breaks a key assumption
→ You can't compare adjusted means because “adjusting” does not make sense when the lines aren’t parallel

📈 3. Visual intuition: this is the whole idea

If slopes are equal → lines are parallel

If slopes differ → lines fan out, cross, or diverge

Parallel lines → ANCOVA works
Non-parallel lines → ANCOVA breaks

(Imagine 3 lines on a scatterplot, one for each program.)

🔍 4. How does Minitab check slope equality?

It tests the Program × Weight interaction.

If p > 0.05 → slopes are equal → ANCOVA assumption is met

If p < 0.05 → slopes differ → ANCOVA assumption is violated

This is not about which program is “better.”
It’s about whether the covariate works the same way across groups.

📝 5. Why slopes must be equal for ANCOVA to work

Because ANCOVA “adjusts” group means by assuming:

“If everyone weighed the same amount, what would their squat be?”

If the slopes differ, then the adjustment depends on weight differently for each group, so there is no single fair adjustment point.

This is also why Minitab warns you in textbooks:

Check the homogeneity of regression slopes assumption.

🧠 6. Summary

Testing the covariate slope answers:
→ Does weight affect squat at all?

Testing slope equality across groups answers:
→ Does weight affect squat the same way in Program A, B, and C?
→ If no, ANCOVA is invalid.

