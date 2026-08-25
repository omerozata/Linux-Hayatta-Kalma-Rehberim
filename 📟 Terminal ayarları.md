## Ghostty Config

```bash
keybind = ctrl+c=copy_to_clipboard
keybind = ctrl+v=paste_from_clipboard

keybind = ctrl+shift+c=text:\x03

theme = TokyoNight
font-family = "JetBrains Mono"
```

---

## Terminal Kullanıcı@Makine Adı Rengini Değiştirme

**Dosyayı aç:**

```bash
nano ~/.bashrc
```

**Şu satırı bul:**

```bash
PS1='[\u@\h \W]\$ '
```

**Tamamen silip yerine şunu yaz:**

```bash
PS1='[\[\e[1;32m\]\u@\h\[\e[0m\] \W]\$ '
```

> Kaydet ve çık: `Ctrl+O` → `Enter` → `Ctrl+X`

**Değişikliğin hemen etkili olması için:**
```bash
source ~/.bashrc
```

Sadece kullanıcı@makine adı değil, köşeli parantezler dahil tamamının renkli olmasını istersen:

```bash
PS1='[\[\e[1;32m\]\u@\h \W\[\e[0m\]]\$ '
```

Farklı bir renk istersen kod kısmındaki (`1;32m`) sayıyı aşağıdaki tablodan seçtiğin renkle değiştir.

| Renk | Kod |
|---|---|
| Kırmızı | `1;31m` |
| Yeşil | `1;32m` |
| Sarı | `1;33m` |
| Mavi | `1;34m` |
| Mor | `1;35m` |
| Cyan | `1;36m` |
