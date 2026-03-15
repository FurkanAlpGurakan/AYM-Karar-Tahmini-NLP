# AYM Kararı Tahmini ve Doğal Dil İşleme (NLP) Analizi ⚖️🤖

Bu proje, Anayasa Mahkemesi (AYM) Bireysel Başvuru kararlarının metinlerini Doğal Dil İşleme (NLP) teknikleriyle analiz ederek, mahkemenin nihai kararını (İhlal Var / İhlal Yok / Kabul Edilemez) esastan tahmin etmeyi amaçlayan kapsamlı bir yapay zeka çalışmasıdır.

## 🎯 Proje Kapsamı ve Veri Toplama
Hukuki metinlerin uzun ve karmaşık yapısını bilgisayarlı dil modelleriyle çözmek amaçlanmıştır. Proje kapsamında:
* AYM Kararlar Bilgi Bankası üzerinden sistematik bir inceleme yapılarak, karar sonuçlarına göre (İhlal Var, İhlal Yok, Kabul Edilemez) dengeli bir dağılım gözetilerek **1.800 karar manuel olarak derlenmiş** ve makine öğrenmesine uygun, sınıflandırılmış özgün bir veri seti (corpus) oluşturulmuştur.
* Geleneksel NLP yaklaşımları ile modern Transformer mimarileri kıyaslanmıştır.

## 💾 Veri Seti (Kaggle)
Proje kapsamında, karar sonuçlarına göre dengeli bir dağılımla manuel olarak derlenen 1.800 kararlık özgün NLP veri setimize ve sınıflandırma detaylarına Kaggle üzerinden ulaşabilirsiniz:
👉 [**Turkish Court Decisions NLP Dataset**](https://www.kaggle.com/datasets/furkanalpgrakan/turkish-court-decisions-nlp)

## 🧹 Veri Sızıntısını (Data Leakage) Önleme
Hukuk metinlerinin en sonunda yer alan ve nihai kararı açıkça belirten "HÜKÜM" veya "SONUÇ" kısımları, modelin kopya çekmesini (Data Leakage) önlemek amacıyla **Regex** kullanılarak metinlerden tamamen ayıklanmıştır. Model, kararı sadece olayın gelişimi, iddialar ve hukuki gerekçelere bakarak tahmin etmeye zorlanmıştır.

## ⚙️ Modeller ve Mimari
Projede iki farklı yaklaşım geliştirilmiş ve kıyaslanmıştır:

1. **TF-IDF + Makine Öğrenmesi (Baseline Model):**
   * Metinler TF-IDF yöntemiyle vektörize edilmiş ve geleneksel sınıflandırma algoritmalarıyla eğitilmiştir.
2. **RoBERTa (Fine-Tuning):**
   * Semantik bağlamı (kelimelerin cümle içindeki anlamını) yakalamak için Transformer tabanlı güçlü bir dil modeli olan RoBERTa, kendi hukuki veri setimiz üzerinde *fine-tune* edilmiştir.

## 📊 Performans ve Sonuçlar
Modellerin başarısını en güvenilir şekilde ölçmek ve aşırı öğrenmenin (overfitting) önüne geçmek için **10-Fold Cross-Validation (Çapraz Doğrulama)** yöntemi kullanılmıştır. 

Elde edilen başarı (Accuracy) oranları şöyledir:

| Model / Yöntem | Başarı Oranı (Accuracy) | Açıklama |
| :--- | :---: | :--- |
| **TF-IDF Pipeline** | **%85.4** | Kelime frekanslarına dayalı geleneksel temel model. |
| **RoBERTa (Fine-tuned)** | **%92.5** | Semantik yapıyı ve hukuki bağlamı kavrayan derin öğrenme modeli. |

Sonuçlar, Transformer tabanlı modellerin (RoBERTa) hukuki metinlerin karmaşık bağlamını anlamada geleneksel yöntemlere (TF-IDF) göre belirgin bir üstünlük sağladığını göstermektedir.

*(Not: Fine-tune edilmiş RoBERTa modelinin ağırlık dosyaları, GitHub dosya boyutu kısıtlamaları nedeniyle bu repoya eklenmemiş olup, test aşamasında Google Drive üzerinden entegre çalışmaktadır.)*

## 🛠️ Kullanılan Teknolojiler
* **Dil & Ortam:** Python, Google Colab
* **Veri İşleme:** Pandas, Regex, Selenium, python-docx
* **NLP & Derin Öğrenme:** Hugging Face Transformers (RoBERTa), Scikit-Learn (TF-IDF)
