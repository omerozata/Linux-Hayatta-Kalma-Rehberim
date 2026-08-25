> [!NOTE]
> MSI Katana laptopta fan kontrolünü elle (custom eğri) yönetebilmek için uyguladığımız yöntem.

**EC (Embedded Controller) sürücüsünü kur:**

```bash
yay -S msi-ec-dkms-git
```

**EC'ye yazma izni ver:**

```bash
echo "options ec_sys write_support=1" | sudo tee /etc/modprobe.d/mcontrolcenter.conf
echo "ec_sys" | sudo tee /etc/modules-load.d/ec_sys.conf
```


> [!TIP]
> Değişikliklerin aktif olması için sistemi yeniden başlat. Restart atmak istemiyorsan aşağıdaki komut da aynı işi görür:
> 
> ```bash
> sudo modprobe ec_sys
> ```

**Fan kontrol aracını (isw) kur:**

```bash
yay -S isw
```

**Kendi laptop modelini listeden bul:**

```bash
grep -E "^\s*\[" /etc/isw.conf
```

> [!WARNING]
> Listede birebir model adın olmayabilir; bu durumda donanımına en yakın MSI EC profilini seçmen gerekir. Bu örnekte seçilen profil `16K5EMS1`.

**Servisi seçilen profille etkinleştir:**

```bash
sudo systemctl enable --now isw@16K5EMS1
```

**Servisin çalıştığını doğrula:**

```bash
sudo systemctl status isw@16K5EMS1
```

**Fan eğrisini düzenlemek için konfigürasyon dosyasını aç:**

```bash
sudo nano /etc/isw.conf
```

> [!TIP]
> Dosya içinde `16K5EMS1` profilini bul ve aşağıdaki gibi sıcaklık/fan hızı eğrisini kendine göre ayarla.

```TOML
[16K5EMS1]
# GS63_8RE
# 16K5EMS1.104
address_profile = MSI_ADDRESS_DEFAULT
fan_mode = 140
# CPU
cpu_temp_0 = 45
cpu_temp_1 = 55
cpu_temp_2 = 65
cpu_temp_3 = 75
cpu_temp_4 = 80
cpu_temp_5 = 90
cpu_fan_speed_0 = 5
cpu_fan_speed_1 = 10
cpu_fan_speed_2 = 20
cpu_fan_speed_3 = 40
cpu_fan_speed_4 = 60
cpu_fan_speed_5 = 80
cpu_fan_speed_6 = 85
# GPU
gpu_temp_0 = 45
gpu_temp_1 = 55
gpu_temp_2 = 65
gpu_temp_3 = 75
gpu_temp_4 = 80
gpu_temp_5 = 90
gpu_fan_speed_0 = 3
gpu_fan_speed_1 = 10
gpu_fan_speed_2 = 20
gpu_fan_speed_3 = 40
gpu_fan_speed_4 = 60
gpu_fan_speed_5 = 80
gpu_fan_speed_6 = 85
```