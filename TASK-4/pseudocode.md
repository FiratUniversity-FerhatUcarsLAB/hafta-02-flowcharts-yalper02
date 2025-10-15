İsim - Soy isim:Yiğit Alper Ayhan
Öğrenci No:250542014

BAŞLA

   TANIMLA:
      maxKredi ← 30
      toplamKredi ← 0
      secilenDersler ← BOŞ_LİSTE
      dersListesi ← SISTEMDEN_AL()
      dersSayisi ← UZUNLUK(dersListesi)

   // --- GİRİŞ AŞAMASI ---
   YAZ "Öğrenci numaranızı girin:"
   oku ogrNo
   YAZ "Şifrenizi girin:"
   oku sifre

   EĞER KIMLIK_DOGRULA(ogrNo, sifre) = DOĞRU İSE
      YAZ "Giriş başarılı. Ders listesi yükleniyor..."
   DEĞİLSE
      YAZ "Kimlik doğrulama başarısız!"
      DUR
   SON

   // --- DERS LİSTESİ GÖSTERME ---
   YAZ "Alınabilecek dersler:"
   DÖNGÜ i ← 1'DEN dersSayisi'NE
      YAZ dersListesi[i].kod, dersListesi[i].ad, " (", dersListesi[i].kredi, " kredi)"
   SON

   // --- DERS SEÇİMİ ---
   cevap ← "E"
   DÖNGÜ cevap = "E" VE toplamKredi < maxKredi İKEN
      YAZ "Seçmek istediğiniz ders kodunu girin:"
      oku dersKod
      ders ← DERS_BUL(dersListesi, dersKod)

      EĞER ders VAR İSE
         // --- KONTENJAN KONTROLÜ ---
         EĞER ders.kontenjan > 0 İSE
            // --- ÖN KOŞUL KONTROLÜ ---
            EĞER ders.onKosul = YOK VEYA ONKOSUL_GECILDI_MI(ogrNo, ders.onKosul) = DOĞRU İSE
               // --- ZAMAN ÇAKIŞMASI KONTROLÜ ---
               EĞER ZAMAN_CAKISMASI_YOK(secilenDersler, ders) = DOĞRU İSE
                  // --- KREDİ LİMİTİ KONTROLÜ ---
                  EĞER toplamKredi + ders.kredi ≤ maxKredi İSE
                     // TÜM KONTROLLER GEÇİLDİ
                     EKLE(secilenDersler, ders)
                     toplamKredi ← toplamKredi + ders.kredi
                     ders.kontenjan ← ders.kontenjan - 1
                     YAZ "Ders başarıyla eklendi:", ders.ad
                  DEĞİLSE
                     YAZ "Toplam kredi limiti aşıldı! (", toplamKredi, "/", maxKredi, ")"
                  SON
               DEĞİLSE
                  YAZ "Zaman çakışması tespit edildi!"
               SON
            DEĞİLSE
               YAZ "Ön koşul dersi tamamlanmamış:", ders.onKosul
            SON
         DEĞİLSE
            YAZ "Kontenjan dolu:", ders.ad
         SON
      DEĞİLSE
         YAZ "Girilen ders kodu geçersiz!"
      SON

      YAZ "Başka ders eklemek ister misiniz? (E/H)"
      oku cevap
   SON

   // --- DERS SEÇİMİ TAMAMLANDI ---
   YAZ "Toplam seçilen ders sayısı:", UZUNLUK(secilenDersler)
   YAZ "Toplam kredi:", toplamKredi

   // --- DANIŞMAN ONAYI ---
   EĞER UZUNLUK(secilenDersler) > 0 İSE
      YAZ "Ders listesi danışmana gönderiliyor..."
      EĞER DANIŞMAN_ONAYI(ogrNo, secilenDersler) = ONAY İSE
         YAZ "Danışman onayı alındı. Kayıt tamamlandı."
      DEĞİLSE
         YAZ "Danışman onayı reddedildi. Lütfen derslerinizi düzenleyin."
      SON
   DEĞİLSE
      YAZ "Hiç ders seçilmedi. Kayıt tamamlanmadı."
   SON

BİTİR
