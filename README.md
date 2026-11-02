🕒 Windows & macOS Dual-Boot Time Fix

Fix the incorrect Windows clock that can occur when dual-booting Windows and macOS on the same PC.

🔍 The Problem

When Windows and macOS are installed on the same computer, you may notice that the time in Windows is several hours ahead or behind after booting from macOS.

This happens because the two operating systems normally interpret the computer’s hardware clock (RTC) differently:

* macOS treats the hardware clock as UTC
* Windows normally treats the hardware clock as local time

When switching between the two operating systems, this difference can cause Windows to display the wrong time.

✅ The Fix

Windows supports a registry setting called:

RealTimeIsUniversal

Enabling it tells Windows to treat the hardware clock as UTC, just like macOS.

Supported Windows Versions

* Windows 11
* Windows 10

🛠️ Installation

Option 1 — Create a Registry File

1. Open Notepad.
2. Copy the following code:

```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
"RealTimeIsUniversal"=dword:00000001
```

3. Click File → Save As.
4. Set Save as type to All Files.
5. Name the file:

```
Windows-UTC-Time.reg
```

6. Double-click the .reg file.
7. Approve the Windows Registry/UAC prompts.
8. Restart Windows.

That’s it! Windows and macOS should now agree on how the hardware clock is stored.

⚙️ Windows Settings

After applying the fix, make sure Windows has the correct time zone configured.

Go to:

Settings → Time & language → Date & time

Make sure:

* Set time automatically is enabled
* Your Time zone is correct

You do not need to set your Windows time zone to UTC. Windows will convert the UTC hardware clock to your local time automatically.

↩️ Undo the Fix

If you want Windows to return to its default hardware-clock behavior, create another .reg file containing:

Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
"RealTimeIsUniversal"=-

Save it as:

Undo-Windows-UTC-Time.reg

Run the file and restart Windows.

💡 How It Works

Your computer has a hardware Real-Time Clock (RTC) that continues keeping time even when the computer is turned off.

The problem isn’t that either operating system has the wrong time. The problem is that Windows and macOS normally make different assumptions about what the RTC represents.

Without the fix:

Hardware Clock
     │
     ├── macOS   → interprets RTC as UTC
     │
     └── Windows → interprets RTC as local time

With RealTimeIsUniversal enabled:

Hardware Clock (UTC)
     │
     ├── macOS   → UTC → Local Time
     │
     └── Windows → UTC → Local Time

Both operating systems now use the same convention.

⚠️ Important

Editing the Windows Registry incorrectly can cause system problems. This tweak only changes how Windows interprets the hardware clock, but you should still make sure you understand the change before applying it.

📜 Registry Setting

Setting	Value
Registry Key	HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation
Value Name	RealTimeIsUniversal
Type	REG_DWORD
Value	1

⸻

⭐ Found this useful?

If this fixed your Windows/macOS dual-boot clock problem, consider starring the repository so other dual-boot users can find it.