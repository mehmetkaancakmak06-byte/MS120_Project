# 📓 Proje Günlüğü — Egzersiz Öneri Sistemi

---

## 19.05.2026

**Ne yaptım?**  
Proje konusunu araştırdım. Kaggle'da birkaç farklı egzersiz veri seti inceledim. Sonunda "The Ultimate Gym Exercises Dataset for All Levels" (peshimaammuzammil) veri setine karar verdim. Veri seti 52 egzersiz içeriyor; Body Part, Type of Muscle, Workout, Sets, Reps per Set sütunları var. Projenin genel mimarisini ve hangi YZ tekniğini kullanacağımı planladım.

**Kullandığım kaynak:**  
Kaggle veri seti arama, Claude ile proje fikri ve mimari planlaması.

**Karşılaştığım sorun ve nasıl çözdüm:**  
Başta kullanıcıyı seviyeye (beginner/advanced) göre sınıflandırmak istedim ancak veri setinde seviye sütunu yoktu. Bu yüzden içerik tabanlı filtreleme (TF-IDF) yaklaşımına geçtim — bu hem veri setine daha uygun hem de öneri sistemi olarak ödev kriterlerini karşılıyor.

**Sonraki adım:**  
Jupyter Notebook kurmak, gerekli kütüphaneleri yüklemek ve veri setini ilk kez yükleyip incelemek.

---

## 21.05.2026

**Ne yaptım?**  
Geliştirme ortamını kurdum, requirements.txt'teki kütüphaneleri pip ile yükledim. Workout.csv'yi notebook'a yükledim, df.head(), df.info() ve df.describe() ile genel yapıyı inceledim. Body Part ve Type of Muscle sütunlarının dağılımlarını bar grafikleriyle görselleştirdim ve eda_grafik.png olarak kaydettim.

**Kullandığım kaynak:**  
pandas ve matplotlib dokümantasyonu, Claude'a grafik düzenleme kodunu sordum.

**Karşılaştığım sorun ve nasıl çözdüm:**  
Grafiklerde Türkçe karakter (ş, ğ, ü gibi) bozuk çıkıyordu. `plt.rcParams['font.family'] = 'DejaVu Sans'` satırını ekleyerek düzelttim.

**Sonraki adım:**  
Özellik mühendisliği (feature engineering) aşamasına geçmek — TF-IDF için metin özelliği oluşturmak.

---

## 23.05.2026

**Ne yaptım?**  
Body Part, Type of Muscle ve Workout sütunlarını birleştirerek `text_feature` adında yeni bir sütun oluşturdum. Bu sütunu TF-IDF vektörleştirici ile matrise dönüştürdüm. Oluşan matrisin boyutunu kontrol ettim (52 x N). Cosine similarity matrisini hesaplayıp iki egzersiz arasındaki benzerliği elle kontrol ettim.

**Kullandığım kaynak:**  
sklearn TF-IDF dokümantasyonu, Claude'a "TF-IDF nasıl çalışır ve stop_words ne işe yarar" diye sordum.

**Karşılaştığım sorun ve nasıl çözdüm:**  
`stop_words='english'` parametresi bazı kısa egzersiz kelimelerini matrise dahil etmiyordu. Bunun TF-IDF'in normal bir davranışı olduğunu öğrendim; kısa tek kelimeli egzersiz adları için sorun çıkarmadı.

**Sonraki adım:**  
Greedy Max Diversity algoritmasını kullanarak öneri fonksiyonunu yazmak.

---

## 25.05.2026

**Ne yaptım?**  
`egzersiz_programi_olustur()` fonksiyonunu yazdım. Fonksiyon önce hedef kas grubuna göre veri setini filtreliyor, ardından Greedy Max Diversity algoritmasıyla birbirine en az benzeyen egzersizleri seçiyor ve günlere dengeli dağıtıyor. Fonksiyonu "Chest 3 gün", "Back 4 gün" ve "Legs 3 gün" ile test ettim, çıktılar mantıklı göründü.

**Kullandığım kaynak:**  
Claude'a Greedy Max Diversity algoritmasının mantığını ve Python implementasyonunu sordum. Stack Overflow'da benzer seçim algoritmalarına baktım.

**Karşılaştığım sorun ve nasıl çözdüm:**  
Bazı kas gruplarında toplam ihtiyaçtan az egzersiz vardı (örn. Shoulders için 5 günlük program istenince). İndex hatası alıyordum. Mevcut egzersizleri döngüsel olarak tekrarlayan bir while döngüsü ekleyerek çözdüm.

**Sonraki adım:**  
10 farklı senaryo ile sistemi değerlendirmek, çeşitlilik skoru hesaplamak ve grafik oluşturmak.

---

## 27.05.2026

**Ne yaptım?**  
10 farklı test senaryosu tanımlayıp hepsini çalıştırdım. Her senaryo için Çeşitlilik Skoru (benzersiz hareket / toplam hareket) hesapladım. Sonuçları tablo olarak yazdırıp bar grafik ve yatay grafik ile görselleştirdim; degerlendirme_grafik.png olarak kaydettim. Ortalama skoru README'ye eklemek üzere not aldım.

**Kullandığım kaynak:**  
matplotlib ile çift panel grafik oluşturma — Claude'a renk kodlama (skor >= 0.8 mavi, >= 0.6 turuncu, diğerleri kırmızı) kısmını sordum.

**Karşılaştığım sorun ve nasıl çözdüm:**  
"Arms" kas grubunda sadece birkaç egzersiz olduğu için 5 günlük program istendiğinde skor düşük çıkıyordu. Bunu sınırlılık olarak not aldım; veri setinin küçük olmasından kaynaklanıyor.

**Sonraki adım:**  
README.md ve gunluk.md dosyalarını tamamlamak, GitHub reposunu oluşturup push etmek.

---

## 31.05.2026

**Ne yaptım?**  
README.md dosyasını tüm başlıklarla (problem tanımı, veri seti, yöntem, nasıl çalıştırılır, sonuçlar, sınırlılıklar) doldurdum. Proje günlüğünü tamamladım. GitHub'da public repo açtım, tüm dosyaları push ettim. sunum.md taslağını oluşturmaya başladım.

**Kullandığım kaynak:**  
Claude ile README taslağı ve sunum yapısı. GitHub dokümantasyonu.

**Karşılaştığım sorun ve nasıl çözdüm:**  
GitHub'a push ederken `remote: Support for password authentication was removed` hatası aldım. Personal Access Token (PAT) oluşturup git credential olarak kaydederek çözdüm. GitHub'ın bu konudaki dokümantasyonunu takip ettim.

**Sonraki adım:**  
sunum.md'yi bitirmek ve sözlü sunuma hazırlanmak.
