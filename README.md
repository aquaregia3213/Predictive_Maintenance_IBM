# PS39 — Predictive Maintenance of Industrial Machinery

> **AICTE IBM SkillsBuild Summer Internship Program (SIP) 2026**  
> Organised by **Edunet Foundation** in collaboration with **IBM**

---

## Project Overview

Industrial machines such as lathes, CNC mills, and pumps are prone to unexpected failures that cause significant production loss and high repair costs. This project builds a **multi-class classification model** using **IBM watsonx.ai AutoAI** to predict the type of machine failure before it occurs — enabling proactive maintenance and reducing downtime.

---

## Problem Statement

**PS No. 39 — Predictive Maintenance of Industrial Machinery**

Given real-time sensor data from industrial machines, predict the type of failure from the following classes:

| Failure Type | Key Trigger |
|---|---|
| ✅ No Failure | All sensors within normal range |
| ⚡ Power Failure | Extremely high RPM + very low torque |
| 🔧 Tool Wear Failure | Tool wear exceeds 200 minutes |
| 💥 Overstrain Failure | Very low RPM + high torque + high tool wear |
| 🌡️ Heat Dissipation Failure | Air temp above 300K + high torque |

---

## Dataset

- **Source:** Kaggle — [Machine Predictive Maintenance Classification](https://www.kaggle.com/datasets/shivamb/machine-predictive-maintenance-classification)
- **File:** `predictive_maintenance.csv`
- **Rows:** ~10,000
- **Columns:** 10 (UDI, Product ID, Type, Air temp, Process temp, RPM, Torque, Tool wear, Target, Failure Type)
- **Target column:** `Failure Type` (multi-class)

### Features Used

| Feature | Type | Description |
|---|---|---|
| Type | String | Machine quality — L / M / H |
| Air temperature [K] | Decimal | Ambient air temperature |
| Process temperature [K] | Decimal | Operating temperature |
| Rotational speed [rpm] | Integer | Spindle speed |
| Torque [Nm] | Decimal | Applied torque |
| Tool wear [min] | Integer | Cumulative tool wear time |

---

## Solution Approach

Built using **IBM watsonx.ai Studio — AutoAI** (no-code automated ML pipeline):

1. Dataset uploaded to IBM watsonx.ai Studio project
2. AutoAI experiment configured with `Failure Type` as prediction column
3. AutoAI automatically ran preprocessing, feature engineering, and algorithm selection
4. **9 pipelines** generated and evaluated
5. Best model selected — **Pipeline 5** (Batched Tree Ensemble Classifier)
6. Model deployed as **Online deployment** on IBM watsonx.ai
7. Predictions tested for all 5 failure types

---

## Results

| Metric | Value |
|---|---|
| **Algorithm** | Batched Tree Ensemble Classifier (Snap Random Forest) |
| **Accuracy** | **99.5%** (Cross Validation Score) |
| **Enhancements** | HPO-1, Feature Engineering (FE), HPO-2, BATCH (INCR) |
| **Pipelines Generated** | 9 |
| **Build Time (Best Pipeline)** | 55 seconds |
| **Deployment Type** | Online (Real-time inference) |

---

## Technology Stack

| Component | Tool |
|---|---|
| Cloud Platform | IBM Cloud Lite |
| ML Studio | IBM watsonx.ai Studio |
| ML Service | IBM WatsonMachineLearning (watsonx.ai Runtime) |
| AutoML | AutoAI |
| Dataset | Kaggle (CSV) |
| Deployment | IBM watsonx.ai Online Deployment |

---

## Repository Structure

```
PS39_Predictive_Maintenance/
│
├── predictive_maintenance.csv       # Original Kaggle dataset
├── Problem_Statement_PS39.pdf       # Problem statement document
├── PS39_Predictive_Maintenance.pptx # Project submission PPT (17 slides)
├── AutoAI_Notebook.ipynb            # AutoAI notebook from IBM watsonx.ai
└── README.md                        # This file
```

---

## How to Reproduce

### Step 1 — Set Up IBM Cloud
1. Create a free IBM Cloud Lite account at [cloud.ibm.com](https://cloud.ibm.com)
2. Create a **watsonx.ai Studio** instance
3. Create a **WatsonMachineLearning** service instance (Lite plan)

### Step 2 — Create Project
1. Go to IBM Cloud Pak for Data → Projects → New Project
2. Name: `Predictive_Maintenance`
3. Associate the WatsonMachineLearning service

### Step 3 — Run AutoAI Experiment
1. Click **"Build machine learning models automatically"**
2. Upload `predictive_maintenance.csv`
3. Set prediction column → `Failure Type`
4. Prediction type → Multiclass Classification (auto-detected)
5. Optimized metric → Accuracy
6. Click **"Run Experiment"**

### Step 4 — Deploy Best Model
1. Select **Pipeline 5** (Rank 1, Accuracy 99.5%)
2. Click **"Save as"** → **"Model"**
3. Promote to deployment space
4. Create **Online** deployment
5. Test in the **Test** tab with sample data

### Step 5 — Test Prediction
Use the following sample inputs to verify all failure types:

```
No Failure     → Type=M, Air=298.3, Process=308.8, RPM=1520, Torque=43.5, Wear=12
Power Failure  → Type=L, Air=298.9, Process=309.1, RPM=2861, Torque=4.6,  Wear=143
Tool Wear      → Type=L, Air=298.8, Process=308.9, RPM=1455, Torque=41.3, Wear=208
Overstrain     → Type=L, Air=298.4, Process=308.2, RPM=1282, Torque=60.7, Wear=216
Heat Dissip.   → Type=M, Air=300.8, Process=309.4, RPM=1342, Torque=62.4, Wear=113
```

---

## Internship Details

| Field | Details |
|---|---|
| **Program** | AICTE IBM SkillsBuild Summer Internship Program 2026 |
| **Duration** | June 12– July 10, 2026 |
| **Student** | Atharva Jadhav |
| **Institution** | MIT Academy of Engineering (MIT AOE), Pune |
| **Branch** | B.Tech Computer Science |
| **Problem Statement** | PS 39 — Predictive Maintenance of Industrial Machinery |

---

## Acknowledgements

- **IBM** for providing watsonx.ai platform and IBM Cloud Lite access
- **Edunet Foundation** for organizing the AICTE SIP program
- **Kaggle / Shivam Bansal** for the predictive maintenance dataset
- **AICTE** for facilitating the internship program

---

*Built with IBM watsonx.ai AutoAI — No-code automated machine learning*
