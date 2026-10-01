# 🤖 **Leukas Priv Botu**, Discord sunucularına gelişmiş yönetim, moderasyon, eğlence ve kullanıcı takip sistemleri sunan çok fonksiyonlu bir Discord botudur. Discord.js v14 Components V2 mimarisiyle yazılmıştır.

---

## 📋 İçindekiler

- [Kurulum](#kurulum)
- [Yapılandırma](#yapılandırma)
- [Sistemler](#sistemler)
- [Komutlar](#komutlar)
- [Slash Komutları](#slash-komutları)
- [Proje Yapısı](#proje-yapısı)

---

## 🚀 Kurulum

### Gereksinimler
- Node.js v18+
- MongoDB (Atlas veya yerel)

### Adımlar

```bash
# Bağımlılıkları yükle
npm install

# Botu başlat
node leukas.js
```

---

## ⚙️ Yapılandırma

`config.json` dosyasını düzenle:

```json
{
  "token":      "BOT_TOKEN",
  "mongoURI":   "MONGODB_URI",
  "clientId":   "BOT_CLIENT_ID",
  "prefix":     ".",
  "embedColor": "#5865F2",
  "ownerID":    "SUNUCU_KURUCU_ID",
  "botName":    "BOT_İSMİ",
  "cooldown":   5
}
```

| Alan | Açıklama |
|---|---|
| `token` | Discord bot token'ı |
| `mongoURI` | MongoDB bağlantı adresi |
| `clientId` | Bot'un Application ID'si (slash komutlar için) |
| `prefix` | Prefix komutlar için önek |
| `embedColor` | Varsayılan embed rengi |
| `ownerID` | Sunucu kurucusunun ID'si |
| `cooldown` | Komutlar arası bekleme süresi (saniye) |

---

## 🛠️ Sistemler

### 📊 Seviye & XP Sistemi
Üyeler mesaj attıkça ve ses kanalında vakit geçirdikçe XP kazanır. Haftalık/aylık periyotlu istatistikler MongoDB'de tutulur.

### 🎙️ Özel Oda Sistemi
`.özeloda` komutuyla kurulur. Üyeler "Özel Oda Oluştur" sesine girince kişisel ses kanalı otomatik açılır. Kontrol panelinden oda ismi, limit, kilit, gizleme, kişi ekleme/çıkarma ve sahiplik devretme yapılabilir.

### 📋 Log Sistemi
Mesaj, ses, davet ve giriş/çıkış logları ayrı kanallara gönderilir. `.kurulum` komutuyla yapılandırılır.

### 😴 AFK Sistemi
`.afk [sebep]` ile AFK moduna geçilir. Etiketlenince bildirim gönderilir, mesaj atınca otomatik çıkılır.

### 🎵 Spotify Entegrasyonu
Discord Presence üzerinden kullanıcının dinlediği şarkıyı canvas kartıyla gösterir.

---

## 📌 Komutlar

### 👤 Kullanıcı Komutları

| Komut | Açıklama |
|---|---|
| `.afk [sebep]` | AFK modunu açar |
| `.avatar [@kullanıcı]` | Kullanıcının avatarını gösterir |
| `.banner [@kullanıcı]` | Kullanıcının bannerını gösterir |
| `.cihaz [@kullanıcı]` | Aktif cihaz durumunu gösterir |
| `.git @kullanıcı` | Ses kanalına katılma isteği gönderir |
| `.kullanıcı [@kullanıcı]` | Kullanıcı bilgilerini gösterir |
| `.rank [@kullanıcı]` | Seviye kartını gösterir |
| `.spotify [@kullanıcı]` | Spotify'da dinlenen şarkıyı gösterir |
| `.top` | Sunucu sıralama tablosunu gösterir |
| `.yardim` | Yardım menüsünü açar |

### 🎉 Eğlence Komutları

| Komut | Açıklama |
|---|---|
| `.ship [@kullanıcı]` | İki kullanıcı arasındaki uyumu gösterir |
| `.tweet @kullanıcı [metin]` | Sahte tweet görseli oluşturur |

### 🛡️ Moderasyon Komutları

| Komut | Açıklama |
|---|---|
| `.ban @kullanıcı` | Kullanıcıyı banlar (dropdown sebep seçimi) |
| `.unban [id]` | Banlı kullanıcının banını kaldırır |
| `.sil [sayı]` | Belirtilen sayıda mesajı siler |
| `.kilit` | Kanal kilit panelini açar |
| `.yavaşmod [süre]` | Kanalın yavaş mod süresini ayarlar |
| `.yazdır #kanal [metin]` | Bot adına mesaj gönderir |
| `.çek @kullanıcı` | Kullanıcıyı ses kanalına çeker |
| `.say` | Sunucu üye istatistiklerini gösterir |
| `.rol` | Rol yönetim panelini açar |

### ⚙️ Yönetici Komutları

| Komut | Açıklama |
|---|---|
| `.kurulum` | Log kanalları ve bot ayarlarını yapılandırır |
| `.özeloda` | Özel oda sistemini kurar |

---

## ⚡ Slash Komutları

Slash komutlarını Discord'a register etmek için:

```bash
# Belirli bir sunucuya (anında aktif)
node deploy.js SUNUCU_ID

# Global (tüm sunucular, ~1 saat gecikme)
node deploy.js
```

| Slash Komutu | Açıklama |
|---|---|
| `/ban kullanici: sebep:` | Kullanıcıyı banlar |

---

## 📁 Proje Yapısı

```
bot/
├── commands/          # Komut dosyaları
├── events/            # Event handler'ları
│   ├── messageCreate.js
│   ├── voiceStateUpdate.js
│   ├── ozelOdaInteraction.js
│   ├── slashHandler.js
│   ├── davetLog.js
│   ├── guildMemberAdd.js
│   ├── guildMemberRemove.js
│   ├── messageLog.js
│   └── ready.js
├── models/            # MongoDB şemaları
│   ├── Afk.js
│   ├── GuildSettings.js
│   └── Level.js
├── utils/             # Yardımcı fonksiyonlar
│   ├── kartBuilder.js
│   └── periyot.js
├── assets/            # Görseller
├── config.json        # Bot yapılandırması
├── deploy.js          # Slash komut register scripti
├── leukas.js          # Ana giriş noktası
└── package.json
```

---

## 🔧 Teknik Bilgiler

| | |
|---|---|
| **Discord.js** | v14+ (Components V2) |
| **Node.js** | v18+ |
| **Veritabanı** | MongoDB (Mongoose) |
| **Canvas** | @napi-rs/canvas |
| **Prefix** | `.` |
| **Toplam Komut** | 22 |
