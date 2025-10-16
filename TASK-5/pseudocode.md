İsim - Soy isim:Yiğit Alper Ayhan 
Öğrenci No:250542014

BAŞLA

TANIMLA sistemDurumu ← "AKTİF"

DÖNGÜ sistemDurumu = "AKTİF" İKEN

    // 1. Sensör verilerini oku
    sensörVerisi ← SensörOku()

    // 2. Tehdit algıla
    EĞER sensörVerisi.tehditVar = EVET İSE

        // 3. Alarmı çalıştır
        AlarmÇalıştır()

        // 4. Bildirim gönder
        BildirimGönder("Tehdit algılandı! Alarm devrede!")

    DEĞİLSE
        YAZ "Sistem normal çalışıyor."

    BİTİR_EĞER

    // 5. Kısa süre bekle (örnek: 1 saniye)
    BEKLE(1 saniye)

DÖNGÜSONU

BİTİR
