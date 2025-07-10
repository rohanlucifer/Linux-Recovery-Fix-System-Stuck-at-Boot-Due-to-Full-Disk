
🛠️ Linux Recovery: Fix System Stuck at Boot Due to Full Disk

When a Linux system is stuck during boot (e.g., at /dev/sda2: clean ...) and you can't access the desktop or terminal, it's often due to disk space being full. This guide walks through the recovery process using GRUB Recovery Mode.


---

✅ Symptoms
```

System hangs at boot with messages like:

/dev/sda2: clean, 2343053/7782400 files, 29658082/31127296 blocks

Cannot access terminal using Ctrl + Alt + F2

Disk is full; system can't start GUI or shell
```


---

🧭 Steps to Fix
```
1. Boot into Recovery Mode

1. Reboot the system.
```



2. When the GRUB menu appears, select:

```
Advanced options for Ubuntu
```

3. Then choose a kernel with:

```
(recovery mode)

```

4. From the Recovery Menu, select:
```
root - Drop to root shell prompt
```



---

2. Remount Root Filesystem as Read/Write

```
By default, it's mounted as read-only. Run:

mount -o remount,rw /

```


---

3. Clean Up Disk Space

```
🔹 Clean APT cache:

apt clean

🔹 Delete unnecessary logs:

rm -rf /var/log/*.gz
rm -rf /var/log/*.1
rm -rf /var/log/journal/*
rm -rf /var/tmp/*
rm -rf /tmp/*

🔹 Delete user cache (safe):

rm -rf /home/*/.cache

🔹 Optional: Remove large files in Downloads (if needed)

rm -rf /home//Downloads/

```
---

4. (Optional) Find Large Files

If you want to manually find big files:
```
du -ah /home | sort -rh | head -n 20

Or find largest folders by level:

du -h --max-depth=1 /
du -h --max-depth=1 /home

```
---

5. Reboot

After cleaning space:
```
reboot
```

---

✅ System should now boot normally


---

📌 Notes

Removing .cache is completely safe; applications will recreate it.

Avoid deleting files in /boot, /bin, or /etc unless you're absolutely sure.

If you regularly face this issue, consider resizing partitions or setting up monitoring.
