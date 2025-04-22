<p align="center"><strong> MohammadAmin M. Shabestari </strong></p>

---

**Date**: 04/17/2025  
[LinkedIn Profile](https://www.linkedin.com/in/mohammadamin-shabestari) | [GitHub Profile](https://github.com/Msh8303)  
✉️ **Email**: shabestari8303p@gmail.com  

---

# [🏦 Fraud Detection in Credit Card Transactions - colab](https://colab.research.google.com/drive/15fk3srLz3C3Cz0ISA4GzSmxdPkJodlxh?usp=sharing)  
**A Comparative Study of Neural Networks and Traditional Machine Learning Models**

---

## 📜 Abstract  
This project investigates fraud detection in highly imbalanced credit card transaction data. We implement deep learning models (MLPs) with regularization techniques, compare them against traditional methods (Logistic Regression, XGBoost), and evaluate performance using precision, recall, F1-score, and AUC-ROC. Key findings reveal that **XGBoost outperforms neural networks** in balancing precision and recall, achieving an F1-score of 0.85 on imbalanced data. We also demonstrate the risks of overfitting in unregularized models and the importance of class imbalance mitigation.

---

## 📚 Table of Contents  
1. [Dataset Overview](#-dataset-overview)  
2. [Methodology](#-methodology)  
3. [Key Results](#-key-results)  
4. [Critical Analysis](#-critical-analysis)  
5. [Conclusion](#-conclusion)  

---

## 🏦 Dataset Overview  
### **Source**: [Credit Card Fraud Detection Dataset](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)  
#### **Features**:  
- **V1-V28**: Anonymized PCA-transformed features  
- **Time**: Seconds since first transaction  
- **Amount**: Transaction value  
- **Class**: Binary label (`0`: Non-fraud, `1`: Fraud)  

#### **Class Distribution**:  
| Class      | Count    | Percentage |  
|------------|----------|------------|  
| Non-Fraud  | 284,315  | 99.83%     |  
| Fraud      | 492      | 0.17%      |  

---

## 🧠 Methodology  
### 1. **Neural Network Architectures**  
- **Simple Network**: 1 hidden layer (64 units), ReLU activation  
- **Deep Network**: 2 hidden layers (128 → 64 units), ReLU activation  
- **Regularization**: Dropout (rate=0.2–0.4) and L2 penalty (λ=0.0001–0.001)  

### 2. **Training Pipeline**  
- **Class Balancing**: SMOTE-ENN oversampling  
- **Loss Weighting**: BCEWithLogitsLoss with `pos_weight` for minority class  
- **Early Stopping**: Patience=5 epochs, min Δ=0.01  

### 3. **Evaluation Metrics**  
- Precision, Recall, F1-Score, AUC-ROC  
- Comparative analysis with Logistic Regression and XGBoost  

---

## 📊 Key Results  
### **Top Performing Models**  
| Model                 | Dataset     | Precision | Recall | F1-Score | AUC   |  
|-----------------------|-------------|-----------|--------|----------|-------|  
| XGBoost               | Imbalanced  | 0.98      | 0.74   | 0.85     | 0.99  |  
| MLP (Balanced + Reg.) | Balanced    | 0.55      | 0.84   | 0.67     | 0.98  |  
| Logistic Regression   | Imbalanced  | 0.07      | 0.88   | 0.12     | 0.72  |  

### **Hyperparameter Tuning (Grid Search)**  
| Parameter         | Optimal Value |  
|-------------------|---------------|  
| Hidden Layer Size | 64            |  
| Dropout Rate      | 0.4           |  
| L2 Lambda         | 0.0001        |  
| Batch Size        | 64            |  

---

## 🔍 Critical Analysis  
### ❌ **Why Model 1 (Unbalanced, No Regularization) Fails**  
| Aspect               | Model 1 Behavior                | Ideal Behavior                  |  
|----------------------|----------------------------------|---------------------------------|  
| **Validation Loss**  | Drops to 0 (overfitting)        | Plateaus at small value (e.g., 0.002) |
| **Generalization**   | Fails on new fraud patterns     | Adapts to unseen data           |  

#### **Explanation**:  
1. **No Regularization**: Unconstrained weights memorize noise in training data.  
2. **Class Imbalance Ignorance**: Optimizes for majority class (non-fraud), achieving 99.9% accuracy but 0% fraud detection. 

---

## 🏆 Conclusion  
1. **Best Model**: **XGBoost** trained on **imbalanced data** achieves the highest F1-score (0.85) and precision (0.98), making it suitable for production.  
2. **Deep Learning Insights**:  
   - SMOTE-ENN balancing 
   - Regularization (dropout + L2) stabilizes training 
3. **Practical Recommendation**: Prioritize tree-based models (XGBoost) for imbalanced fraud detection tasks due to their robustness and interpretability.  
