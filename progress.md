# CSC172 Association Rule Mining Project Progress Report
**Student:** Chris Adrian D. Gumisad, 2020-3275  
**Date:** December 16, 2025  
**Repository:** https://github.com/Aeonalyxx/CSC172_AssociationMining  

## 📊 Current Status
| Milestone              | Status        | Notes                                                    |
| ---------------------- | ------------- | -------------------------------------------------------- |
| Dataset Preparation    | ✅ Completed   | 6000 realistic compatible PC build transactions generated |
| Data Preprocessing     | ✅ Completed   | Binned numeric features; one-hot encoded matrix ready    |
| EDA & Visualization    | ⏳ In Progress | Item frequency distribution and top items computed       |
| Apriori Implementation | ⏳ Pending     | Initial run planned after EDA                            |
| Rule Evaluation        | ⏳ Not Started | Planned after Apriori rules are generated                |

## 1. Dataset Progress
- **Total transactions:** 6000
- **Unique items:** ~189 → Filtered to top 132 items (support > 0.01)
- **Matrix size:** 6000 transactions × 132 items (11.17% density)
- **Preprocessing applied:** Missing values removed, TDP/VRAM/Watt/Size binned, DDR3 excluded, CPU↔MB↔RAM compatibility enforced, one-hot encoding applied

**Sample transaction preview:**
Transaction 1: ['CPU_Producer:Intel', 'CPU_Socket:1200', 'CPU_TDP:96-125W',
 'MB_Producer:ASUS', 'MB_Socket:1200', 'MB_Chipset:Z590', 'MB_Memory:DDR4',
 'RAM_Producer:Crucial', 'RAM_Type:DDR4', 'RAM_Size:16GB',
 'GPU_Producer:EVGA', 'GPU_VRAM:8GB', 'GPU_TDP:151-250W',
 'PSU_Producer:Xilence', 'PSU_Watt:451-600W']

Transaction 2: ['CPU_Producer:AMD', 'CPU_Socket:AM4', 'CPU_TDP:<=65W',
 'MB_Producer:MSI', 'MB_Socket:AM4', 'MB_Chipset:B550', 'MB_Memory:DDR4',
 'RAM_Producer:G.Skill', 'RAM_Type:DDR4', 'RAM_Size:16GB',
 'GPU_Producer:Gigabyte', 'GPU_VRAM:6GB', 'GPU_TDP:<=150W',
 'PSU_Producer:PHANTEKS', 'PSU_Watt:901-1200W']

## 2. EDA Progress

**Key Findings (so far):**
![Item Frequency Distribution](results/item_frequencies.png)
- CPU TDP categories: <=65W, 66-95W, 96-125W, >125W
- GPU TDP categories: <=150W, 151-250W
- PSU Watt categories: 451-600W, 601-750W, 751-900W, 901-1200W
- RAM sizes: 8GB, 16GB, 32GB, 64GB
- Most common CPU producer: Intel
- Most common motherboard memory: DDR4
- Average number of items per transaction: ~15

**Current Metrics:**
| Metric               | Value                    |
| -------------------- | ------------------------ |
| Transactions cleaned | 6000/6000 (100%)           |
| Sparsity             | 92.1%                    |
| Top item support     | CPU_Producer:Intel ~0.38 |

## 3. Challenges Encountered & Solutions
| Issue                              | Status  | Resolution                                                 |
| ---------------------------------- | ------- | ---------------------------------------------------------- |
| Ensuring CPU-MB-RAM compatibility  | ✅ Fixed | Transactions generated respecting Socket and RAM type      |
| Small number of valid transactions | ✅ Fixed | Generated randomized compatible builds (~6000 transactions) |
| Non-numeric attributes for ARM     | ✅ Fixed | Binned numeric features (TDP, Watt, VRAM, RAM size)        |
| Outdated components (DDR3)         | ✅ Fixed | DDR3 removed during preprocessing                          |

## 4. Next Steps (Before Final Submission)
- [ ] Complete co-occurrence heatmap
- [ ] Run Apriori algorithm (min_support=0.02, min_confidence=0.6, min_lift=1.2)
- [ ] Generate top 25 rules with metrics
- [ ] Create rule scatter plot 
- [ ] Record 5-min demo video
- [ ] Write complete README.md 
