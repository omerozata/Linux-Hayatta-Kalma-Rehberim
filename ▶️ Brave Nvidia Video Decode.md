
> [!NOTE] 
> Nvidia ile Chromium arasındaki husumeti çözmek ve tarayıcıda izlenen videolarda ekran kartının kullanılmasını sağlamak için uyguladığımız yöntem


**Nvidia VA-API köprüsünü ve Brave'i kur:**

```bash
sudo pacman -S libva-nvidia-driver
yay -S brave-bin
```

**VA-API ortam değişkenlerini ayarla:**

```bash
mkdir -p ~/.config/environment.d
cat << 'EOF' > ~/.config/environment.d/nvdec.conf
LIBVA_DRIVER_NAME=nvidia
NVD_BACKEND=direct
EOF
```

**Brave'e gerekli flag'leri tanımla:**

```bash
cat << 'EOF' > ~/.config/brave-flags.conf
--ignore-gpu-blocklist
--enable-features=VaapiVideoDecoder,VaapiOnNvidiaGPUs
--enable-gpu-rasterization
--enable-zero-copy
EOF
```


> [!TIP]
> ### Test
> Terminalde bu komutu çalıştır
> 
> ```bash
> nvidia-smi dmon -s u 
> ```
> 

> Video oynatırken `dec` sütunundaki değer artıyorsa donanımsal decode aktif demektir.

> [!WARNING]
>  YouTube'da AV1 formatı bu köprüyü desteklemediği için decode'u engelleyebilir; bu durumda **enhanced-h264ify** eklentisiyle AV1'i devre dışı bırakıp desteklenen formatlara zorlamak gerekebilir.


