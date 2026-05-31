# 🏋️ Egzersiz Öneri Sistemi

Kas grubuna göre kişiselleştirilmiş haftalık antrenman programı oluşturucu.

---

## Problem Tanımı

Egzersiz yapmak isteyen bireyler hangi hareketleri, kaç set ve tekrarla yapacaklarını bilmekte zorlanmaktadır. Bu proje, kullanıcının hedef kas grubunu ve program süresini girmesiyle veri setindeki egzersizlerden kişiselleştirilmiş ve çeşitli bir haftalık antrenman programı önermektedir. İçerik tabanlı filtreleme yaklaşımıyla benzer hareketlerin tekrarı önlenir ve dengeli bir program oluşturulur.

---

## Kullanılan Veri Seti

**The Ultimate Gym Exercises Dataset for All Levels**  
Kaynak: [Kaggle — peshimaammuzammil](https://www.kaggle.com/datasets/peshimaammuzammil/the-ultimate-gym-exercises-dataset-for-all-levels)
Dosya: `Workout.csv`  
İçerik: 52 egzersiz — `Body Part`, `Type of Muscle`, `Workout`, `Sets`, `Reps per Set`

---

## Kullanılan Model / Yöntem

| Bileşen | Açıklama |
|---------|----------|
| **Yöntem** | İçerik Tabanlı Filtreleme (Content-Based Filtering) |
| **Özellik** | TF-IDF (Term Frequency - Inverse Document Frequency) |
| **Benzerlik** | Cosine Similarity |
| **Seçim Algoritması** | Greedy Max Diversity — en çeşitli egzersiz setini seçer |

---

## Nasıl Çalıştırılır

### 1. Gereksinimleri yükle

```bash
pip install -r requirements.txt
```

### 2. Repoyu klonla

```bash
git clone https://github.com/KULLANICI_ADIN/egzersiz-oneri
cd egzersiz-oneri
```

### 3. Veri setini hazırla

Kaggle'dan [bu linkteki](https://www.kaggle.com/datasets/peshimaammuzammil/the-ultimate-gym-exercises-dataset-for-all-levels) veri setini indir.  
`Workout.csv` dosyasını proje klasörüne koy.

### 4. Notebook'u çalıştır

```bash
jupyter notebook egzersiz_oneri.ipynb
```

Hücreleri sırayla çalıştır. 7. hücrede hedef kas grubunu ve kaç günlük program istediğini gir.

---

## Sonuçlar

- 10 farklı senaryo ile değerlendirme yapıldı
- Ortalama Çeşitlilik Skoru: **_(0.81 / 1.00)_**
- EDA grafiği: `eda_grafik.png`
- Değerlendirme grafiği: `degerlendirme_grafik.png`

---

## Sınırlılıklar ve Geliştirme Önerileri

**Sınırlılıklar:**
- Veri seti küçük (52 egzersiz) — bazı kas gruplarında az seçenek var
- Kullanıcının fitness düzeyi ve sağlık durumu dikkate alınmıyor
- Tek seferde yalnızca bir kas grubu seçilebiliyor
- Egzersizler arası dinlenme süresi önerilmiyor

**Geliştirme Önerileri:**
- Daha büyük bir veri setiyle genişletilebilir
- Beginner / Intermediate / Advanced seviye filtresi eklenebilir
- Birden fazla kas grubu seçimi desteklenebilir
- Streamlit ile interaktif web arayüzü eklenebilir
- Egzersiz açıklamaları ve video bağlantıları eklenebilir
