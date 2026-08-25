>[!TIP]
>#### Tek satırlık basit bir çözüm ama hayat kurtarıyor. Led ışığı çalışmayan mute tuşunu kendine getiriyor

> [!WARNING]
> Bunun çalışabilmesi için önce ec modülünün yüklenmesi ve yazma izni verilmesi gerekiyor.
> Fan ayarlarını yaparken eklediğimiz için burada tekrar vermiyorum


```bash
# Realtek ALSA ses çipi için Mute LED tanımı
echo "options snd-hda-intel model=alc233-eapd" | sudo tee /etc/modprobe.d/msi-mute-led.conf
```