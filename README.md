# [Project Title: e.g. Retail Market Basket Analysis]
**CSC172 Data Mining and Analysis Final Project**  
*Mindanao State University - Iligan Institute of Technology*  
**Student:** Chris Adrian D. Gumisad, 2020-3275  
**Semester:** AY 2025-2026 Sem 1  

## Abstract
This project proposes the use of the Apriori algorithm to discover compatibility and co-occurrence patterns among PC components (CPU, GPU, RAM, motherboard, PSU, storage). Using a public hardware specifications dataset, the study will transform attributes into itemsets and mine association rules to identify relationships such as CPU socket ↔ motherboard chipset or GPU tier ↔ PSU wattage. The workflow includes preprocessing, exploratory data analysis (EDA), rule generation, and evaluation using support, confidence, lift, and conviction.

## Table of Contents
- [Abstract](#abstract)
- [1. Introduction](#1-introduction)
  - [1.1 Problem Statement](#11-problem-statement)
  - [1.2 Objectives](#12-objectives)
  - [1.3 Scope and Limitations](#13-scope-and-limitations)
- [2. Dataset Description](#2-dataset-description)
  - [2.1 Source and Acquisition](#21-source-and-acquisition)
  - [2.2 Data Structure](#22-data-structure)
  - [2.3 Sample Transactions](#23-sample-transactions)
- [3. Methodology](#3-methodology)
  - [3.1 Data Preprocessing](#31-data-preprocessing)
  - [3.2 Exploratory Data Analysis](#32-exploratory-data-analysis)
  - [3.3 Apriori Algorithm Implementation](#33-apriori-algorithm-implementation)
  - [3.4 Evaluation Metrics](#34-evaluation-metrics)
- [4. Results](#4-results)
  - [4.1 Top Association Rules](#41-top-association-rules)
  - [4.2 Key Visualizations](#42-key-visualizations)
  - [4.3 Performance Metrics](#43-performance-metrics)
- [5. Discussion](#5-discussion)
  - [5.1 Business Insights](#51-business-insights)
  - [5.2 Actionable Recommendations](#52-actionable-recommendations)
  - [5.3 Limitations](#53-limitations)
- [6. Conclusion](#6-conclusion)
- [7. Video Presentation](#7-video-presentation)
- [References](#references)
- [Appendix: Full Results](#appendix-full-results)



## 1. Introduction
### 1.1 Problem Statement
PC building requires matching components that are technically compatible. Understanding these relationships (e.g., socket type, wattage requirements, memory support) is essential for system integrators, retailers, and recommendation engines. This project aims to discover hidden compatibility patterns using association rule mining.

### 1.2 Objectives
- Preprocess PC hardware specifications for association analysis
- Transform attribute values into transactional-style itemsets
- Implement the Apriori algorithm to extract strong rules
- Evaluate rules using support, confidence, lift, and conviction
- Identify meaningful compatibility and co-occurrence patterns

### 1.3 Scope and Limitations
**Scope:** 
  - Single dataset of PC component specifications
  - Attribute-based association rule mining
  - Apriori algorithm only
**Limitations:** 
  - Dataset is not originally transactional
  - Requires encoding/bucketing continuous hardware specifications
  - No temporal or performance-based analysis

## 2. Dataset Description
### 2.1 Source and Acquisition
**Source:** General Computer Hardware Dataset – Kaggle (https://www.kaggle.com/datasets/dilshaansandhu/general-computer-hardware-dataset)
**Contents:** CPU, GPU, RAM, storage, motherboard, PSU specs  
**Size:** 9,835 transactions, 169 unique items  
**Format:** Member ID + timestamp + product name → Transaction basket format

### 2.2 Data Structure
Sample columns may include:
- component_type
- brand
- socket
- chipset
- memory_type
- psu_wattage
- gpu_tier
- capacity

### 2.3 Sample Transactions
| component_type | brand   | socket | chipset | wattage          | memory_type |
| -------------- | ------- | ------ | ------- | ---------------- | ----------- |
| CPU            | AMD     | AM4    | —       | 65W              | —           |
| GPU            | NVIDIA  | —      | —       | 550W recommended | —           |
| RAM            | Corsair | —      | —       | —                | DDR4        |

## 3. Methodology

### 3.1 Data Preprocessing
1. **Missing Value Handling:** Removed 127 incomplete transactions (1.3%)
2. **One-Hot Encoding:** Converted to 9,708 × 169 binary transaction matrix
3. **Item Filtering:** Retained top 50 items (support > 0.01) → 9,708 × 50 matrix
4. **Final Dataset:** 9,708 transactions × 50 items (98.7% sparsity reduced to manageable size)

**Before/After Statistics:**
| Metric | Raw Data | Processed Data |
|--------|----------|----------------|
| Transactions | 9,835 | 9,708 |
| Unique Items | 169 | 50 |
| Density | 0.12% | 2.1% |

### 3.2 Exploratory Data Analysis
- **Top 10 Items:** whole milk (25.3%), other vegetables (19.1%), rolls/buns (17.4%)
- **Basket Size:** Mean=2.4 items, 68% transactions contain 1-3 items
- **Co-occurrence:** whole milk appears with 89% of top 20 items

### 3.3 Apriori Algorithm Implementation
**Implementation:** mlxtend.frequent_patterns.apriori() with association_rules()

### 3.4 Evaluation Metrics
- **Support:** \( \frac{\text{support}(A \cup B)}{N} \) - Absolute frequency
- **Confidence:** \( \frac{\text{support}(A \cup B)}{\text{support}(A)} \) - Rule strength
- **Lift:** \( \frac{\text{confidence}(A \to B)}{\text{support}(B)} \) - Rule interestingness (>1 = positive association)


## 4. Results
### 4.1 Top Association Rules

| Rank | Antecedents | Consequents | Support | Confidence | Lift | Conviction | Leverage |
|------|-------------|-------------|---------|------------|------|------------|----------|
| 1 | {other vegetables} | {root vegetables} | 0.023 | 0.74 | 3.15 | 3.42 | 0.017 |
| 2 | {yogurt} | {whole milk} | 0.028 | 0.68 | 2.12 | 2.31 | 0.015 |
| 3 | {rolls/buns} | {whole milk} | 0.032 | 0.62 | 1.98 | 2.01 | 0.016 |
| 4 | {sausage} | {frankfurter} | 0.015 | 0.81 | 4.23 | 4.67 | 0.012 |
| 5 | {tropical fruit} | {other vegetables} | 0.021 | 0.65 | 2.34 | 2.41 | 0.014 |

### 4.2 Key Visualizations
![Item Frequency Distribution](results/item_frequencies.png) 

### 4.3 Performance Metrics
Runtime: Preprocessing=42s, Apriori=18s, Rules=3s (Total: 63s)
Scalability: Handles 10K+ transactions on standard laptop


## 5. Discussion

### 5.1 Business Insights
1. **Dairy Clustering:** whole milk as "hub item" (89% co-occurrence)
2. **Vegetable Pairing:** root vegetables strongly associated with other vegetables
3. **Breakfast Bundle:** yogurt + whole milk + rolls/buns (lift=2.1)

### 5.2 Actionable Recommendations
1. **Shelf Placement:** Place root vegetables near other vegetables
2. **Bundling:** Promote "Breakfast Pack" (yogurt + milk + rolls)
3. **Cross-promotion:** sausage → frankfurter discount coupons
4. **Inventory:** Stock 25% more whole milk based on pairing frequency

### 5.3 Limitations
- Single time period (no seasonality)
- No customer demographics
- Binary presence/absence (no quantities)

## 6. Conclusion
The Apriori algorithm successfully identified 25 actionable association rules from 9,708 grocery transactions. Strongest patterns reveal natural product groupings (lift > 3.0) suitable for retail optimization. Future work includes temporal analysis, customer segmentation, and FP-Growth comparison.


## 7. Video Presentation
[![Final Presentation](demo/CSC172_[LastName]_Final.mp4)](demo/CSC172_[LastName]_Final.mp4)  
*5-minute demo: Problem → Dataset → Methods → Key Findings → Business Insights*

## References
1. Agrawal, R., & Srikant, R. (1994). Fast Algorithms for Mining Association Rules. VLDB.
2. mlxtend Documentation: https://rasbt.github.io/mlxtend/
3. Groceries Dataset: https://www.kaggle.com/datasets/heeraldedhia/groceries-dataset

## Appendix: Full Results
**Complete rules CSV:** [results/rules_top25.csv](results/rules_top25.csv)  


