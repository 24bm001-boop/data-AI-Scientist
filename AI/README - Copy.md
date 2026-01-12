 **NEWS2-Based Early Warning System** – **Logic**

This folder contains the clinical scoring and risk estimation logic used in the Early Warning System (EWS).    
The implementation is strictly grounded in the **Royal College of Physicians NEWS2 standard.**

### **1\. Total Score Calculation**

Each physiological parameter is assigned a NEWS2 score (0–3).

The aggregate score is calculated as:

Score\_total \= S\_HR \+ S\_Temp \+ S\_SpO2 \+ S\_RR \+ S\_Oxygen

Where:  
\- S\_HR \= Heart Rate score  
\- S\_Temp \= Temperature score  
\- S\_SpO2 \= Oxygen Saturation score  
\- S\_RR \= Respiratory Rate score  
\- S\_Oxygen \= \+2 if patient requires supplemental oxygen

### **2\. Clinical Weights (Supplemental Oxygen)**

According to NEWS2 guidelines, patients receiving supplemental oxygen are at higher risk of deterioration.

Therefore:  
\- \+2 points are added to the total score if oxygen therapy is required.

This aligns with 2026 clinical escalation standards and hospital practice.

###  **3\. Risk Percentage Calculation**

To convert NEWS2 scores into an interpretable "Risk %", a sigmoid function is used:

Risk (%) \= 1 / (1 \+ e^(-k × (Score − Threshold)))

Where:  
\- Threshold \= 5 (Urgent Response Threshold)  
\- k \= 0.8 (controls steepness)

### 

### **Interpretation:**

\- Scores \< 5 → Low risk, gradual increase  
\- Scores 5–6 → Sharp risk escalation  
\- Scores ≥ 16 → Risk approaches 100%

This reflects real-world clinical deterioration patterns rather than linear scaling.

###  **4\. Risk Tiers Used in Software**

| NEWS2 Score | Risk Level | Clinical Action |
| :---: | :---: | :---: |
|  0–4  | Low risk |  Ward-based care, routine monitoring |
| 5-6 | Medium risk | Urgent clinical review |
| 7 | High risk | Emergency response / ICU transfer |

###  **5\. Key Point**

This system does NOT replace clinicians.    
It provides **early, interpretable, and standards-based risk alerts** suitable for hospital and remote patient monitoring.

