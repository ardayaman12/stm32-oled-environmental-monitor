# stm32-oled-environmental-monitor
# STM32 I2C OLED & Encoder Tabanlı Ortam İzleme ve Alarm Sistemi

Bu proje, **STM32F407** mikrodenetleyicisi üzerinde ADC, EXTI (Harici Kesmeler) ve I2C çevre birimlerini kullanarak çevresel parametreleri (sıcaklık ve ışık) izleyen, kullanıcıya rotary enkoder kontrollü bir OLED arayüzü sunan gömülü bir sistemdir.

---

## 📌 Proje Özeti
Sistem, ortamdaki sıcaklık ve ışık seviyelerini analog sensörler üzerinden gerçek zamanlı olarak okur. Elde edilen veriler matematiksel modellere tabi tutularak I2C haberleşmeli SSD1306 OLED ekranda görüntülenir. Eşik değerler aşıldığında sistem sesli ve görsel çıkışlarla uyarı verir. Kullanıcı, rotary enkoder yardımıyla menüler arasında geçiş yapabilir.

---

## 🛠 Donanım Mimarisi

### 1. Giriş Birimleri (Inputs)
* **LDR (Işık Sensörü) -> PA0 (ADC1_IN0):** Ortamdaki ışık şiddetini analog olarak ölçer.
* **NTC Termistör (10k) -> PA1 (ADC1_IN1):** Ortam sıcaklığını ölçer. Okunan ADC değeri, kod içinde **Steinhart-Hart/Beta formülü** kullanılarak gerçek Celsius derecesine dönüştürülür.
* **Rotary Enkoder -> PD4, PD5 (EXTI) & PD6 (GPIO In):** Ekran menüleri arasında gezinmeyi sağlayan mekanik arayüz. Tuş sıçramaları (switch bounce) yazılımsal debounce ile filtrelenmiştir.

### 2. Çıkış Birimleri (Outputs)
* **SSD1306 0.96" OLED Ekran -> PB6 (SCL), PB7 (SDA):** I2C protokolü üzerinden menüleri, sıcaklık durumunu ve ışık yüzdesini dinamik olarak basar.
* **3 Kademeli Durum LED'leri (PD0, PD1, PD2):** Işık seviyesine göre düşük, orta ve yüksek durumlarını görselleştirir (Kırmızı, Sarı, Yeşil).
* **Buzzer / Alarm Çıkışı (PD7):** Sıcaklık 40°C eşik değerini aştığında kritik durum uyarısı tetikler.

---

## ⚙️ Teknik Özellikler ve Algoritmalar
* **Mikrodenetleyici:** ARM Cortex-M4 (STM32F407VGT6)
* **Haberleşme:** 100 kHz Standart Hızda I2C1 Arayüzü
* **Analog Ölçüm:** 12-bit Çözünürlük (0 - 4095)


---



