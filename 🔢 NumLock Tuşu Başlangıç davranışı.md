> [!NOTE] 
> NumLock tuşu sistem boot edilirken otomatik olarak kapatılıyordu. Ben ise açık olmasını istiyordum. İşte bunun çözümü:

##### **İlk olarak KDE Plasma için varsayılan ayarı değiştir:**

```bash
kwriteconfig6 --file kcminputrc --group Keyboard --key NumLock 0
```

##### **İkinci olarak şifre ekranı için varsayılan ayarı değiştir:**

```bash
sudo mkdir -p /root/.config sudo kwriteconfig6 --file /root/.config/kcminputrc --group Keyboard --key NumLock 0
```

##### **Üçüncü olarak da geçişlerde handoff problemi olmaması için işletim sistemindeki bu işten sorumlu elemana talimat ver:**

Scripti oluştur:

```bash
sudo bash -c 'cat > /usr/local/bin/numlock-vt << "EOF"
#!/bin/bash
for tty in /dev/tty{1..6}; do
    /usr/bin/setleds -D +num < "$tty" 2>/dev/null
done
EOF'
```

Scripti çalıştırılabilir yap:

```bash
sudo chmod +x /usr/local/bin/numlock-vt
```

Bu emri çekirdeğe işleyecek systemd servisini yaz:

```bash
sudo bash -c 'cat > /etc/systemd/system/numlock-tty.service << "EOF"
[Unit]
Description=Set NumLock Default on Kernel VTs
DefaultDependencies=no
After=local-fs.target
Before=sysinit.target display-manager.service

[Service]
Type=oneshot
ExecStart=/usr/local/bin/numlock-vt
RemainAfterExit=yes

[Install]
WantedBy=sysinit.target
EOF'
```

Servisi aktifleştir:

```bash
sudo systemctl enable numlock-tty.service
```

> [!TIP]
> Artık emirlerine itaat edip NumLock tuşunu otomatik açan bir sistem var



