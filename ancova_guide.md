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
