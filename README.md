# Metro Ağı Modeli

Bu proje, bir metro ağı içerisindeki istasyonlar arasındaki bağlantıları modelleyen ve farklı yol arama algoritmaları kullanarak, en az aktarma yapılan rotayı ve en hızlı yolu bulan bir simülasyondur.

## Kullanılan Teknolojiler ve Kütüphaneler

- **Python**: Projenin temel programlama dili.
- **collections**:
  - `defaultdict`: Hatlar için otomatik liste oluşturulmasını sağlar.
  - `deque`: BFS algoritmasında kuyruk yapısı olarak kullanılır.
- **heapq**: En hızlı rota arama algoritmasında (Dijkstra/A* yaklaşımına benzer) öncelikli kuyruk yapısı oluşturmak için kullanılmıştır.
- **typing**: Kodun okunabilirliğini ve güvenliğini artırmak için tip belirteçleri (`Dict`, `List`, `Tuple`, `Optional`) kullanılmıştır.

## Algoritmaların Çalışma Mantığı

### BFS Algoritması (En Az Aktarma)

- **Çalışma Prensibi**:
  - Başlangıç istasyonundan itibaren, tüm komşu istasyonlar genişlik öncelikli olarak (FIFO kuyruğu kullanılarak) ziyaret edilir.
  - Her adımda, mevcut istasyondan ulaşılabilen komşu istasyonlar kuyruğa eklenir.
  - Hedef istasyona ulaşıldığında, izlenen yol en az aktarma yapılan rota olarak döndürülür.
  
- **Neden Kullanıldı?**:
  - BFS, ağırlıksız graf yapılarında en kısa yol (en az aktarma) problemini çözmede etkili ve basit bir yöntemdir.

### A* (Dijkstra Yaklaşımı) Algoritması (En Hızlı Rota)

- **Çalışma Prensibi**:
  - Projede, `heapq` modülü kullanılarak öncelikli kuyruk yapısı ile toplam seyahat süresi hesaplanır.
  - Her adımda, mevcut istasyon ve biriken süre dikkate alınarak en düşük maliyetli (süre açısından) yol seçilir.
  - Hedefe ulaşıldığında, toplam seyahat süresi ve izlenen rota döndürülür.
  
- **A* ve Dijkstra Arasındaki Not**:
  - Uygulamada kullanılan yöntem, gerçek A* algoritmasında yer alan "heuristic" (kalan mesafe/süre tahmini) kullanılmadan Dijkstra algoritması olarak çalışmaktadır.
  - Eğer uygun bir tahmin fonksiyonu eklenirse, algoritma tam anlamıyla A* algoritmasına dönüşebilir.

- **Neden Kullanıldı?**:
  - Ağırlıklı graf yapılarında (yol sürelerinin farklılık gösterdiği durumlarda) en hızlı rotayı bulmak için Dijkstra algoritması, doğru ve verimli sonuçlar üretir.
  - Gerekli genişleme yapılarak A* algoritmasıyla entegre edilebilir, bu da gelecekteki geliştirmeler için esnek bir temel sunar.

## Örnek Kullanım ve Test Sonuçları

Projede aşağıdaki senaryolar test edilmiştir:

1. **AŞTİ'den OSB'ye**:
   - **En az aktarmalı rota**: AŞTİ, aktarma noktası olan Kızılay, ve diğer istasyonlar üzerinden OSB'ye ulaşan rota.
   - **En hızlı rota**: Toplam seyahat süresi hesaplanarak en kısa sürede varış sağlayan rota.

2. **Batıkent'ten Keçiören'e**:
   - Batıkent ile Keçiören arasındaki en uygun rota, ilgili hat üzerindeki istasyonlar kullanılarak hesaplanmıştır.

3. **Keçiören'den AŞTİ'ye**:
   - Hem en az aktarmalı hem de en hızlı rotalar belirlenip, karşılaştırmalı sonuçlar elde edilmiştir.

Test çıktıları, konsolda rota isimleri ve süre bilgileri şeklinde görüntülenmektedir.

## Projeyi Geliştirme Fikirleri

- **Heuristic Fonksiyonu Eklenmesi**:
  - Mevcut en hızlı rota arama algoritmasına uygun bir "heuristic" eklenerek tam anlamıyla A* algoritması uygulanabilir.
- **Grafiksel Arayüz**:
  - Metro ağı ve rotaların görsel olarak gösterilebileceği bir GUI (örneğin, Tkinter veya PyQt kullanılarak) geliştirilebilir.
- **Dinamik Güncellemeler**:
  - Gerçek zamanlı verilerle (örneğin, saatlik trafik yoğunluğu, sefer güncellemeleri) hat durumları ve seyahat süreleri dinamik olarak güncellenebilir.
- **Ek Özellikler**:
  - Bilet fiyatları, yolcu yoğunluğu, istasyon özellikleri gibi ek parametreler modele dahil edilerek daha kapsamlı bir simülasyon yapılabilir.
