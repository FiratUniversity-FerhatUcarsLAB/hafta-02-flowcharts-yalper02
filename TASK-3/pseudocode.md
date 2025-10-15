İsim - Soy isim:Yiğit Alper Ayhan 
Öğrenci No:250542014

BAŞLA

   // --- DEĞİŞKENLERİ TANIMLA ---
   TANIMLA:
      tcNo, sifre, girilenTC, girilenSifre
      kimlikDogrulandi ← YANLIŞ
      islemSecimi
      // Randevu için:
      poliklinikListesi, doktorListesi, saatListesi
      secilenPoliklinik, secilenDoktor, secilenSaat
      randevuOnay ← "H"
      // Tahlil için:
      tahlilVar ← YANLIŞ
      sonucHazir ← YANLIŞ
      indirmeOnay ← "H"

   // --- KİMLİK DOĞRULAMA ---
   YAZ "TC Kimlik Numaranızı Giriniz:"
   OKU girilenTC
   YAZ "Şifrenizi Giriniz:"
   OKU girilenSifre

   EĞER girilenTC = tcNo VE girilenSifre = sifre İSE
        kimlikDogrulandi ← DOĞRU
   DEĞİLSE
        YAZ "Kimlik doğrulama başarısız!"
        DUR
   SON

   // --- ANA MENÜ ---
   EĞER kimlikDogrulandi = DOĞRU İSE
        YAZ "Lütfen yapmak istediğiniz işlemi seçiniz:"
        YAZ "1 - Randevu Al"
        YAZ "2 - Tahlil Sonucu Görüntüle"
        OKU islemSecimi
   SON

   // --- RANDEVU ALMA İŞLEMİ ---
   EĞER islemSecimi = 1 İSE

        YAZ "Poliklinik Listesi:"
        LİSTELE poliklinikListesi
        YAZ "Bir poliklinik seçiniz:"
        OKU secilenPoliklinik

        doktorListesi ← secilenPoliklinik.doktorlar
        YAZ secilenPoliklinik, " için uygun doktorlar:"
        LİSTELE doktorListesi
        YAZ "Bir doktor seçiniz:"
        OKU secilenDoktor

        saatListesi ← secilenDoktor.uygunSaatler
        YAZ secilenDoktor, " için uygun randevu saatleri:"
        LİSTELE saatListesi
        YAZ "Bir saat seçiniz:"
        OKU secilenSaat

        YAZ "Randevunuz: ", secilenPoliklinik, "-", secilenDoktor, "-", secilenSaat
        YAZ "Onaylıyor musunuz? (E/H):"
        OKU randevuOnay

        EĞER randevuOnay = "E" İSE
             YAZ "Randevu kaydediliyor..."
             SMS_GÖNDER("Randevunuz başarıyla oluşturuldu: " + secilenSaat)
             YAZ "Randevu başarıyla oluşturuldu ve SMS gönderildi."
        DEĞİLSE
             YAZ "Randevu iptal edildi."
        SON

   // --- TAHLİL SONUCU GÖRÜNTÜLEME ---
   DEĞİLSE EĞER islemSecimi = 2 İSE

        tahlilVar ← HASTANE_SİSTEMİNDEN_TAHLİL_KONTROL(girilenTC)
        EĞER tahlilVar = YANLIŞ İSE
             YAZ "Sistemde kayıtlı tahlil bulunamadı."
             DUR
        SON

        sonucHazir ← TAHLİL_SONUCU_DURUMU(girilenTC)

        EĞER sonucHazir = DOĞRU İSE
             YAZ "Tahlil sonuçlarınız hazır!"
             GÖRÜNTÜLE_TAHLIL_SONUCU(girilenTC)

             YAZ "Sonuçları PDF olarak indirmek ister misiniz? (E/H):"
             OKU indirmeOnay

             EĞER indirmeOnay = "E" İSE
                  PDF_OLUSTUR_VE_INDIR(girilenTC)
                  YAZ "PDF başarıyla indirildi."
             DEĞİLSE
                  YAZ "PDF indirme işlemi iptal edildi."
             SON

        DEĞİLSE
             YAZ "Tahlil sonuçlarınız henüz hazır değil. Lütfen daha sonra tekrar deneyiniz."
        SON

   // --- GEÇERSİZ SEÇİM DURUMU ---
   DEĞİLSE
        YAZ "Geçersiz seçim yaptınız. Lütfen tekrar deneyiniz."
   SON

BİTİR
