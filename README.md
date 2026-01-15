# **Customer Churn Prediction & Retention Strategy Report**

## **Client Background**
Elist Electronics, established in 20 21 , is a global e-commerce company that sells popular consumer products worldwide via its website and mobile app.
The company has significant amounts of data on its customers data that has been previously underutilized. This project thoroughly analyzes and synthesizes this data in order to uncover critical insights that will improve Elist's retention.

## **Executive Summary**
Based on the analysis of 5,630 customer records using a Random Forest Model (97.8% Accuracy), we identified that churn is primarily driven by experience failures rather than price sensitivity. Our strategy must shift from broad demographic targeting to precision behavioral intervention.

**1. Service Failure is the #1 Churn Driver**
Insight: "Service Recovery" is more critical than product quality. Data confirms a "toxic combination": users with a complaint history and low satisfaction scores (<3) exhibit a churn probability approaching 100%.
Implication: Historical spending does not buy forgiveness. A single unresolved complaint wipes out years of loyalty.

**2. The "Month-1" Golden Window**
Insight: Retention is an "Onboarding Challenge." The highest churn risk occurs within Tenure < 1 month. Once users survive this period, retention rates stabilize significantly.
Implication: Marketing resources should be front-loaded to the first 30 days to ensure activation, rather than spread evenly across the lifecycle.

**3. Logistics Friction Erodes Frequency**
Insight: Physical distance (WarehouseToHome) acts as a hidden tax on loyalty. Longer delivery times directly suppress purchase Frequency, causing users in remote areas to drift away.
Implication: Since we cannot change physical distance, we must compensate with "psychological speed" (e.g. priority shipping perks for high-value remote users).

**4. Demographics are Obsolete**
Insight: Traditional segmentation based on Gender or City Tier is statistically irrelevant (Feature Importance < 0.03).
Implication: Stop budget allocation based on "Who they are." Start allocating based on "What they do" (Behavioral Triggers).

**5. Strategic Pivot: The ROI Filter**
Strategy: By overlaying RFM Value with Predicted Churn Risk, we identified a specific segment of "High Value - High Risk" customers (The "Red Giants").
Action: Immediate manual intervention is required for this group to save revenue, while "Low Value - High Risk" users should be strategically abandoned to optimize marketing ROI.

## Dataset Structure & ERD
The database structure as seen below consists of two tables: customer, behaviour info, with a total row count of 5,630 records.
<img width="468" height="341" alt="image" src="https://github.com/user-attachments/assets/b79408ec-ecab-48be-9858-c0d188f0873e" />

## **Insights Deep-Dive**

### **Key Drivers Analysis**
To drive the North Star Metric—Customer Lifetime Value (CLV)— Random Forest classification model is used to analyze the behaviors of 5,630 customers. The following insights bridge our data findings directly to strategic conclusions.

**1. The "Golden Window" for Retention is Month 1**
There is a strong negative correlation between Tenure and churn risk. Specifically, the data highlights that users with a tenure of less than 1 month have the highest churn rate(50.6%), which drops precipitously after this initial period. This data confirms that retention is fundamentally an "Onboarding" challenge. That means the
company is losing the majority of customers before they generate enough value to cover their Customer Acquisition Cost (CAC), indicating that resources should be front-loaded to the first 30 days of the user journey.

<img width="313" height="153" alt="image" src="https://github.com/user-attachments/assets/450b50b8-c5bd-4d0e-a775-735eae63fab9" />

**2. Logistics Friction Erodes Purchase Frequency**
The Warehouse_To_Home metric consistently ranks as a high-impact feature in the model. The data distribution reveals a clear trend where churn rates rise monotonically as the distance from the warehouse increases. This trend demonstrates that longer delivery times (proxied by distance) are creating "logistics friction". This friction directly degrades customer satisfaction and suppresses the "Frequency" multiplier in our CLV model, particularly for users in remote areas.
<img width="226" height="145" alt="image" src="https://github.com/user-attachments/assets/7c109646-e1d0-4924-b90e-7b29a1201787" /> <img width="215" height="148" alt="image" src="https://github.com/user-attachments/assets/ce97518a-32f4-4e9c-89dd-e0b447d01c7a" />


**3. Demographics are Irrelevant for Strategy**
Feature Importance scores for Gender, CityTier, and MaritalStatus are statistically negligible (all scores < 0.03), with no significant difference in churn rates observed across these groups. This lack of predictive power indicates that traditional segmentation based on demographics is obsolete for this user base. Consequently, marketing strategies must shift entirely from "Identity-based targeting" to "Behavior-based targeting" (e.g.usage drops, complaints).

**4. Model Selection & Performance**
After comparing Logistic Regression, SVM, and Decision Trees, Random Forest has been selected as the production model because the accuracy of random forest is 97.8%, and ROC-AUC is 98.6% – Exceptional ability to distinguish between "Churn" and "Retain" users.

The high precision data confirms that the model is robust enough to automate high-stakes retention incentives. The high-value coupons can be confidently issued to predicted churners with minimal risk of "False Positives" (wasting budget on users who would have stayed anyway).  
<img width="343" height="84" alt="image" src="https://github.com/user-attachments/assets/8a9943d5-a5bd-4cdc-921e-96c8103ecbaf" />


**5. User Segmentation (RFM Model)**
In order to prioritize the company’s resources, customer has been segmented into 4 segmentations: The Red Giants, The Drifting Bubbles, The Red Sand, The Green Seedlings according to rfm model.

**Visual Pattern I: "The Red Giants" (Critical Alert)**
- **Visual Location**
Top-Left (Low Recency, High Frequency), large Bubbles (High Monetary), Deep Red Color.
- **Insight:**
    o The Anomaly: These are your best customers. They bought recently and buy often, yet the model predicts they are about to leave.
    o Root Cause: This almost always indicates a recent "Service Failure." They likely placed a large order but experienced a critical failure (e.g., lost package, rude support, damaged goods).
    o Risk: Their churn is not just financial; it's reputational. High-value users often have high social influence.
- **Recommendation: "Operation Code Red"**
    o Strategy: Manual, High-Touch Intervention.
    o Action: Do not send automated emails. Export this list immediately to your VIP Customer Service Team.
    o Tactic: Offer "No-questions-asked" compensation (Refunds, High-value Gifts).

**Visual Pattern II: "The Drifting Bubbles" (Fading Habits)**
- **Visual Location:**
Middle -> Right (Recency is increasing), medium-sized bubbles transitioning from Green to Yellow to Red.
- **Insight:**
o The Process: Churn is a journey, not an event. These users are "drifting." They went from buying weekly to monthly, and now haven't visited in 60 days.
o Psychology: Their habit loop is breaking. They are forgetting the platform or testing a competitor.
- **Recommendation: "Habit Reactivation"**
    o Strategy: Periodic Wake-up Calls.
    o Action: Implement automated triggers based on specific Recency thresholds.
    o Tactics:
       § At 30 Days: "Price Drop Alert" on items in their cart (Re-engagement).
       § At 60 Days: "We Miss You" Coupon (Aggressive Win-back).
    o Goal: Push the bubble back to the Left (Decrease Recency).

**Visual Pattern III: "The Red Sand" (The ROI Trap)**
- **Visual Location:**
Bottom-Right (High Recency, Low Frequency).Tiny Bubbles, Deep Red.
- **Insight:**
    o Dead Inventory: These users haven't visited in a long time, rarely bought when they did, and spent very little.
    o The Trap: In many companies, 50% of the marketing budget is wasted chasing these users because they are numerous.
    o Reality: The cost of an SMS or coupon often exceeds their potential future profit.
- **Recommendation: "Strategic Abandonment"**
    o Strategy: Stop the Bleeding.
    o Action: Remove them from all Paid Media audiences (Facebook/Google Ads exclusion lists).
    o Tactic: Use only zero-cost channels (App Push, Email) or let them churn naturally to clean up your database.

**Visual Pattern IV: "The Green Seedlings" (Untapped Potential)**
- **Visual Location:**
Bottom-Left (Low Recency, Low Frequency).Small Bubbles, Bright Green.
- **Insight:**
    o New/Casual Users: They just arrived or buy occasionally. They are happy (Low Risk), but they haven't formed a strong habit yet.
    o Opportunity: They are safe for now, but if ignored, they will drift right (become inactive).
- **Recommendation: "Nurture & Gamification"**
    o Strategy: Cross-Sell & Frequency Building.
o Action: Don't just give discounts; give them a "Reason to Return."
o Tactics:
§ Gamification: "Complete 2 more orders this month to unlock VIP Status" (Push bubble Up).
§ Cross-Sell: "You bought a Coffee Maker; here are our top-rated beans" (Make bubble Bigger).  
<img width="307" height="205" alt="image" src="https://github.com/user-attachments/assets/e8e76520-d71e-4e0f-a06d-0a29c0561986" />


# **Recommendations**

Based on the data insights above, the following recommendations have been provided:

### **Short-Term: Operation Quick-Win**

1. "Complaint-Alert" Circuit Breaker
    o _Current State:_ Complaints are merely recorded.
    o Action: When the system detects a "Low Satisfaction Score" accompanied by a "Complaint Record," trigger an immediate VIP Human Follow-up. Do not use chatbots. Service recovery must be personal for these high-risk users.
2. "Relocation Retention" Campaign
    o _Insight:_ Data shows that adding more than 2 addresses in a month is often a precursor to churn (or a life event like moving).
    o Action: Trigger a "New Home Welcome Coupon" or home-goods recommendation when address changes are detected. Lock in their spending habits at their new location immediately.

### **Mid-to-Long Term: Structural Optimization**

3. Logistics Experience Compensation
  o Insight: High WarehouseToHome scores lead to churn.
  o Action: Since physical distance cannot be changed, reduce the "psychological distance." Offer "Priority Shipping" or "Shipping Fee Waivers" to high-value users located far from warehouses to offset the negative delivery experience.

### **Resource Reallocation: From "Identity" to "Behavior"**

- Insight: Gender and CityTier have negligible impact on churn (Feature Importance < 0.03).
- Action: Stop broad marketing campaigns based on gender or city tier. Reallocate budget to behavioral triggers (e.g., detecting when a user's App session time drops or click through rate declines), as these yield a significantly higher ROI.
