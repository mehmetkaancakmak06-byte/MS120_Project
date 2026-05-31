# 🏋️ Egzersiz Öneri Sistemi
### Yapay Zeka Temelleri — Dönem Sonu Projesi

---

## Slayt 1 — Problem

**Problem:** Egzersiz yapmak isteyen bireyler hangi hareketleri, kaç set ve tekrarla yapacaklarını bilmekte zorlanıyor.

**Neden YZ gerekiyor?**
- Veri setinde 52 egzersiz var; elle seçmek zaman alır ve tekrara düşer
- İçerik tabanlı filtreleme, egzersizler arasındaki benzerliği otomatik ölçerek **çeşitli ve dengeli** bir program oluşturuyor

**Hedef:**  
Kullanıcı → hedef kas grubu + kaç gün → sistem → kişiselleştirilmiş haftalık program

---

## Slayt 2 — Veri Seti

**The Ultimate Gym Exercises Dataset for All Levels**  
Kaynak: Kaggle (peshimaammuzammil)

| Sütun | Açıklama | Örnek |
|-------|----------|-------|
| Body Part | Hedef kas grubu | Chest, Back, Legs... |
| Type of Muscle | Spesifik kas | Upper, Biceps, Triceps... |
| Workout | Egzersiz adı | Bench Press, Pull Up... |
| Sets | Set sayısı | 3, 4 |
| Reps per Set | Tekrar sayısı | 10, 12, 15 |

**52 egzersiz — 7 kas grubu:** Arms (10), Chest (9), Legs (9), Back (7), Abs (6), Forearms (6), Shoulders (5)

---

## Slayt 3 — Yöntem

**İçerik Tabanlı Filtreleme (Content-Based Filtering)**

```
Adım 1 → Feature Engineering
Body Part + Type of Muscle + Workout  →  "text_feature" sütunu
örn: "chest upper chest bench press"

Adım 2 → TF-IDF
text_feature  →  52 × N sayısal matris
(Her egzersiz bir vektör)

Adım 3 → Cosine Similarity
Egzersizler arası benzerlik matrisi hesaplanır

Adım 4 → Greedy Max Diversity
Seçilenlere en az benzeyen egzersiz → programa eklenir
→ Çeşitli ve tekrarsız program garantisi
```

---

## Slayt 4 — Sonuçlar

**Değerlendirme:** 10 farklı senaryo test edildi  
**Metrik:** Çeşitlilik Skoru = Benzersiz Hareket / Toplam Hareket

| Sonuç | Değer |
|-------|-------|
| Ortalama Çeşitlilik Skoru | **0.81 / 1.00** |
| En iyi kas grubu | Arms, Legs (1.0) |
| En düşük kas grubu | Back (0.63) |

**Yorum:**  
- 0.81 skoru, programların %81'inin benzersiz hareketten oluştuğunu gösteriyor  
- Back ve Shoulders'da düşük skor veri setinin küçüklüğünden kaynaklanıyor (7 ve 5 egzersiz)  
- Arms ve Legs gruplarında mükemmel çeşitlilik sağlandı

---

## Slayt 5 — Çıkarımlar & Geliştirme

**Ne öğrendim?**
- TF-IDF sadece metinler için değil, egzersiz özellikleri gibi kategorik veriler için de çalışıyor
- Greedy algoritması küçük veri setlerinde içerik filtrelemeye iyi bir alternatif
- Veri seti büyüklüğü doğrudan sonuç kalitesini etkiliyor

**Sınırlılıklar:**
- Veri seti küçük (52 egzersiz) — bazı kas gruplarında az seçenek
- Kullanıcının fitness düzeyi dikkate alınmıyor
- Tek kas grubu seçilebiliyor

**Geliştirme Önerileri:**
- Seviye filtresi (Beginner / Intermediate / Advanced) eklenebilir
- Birden fazla kas grubu seçimi desteklenebilir
- Streamlit ile web arayüzü yapılabilir
