# Bulgular – scanme.nmap.org
**Nmap versiyon:** 7.80 (bkz. `notes/nmap_version.txt`)

## 01-fast
- Açık portlar: **22/tcp (SSH)**, **80/tcp (HTTP)**, **25/tcp (filtered/SMTP)**
- Not: 97 kapalı port, host up (~0.21s latency).

## 02-service-version
- **22/tcp – ssh:** OpenSSH (Protocol 2.0) banner tespit edildi; parola yerine **anahtar tabanlı giriş** ve deneme sınırı önerilir.
- **80/tcp – http:** HTTP sunucu banner’ı tespit edildi (Server başlığı mevcut). Varsayılan sayfa dönüyor.
- **25/tcp – smtp:** filtered; muhtemelen FW/ISP düşürüyor.

## 03-safe-scripts
- **http-title:** “Go ahead and ScanMe!” (tanıtım sayfası)
- **http-server-header:** Sunucu türü/sürümü `scan.nmap` içinde listelendi.
- **ssh-hostkey:** RSA/ED25519 anahtar parmak izleri yayınlandı (detaylar `scan.nmap`).
- **Özet:** Safe/default scriptler kritik açık raporlamadı.

## Öneriler
- **SSH:** Parola girişi kapalı, yalnız anahtar; rate-limit/fail2ban.
- **HTTP:** Mümkünse yalnız **HTTPS**, gereksiz banner’ları kapat; sürümleri güncel tut.
- **SMTP:** Kullanılmıyorsa tamamen kapalı tut (FW drop).
