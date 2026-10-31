$b=[byte[]]@(7,27,112,0,100,250); foreach($n in [IO.Ports.SerialPort]::GetPortNames()){ "Testing $n"; try{ $p=New-Object IO.Ports.SerialPort $n,9600; $p.Open(); $p.DtrEnable=$true; $p.RtsEnable=$true; $p.Write($b,0,6); sleep 1; $p.DtrEnable=$false; $p.RtsEnable=$false; $p.Close() }catch{ "  failed: $_" }; sleep 2 }
# SimplePOS

A simple point-of-sale register for one Windows computer. One file, nothing to install.

**[Download SimplePOS.exe](https://github.com/y1wei/simplepos/releases/latest/download/SimplePOS.exe)**

Requires 64-bit Windows 10 or 11. This repository only hosts releases. The source code is private.

## Install

1. Create the folder `C:\SimplePOS` and put `SimplePOS.exe` in it. Do not use `Program Files`.
2. Double-click `SimplePOS.exe`. If SmartScreen appears, choose **More info > Run anyway**.
3. Tap **Admin** on the sign-in screen and set the admin password.
4. In **Settings**, set the shop name and printer. Replace the sample products and employees, and set each product's tax rate: 0%, 9% or 21%.
5. Change the sample employee's PIN. It starts as `1234`.

To start it automatically, put a shortcut in the Startup folder (Win+R, `shell:startup`).

## Printer and cash drawer

The printer must support ESC/POS, as nearly all thermal receipt printers do. The cash drawer plugs into the printer's RJ11 port.

- **Serial**: choose **Serial printer (COM port)**, then the COM port and baud rate. On some POS computers a COM port looks like a network socket, so check the label.
- **USB**: install the printer in Windows first, then choose it in Settings.
- **Network**: enter the printer's IP address.

Set **Printer type** to **Star** for Star printers. Use **Print test page** and **Test drawer** in Settings to check it.

## Reports from another device

Find the register's IP address with `ipconfig`, then open this on any device on the same network:

```
http://<register-ip>:5080/admin
```

## Updates

Open **Admin > Settings > Software update**, then **Check for updates** and **Install update**. Your data is kept. Updates never install by themselves.

## Your data

Everything is in the `data` folder next to the exe, including daily backups. Copy that folder to another drive regularly. To move to a new computer, copy the exe and `data` together.
