# Resizing a VirtualBox VDI on Windows (Command-Line Only)

This guide shows how to back up, resize, and reattach a VirtualBox VDI disk **entirely via the command line** on Windows.

---

## 1️⃣ Add `VBoxManage` to your PATH
> So you can run VBoxManage from any terminal (only needed once).

```powershell
# For the current user (no admin required)
setx PATH "$($env:PATH);C:\Program Files\Oracle\VirtualBox"

# --- or ---
# System-wide (requires Administrator PowerShell)
setx /M PATH "$($env:PATH);C:\Program Files\Oracle\VirtualBox"

# Open a **new** terminal to refresh PATH
VBoxManage -v   # should print VirtualBox version
```

---

## 2️⃣ Back up the VDI

```powershell
Copy-Item "C:\Users\Ricky\VirtualBox VMs\Ubuntu\Ubuntu.vdi" `
          "C:\Users\Ricky\VirtualBox VMs\Ubuntu\Ubuntu-backup.vdi"
```

> Always make a backup before resizing.

---

## 3️⃣ Detach the disk from the VM
> The VM must be **powered off** (not saved state).

```powershell
# List all VMs
VBoxManage list vms

# Show controller/port info
VBoxManage showvminfo "Ubuntu"

# Detach the disk
VBoxManage storageattach "Ubuntu" `
  --storagectl "SATA" `
  --port 0 `
  --device 0 `
  --type hdd `
  --medium none
```

---

## 4️⃣ Resize the VDI

```powershell
# Size is in MB (example: 20480 = 20 GB)
VBoxManage modifymedium "C:\Users\Ricky\VirtualBox VMs\Ubuntu\Ubuntu.vdi" --resize 20480
```

---

## 5️⃣ Reattach the disk

```powershell
VBoxManage storageattach "Ubuntu" `
  --storagectl "SATA" `
  --port 0 `
  --device 0 `
  --type hdd `
  --medium "C:\Users\Ricky\VirtualBox VMs\Ubuntu\Ubuntu.vdi"
```

---

## 6️⃣ Grow the partition inside the guest OS

- **Linux guest**

```bash
sudo growpart /dev/sda 1   # adjust device if needed
sudo resize2fs /dev/sda1
```

- **Windows guest**

> Use **Disk Management** → right-click the volume → **Extend Volume**.

---

### 📌 Full Flow Summary

1. Add VirtualBox folder to PATH → open new shell → `VBoxManage -v`.
2. Back up the `.vdi`.
3. Power off VM → detach disk (`storageattach … --medium none`).
4. Resize (`modifymedium … --resize <MB>`).
5. Reattach (`storageattach … --medium <vdi>`).
6. Start VM and extend the partition inside the guest.

---

✅ **Tip:** If the guest still shows the old size, verify that you reattached the correct VDI and that the partition was extended properly.