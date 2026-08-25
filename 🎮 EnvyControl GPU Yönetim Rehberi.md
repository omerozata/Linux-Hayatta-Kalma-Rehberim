
**EnvyControl paketini kur**

```bash 
yay -S envycontrol 
```


> [!TIP]
> Mod değiştiren her komuttan sonra sistemin yeniden başlatılması (`reboot`) şarttır.

## 🛠️ Temel Komutlar

```bash
# 1. Şu an hangi ekran kartı modunda olduğunu sorgula
envycontrol -q

# 2. Sadece Nvidia Modu (7/24 Maksimum Performans - Masaüstü Dahil)
sudo envycontrol -s nvidia

# 3. Hibrit Mod (Pil Dostu: Masaüstünü İşlemci Çizer, Oyunlarda Nvidia Açılır)
sudo envycontrol -s hybrid

# 4. Sadece İşlemci Grafiği (Maksimum Pil Tasarrufu: Nvidia Tamamen Kapanır)
sudo envycontrol -s integrated

# 5. Tüm EnvyControl Ayarlarını Sıfırla (Varsayılan Duruma Dön)
sudo envycontrol --reset