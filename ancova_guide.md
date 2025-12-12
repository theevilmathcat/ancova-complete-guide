# ANCOVA Guide for Weightlifting Example

## 1. What is ANCOVA
ANCOVA = **AN**alysis of **CO**variance  
It combines:  
- **ANOVA** (comparing group means)  
- **Regression** (using a numerical predictor)

Formally:  
**ANCOVA = ANOVA + a regression line adjustment.**

---

## 2. The Role of the Covariate
A **covariate** is a numerical variable included to account for differences between individuals that are *not part of your main experimental groups*. It reduces unexplained error, adjusts group means, and increases power.

### In the weightlifting example
- **Response (Y):** Max squat (kg)  
- **Factor:** Training program (A/B/C)  
- **Covariate:** Body weight (kg)

You include body weight to **control for it**, not study it.

---

## 3. Why Use a Covariate?
Without body weight:  
- Programs might look different due to athletes' sizes.

With the covariate:  
- Squat scores are adjusted "as if" all athletes had the same body weight.

This creates a fair comparison.

---

## 4. ANCOVA as Regression
ANCOVA is **multiple regression** with a categorical + numerical predictor.


This is why exercises often involve both ANCOVA and regression — they are the same model written differently.

---

## 5. Example With 8 Athletes

| Athlete | Program | Body_weight | Max_Squat |
|---------|---------|-------------|-----------|
| 1       | A       | 70          | 150       |
| 2       | A       | 82          | 180       |
| 3       | B       | 77          | 172       |
| 4       | B       | 85          | 190       |
| 5       | C       | 68          | 145       |
| 6       | C       | 79          | 170       |
| 7       | A       | 90          | 200       |
| 8       | B       | 72          | 160       |

ANCOVA adjusts for weight before comparing programs.

---

## 6. Running ANCOVA in Minitab
**Stat → ANOVA → General Linear Model**

- **Response:** Max Squat  
- **Model:** Program Weight  
- Program = categorical  
- Weight = covariate

Key outputs:  
- Covariate slope  
- Adjusted program means  
- p-value for Program (after adjusting)

---

## 7. Interpretation

### If Weight is significant:
Heavier athletes squat more.

### If Program is significant:
Programs differ even after controlling for weight.

### Adjusted means:
Fair comparison of programs.

---

## 8. Covariate Idea
Think of the covariate as a **fairness correction variable**.

---

## Summary

| Term            | Meaning                                                  |
|-----------------|----------------------------------------------------------|
| Response        | max squat                                                |
| Factor          | training program                                         |
| Covariate       | body weight                                              |
| ANCOVA          | compares programs while adjusting for weight             |
| Regression link | ANCOVA = regression with categorical variables           |

---

## About regression
ANCOVA is closely related to regression, so you might encounter exam questions like these:

### QUESTION 1: Is the slope of the covariate (Weight) significantly different from 0 at α = 0.05?

**Steps**  
1. Stat → ANOVA → General Linear Model → Fit General Linear Model  
2. Response: Squat  
   Model: Program Weight  

**Decision rule**  
- If p-value for Weight < 0.05 → slope is significantly different from 0  
- If p-value > 0.05 → slope is NOT significant  

**Interpretation**  
There is (or is not) a significant linear relationship between body weight and max squat at the 5% level.

### QUESTION 2: Does Program A have a different slope than other programs?  
(This tests the **homogeneity of regression slopes** assumption)

**Steps**  
1. Same menu as above  
2. In the Model box add: Program, Weight, and the Program*Weight interaction  
3. Run the model  

**Decision rule**  
- If interaction P < 0.05 → slopes differ between programs  
- If interaction P > 0.05 → slopes do NOT differ (standard ANCOVA is valid)

**Interpretation**  
The Program × Weight interaction is (or is not) significant at the 5% level, indicating that the relationship between weight and squat does / does not differ among training programs.

---

### 1. What is a slope in ANCOVA?
In ANCOVA, the slope is the relationship between the covariate and the response.  
Here: Covariate = Weight, Response = Max Squat  

It answers:  
**“For each extra kilogram of body weight, how many extra kg can someone squat?”**

Example: slope = +1.5 → every +1 kg body weight → expected squat +1.5 kg

---

### 2. Why do slopes matter in ANCOVA? Two reasons

**A. Is the covariate useful?**  
Test slope ≠ 0 (Weight p-value in Minitab).

**B. Do groups have the same slope?**  
Test Program × Weight interaction.

| Program | Slope (kg squat per kg body weight) |
|---------|--------------------------------------|
| A       | 1.0                                  |
| B       | 1.0                                  |
| C       | 1.0                                  |
→ Equal slopes → standard ANCOVA valid

| Program | Slope |
|---------|-------|
| A       | 3.0   |
| B       | 1.0   |
| C       | 1.0   |
→ Unequal slopes → assumption violated → cannot compare adjusted means

---

### 3. Visual intuition
- Parallel lines → ANCOVA works  
- Non-parallel lines → ANCOVA breaks

---

### 4. How Minitab checks slope equality
Tests the **Program × Weight** interaction term.

---

### 5. Why slopes must be equal
ANCOVA assumes a single fair adjustment point (“as if everyone had the same weight”). Unequal slopes destroy that common adjustment.

---

### 6. Quick recap
- Covariate slope test → Does weight affect squat at all?  
- Interaction test → Does weight affect squat the **same way** across programs?  
  - If no → standard ANCOVA is invalid
 
### Solved Exercises
As you know by now your teacher is a moron. And they make a point of overly complicating things into oblivion. So my job as a cat is to call your teacher a retard and simplify your life. You are not my enemy as long as you bring me food. So in the spirit of college complication here we go:
#### Overly complicated questions to answer
"We want to verify the effect of 2 substances (A and B) on the growth of the circumference of algae X. For each medium, we measured the average cell circumference every 2 days."

"Culture days: 1, 3, 5, 7, 9;
Medium A: 12.2, 14.2, 16.7, 18, 27.3;
Medium B: 9.8, 10.8, 13.3, 15.7, 20.8.

a) Can we say, with a 5% risk, that substances A and B have a different effect on algae growth?
b) In a natural medium, the slope of the growth line is 0.84. Do A and B significantly influence growth?
c) If we sample after 4 days, what will be the estimated value of the average algae circumference in medium A, and its 95% confidence interval / safety coefficient?"

#### Solution
Response (Y): Average circumference (like max squat).
Factor: Medium/Substance (A or B, like training program).
Covariate: Days (like body weight)—a numerical predictor to control for time's effect on growth.

The goal is to compare A vs. B while adjusting for days, assuming the relationship (slope) between days and circumference is the same for both (parallel lines). If slopes differ, standard ANCOVA doesn't apply directly.

Data Setup in Minitab

Open Minitab and enter the data into a worksheet:
Column C1: Days – enter 1, 3, 5, 7, 9 (twice, once for A and once for B).
Column C2: Medium – enter A, A, A, A, A, B, B, B, B, B.
Column C3: Circumference – enter 12.2, 14.2, 16.7, 18, 27.3, 9.8, 10.8, 13.3, 15.7, 20.8.
It should look like your guide's athlete table:
Days,Medium,Circumference
1,A,12.2
3,A,14.2
5,A,16.7
7,A,18.0
9,A,27.3
1,B,9.8
3,B,10.8
5,B,13.3
7,B,15.7
9,B,20.8

Minitab Steps (Following Your Guide)
Follow Stat → ANOVA → General Linear Model → Fit General Linear Model (like section 6 in your guide).
Step 1: Check if Slopes Differ Between A and B (Homogeneity Assumption, Like QUESTION 2 in Your Guide)

Response: Circumference.
Model: Click the box, add Days (covariate) and Medium (factor). Then click "Add interaction" to include Days × Medium.
Run the model.

Key outputs (what Minitab shows, confirmed by computation):

Slope for Days (overall relationship): 1.700, p = 0.002 (significant, like QUESTION 1 in your guide—covariate is useful).
Interaction (Days × Medium): Coefficient = -0.355, p = 0.468 (> 0.05).
Interpretation (from your guide): Slopes do NOT differ between A and B (p > 0.05). The relationship between days and circumference is the same for both. Standard ANCOVA is valid—proceed without interaction to compare adjusted groups.


Step 2: Run Standard ANCOVA (Without Interaction, Like Main Guide Steps)

Response: Circumference.
Model: Days and Medium (no interaction).
Run the model.

Key outputs:

Slope for Days: 1.523, p < 0.001 (significant—days affect circumference).
Medium (B vs. A): Coefficient = -3.600, p = 0.024 (< 0.05).
Interpretation: After adjusting for days, A and B differ significantly. The adjusted mean circumference is higher for A by 3.6 units.


For Part a): Do A and B Have Different Actions on Growth? (5% Risk = α=0.05)

This is the p-value for Medium in the standard ANCOVA above (p=0.024 < 0.05).
Answer: Yes, you can say with 5% risk that A and B have different actions on algae growth. Substance A leads to higher average circumference after controlling for days (fair comparison, like your guide's section 3).
If you want to visualize: Graph → Scatterplot with fit lines (group by Medium) to see parallel lines with different intercepts.

For Part b): Do A and B Significantly Influence Growth Compared to Natural Slope of 0.84?

Since slopes don't differ (from Step 1), A and B have the same growth rate (slope = 1.523 from Step 2). But the question asks about A and B separately vs. natural.
Run separate regressions (like your guide's regression link, section 4): Stat → Regression → Fit Regression Model.
Subset for A: Response = Circumference, Continuous = Days (filter rows where Medium = A).
Slope = 1.700, SE = 0.410, p (vs. 0) = 0.025.
Test vs. 0.84: t = (1.700 - 0.84) / 0.410 = 2.10, df=3, p ≈ 0.127 (>0.05). Not significant.

Subset for B: Same steps (filter Medium = B).
Slope = 1.345, SE = 0.206, p (vs. 0) = 0.007.
Test vs. 0.84: t = (1.345 - 0.84) / 0.206 = 2.45, df=3, p ≈ 0.092 (>0.05). Not significant.


Answer: No, neither A nor B significantly influences the growth rate compared to the natural slope of 0.84 (both p > 0.05 at 5% risk). The slopes are higher but not statistically different from natural. (If your exam allows marginal significance, note B is close at p=0.092, but strictly no at 5%.)
Tip: To get p for t=2.10 or 2.45 (df=3), use Calc → Probability Distributions → t in Minitab, or a t-table.

For Part c): Estimated Average Circumference for A After 4 Days, with 95% Confidence Interval

Use the regression for A (from part b).
After fitting, go to Stat → Regression → Predict.
Enter Days = 4.
Select "Confidence limits" for the mean (not prediction interval—question asks for average/mean circumference).

Output:
Estimated value: 15.98.
95% Confidence Interval: 12.07 to 19.89.

Answer: The estimated average circumference for medium A after 4 days is 15.98. The 95% confidence interval is [12.07, 19.89]. (This is the "fairness correction" from your guide—adjusted via the regression line.)
