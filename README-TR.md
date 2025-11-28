Q-Öğrenme Kullanarak Otonom Taksi Ajanı

Bu proje, Gymnasium kütüphanesini kullanarak bir taksi sürücüsü için özel bir ortam oluşturan bir pekiştirmeli öğrenme projesidir. Taksi sürücüsü, Q-Öğrenme algoritması ile çevrede gezinmek, yolcu almak ve bırakmak için eğitilir. Taksi, ödülünü maksimize etmek için yolunu optimize etmeyi, engellerden ve yasaklı bölgelerden kaçınmayı öğrenir.
Projem için referans olarak şunu kullandım:
https://github.com/woutervanheeswijk/taxi_environment?tab=readme-ov-file

- Özel ortam (environment):
    Proje, 5 alma/bırakma noktası ve 2 yasaklı alan içeren özel 6x6 bir ızgaraya sahiptir.

```
MAP = [
"+-----------+",
"| : | : : : |",
"|A: | :B: : |",
"| :R: : : |C|",
"| : : : : :R|",
"|D| : : : : |",
"| | : : : |E|",
"+-----------+",
]
```


A, B, C, D, E harfleri alma ve bırakma noktalarını temsil eder. R harfi kırmızı kare ile gösterilen yasaklı alanı belirtir. ‘|’ sembolü ortamın duvarlarını ifade eder.

- Q-Öğrenme algoritması:
    Projede taksi sürücüsünü eğitmek için Q-Öğrenme algoritması uygulanmıştır. Algoritma, alınan ödüllere ve taksinin eylemlerine bağlı olarak Q-değerlerini günceller. Q-Tablosu, yeniden eğitime gerek kalmadan gelecekte kullanılmak üzere bir CSV dosyasına kaydedilir.

- Değerlendirme:
    Ajan, eğitim sırasında her 300 bölümde bir değerlendirilir. Daha sonra kümülatif ödüle göre en iyi model takip edilir ve kaydedilir.

- Ödül sistemi:
    Ödül sistemi Gymnasium Taxi-v3 ortamı ile aynıdır:

    - Her zaman adımı için -1
    - Yolcuyu başarıyla bırakmak için +20
    - Yasaklı alma/bırakma işlemi için -10

- Actions:
Toplam 6 action vardır:

    0: güneye hareket
    1: kuzeye hareket
    2: doğuya hareket
    3: batıya hareket
    4: yolcu alma
    5: yolcu bırakma        

• Hiperparametreler:
    - Bölüm sayısı: 10,000
    - Alpha (Öğrenme Oranı): 0.1
    - Gamma (İskonto Faktörü): 1.0
    - Epsilon (Keşif Oranı): 0.1    

Nasıl çalıştırılır:
    Ajanı sıfırdan eğitmek için:

   1. taxi_q_learning.ipynb Jupyter Notebook dosyasını açın.
   2. TaxiEnv sınıfı tanımını ve görselleştirme yöntemlerini içeren     hücreleri çalıştırın.
   3. Eğitim hücresini çalıştırın.
        o Bu işlem ajanı 10,000 bölüm boyunca eğitir.
        o En iyi Q-Tablosunu otomatik olarak taxi_q_table.csv dosyasına kaydeder.
    4. Eğitimden sonra politika performansını test etmek için:
        o Test hücresini çalıştırın.
        o  Bu işlem CSV dosyasından Q-Tablosunu yükler ve ajanı ortamda çalıştırır.
        o Son ödülü ve ajanın yolunun görselleştirmesini görüntüler.

• Sonuçlar:

  ![res1](res1.png)
  
  ![res2](res2.png)

    Sonuçlara göre ajan oldukça başarılı bir performans göstermiş ve oldukça erken öğrenmiştir. 488. bölümde 16.0 en iyi kümülatif ödülüne ulaşmıştır.
