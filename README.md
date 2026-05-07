# Demir Group Gayrimenkul – Kurulum Kılavuzu

## Dosya Yapısı

```
demir-group/
├── index.html       ← Ana site (ziyaretçiler görür)
├── admin.html       ← İlan yönetim paneli (sadece siz)
├── listings.json    ← Tüm ilan verisi (otomatik güncellenir)
└── README.md
```

---

## Adım 1 – GitHub Reposu Oluştur

1. [github.com](https://github.com) → **New repository**
2. Repository name: `demir-group` (veya istediğiniz isim)
3. **Public** seçin (GitHub Pages için gerekli)
4. **Create repository** tıklayın

---

## Adım 2 – Dosyaları Yükle

Repo sayfasında **Add file → Upload files** seçin ve şu dosyaları yükleyin:
- `index.html`
- `admin.html`
- `listings.json`

Commit mesajı yazıp **Commit changes** tıklayın.

---

## Adım 3 – GitHub Pages Aktif Et

1. Repo → **Settings** → sol menüden **Pages**
2. Source: **Deploy from a branch**
3. Branch: **main** → **/ (root)**
4. **Save** tıklayın
5. Birkaç dakika sonra siteniz şu adreste yayında olur:
   ```
   https://KULLANICI_ADINIZ.github.io/demir-group/
   ```

---

## Adım 4 – index.html'i Güncelle

`index.html` dosyasındaki şu satırları bulun ve kendi bilgilerinizle doldurun:

```javascript
const GITHUB_USER = 'KULLANICI_ADINIZ';   // GitHub kullanıcı adınız
const GITHUB_REPO = 'REPO_ADINIZ';        // Repo adı (örn: demir-group)
```

Dosyayı kaydedin ve GitHub'a tekrar yükleyin.

---

## Adım 5 – GitHub Token Alın

Token, admin panelinin `listings.json` dosyasını güncellemesi için gereklidir.

1. GitHub → sağ üst profil → **Settings**
2. Sol altta **Developer settings**
3. **Personal access tokens** → **Tokens (classic)**
4. **Generate new token (classic)**
5. Note: `demir-group-admin`
6. Expiration: **No expiration** (veya 1 year)
7. Scope: ✅ **repo** (sadece bunu işaretleyin)
8. **Generate token** → Kodu kopyalayın ve saklayın!

> ⚠️ Token bir daha gösterilmez. Kopyalayıp güvenli bir yere kaydedin.

---

## Admin Paneline Giriş

Tarayıcıda şu adrese gidin:
```
https://KULLANICI_ADINIZ.github.io/demir-group/admin.html
```

Giriş ekranında doldurun:
- **GitHub Kullanıcı Adı:** github kullanıcı adınız
- **Repo Adı:** demir-group
- **Personal Access Token:** 5. adımda aldığınız token
- **Admin Şifresi:** `demir2025` (ilk giriş, sonra değiştirin!)

---

## Nasıl Çalışır?

```
Ziyaretçi            Admin
    │                   │
    ▼                   ▼
index.html          admin.html
    │                   │
    │ fetch()           │ GitHub API
    ▼                   ▼
listings.json  ←→  listings.json
(GitHub'da)        (GitHub'da)
```

- **Okuma:** `index.html` listings.json'ı raw URL ile okur (token gerekmez)
- **Yazma:** `admin.html` GitHub API ile listings.json'ı günceller (token gerekir)
- Her ilan kaydı otomatik olarak GitHub'a commit atılır
- Versiyon geçmişi GitHub'da saklanır

---

## Güvenlik Notları

- Token'ı kimseyle paylaşmayın
- Admin şifresini ilk girişten sonra değiştirin (Ayarlar menüsünden)
- Token sadece tarayıcı oturumunda saklanır, kapattığınızda temizlenir
- Repo'yu Public yaparken token'ın kod içinde olmadığından emin olun

---

## Özel Domain Bağlama (İsteğe Bağlı)

`www.demirgroupgayrimenkul.com` gibi bir domain varsa:

1. Repo → Settings → Pages → **Custom domain**
2. Domain adresinizi yazın
3. DNS ayarlarında CNAME kaydı ekleyin:
   ```
   www  →  KULLANICI_ADINIZ.github.io
   ```

---

## Sorun Giderme

**İlanlar görünmüyor:**
- `index.html` içindeki `GITHUB_USER` ve `GITHUB_REPO` değerlerini kontrol edin
- Repo'nun Public olduğunu kontrol edin
- `listings.json` dosyasının repoda olduğunu kontrol edin

**Kayıt edilemiyor:**
- Token'ın `repo` yetkisine sahip olduğunu kontrol edin
- Token'ın süresinin dolmadığını kontrol edin
- Kullanıcı adı ve repo adının doğru yazıldığını kontrol edin
