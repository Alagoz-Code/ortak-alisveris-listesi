# Bizim Liste

İki kişinin ortak kullanacağı, Android için online senkronize alışveriş listesi.

## Özellikler

- Üyelik / kullanıcı hesabı yok.
- İki telefon aynı ortak listeyi kullanır.
- Ürün ekleme, tamamlama ve silme.
- Gerçek zamanlı senkronizasyon.
- İnternet yokken son liste cihazda görünür.
- İnternet geri geldiğinde değişiklikler senkronize edilir.
- Uygulama adı: Bizim Liste.

## Gereken tek harici servis

Supabase ücretsiz bir proje gerekiyor. Uygulama kullanıcılarından üyelik istemez; Supabase sadece arka plandaki veritabanı ve realtime senkronizasyon içindir.

### 1. Supabase projesi

Supabase'te yeni bir proje oluşturun.

### 2. SQL'i çalıştırın

`supabase/schema.sql` dosyasındaki SQL'in tamamını Supabase SQL Editor'da çalıştırın.

### 3. Uygulama ayarları

`lib/app_config.dart` dosyasını açın:

```dart
class AppConfig {
  static const supabaseUrl = 'BURAYA_SUPABASE_URL';
  static const supabaseAnonKey = 'BURAYA_SUPABASE_PUBLISHABLE_KEY';
  static const listId = '00000000-0000-0000-0000-000000000001';
}
```

Supabase Dashboard > Connect bölümündeki URL ve publishable/anon key değerlerini girin.

> Service role key'i kesinlikle uygulamaya koymayın.

### 4. Çalıştırma

```bash
flutter pub get
flutter run
```

APK:

```bash
flutter build apk --release
```

APK şu konumda oluşur:

`build/app/outputs/flutter-apk/app-release.apk`

## GitHub Actions

`.github/workflows/build-apk.yml` dosyası GitHub üzerinde APK üretir.

GitHub repository Settings > Secrets and variables > Actions bölümüne:

- `SUPABASE_URL`
- `SUPABASE_ANON_KEY`

secret'larını ekleyin.

Workflow bu değerleri derleme sırasında `--dart-define` ile uygulamaya aktarır.

## Güvenlik

Bu uygulama hesap sistemi kullanmaz. İki kişilik özel kullanım için tasarlanmıştır.

Supabase tarafındaki RLS, sadece uygulamanın kullandığı sabit liste kimliğine erişime izin verir. Public GitHub repository kullanıyorsanız Supabase publishable/anon key'in gizli olmadığını unutmayın; asıl güvenlik RLS politikalarıdır.

Daha güçlü gizlilik istenirse ikinci sürümde cihaz bazlı davet kodu / şifreli liste erişimi eklenebilir.
