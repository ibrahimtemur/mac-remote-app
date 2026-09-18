# 🚀 Mac Remote — iOS App Store Yayınlama Kılavuzu & Kontrol Listesi

Bu kılavuz, **Mac Remote** iOS uygulamasını App Store Connect üzerinden sıfırdan App Store'a göndermek için adım adım takip etmeniz gereken tam rehberdir.

---

## 📋 Genel Bakış: 5 Temel Aşama

1. **Ön Hazırlık & Apple Developer Hesabı**
2. **Xcode'da Takım (Team) ve İmzalama Ayarı**
3. **App Store Connect'te Yeni Uygulama Kaydı Oluşturma**
4. **Xcode ile Uygulama Arşivi (Archive) Alıp App Store Connect'e Yükleme**
5. **Mağaza Bilgileri, Ekran Görüntüleri ve İncelemeye Gönderme (Submit for Review)**

---

## 1. Adım: Ön Hazırlık

- [ ] **Apple Developer Program Üyeliği:** [developer.apple.com](https://developer.apple.com) üzerinde aktif bir bireysel veya kurumsal Apple Developer hesabınızın (yıllık \$99) bulunması gerekir.
- [ ] **Bundle Identifier:** Projemizin tanımlayıcısı:
  `com.ibrahimtemur.macremote.ios` (veya kendi Developer hesabınızdaki ters domain yapınız).
- [ ] **Gizlilik Politikası (Privacy Policy URL):** App Store tüm uygulamalarda gizlilik politikası bağlantısı zorunlu tutar.
  - Projemizin hazır URL'i: `https://github.com/ibrahimtemur/mac-remote/blob/main/docs/wiki/Privacy-Policy.md`

---

## 2. Adım: Xcode'da Takım ve İmzalama (Signing)

1. Xcode'da `ios-app/MacRemote.xcodeproj` projesini açın.
2. Sol gezginden en üstteki **MacRemote** (mavi simge) proje dosyasına tıklayın.
3. **TARGETS** altından **MacRemote**'u seçin.
4. Üst sekmelerden **Signing & Capabilities** sekmesine geçin:
   - **Automatically manage signing** kutucuğunun işaretli olduğundan emin olun.
   - **Team:** Kendi Apple Developer hesabınızı (adınız veya kurumunuz) seçin.
   - **Bundle Identifier:** `com.ibrahimtemur.macremote.ios` (Hesabınızda kayıtlı değilse Xcode otomatik oluşturacaktır).

---

## 3. Adım: App Store Connect'te Uygulama Oluşturma

1. [appstoreconnect.apple.com](https://appstoreconnect.apple.com) adresine giriş yapın.
2. **My Apps (Uygulamalarım)** bölümüne gidin ve sol üstteki **"+" -> New App (Yeni Uygulama)** seçin.
3. Formu doldurun:
   - **Platforms:** iOS seçin.
   - **Name:** `Mac Remote — Kablosuz Trackpad` (veya `Mac Remote`)
   - **Primary Language:** English (U.S.) veya Turkish.
   - **Bundle ID:** Açılır listeden `com.ibrahimtemur.macremote.ios` seçin.
   - **SKU:** Benzersiz bir kod girin (örn: `MACREMOTE-IOS-001`).
   - **User Access:** Full Access.
4. **Create (Oluştur)** butonuna basın.

---

## 4. Adım: Xcode ile Derleme & Yükleme (Archive & Distribute)

1. Xcode üst çubuğundaki cihaz seçiciden simülatör yerine **"Any iOS Device (arm64)"** seçin.
2. Üst menüden: **Product -> Archive** seçeneğine tıklayın.
3. Derleme tamamlandığında **Organizer** penceresi açılacaktır.
4. Arşiv listesinden en son oluşan `Mac Remote` arşivini seçin ve sağdaki **Distribute App** butonuna tıklayın.
5. **App Store Connect** -> **Upload** seçeneğini seçin.
6. Otomatik imzalama (Automatically manage signing) adımlarını onaylayıp **Upload** deyin.
7. Yükleme tamamlandığında ("Upload Successful") App Store Connect arkaplanda ikili dosyayı işleyecektir (5-15 dakika sürer).

---

## 5. Adım: Mağaza Bilgileri & İncelemeye Gönderme

App Store Connect'teki uygulamanızın sayfasına gidin:

### A. Ekran Görüntüleri (Screenshots)
- iPhone için en az bir ekran boyutu zorunludur:
  - **6.9" / 6.7" Display:** iPhone 16 Pro Max / 15 Pro Max ekran görüntüleri (Simülatörden `Cmd + S` ile alınabilir).
  - **6.5" Display:** iPhone 14 Plus / 11 Pro Max (isteğe bağlı).
  - **iPad (13" / 12.9"):** Universal olduğu için iPad Pro simülatöründen alınan görüntüler.

### B. Metinler & Açıklamalar (`docs/app_store/metadata.md` içinden hazır):
- **Promotional Text / Subtitle:** `Mac'inizi Telefonunuzdan Yönetin` / `Control your Mac from your phone`
- **Description:** `docs/app_store/metadata.md` içindeki Türkçe ve İngilizce açıklamayı yapıştırın.
- **Keywords:** `mac remote, trackpad, kablosuz klavye, mac kontrol, presentation clicker, media remote`
- **Support URL:** `https://github.com/ibrahimtemur/mac-remote/issues`
- **Marketing URL:** `https://github.com/ibrahimtemur/mac-remote`

### C. Build (Derleme) Seçimi
- İşleme tamamlandıktan sonra **Build** bölümünden yüklediğiniz `1.2.0 (1)` sürümünü seçin.

### D. App Review Bilgileri (İnceleme Ekibi Notları)
- **Sign-in Required:** Hayır (Hesap gerektirmez).
- **Contact Info:** Adınız, e-postanız ve telefon numaranız.
- **Review Notes:**
  > "Mac Remote discovers a Mac computer running the free companion open-source Mac Remote server over local Wi-Fi via Bonjour. It sends trackpad movements and media commands via WebSocket within the local network. Companion server is available at https://github.com/ibrahimtemur/mac-remote"

### E. Gönderim
- Sağ üstteki **Add for Review** -> **Submit to App Review** butonuna basın.
- Apple incelemesi genellikle 24-48 saat içinde sonuçlanır.
