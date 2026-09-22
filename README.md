# Personel Bildirim — yayınlar

Bu depo [Personel Bildirim](https://personel.maliofis.tr) uygulamasının kurulum paketlerini ve
otomatik güncelleme bilgisini barındırır. **Kaynak kod burada değildir.**

## Otomatik güncelleme

Kurulu uygulamalar ofis panelindeki **Sürüm** ekranından `latest.json` dosyasını okur:

```json
{
  "surum": "1.0.0",
  "dosya": "personel-bildirim-1.0.0.tar.gz",
  "sha256": "…64 hane…",
  "url": "https://github.com/yasinmutlu1878/personel-bildirim-releases/releases/download/v1.0.0/personel-bildirim-1.0.0.tar.gz",
  "notlar": "Sürüm notları",
  "yayinTarihi": "2026-09-22"
}
```

Uygulama paketi indirir, SHA-256 özetini doğrular ve NAS'taki yardımcı konteynere kurulum isteği
bırakır. Kurulum başarısız olursa önceki sürüme geri dönülür.

## Yayın akışı

Sürümler kaynak depodaki `yayinla.ps1` betiğiyle üretilir:

```powershell
.\yayinla.ps1 -Yayinla -Notlar "Değişiklik özeti"
```

Betik imajı derler, `personel-bildirim-<sürüm>.tar.gz` arşivini oluşturur, bu depoda sürüm açar ve
`latest.json` dosyasını günceller.

## Paketler

Her sürüm arşivi, uygulamanın çalışması için gereken her şeyi içeren tek bir Docker imajıdır
(`docker load` ile yüklenir). Veritabanı şeması güncellemeleri uygulama açılırken otomatik uygulanır.
