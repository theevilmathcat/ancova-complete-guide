
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

## 8. Covariate Confusion Fix
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
