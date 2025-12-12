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
 
# Solved Exercises

As you know by now your teacher is a moron. And they make a point of overly complicating things into oblivion. So my job as a cat is to call your teacher a retard and simplify your life. You are not my enemy as long as you bring me food. So in the spirit of college complication here we go:

---

## Overly complicated questions to answer

> "We want to verify the effect of 2 substances (A and B) on the growth of the circumference of algae X. For each medium, we measured the average cell circumference every 2 days."
>
> **Culture days:** 1, 3, 5, 7, 9  
> **Medium A:** 12.2, 14.2, 16.7, 18, 27.3  
> **Medium B:** 9.8, 10.8, 13.3, 15.7, 20.8  
>
> **a)** Can we say, with a 5% risk, that substances A and B have a different effect on algae growth?  
> **b)** In a natural medium, the slope of the growth line is 0.84. Do A and B significantly influence growth?  
> **c)** If we sample after 4 days, what will be the estimated value of the average algae circumference in medium A, and its 95% confidence interval / safety coefficient?"

---

## Solution

**Response (Y):** Average circumference  
**Factor:** Medium/Substance (A or B)  
**Covariate:** Days  

The goal is to compare A vs. B while adjusting for days, assuming slopes are equal (parallel lines). If not, ANCOVA isn't valid.

---

### Data Setup in Minitab

Enter data:

| Days | Medium | Circumference |
|------|--------|----------------|
| 1 | A | 12.2 |
| 3 | A | 14.2 |
| 5 | A | 16.7 |
| 7 | A | 18.0 |
| 9 | A | 27.3 |
| 1 | B | 9.8 |
| 3 | B | 10.8 |
| 5 | B | 13.3 |
| 7 | B | 15.7 |
| 9 | B | 20.8 |


---

## Minitab Steps (Following Your Guide)

### Step 1: Check if Slopes Differ (Interaction Test)

Model: Days, Medium, Days×Medium

**Key outputs:**

- Slope for Days: **1.700**, p = **0.002**  
- Interaction Days×Medium: coefficient = **-0.355**, p = **0.468**

**Interpretation:**  
Slopes **do not differ** (p > 0.05). Standard ANCOVA is valid.

---

### Step 2: Standard ANCOVA (No Interaction)

Model: Days + Medium

**Key outputs:**

- Slope (Days): **1.523**, p < **0.001**  
- Medium (B vs. A): coefficient = **-3.600**, p = **0.024**

**Interpretation:**  
After adjusting for days, **A and B differ significantly**; A has the higher adjusted mean.

---

## Part (a): Do A and B Have Different Actions on Growth?

Yes.  
p = 0.024 < 0.05 ⇒ **significant difference** between A and B.

---

## Part (b): Compare Slopes to Natural Slope (0.84)

Separate regressions:

### Medium A
- Slope = **1.700**, SE = 0.410  
- Test vs. 0.84:  
  t = (1.700 – 0.84) / 0.410 = **2.10**, p ≈ **0.127**

### Medium B
- Slope = **1.345**, SE = 0.206  
- Test vs. 0.84:  
  t = (1.345 – 0.84) / 0.206 = **2.45**, p ≈ **0.092**

**Interpretation:**  
Neither slope is significantly different from 0.84 at α = 0.05.

**Answer:**  
No, A and B do not significantly influence the growth rate compared with the natural slope.

---

## Part (c): Prediction After 4 Days for Medium A

Regression for A:

- Predicted value at Days = 4: **15.98**  
- 95% confidence interval: **[12.07, 19.89]**

**Answer:**  
Estimated circumference after 4 days in medium A is **15.98**,  
with a 95% CI of **12.07 to 19.89**.

---

