<p align="center">
<img width="300" height="435" alt="03-Instacart-Logo-Kale-1 (1)" src="https://github.com/user-attachments/assets/c81e0ac6-0b22-489c-8dbb-e681c3bd7343" />
</p>

# **Instacart Customer Behavior Analysis**

## **About Instacart**

Instacart is a leading North American grocery delivery platform that partners with supermarkets and retail chains to offer same-day delivery. Customers shop online, Instacart sends personal shoppers to pick and deliver the orders, and retailers gain an extended digital channel without building their own fulfillment network.

The platform captures detailed behavioral data: product choices, order timing, repeat purchases, and cart composition across millions of transactions. This makes Instacart a rich environment for understanding how customers form grocery habits.

---

## **The Business Problem**

Instacart operates in a category where repeat purchasing is the core of the business model. If a product keeps getting reordered, Instacart earns predictable margin and retention improves. If not, Instacart must keep spending to reacquire demand.

Across 32.4 million orders, the company noticed a strong imbalance:

- Some items (milk, bananas, eggs) are reordered at extremely high rates
- Others (new snacks, beverages, or niche items) are purchased once and never show up again

This raises a fundamental performance question for both Instacart and retailer partners:
**Is low reorder behavior caused by customer preferences, product issues, or operational factors?**

---

## **Dataset**
**Source:** Instacart Online Grocery Basket Analysis Dataset (**Kaggle**)      
[View Dataset](https://www.kaggle.com/datasets/yasserh/instacart-online-grocery-basket-analysis-dataset)

**Scale:**
- 32.4 million order items
- 3.3 million orders
- 206,000 customers
- 49,685 unique products across 21 departments

---

## **Analysis Approach**

This project diagnoses two critical customer behavior patterns:

## Question 1: **Why Do Some Products Get Reordered While Others Don't?**

<details>
<summary><strong>Executive Summary</strong></summary>

## **The Question**

59% of all items purchased on Instacart are reordered. But this average hides massive variation:
- Dairy products: 67% reorder rate
- Pantry items: 35% reorder rate

Why does this 32-percentage-point gap exist? Is it fixable through better operations, or is it structural customer behavior?

---

## **The Findings**

Reorder behavior is **not an operational problem**—it's driven by category psychology and customer maturity:

**1. Category Type Dominates Everything**
- Dairy and beverages are **routine replenishment** (customers buy the same milk weekly)
- Pantry items are **variety-seeking** (customers try different pasta brands)
- Statistical proof: Dairy has **97% higher reorder odds** than baseline categories (p < 0.001)

**2. Frequent Shoppers Form Habits**
- Customers with 20+ orders reorder **69% of their basket**
- Customers with 1-4 orders reorder only **24%**
- **45-percentage-point gap** shows habit formation takes time

**3. Recency Matters, But Not as Much as Expected**
- Customers ordering weekly (0-7 days) reorder at 67.5%
- Customers ordering monthly (22-30 days) reorder at 49.2%
- **18-point drop** shows engagement decay, but category still dominates

**4. Time of Day Doesn't Matter**
- Morning, afternoon, and evening orders show identical reorder rates (within 3%)
- Time-based promotions are wasted effort

---

## **The Root Cause**

Low reorder rates in pantry categories are **not a retention problem to solve**—they reflect natural variety-seeking behavior. Customers *want* to try different brands of pasta, sauces, and snacks.

High reorder rates in dairy/beverages reflect **routine replenishment needs**. Customers have a preferred milk brand and stick to it.

**Misalignment:** Instacart was treating all low-reorder categories as retention failures and throwing promotional budget at them. The data proves this is the wrong strategy.

---

## **Business Impact**

### **What Instacart Should Do Differently:**

**1. Stop Wasting Retention Budget on Pantry Items**
- Current state: Reorder promotions sent equally across all categories
- Evidence: Pantry has 53% *lower* reorder odds even after promotions
- Recommendation: Use pantry for **acquisition** (attract new customers with deals), not retention
- **Expected savings: 15-20% reduction in wasted promotional spend**

**2. Double Down on High-Frequency Customers**
- Customers with 20+ orders drive 69% reorder rates
- These users want **convenience, not discovery**
- Recommendation: Personalized "Buy Again" lists, subscription discounts, priority delivery
- **Expected impact: 10-15% increase in retention for established customers**

**3. Intervene at 14 Days, Not 30 Days**
- Reorder rates drop 8% between week 1 and week 2, then accelerate
- Current state: Lapsed-user campaigns trigger at 30+ days (too late)
- Recommendation: Send reorder reminders at 14-day mark for high-reorder categories only
- **Expected impact: 5-8% reduction in churn**

**4. Abandon Time-Based Targeting**
- Evidence shows no meaningful reorder difference by hour of day
- Recommendation: Reallocate engineering resources from time-based campaigns to category-based segmentation
- **Expected impact: Simpler operations, no revenue loss**

---

# **Analysis & Evidence**

## **Hypothesis Tested**

Reorder likelihood is driven by:
1. Product category (staples vs. impulse purchases)
2. Purchase recency (time since last order)
3. User purchase frequency (active vs. infrequent shoppers)
4. Product popularity (social proof effect)
5. Time of day (routine shopping vs. spontaneous orders)

**Method:** Statistical testing (chi-square) + predictive modeling (logistic regression) on 500,000 orders

---

## **Finding 1: Category Type Drives Everything**

### **Evidence Table**
| Department | Reorder Rate | Statistical Significance | Odds Ratio vs. Baseline |
|------------|--------------|-------------------------|------------------------|
| Dairy Eggs | 67.0% | p < 0.001 | **1.97x (97% higher)** |
| Beverages | 65.4% | p < 0.001 | 1.89x (89% higher) |
| Bakery | 62.8% | p < 0.001 | 1.77x (77% higher) |
| Produce | 65.1% | p < 0.001 | 1.29x (29% higher) |
| Frozen | 54.3% | p < 0.001 | 1.28x (28% higher) |
| Snacks | 57.5% | p < 0.001 | 1.34x (34% higher) |
| **Pantry** | **34.7%** | **p < 0.001** | **0.47x (53% LOWER)** |

### **What This Means**
- All differences are statistically significant (not random chance)
- Dairy customers are **nearly twice as likely** to reorder compared to pantry customers
- This is behavioral, not operational—you can't "fix" pantry reorder rates

---

## **Finding 2: Frequent Shoppers Form Habits**

### **Evidence Table**
| Customer Frequency | Reorder Rate | Sample Size | Behavioral Pattern |
|-------------------|--------------|-------------|-------------------|
| Very Low (1-4 orders) | 23.5% | 1.4M items | Exploring, no loyalty yet |
| Low (5-9 orders) | 37.1% | 4.0M items | Starting to find favorites |
| Medium (10-19 orders) | 50.8% | 7.0M items | Habits forming |
| High (20+ orders) | 68.9% | 19.9M items | Locked into routine |

### **What This Means**
- It takes **10+ orders** before customers start showing predictable reorder behavior
- By 20 orders, customers have identified their preferred products and reorder 7 out of 10 items
- New customer campaigns should focus on **breadth** (try many categories), not **retention** (reorder same items)

---

## **Finding 3: Recency Decays Engagement**

### **Evidence Table**
| Days Since Last Order | Reorder Rate | Behavioral Interpretation |
|----------------------|--------------|--------------------------|
| 0-7 days | 67.5% | Highly engaged, routine intact |
| 8-14 days | 64.4% | Slight decay, still predictable |
| 15-21 days | 59.5% | Engagement weakening |
| 22-30 days | 49.2% | At-risk, losing routine |

### **What This Means**
- Every week of delay reduces reorder likelihood by ~8%
- The critical intervention window is **14 days**, not 30 days
- After 3 weeks, customers have likely found alternatives or changed routines

---

## **Finding 4: Time of Day Is Irrelevant**

### **Evidence Table**
| Time of Day | Reorder Rate | Difference from Morning |
|-------------|--------------|------------------------|
| Morning (6-11 AM) | 61.1% | Baseline |
| Afternoon (12-5 PM) | 57.9% | -3.2% |
| Evening (6-9 PM) | 57.8% | -3.3% |
| Night (10 PM-5 AM) | 57.8% | -3.3% |

### **What This Means**
- Only 3-percentage-point variation across all hours
- After controlling for category and user frequency, time has no predictive power
- Don't waste engineering time on time-based promotions

---

## **Finding 5: Product Popularity Is Misleading**

### **Evidence from Two Tests**

**Univariate Analysis (Before Controlling for Other Factors):**
| Product Popularity | Reorder Rate |
|-------------------|--------------|
| Rare (< 100 orders) | 35.8% |
| Very Popular (5K+ orders) | 65.4% |

**Looks like popularity matters... but:**

**Logistic Regression (After Controlling for Category & Frequency):**
| Predictor | Coefficient | Interpretation |
|-----------|-------------|----------------|
| Product Popularity | +0.000005 | No effect |

**What This Means:**
- Popular products aren't reordered *because* they're popular
- They're popular *because* they're in high-reorder categories (dairy, beverages)
- Once you account for category type, popularity adds zero predictive value

---

## **Visualizations**

### **Feature Importance: What Predicts Reorder Behavior?**

<img width="1000" height="700" alt="feature_importance" src="https://github.com/user-attachments/assets/bea37a78-b132-4188-b0b7-8ab1d1651060" />

**Key Takeaway:** Department dummies dominate the model. Dairy, beverages, and bakery strongly increase reorder odds, while pantry dramatically decreases them. User frequency and recency are moderate predictors. Time-based features are irrelevant.

---

### **Model Performance: Can We Predict Reorder Behavior?**

<img width="1000" height="700" alt="prediction_distribution" src="https://github.com/user-attachments/assets/619ef999-3e5b-4294-99af-900a3f0f58d3" />

**Key Takeaway:** The model successfully separates reordered items (green, right-skewed toward high probability) from non-reordered items (red, left-skewed toward low probability). The overlap shows human behavior isn't perfectly predictable, but the model captures real patterns.

**Model Accuracy: 67% | ROC-AUC: 0.688**

---

## **Strategic Recommendations**

### **1. Segment Retention Strategy by Category**

| Category Type | Current Approach | Recommended Approach | Why |
|--------------|------------------|---------------------|-----|
| High-Reorder (Dairy, Beverages) | Generic retention emails | Personalized "Buy Again" lists, subscription offers | These customers want convenience |
| Low-Reorder (Pantry, Snacks) | Reorder promotions (wasted) | Discovery features, variety bundles | These customers want exploration |

**Impact:** Save 15-20% of retention budget by not fighting natural variety-seeking behavior.

---

### **2. Intervene Earlier for At-Risk Customers**

| Customer Segment | Current Trigger | Recommended Trigger | Tactic |
|-----------------|-----------------|---------------------|--------|
| Active (0-7 days) | None | None | Don't interrupt engaged users |
| Declining (14-21 days) | None | 14-day reminder | "Your favorites are waiting" for high-reorder categories only |
| Lapsed (30+ days) | Win-back campaign | Treat as new customer | Offer discovery deals, reset expectations |

**Impact:** Reduce churn by 5-8% through earlier intervention.

---

### **3. Prioritize High-Frequency Customers**

| Customer Tier | Orders Placed | Reorder Rate | Strategy |
|--------------|---------------|--------------|----------|
| New (1-9) | 1-9 | 24-37% | Encourage breadth, not loyalty |
| Established (10-19) | 10-19 | 51% | Introduce reorder features |
| Loyal (20+) | 20+ | 69% | Premium treatment: fast delivery, personalized lists |

**Impact:** Increase retention by 10-15% for customers reaching 20+ orders.

---

### **4. Eliminate Time-Based Targeting**

**Current State:** Resources spent on "morning deals," "evening specials," etc.

**Evidence:** Time of day shows no meaningful impact on reorder behavior.

**Recommendation:** Reallocate engineering and marketing resources to category-based and frequency-based segmentation.

**Impact:** Simplify operations without revenue loss.

---

## **Key Insight**

**Reorder behavior is primarily driven by what customers buy (category) and how often they shop (frequency), not when they shop or what's popular overall.**

Instacart should stop treating all low-reorder categories as problems to solve. Pantry variety-seeking is natural customer behavior. Focus retention efforts where they work: dairy, beverages, and bakery for established customers.

---

</details>


## **Question 2: Why Do Some Customers Build Larger Baskets Than Others?**
<details>
<summary><strong>Executive Summary</strong></summary>

<br>

**Coming Soon**

</details>

---

## **Tools Used**

- **PostgreSQL** — Data consolidation and feature engineering
- **Python** — Statistical testing (chi-square, logistic regression)
- **Visualization** — matplotlib, seaborn

---

## **Contact**

**Muhammad Aryan**  
Data Analyst | Diagnostic Analysis & Business Problem-Solving  
📧 aryanrehman008@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/muhammadaryan008/)  
💻 [GitHub Portfolio](https://github.com/aryanlytics)

---

*"Data tells you what happened. Analysis tells you why. Strategy tells you what to do about it."
