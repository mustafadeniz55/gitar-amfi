# Gitar Amfi (Android)

Telefonun mikrofonundan aldığı enstrüman sesini amfi simülasyonundan geçirip kulaklığa veren uygulama.

## Çalıştırma
1. Android Studio (Koala veya üstü) ile bu klasörü aç, Gradle senkronizasyonunu bekle.
2. Gerçek bir telefona kur (emülatörde mikrofon/gecikme sağlıklı çalışmaz).
3. Kulaklığı tak, uygulamayı aç, mikrofon iznini ver, **Başlat**'a bas.

## Ses zinciri
Mikrofon → DC filtre → giriş kazancı → noise gate → 80 Hz HPF → preamp (tanh) →
(Lead: 2. kademe) → fizz LPF → Bass/Mid/Treble → kabin simülasyonu → reverb → master → limiter

## Dosyalar
- `AmpEngine.kt` – AudioRecord/AudioTrack döngüsü ve tüm DSP
- `Biquad.kt` – EQ ve kabin filtreleri
- `Reverb.kt` – hafif reverb
- `MainActivity.kt` – arayüz (sürgüler, model seçimi, giriş ölçeri)

## Bilinen sınırlar
- Gecikme cihaza göre yaklaşık 40–100 ms olur. 10–20 ms için Oboe (C++) gerekir.
- Arka planda çalışmaz (Android mikrofonu sessize alır); foreground service eklenebilir.
- Distorsiyonda oversampling yok; yüksek gain'de hafif aliasing olabilir.
