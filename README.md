# STM32 GPIO ile Dijital Kontrol ve LED Animasyonu 

Bu proje, STM32 mikrodenetleyicisinin temel taşı olan **GPIO (General Purpose Input Output)** biriminin hem "Dijital Çıkış" (LED kontrolü) hem de "Dijital Giriş" (Buton okuma) yeteneklerini donanım seviyesinde incelemek amacıyla tasarlanmıştır[cite: 8]. 

Gömülü sistem programlamanın klasik "Kara Şimşek" efekti, sisteme eklenen anlık kullanıcı girdileriyle (Hızlandırma, Durdurma, Tümünü Yakma) dinamik bir yapıya kavuşturulmuştur[cite: 8].

## 🚀 Öne Çıkan Özellikler (Highlights)

*   **Push-Pull Donanım Sürme:** Harici devrelere (Örn: LED) güç sağlayabilmek için çıkış pinleri donanımsal olarak **Push-Pull (İt-Çek)** modunda konfigüre edilmiştir[cite: 8]. (Sistemde koruma için 220Ω / 330Ω dirençler kullanılmıştır)[cite: 8].
*   **Pull-Down Kavramı:** Giriş pinlerinde "Floating (Yüzen Pin)" tehlikesini önlemek ve sinyal kararlılığını sağlamak amacıyla donanımsal mantık kurulmuştur[cite: 8]. Butonlar için mikrodenetleyicinin dahili `Pull-down` özelliği aktif edilmiştir[cite: 8].
*   **Dinamik Animasyon Kontrolü:** Kod algoritması; `HAL_GPIO_ReadPin` ile anlık buton durumlarını okuyarak animasyonu durdurabilen (Pause), hızlandırabilen veya tüm LED'leri SET edebilen durum makineleri barındırır[cite: 8].

## 🛠️ Donanım ve Pin Yapılandırması

Sistemdeki dış birimlerin STM32 Nucleo-F072RB üzerindeki pin atamaları ve yapılandırmaları aşağıdaki gibidir[cite: 8]:

| Bileşen | Pin Kodu | Kullanım Modu | Açıklama |
| :--- | :--- | :--- | :--- |
| **LED 1-8** | `PA0-PA7` | GPIO_Output | 8 adet kırmızı LED'in sürülmesi için Port A çıkış pinleri[cite: 8]. |
| **Buton 1** | `PB0` | GPIO_Input (Pull-Down) | Tüm LED'leri yakma (Set All) giriş pini[cite: 8]. |
| **Buton 2** | `PB1` | GPIO_Input (Pull-Down) | Animasyonu olduğu yerde dondurma (Pause) giriş pini[cite: 8]. |
| **Buton 3** | `PB2` | GPIO_Input (Pull-Down) | Animasyon hızını artırma (Speed Up) giriş pini[cite: 8]. |

## 📂 Yazılım Mimarisi (Algoritma)

Sistem sonsuz bir döngü (`while(1)`) içerisinde çalışır ve donanımı kontrol etmek için temel HAL kütüphanesi fonksiyonlarını (`HAL_GPIO_WritePin`, `HAL_GPIO_ReadPin`, `HAL_Delay`) kullanır[cite: 8].

1.  **İleri Yön Döngüsü:** LED'ler sırayla yanar[cite: 8]. Her adımdan önce butonlar kontrol edilir[cite: 8].
2.  **Kullanıcı Girdileri:**
    *   **Buton 1 (PB0):** Lojik-1 durumundayken `while` döngüsüne girilip tüm LED'lere `GPIO_PIN_SET` gönderilir[cite: 8].
    *   **Buton 2 (PB1):** Lojik-1 durumundayken kod satırında sonsuz bir bekleme yaratılarak animasyon durdurulur[cite: 8].
    *   **Buton 3 (PB2):** Lojik-1 durumundayken `beklemeSuresi` değişkeni `50ms`'ye düşürülerek animasyon hızlandırılır[cite: 8].

## 💻 Nasıl Çalıştırılır?

1.  STM32CubeIDE ile projeyi açın.
2.  Kodu derleyin (`Build`) ve karta yükleyin[cite: 8].
3.  Varsayılan durumda LED animasyonu yavaş hızda (250ms) çalışacaktır[cite: 8].
4.  Breadboard üzerindeki butonları kullanarak yazılan algoritmik kontrol mekanizmalarını test edebilirsiniz[cite: 8].

   <img width="1126" height="720" alt="df" src="https://github.com/user-attachments/assets/97474552-c566-4681-882f-1e1987c3ca55" />
