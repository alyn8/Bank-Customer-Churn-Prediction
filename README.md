# 🏦 Banka Müşteri Terk (Churn) Tahmini

Bu projede, bir bankanın müşteri verileri kullanılarak müşterilerin bankadan ayrılıp ayrılmayacağı (churn) tahmin edilmiştir. 

---

## 🎯 Proje Amacı

Makine öğrenmesi tabanlı bir model oluşturarak, bankaların müşteri kaybını önceden tahmin edip bu kayıpları azaltabilecek stratejik aksiyonlar almasına yardımcı olmak.

---

## 📦 Veri Seti

- **Kaynak:** [Kaggle – Churn Modelling Dataset](https://www.kaggle.com/datasets/adammaus/predicting-churn-for-bank-customers)
- **Veri Sayısı:** 10.000
- **Özellikler:**
  - Kredi skoru, ülke, cinsiyet, yaş, bankada kalma süresi, bakiye, ürün sayısı, kredi kartı kullanımı, aktiflik durumu, maaş
- **Hedef Değişken:**
  - `Exited` (1 = müşteri ayrılmış, 0 = müşteri kalmış)

---

## 🔍 Veri Analizi (EDA)

- Müşteri churn oranlarının görselleştirilmesi (pie chart, bar plot)
- `Geography`, `Gender`, `IsActiveMember`, `HasCrCard` gibi değişkenlere göre ayrım
- Korelasyon ısı haritası ile özellikler arası ilişki analizi

---
## 📊 Churn Dağılımı

```python
df['Exited'].value_counts(normalize=True).plot(kind='bar')

```


## 🛠️ Veri Ön İşleme

- Anlamsız sütunlar kaldırıldı: `RowNumber`, `CustomerId`, `Surname`
- Kategorik değişkenler `get_dummies()` ile dönüştürüldü
- Sayısal değişkenler `StandardScaler` ile ölçeklendirildi
- Veriler eğitim ve test kümelerine ayrıldı (%80 - %20) '

---

## 🤖 Kullanılan Modeller

- Logistic Regression
- Random Forest Classifier
- XGBoost Classifier
- SVM(Support Vector Machine)

## 🛠️ GridSearchCV (Random Forest için)

Random Forest modeli için hiperparametre optimizasyonu `GridSearchCV` ile yapılmıştır. Amaç, modelin `n_estimators`,`max_depth`, `min_samples_split` gibi parametreleri için en iyi kombinasyonu bulmaktır.

```python
grid_search = GridSearchCV(estimator=rf_model, param_grid=param_grid, ...)
```

---

## 📈 Model Performans Karşılaştırması

| **Model**             | **Doğruluk (Accuracy)** | **Recall (Churn)** | **Precision (Churn)** | **F1 Skoru (Churn)** |
|-----------------------|--------------------------|---------------------|------------------------|------------------------|
| Logistic Regression   | 0.808                    | 0.19                | 0.59                   | 0.28                   |
| Random Forest         | 0.860                    | 0.46                | 0.78                   | 0.58                   |
| XGBoost    | 0.850                    | **0.49**            | **0.70**               | **0.58**   |
| SVM        | 0.840                    | **0.42**            | **0.65**               | **0.51**  |

XGBoost ve Random Forest en başarılı sonuçları vermiştir. Logistic Regression bir baseline olarak kullanılmış, SVM modeli de alternatif bir doğrusal dışı yöntem olarak denenmiştir.
---


## 📊 Ek Analizler

### 💡 Özellik Önem Düzeyi (XGBoost)

```python
plot_importance(xgb, importance_type='weight')

```
Modelin kararlarında en etkili olan özellikler:
- Yaş (`Age`)
- Aktif müşteri olup olmama (`IsActiveMember`)
- Almanya’da ikamet (`Geography_Germany`)

### 📐 ROC Eğrisi ve AUC Skoru (XGBoost)

```python
fpr, tpr, thresholds = roc_curve(...)
plt.plot(fpr, tpr, label=f"AUC = {roc_auc:.2f}")
```
XGBoost modeli için ROC eğrisi çizildi ve AUC skoru hesaplandı. Bu skor, modelin churn olan müşterileri ne kadar başarılı ayırt ettiğini gösterir. XGBoost için AUC değeri %85’in üzerindedir.

---

## ✅ Sonuç ve Değerlendirme

Üç farklı model karşılaştırılmış, XGBoost modeli hem doğruluk hem de dengeli F1 ve recall skorları ile **final model** olarak seçilmiştir.

Churn tahmini, bankalar için hayati bir konudur ve bu projede geliştirilen model, bankaların churn riski taşıyan müşterileri tespit ederek erken müdahale şansı yaratmasına olanak tanır.

---

## 🔗 Kaggle Notebook Linki

👉 [Kaggle linki](https://www.kaggle.com/code/aeri88/bank-customer-churn-prediction)

---

## 📁 Dosya Yapısı

📦 churn-tahmin-projesi

┣ 📄 bank_churn_prediction.ipynb   
┣ 📄 README.md                     
        

