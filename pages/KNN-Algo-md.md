# K-Nearest Neighbors (KNN) Algorithm Guide

## Introduction

### What is K-Nearest Neighbors (KNN)?

- A simple, powerful machine learning algorithm
- Used to predict outcomes based on similar examples
- Like asking "What happened to students similar to me?"

> **Key Idea:** Similar inputs tend to have similar outputs!

---

## Real-World Scenario

### The Professor's Dilemma 🎓

*Professor Smith wants to help students predict their exam results before the actual exam.*

#### Available Data:
Past student records
- Hours they studied
- Hours they slept
- Their final result (Pass/Fail)

> **Question:** Can we predict a new student's result?

---

## Our Dataset

### 12 Past Students' Data

| Student | Hours Studied | Hours Slept | Result |
|---------|---------------|-------------|--------|
| 1       | 8             | 7           | Pass   |
| 2       | 2             | 6           | Fail   |
| 3       | 9             | 8           | Pass   |
| 4       | 1             | 5           | Fail   |
| 5       | 7             | 7           | Pass   |
| 6       | 3             | 4           | Fail   |
| 7       | 6             | 8           | Pass   |
| 8       | 2             | 3           | Fail   |
| 9       | 8             | 6           | Pass   |
| 10      | 4             | 9           | Fail   |
| 11      | 9             | 7           | Pass   |
| 12      | 1             | 8           | Fail   |

#### Pattern Recognition:
- 📚 More study hours → Usually Pass
- 😴 Good sleep → Better performance
- ⚠️ Very low study hours → Usually Fail

---

## New Student Arrives

### Meet Alex 👨‍🎓

Alex comes to Professor Smith and says:

> *"Professor, I studied for **5 hours** and slept **7 hours**. Will I pass?"*

**Professor thinks:** *"Let me find students similar to Alex and see what happened to them!"*

> This is exactly what KNN does! 🎯

---

## KNN Algorithm Steps

### How KNN Works (3 Simple Steps)

#### 1. Calculate Distance 📏
Find how "similar" Alex is to each past student

#### 2. Find K Nearest Neighbors 👥
Pick the K most similar students

#### 3. Vote & Predict 🗳️
See what happened to those similar students
Majority vote wins!

> **Simple but Powerful!** This approach works for many real-world problems.

---

## Distance Calculation

### Step 1 - Distance Calculation
#### How do we measure "similarity"?

**Euclidean Distance Formula:**
```
Distance = √[(x₁-x₂)² + (y₁-y₂)²]
```

#### Example: Alex vs Student 1
- Alex: (5 study, 7 sleep)
- Student 1: (8 study, 7 sleep)
- Distance = √[(5-8)² + (7-7)²] = √[9+0] = √9 = **3.0**

*Let's calculate one more together!* 🤝

---

## Interactive Calculation

### Alex vs Student 2
- Alex: (5 study, 7 sleep)
- Student 2: (2 study, 6 sleep)

**Your turn to calculate:**
Distance = √[(5-2)² + (7-6)²] = √[?+?] = ?

**Answer:** √[9+1] = √10 = **3.16**

*Great! Now let's see all distances...*

---

## All Distances

### Alex's Distance to All Students

| Student | Study | Sleep | Result | Distance      |
|---------|-------|-------|--------|---------------|
| 7       | 6     | 8     | Pass   | **1.41** ⭐   |
| 5       | 7     | 7     | Pass   | **2.0** ⭐    |
| 1       | 8     | 7     | Pass   | **3.0** ⭐    |
| 2       | 2     | 6     | Fail   | 3.16          |
| 9       | 8     | 6     | Pass   | 3.16          |
| 10      | 4     | 9     | Fail   | 2.24          |
| ...     | ...   | ...   | ...    | ...           |

**Closest neighbors marked with ⭐**

---

## K=3 Prediction

### Step 2: Find 3 Nearest Neighbors

#### Top 3 Closest Students to Alex:
1. Student 7: Distance 1.41 → **Pass** ✅
2. Student 5: Distance 2.0 → **Pass** ✅
3. Student 1: Distance 3.0 → **Pass** ✅

#### Step 3: Vote
- Pass: 3 votes
- Fail: 0 votes

> **Prediction: PASS** 🎉
> **Confidence: 100%**

---

## K=1 Analysis

### What if K=1?
#### Using Only 1 Nearest Neighbor

> **Closest Student to Alex:**
> Student 7: Distance 1.41 → **Pass**

**Prediction: PASS** ✅
**Confidence: 100%**

**Question:** Is this reliable? 🤔

*Think about it: What if that one student was an outlier?*

---

## K=5 Analysis

### What if K=5?
#### Using 5 Nearest Neighbors

#### Top 5 Closest Students:
1. Student 7: **Pass** ✅
2. Student 5: **Pass** ✅
3. Student 10: **Fail** ❌
4. Student 1: **Pass** ✅
5. Student 2: **Fail** ❌

**Vote:** Pass=3, Fail=2

> **Prediction: PASS** ✅
> **Confidence: 60%**

---

## K Comparison

### Different K Values for Alex

| K Value | Neighbors Used | Prediction | Confidence |
|---------|----------------|------------|------------|
| K=1     | 1              | Pass       | 100%       |
| K=3     | 3              | Pass       | 100%       |
| K=5     | 5              | Pass       | 60%        |

> **All agree: Alex will PASS!** 🎯

#### Key Observations:
- Same prediction across all K values
- Different confidence levels
- K=3 provides good balance

---

## Edge Case Challenge

### Meet Sam - The Tricky Case 😅

Sam studied **4 hours** and slept **6 hours**.
*Right on the boundary between pass/fail patterns!*

**Quick Question:** What do you think will happen?
- A) Definitely Pass
- B) Definitely Fail
- C) Could go either way

**Answer:** C) Could go either way - This is what makes it an edge case!

---

## Edge Case Results

### Sam's Prediction Results

| K Value | Prediction | Confidence | Why?                 |
|---------|------------|------------|----------------------|
| K=1     | **Fail**   | 100%       | Closest match failed |
| K=3     | **Fail**   | 67%        | Mixed neighborhood   |
| K=5     | **Fail**   | 80%        | More failing neighbors |

> **Key Insight:** Edge cases show algorithm uncertainty! 📊
> Low confidence scores indicate the algorithm is "unsure"

---

## Choosing K

### How to Pick K Value?

#### ✅ Good K Values:
- **Odd numbers** (avoid ties)
- **K=3 to K=7** often work well
- Test different values

#### ❌ Avoid:
- K=1 (too sensitive)
- K=total data (too general)
- Even numbers (can tie)

> **Rule of thumb:** Start with K=3!

---

## Pros and Cons

### KNN Strengths & Weaknesses

#### Strengths ✅
- Simple to understand
- No training needed
- Works with any data type
- Good for small datasets
- Can handle multi-class problems

#### Weaknesses ❌
- Slow with large data
- Sensitive to irrelevant features
- Struggles with imbalanced data
- Needs good distance measure
- Sensitive to outliers

---

## Real-World Applications

### Where is KNN Used?

- 🏥 **Healthcare:** Diagnose diseases based on similar patients
- 🛒 **E-commerce:** "Customers like you also bought..."
- 🎬 **Netflix:** Recommend movies based on similar users
- 🏠 **Real Estate:** Price houses based on similar properties
- 📧 **Email:** Spam detection
- 🎵 **Music:** Song recommendations
- 🔍 **Search:** Find similar documents

> KNN is everywhere! It's one of the most practical algorithms.

---

## Key Takeaways

### Remember These Points:

1. 🎯 **KNN finds similar examples** to make predictions
2. 📏 **Distance measures similarity** (usually Euclidean)
3. 🗳️ **Majority vote** decides the prediction
4. 🔢 **K=3** is often a good starting choice
5. ⚖️ **Edge cases** reveal algorithm uncertainty
6. 🧪 **Always test** different K values

> **Most Important:** KNN assumes that similar things have similar outcomes!

---

## Practice Exercise

### Your Turn! 🎮

#### New Student Data:
- Maya: 7 hours studied, 5 hours slept
- K = 3

**Challenge:**
1. Calculate distances to all students
2. Find 3 nearest neighbors
3. Make prediction
4. Compare with different K values

*Work in pairs - Take your time!*

**Hint:** Maya studies a lot but doesn't sleep much. What do you think will happen?

---

## Summary

### What We Learned Today 📚

- ✅ KNN algorithm concept and steps
- ✅ Distance calculation (Euclidean)
- ✅ Impact of different K values
- ✅ Edge cases and uncertainty
- ✅ Real-world applications
- ✅ When to use KNN

> **Next Steps:** Try implementing KNN in code! 💻
> Practice with different datasets and see how it performs.

#### Questions?
Feel free to ask about any part of the algorithm!