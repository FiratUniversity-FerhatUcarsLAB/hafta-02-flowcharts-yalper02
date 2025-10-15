İsim - Soy isim:Yiğit Alper Ayhan
Öğrenci No:250542014

BAŞLA

   // --- KULLANICI GİRİŞİ ---
   YAZ "Kullanıcı adı giriniz:"
   OKU kullanıcıAdı
   YAZ "Şifre giriniz:"
   OKU sifre

   EĞER kullanıcıAdı = "admin" VE sifre = "1234" İSE
        YAZ "Giriş başarılı!"
   DEĞİLSE
        YAZ "Hatalı giriş! Program sonlandırılıyor."
        BİTİR
   SON

   // --- SEPET OLUŞTURMA ---
   TANIMLA sepet ← BOŞ
   TANIMLA toplamTutar ← 0
   TANIMLA devamEt ← "E"

   DÖNGÜ devamEt = "E" İKEN
        YAZ "Ürün adı giriniz:"
        OKU ürünAdı
        YAZ "Ürün fiyatını giriniz:"
        OKU ürünFiyat
        YAZ "Stokta var mı? (E/H)"
        OKU stokDurumu

        EĞER stokDurumu = "E" İSE
             SEPETE_EKLE(ürünAdı)
             toplamTutar ← toplamTutar + ürünFiyat
             YAZ "Ürün sepete eklendi."
        DEĞİLSE
             YAZ "Ürün stokta yok!"
        SON

        YAZ "Başka ürün eklemek ister misiniz? (E/H)"
        OKU devamEt
   SON

   // --- İNDİRİM KODU KONTROLÜ ---
   YAZ "İndirim kodunuz var mı? (E/H)"
   OKU kodDurumu

   EĞER kodDurumu = "E" İSE
        YAZ "İndirim kodunu giriniz:"
        OKU indirimKodu
        EĞER indirimKodu = "INDIRIM10" İSE
             toplamTutar ← toplamTutar * 0.9
             YAZ "İndirim uygulandı! Yeni toplam: ", toplamTutar
        DEĞİLSE
             YAZ "Geçersiz indirim kodu!"
        SON
   SON

   // --- KARGO HESAPLAMA ---
   EĞER toplamTutar > 500 İSE
        kargoÜcreti ← 0
        YAZ "500 TL üzeri alışverişlerde kargo ücretsiz!"
   DEĞİLSE
        kargoÜcreti ← 50
        toplamTutar ← toplamTutar + kargoÜcreti
        YAZ "Kargo ücreti eklendi. Yeni toplam: ", toplamTutar
   SON

   // --- ÖDEME AŞAMASI ---
   YAZ "Ödeme yöntemi seçiniz (1-Kredi Kartı / 2-Havale):"
   OKU ödemeYöntemi

   EĞER ödemeYöntemi = 1 İSE
        YAZ "Kart bilgilerinizi giriniz..."
        YAZ "Ödeme başarılı!"
   DEĞİLSE EĞER ödemeYöntemi = 2 İSE
        YAZ "Havale bilgileri e-posta ile gönderildi."
   DEĞİLSE
        YAZ "Geçersiz seçim!"
        BİTİR
   SON

   YAZ "Siparişiniz alınmıştır. Teşekkür ederiz!"

BİTİR
