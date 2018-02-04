Package: macchanger

Confirm your current MAC addresses for your interfaces using ```ip link ```.

Create a new file ```/etc/systemd/system/macspoof@.service``` containing:
```
[Unit]
Description=macchanger on %I
Wants=network-pre.target
Before=network-pre.target
After=sys-subsystem-net-devices-%i.device

[Service]
ExecStart=/usr/bin/macchanger -r %I
Type=oneshot

[Install]
WantedBy=multi-user.target
```

Then create a link for each interface that you want to randomize (in this case WLAN0):

```
systemctl enable macspoof@wlan0.service
```

Then reboot and confirm that the MAC address is changing.


Reference: 
https://forums.kali.org/showthread.php?36072-SOLVED-Could-not-change-MAC-amp-Setup-Macchanger-auto-spoofing-randomization-in-Kali