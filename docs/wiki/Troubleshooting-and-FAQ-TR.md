# 🔧 Sorun Giderme & Sıkça Sorulan Sorular

<p align="center">
  <a href="Troubleshooting-and-FAQ"><b>🇬🇧 English</b></a> •
  <a href="Troubleshooting-and-FAQ-TR"><b>🇹🇷 Türkçe</b></a>
</p>

Mac Remote kullanırken karşılaşabileceğiniz en yaygın sorular ve çözümleri:

---

## ❓ Sıkça Sorulan Sorular

### S1: Telefonum Mac'imi otomatik olarak bulamıyor.
**Kontrol Listesi:**
1. **Aynı Wi-Fi Kontrolü:** Mac'inizin ve telefonunuzun **birebir aynı Wi-Fi ağına** bağlı olduğundan emin olun.
2. **Misafir Ağı / AP İzolasyonu:** Halka açık veya otel Wi-Fi ağlarında cihazların birbiriyle konuşmasını engelleyen *AP İzolasyonu* açık olabilir. Bu durumda **WAN Tüneli** modunu kullanın.
3. **macOS Güvenlik Duvarı:**
   - **Sistem Ayarları > Ağ > Güvenlik Duvarı** bölümüne gidin.
   - `Mac Remote.app` için gelen bağlantılara izin verildiğinden emin olun.
4. **Manuel Bağlantı:** Mac'inizin yerel IP adresiyle doğrudan bağlanabilirsiniz:
   - Mac'inizde IP adresinize bakın (örn: `192.168.1.50`).
   - Mobil uygulamada Manuel Bağlantı alanına `ws://192.168.1.50:8765` yazın.

---

### S2: Bağlantı kuruldu ancak imleç hareket etmiyor.
**Sebep:** macOS Erişilebilirlik izni eksik veya pasif kalmış.
**Çözüm:**
1. **Sistem Ayarları > Gizlilik ve Güvenlik > Erişilebilirlik** bölümüne gidin.
2. `Mac Remote` listelenmişse anahtarı **kapatıp tekrar açın**.
3. Listelenmemişse `+` butonuna basarak `/Applications/Mac Remote.app` dosyasını ekleyin.
4. Mac Remote uygulamasını yeniden başlatın (`✓ Erişilebilirlik İzni: Verildi` görünmelidir).

---

### S3: WAN bağlantısı kurulamıyor veya hata veriyor.
**Olası Nedenler:**
1. **Güvenlik Duvarı:** Bulunduğunuz yerel ağ giden TCP tünel portunu (7835) engelliyor olabilir.
2. **Sunucu Bakımı:** Tünel sunucusu kısa süreli bakımda olabilir.
3. **Sunucu Başlatılmadı:** Mac'te "Sunucuyu Başlat" butonuna bastığınızdan ve ekranda port içeren adresin belirdiğinden emin olun.

---

### S4: Verilerim güvende mi? Tuş vuruşlarım kaydediliyor mu?
**Cevap: Kesinlikle güvende.**
- Yerel bağlantılar doğrudan Wi-Fi ağınız üzerinden cihazlar arası gerçekleşir.
- Hiçbir analitik, izleyici veya harici sunucuya veri gönderilmez; tuşlar kaydedilmez.
- WAN tüneli kullanıldığında veriler izole bir ters tünelden akar, sunucuda saklanmaz.
- Tüm kaynak kodları MIT lisansı altında tamamen açıktır.

