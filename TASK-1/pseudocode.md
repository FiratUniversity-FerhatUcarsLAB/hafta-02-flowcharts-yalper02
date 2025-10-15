İsim - Soy isim:Yiğit Alper Ayhan
Öğrenci No:250542014

BAŞLA

   TANIMLA:
      doğruPIN ← 1234
      bakiye ← 10000
      günlükLimit ← 5000
      kalanHak ← 3
      çekilenToplam ← 0
      işlemTekrarı ← "E"

   // --- PIN DOĞRULAMA ---
   DÖNGÜ kalanHak > 0 VE işlemTekrarı = "E" İKEN

      YAZ "Lütfen PIN'inizi giriniz:"
      OKU girilenPIN

      EĞER girilenPIN = doğruPIN İSE
         YAZ "PIN doğrulandı."

         // --- PARA ÇEKME İŞLEMİ ---
         TEKRARLA

            YAZ "Çekmek istediğiniz tutarı giriniz:"
            OKU tutar

            // --- TUTAR KONTROLÜ ---
            EĞER tutar MOD 20 ≠ 0 İSE
               YAZ "HATA: Tutar 20 TL'nin katı olmalıdır."
            
            DEĞİLSE EĞER tutar > bakiye İSE
               YAZ "HATA: Yetersiz bakiye."
            
            DEĞİLSE EĞER (çekilenToplam + tutar) > günlükLimit İSE
               YAZ "HATA: Günlük çekim limitiniz (", günlükLimit, " TL) aşıldı."
            
            DEĞİLSE
               bakiye ← bakiye - tutar
               çekilenToplam ← çekilenToplam + tutar
               YAZ "İşlem başarılı. ", tutar, " TL çekildi."
               YAZ "Kalan bakiye: ", bakiye, " TL"
               YAZ "Bugün toplam çekilen: ", çekilenToplam, " TL"
            BİTİR_EĞER

            YAZ "Başka bir işlem yapmak ister misiniz? (E/H):"
            OKU işlemTekrarı

         // TEKRARLA sonu
         TA ki işlemTekrarı = "H" OLSUN

         YAZ "Kartınızı almayı unutmayınız."
         ÇIKIŞ_YAP
         DUR

      DEĞİLSE
         kalanHak ← kalanHak - 1
         EĞER kalanHak > 0 İSE
            YAZ "Hatalı PIN. Kalan deneme hakkı: ", kalanHak
         DEĞİLSE
            YAZ "3 kez hatalı giriş yaptınız. Kartınız bloke edilmiştir."
            DUR
         BİTİR_EĞER
      BİTİR_EĞER

   BİTİR_DÖNGÜ

BİTİR  
