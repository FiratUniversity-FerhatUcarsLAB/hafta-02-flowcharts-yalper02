İsim - Soy isim:Yiğit Alper Ayhan 
Öğrenci No:250542014

digraph AkilliEvGuvenlikSistemi {
    rankdir=TB;
    fontsize=12;
    node [style=rounded, fontname="Arial"];

    // --- Düğümler ---
    basla [label="BAŞLA", shape=ellipse, style=filled, fillcolor=lightgreen];
    sensor [label="Sensör verilerini oku", shape=parallelogram, style=filled, fillcolor=lightyellow];
    kontrol [label="Tehdit algılandı mı?", shape=diamond, style=filled, fillcolor=lightblue];
    alarm [label="Alarmı çalıştır", shape=box, style=filled, fillcolor=lightcoral];
    bildirim [label="Bildirim gönder", shape=box, style=filled, fillcolor=orange];
    normal [label="Sistem normal çalışıyor", shape=box, style=filled, fillcolor=white];
    bekle [label="1 saniye bekle", shape=box, style=filled, fillcolor=lightgray];

    // --- Akış ---
    basla -> sensor;
    sensor -> kontrol;

    // Evet yolu (tehdit var)
    kontrol -> alarm [label="Evet", color=red];
    alarm -> bildirim;
    bildirim -> bekle;

    // Hayır yolu (tehdit yok)
    kontrol -> normal [label="Hayır", color=green];
    normal -> bekle;

    // Sonsuz döngü (geri dönüş)
    bekle -> sensor [label="Sürekli", color=blue, fontcolor=blue, style=bold];

    // --- Düzenleme ---
    {rank=same; alarm; normal;}
}
