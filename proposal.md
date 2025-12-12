# CSC172 Association Rule Mining Project Proposal
**Student:** Chris Adrian D. Gumisad, 2020-3275  
**Date:** December 12, 2025

## 1. Project Title 
PC Hardware Compatibility Pattern Mining (Apriori Algorithm)


## 2. Problem Statement
PC builders, hardware retailers, and system integrators rely on understanding compatibility relationships between computer components (CPU, motherboard, RAM, GPU, PSU, etc.). Incorrect component pairing leads to system instability, poor performance, or failed PC builds.

This project applies association rule mining to a PC hardware specifications dataset to uncover meaningful compatibility patterns and co-occurring component characteristics. Insights can assist PC part recommendation systems, automated compatibility checkers, and retail inventory planning.

## 3. Objectives
- Preprocess PC hardware specifications and convert categorical features into itemsets
- Apply the Apriori algorithm to extract strong association rules
- Identify patterns relating component compatibility (e.g., CPU socket ↔ motherboard chipset, GPU tier ↔ PSU wattage)
- Evaluate rules using support, confidence, lift, and conviction

## 4. Dataset Plan
- Source: General Computer Hardware Dataset – Kaggle
  https://www.kaggle.com/datasets/dilshaansandhu/general-computer-hardware-dataset
- Domain: PC component specifications (CPU, GPU, RAM, storage, PSU, motherboard attributes)
- Size: ~1000+ records across multiple component categories
- Acquisition: Download CSV from Kaggle and store under data/pc_hardware.csv

### Dataset Transformation
Although non-transactional, the dataset will be prepared for association rule mining through:

- Binning continuous features (e.g., wattage = low/medium/high)
- Encoding categorical attributes (e.g., socket = AM4, chipset = B550)
- Treating each hardware record as a “transaction” of component attributes

## 5. Technical Approach
- Preprocessing:
    - Categorical encoding
    - Binning numeric features (price, wattage, RAM size)
    - TransactionEncoder for multi-item attribute representation
- Algorithm: Apriori
    - min_support = 0.05
    - min_confidence = 0.6
    - min_lift = 1.2
- Tools & Frameworks:
    - Python
    - pandas, mlxtend, matplotlib
    - Google Colab
- Environment: Google Colab

## 6. Expected Challenges & Mitigations
- Challenge: Dataset is not originally in transactional format
    - Solution: Feature binning + one-hot encoding to construct meaningful itemsets

- Challenge: Large variety of component attributes may produce sparse matrices
    - Solution: Drop extremely rare categories and group similar specs

- Challenge: Rules may be too obvious (e.g., AMD CPU → AM4 socket)
    - Solution: Explore deeper patterns using lift/conviction and limit rules to non-trivial attribute interactions