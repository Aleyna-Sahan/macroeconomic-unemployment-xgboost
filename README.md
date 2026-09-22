# 📈 Macroeconomic Unemployment Rate Prediction with XGBoost

> **Lisans Bitirme Projesi** — Farklı gelişmişlik düzeylerindeki ülkelerin makroekonomik göstergeleri kullanılarak işsizlik oranının XGBoost algoritması ile tahmini ve açıklayıcı analizi.

## 📌 Proje Özeti
Bu çalışma; gelişmiş (ABD, Almanya, Güney Kore) ve gelişmekte olan (Brezilya vb.) ülkelerin 2000–2025 dönemini kapsayan 25 yıllık verilerini temel alarak, makroekonomik göstergeler ile işsizlik oranı arasındaki doğrusal olmayan (non-linear) karmaşık ilişkileri haritalandırmayı amaçlamaktadır.

Klasik ekonometrik modellerin asimetrik şokları ve yüksek varyansı yakalamadaki yetersizliğine alternatif olarak, düzenlileştirme (regularization) yeteneğine sahip **Extreme Gradient Boosting (XGBoost)** algoritması kullanılmıştır.

---

## 📊 Veri Seti & Değişkenler
Veriler **Federal Reserve Economic Data (FRED)** üzerinden aylık bazda temin edilmiştir:
- **Bağımlı Değişken:** `ISSIZLIK` — İşsizlik Oranı (%)
- **Bağımsız Değişkenler:**
  - `TUFE` — Tüketici Fiyat Endeksi (Enflasyon ve satın alma gücü)
  - `SURETIM` — Sanayi Üretim Endeksi (Ekonomik üretim kapasitesi)
  - `ISFAIZ` — İskonto Faizi (Yatırım maliyeti ve sermaye akışı için Proxy değişken)
  - `Ülke Değişkenleri` — Yapısal farklılıkları temsil eden One-Hot Encoded kukla değişkenler

---

## ⚙️ Model Mimarisi & Hiperparametreler
Model, aşırı öğrenmeyi (overfitting) engellemek amacıyla erken durdurma (early stopping) ve alt örnekleme kurallarıyla eğitilmiştir:

| Parametre | Değer | Açıklama |
| :--- | :--- | :--- |
| **Learning Rate** | `0.05` | Adım küçültme ve genelleştirme kontrolü |
| **N Estimators** | `1000` | Sıralı ağaç sayısı |
| **Max Depth** | `6` | Ağaç derinlik limiti |
| **Subsample** | `0.80` | Rastgele veri örneklem oranı |
| **Colsample Bytree**| `0.80` | Rastgele öznitelik örneklem oranı |
| **Early Stopping** | `50` | İyileşme durduğunda eğitimi kesme eşiği |

---

## 🎯 Model Performansı ve Bulgular

Model %80 Eğitim / %20 Test bölünmesi ile test seti üzerinde değerlendirilmiş ve şu metrikler elde edilmiştir:

| Metrik | Değer | Yorum |
| :--- | :--- | :--- |
| **$R^2$ (Belirlilik Katsayısı)** | **%96.69** (0.9669) | Model değişkenlerin varyansını başarıyla açıklamaktadır |
| **MAE (Ortalama Mutlak Hata)** | **0.2024** | Gerçek işsizlik değerinden yalnızca ~0.20 puan sapma |
| **RMSE** | **0.4973** | Ceza ağırlıklı kök ortalama kare hata |

### 🔍 Temel Bulgular (Özellik Önemi - Feature Importance)
1. **En Belirleyici Faktör (TÜFE):** Model karar mekanizmasında en yüksek bilgi kazancını (information gain) Tüketici Fiyat Endeksi elde etmiş; enflasyonist şokların istihdam üzerindeki baskınlığı doğrulanmıştır.
2. **Yapısal Ülke Etkisi:** Güney Kore kukla değişkeni ikinci en yüksek öneme sahip olmuştur; ülkenin teknoloji odaklı sanayi ve istikrarlı işgücü yapısının küresel şoklara karşı koruyucu bir yapı oluşturduğu gözlemlenmiştir.

---

## 📂 Proje Çıktıları & Grafikler

### 1. Korelasyon Matrisi (Isı Haritası)
![Correlation Matrix](results/figures/correlation_heatmap.png)

### 2. Özellik Önemi (Feature Importance)
![Feature Importance](results/figures/feature_importance.png)

---

## 🚀 Çalıştırma

```bash
# Repoyu klonlayın
git clone [https://github.com/Aleyna-Sahan/macroeconomic-unemployment-xgboost.git](https://github.com/Aleyna-Sahan/macroeconomic-unemployment-xgboost.git)

# Bağımlılıkları yükleyin
pip install -r requirements.txt

# Notebook'u çalıştırın
jupyter notebook notebooks/unemployment_prediction_xgboost.ipynb
