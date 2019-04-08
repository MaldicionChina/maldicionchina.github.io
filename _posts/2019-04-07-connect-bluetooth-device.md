---
layout: post
title: "[HOWTO] Connect Bluetooth Device to Kubuntu 18.10"
comments: true
description: "For a long time I've been trying to connect my bluetooth HP Roar Speaker to my Computer without any success. Today I'll show you how I fixed this."
keywords: "bluetooth kubuntu kde error not ready rfkill"
---

For a long time I've been trying to connect my bluetooth HP Roar Speaker to my Computer without any success. Today I'll show you how I fixed this.

First, check you can scan bluetooth devices with `bluetoothctl`'s command'.

```
$ bluetoothctl
Agent registered
[bluetooth]# scan on
Failed to start discovery: org.bluez.Error.NotReady
```

If you get the error above, you can follow these steps :D .

* `Failed to start discovery: org.bluez.Error.NotReady` error.

Be sure `bluetooth`'s service is running with:
```
$ systemctl start bluetooth.service
$ systemctl status bluetooth.service
```

```
$ systemctl status bluetooth.service
● bluetooth.service - Bluetooth service
   Loaded: loaded (/lib/systemd/system/bluetooth.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2019-04-07 19:30:15 -05; 46s ago
     Docs: man:bluetoothd(8)
 Main PID: 11354 (bluetoothd)
   Status: "Running"
    Tasks: 1 (limit: 4915)
   Memory: 924.0K
   CGroup: /system.slice/bluetooth.service
           └─11354 /usr/lib/bluetooth/bluetoothd

abr 07 19:30:15 maldicionchina systemd[1]: Starting Bluetooth service...
abr 07 19:30:15 maldicionchina bluetoothd[11354]: Bluetooth daemon 5.50
abr 07 19:30:15 maldicionchina systemd[1]: Started Bluetooth service.
abr 07 19:30:15 maldicionchina bluetoothd[11354]: Starting SDP server
abr 07 19:30:15 maldicionchina bluetoothd[11354]: Bluetooth management interface 1.14 initialized
abr 07 19:30:15 maldicionchina bluetoothd[11354]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DP
abr 07 19:30:15 maldicionchina bluetoothd[11354]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DP
```
If you don't get any error in the last step, you're done. Just go and connect to device using you favorite tool.

* Bluetooth softblocked rfkill problem - `Failed to set mode: Blocked through rfkill (0x12)` error.

```
$ systemctl status bluetooth.service
● bluetooth.service - Bluetooth service
   Loaded: loaded (/lib/systemd/system/bluetooth.service; enabled; vendor preset: enabled)
   Active: active (running) since Sun 2019-04-07 12:27:56 -05; 7h ago
     Docs: man:bluetoothd(8)
 Main PID: 720 (bluetoothd)
   Status: "Running"
    Tasks: 1 (limit: 4915)
   Memory: 2.2M
   CGroup: /system.slice/bluetooth.service
           └─720 /usr/lib/bluetooth/bluetoothd

abr 07 12:27:56 maldicionchina systemd[1]: Started Bluetooth service.
abr 07 12:27:56 maldicionchina bluetoothd[720]: Starting SDP server
abr 07 12:27:57 maldicionchina bluetoothd[720]: Bluetooth management interface 1.14 initialized
abr 07 12:27:58 maldicionchina bluetoothd[720]: Failed to set mode: Blocked through rfkill (0x12)
abr 07 15:20:30 maldicionchina bluetoothd[720]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DPSo
abr 07 15:20:30 maldicionchina bluetoothd[720]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DPSi
abr 07 19:29:03 maldicionchina bluetoothd[720]: Endpoint unregistered: sender=:1.110 path=/MediaEndpoint/A2DP
abr 07 19:29:03 maldicionchina bluetoothd[720]: Endpoint unregistered: sender=:1.110 path=/MediaEndpoint/A2DP
abr 07 19:29:09 maldicionchina bluetoothd[720]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DPSo
abr 07 19:29:09 maldicionchina bluetoothd[720]: Endpoint registered: sender=:1.110 path=/MediaEndpoint/A2DPSi
```

To solve this, first check if your device is softblocked by `rfkill`

```
# Check if your device is blocked by rfkill
$ rfkill list
0: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: no
2: hci0: Bluetooth
        Soft blocked: yes
        Hard blocked: no
# Yes ? Unblocke it with the following command
$ rfkill -r unblock bluetooth
# And restart the service to see the changes
$ systemctl stop bluetooth.service  
$ systemctl start bluetooth.service  
```

References

* [Bluetoothctl error "Failed to start discovery: org.bluez.Error.NotReady"](https://www.reddit.com/r/linux4noobs/comments/6rchm2/bluetoothctl_error_failed_to_start_discovery/)
* [\[solved\] Bluetooth softblocked rfkill problem](https://forum.manjaro.org/t/solved-bluetooth-softblocked-rfkill-problem/52286)
