# mount_and_read_ntfs.sh

This repository provides a shell script to mount NTFS drives with **read and write** access on macOS using **macFUSE** and **ntfs-3g**.

该项目提供一个 Shell 脚本，用于在 macOS 上通过 **macFUSE** 和 **ntfs-3g** 挂载 NTFS 硬盘，并实现**读写访问**。

---

## 📋 Requirements / 系统要求

- macOS 11 (Big Sur) or later
- [Homebrew](https://brew.sh/) installed
- [Xcode Command Line Tools](https://developer.apple.com/xcode/resources/) (`xcode-select --install`)
- [macFUSE](https://osxfuse.github.io/) installed and approved in **System Settings → Privacy \& Security**
- `ntfs-3g-mac` (installed automatically by the script)
- Administrator privileges (sudo)

---

## ⚠️ Disclaimer / 免责声明

This script modifies system-level configurations and installs kernel extensions.
Use at your own risk. Always back up important data before enabling NTFS write support.

该脚本会修改系统配置并安装内核扩展。
请在理解风险的前提下使用。在启用 NTFS 写入支持前，请务必备份重要数据。

---

## 🔧 Installation \& Usage / 安装与使用

### 1. Download the script / 下载脚本

```bash
cd ~/Downloads
curl -o mount_ntfs.sh [https://raw.githubusercontent.com/yorkzap/mount-ntfs-macos-read-write/main/mount_ntfs.sh](https://raw.githubusercontent.com/yorkzap/mount-ntfs-macos-read-write/main/mount_ntfs.sh)
chmod +x mount_ntfs.sh


2. Run the script / 执行脚本
./mount_ntfs.sh

The script will / 脚本将会：


Check dependencies (Homebrew, macFUSE, ntfs-3g)
Install missing components automatically
Detect NTFS drives
Mount with read & write access
Open the drive in Finder



🔑 System Extension Approval / 系统扩展授权


On Apple Silicon (M1/M2/M3) / Apple Silicon (M1/M2/M3):


Shut down your Mac / 关机
Hold the power button → enter Recovery Mode / 按住电源键进入恢复模式
Go to Startup Security Utility → set to Reduced Security / 打开启动安全性实用工具 → 设置为降低安全性
Check Allow user management of kernel extensions / 勾选允许用户管理内核扩展
Restart and approve macFUSE in System Settings → Privacy & Security / 重启并在系统设置 → 隐私与安全性中允许 macFUSE


On Intel Macs / Intel Mac:


Restart and hold Command + R to enter Recovery Mode / 重启并按住 Command + R 进入恢复模式
Open Startup Security Utility → adjust security as above / 打开启动安全性实用工具 → 按上面步骤调整
Restart and approve in System Settings / 重启并在系统设置中允许


✅ Verify Installation / 验证安装
kmutil showloaded | grep fuse

If you see entries related to fuse or osxfuse, macFUSE is active.
如果输出包含 fuse 或 osxfuse，说明 macFUSE 已激活。


🔄 Uninstall Old NTFS Drivers / 清理旧 NTFS 驱动


Conflicting drivers (e.g., Tuxera, Paragon, DragonNTFS) must be removed.
可能的冲突驱动（如 Tuxera、Paragon、DragonNTFS）需要移除。


sudo rm -rf /Library/Filesystems/ufsd_NTFS.fs
sudo rm -rf /Library/Filesystems/dragonNTFS.fs
sudo rm -rf /Library/Filesystems/tuxeraNTFS.fs

Check for leftovers:
检查是否仍有残留：

ls /Library/Filesystems | grep -i ntfs


❓ Troubleshooting / 常见问题


Drive not detected / 硬盘未检测到
→ Check cables, ports, and use Disk Utility to confirm presence / 检查数据线、接口，并使用磁盘工具确认硬盘存在
macFUSE not loaded / macFUSE 未加载
→ Verify with kmutil showloaded | grep fuse. If empty, recheck Recovery Mode settings / 使用 kmutil showloaded | grep fuse 检查，如果无输出，重新确认恢复模式设置
Permission denied / 权限错误
→ Run the script with admin rights (sudo) / 使用管理员权限运行脚本
Multiple NTFS drivers conflict / 驱动冲突
→ Ensure all third-party NTFS drivers are uninstalled / 确保所有第三方 NTFS 驱动已卸载



🔁 Notes / 注意事项


You only need to run the script once per NTFS drive mounting session. / 每次挂载 NTFS 硬盘都需要运行脚本一次
After reboot, drives may need to be mounted again. / 重启后可能需要再次挂载硬盘
Always safely eject NTFS drives to avoid corruption. / 始终安全退出 NTFS 硬盘以避免损坏

下面是已经整理和补全的完整 markdown 项目说明文档，格式规范、层次分明，中英文对照细节齐全：

# mount_and_read_ntfs.sh

这个仓库提供了一个 Shell 脚本，可在 macOS 上通过 **macFUSE** 和 **ntfs-3g** 挂载 NTFS 硬盘，实现**读写访问**。

This repository provides a shell script to mount NTFS drives with **read and write** access on macOS using **macFUSE** and **ntfs-3g**。

***

## 📋 Requirements / 系统要求

- macOS 11 (Big Sur) 或更高版本  
- 已安装 [Homebrew](https://brew.sh/)  
- 已安装 [Xcode Command Line Tools](https://developer.apple.com/xcode/resources/) (`xcode-select --install`)  
- 已安装 [macFUSE](https://osxfuse.github.io/)，并在「系统设置 → 隐私与安全性」中授权  
- `ntfs-3g-mac` （脚本会自动安装）  
- 需有管理员权限（sudo）

***

## ⚠️ Disclaimer / 免责声明

此脚本会修改系统配置并安装内核扩展，存在一定风险。  
请务必先备份重要数据，再启用 NTFS 写入支持。  
This script modifies system-level configurations and installs kernel extensions.  
Use at your own risk. Always back up important data before enabling NTFS write support。

***

## 🔧 Installation & Usage / 安装与使用

### 1. Download the script / 下载脚本

```bash
cd ~/Downloads
curl -o mount_ntfs.sh https://raw.githubusercontent.com/yorkzap/mount-ntfs-macos-read-write/main/mount_ntfs.sh
chmod +x mount_ntfs.sh
```


### 2. Run the script / 执行脚本

```bash
./mount_ntfs.sh
```

脚本会自动检测依赖（Homebrew、macFUSE、ntfs-3g），并自动安装缺失组件。
自动检测 NTFS 硬盘，挂载为读写状态，并自动在 Finder 打开该硬盘。
The script will:

- Check dependencies (Homebrew, macFUSE, ntfs-3g)
- Install missing components automatically
- Detect NTFS drives
- Mount with read \& write access
- Open the drive in Finder

***

### 🔑 System Extension Approval / 系统扩展授权

#### Apple Silicon (M1/M2/M3) 机型：

1. 关机后按住电源键进入恢复模式
2. 进入「启动安全性实用工具」→ 设置为降低安全性
3. 勾选“允许用户管理内核扩展”
4. 重启，并在系统设置 → 隐私与安全性中批准 macFUSE

#### Intel Mac 机型：

1. 重启后按住 Command + R 进入恢复模式
2. 打开「启动安全性实用工具」→ 按上述方式调整安全级别
3. 重启并在系统设置批准 macFUSE

***

### ✅ Verify Installation / 验证安装

```bash
kmutil showloaded | grep fuse
```

如果有 fuse 或 osxfuse 相关条目，即表示 macFUSE 已激活。
If entries related to fuse or osxfuse appear, macFUSE is active。

***

### 🔄 Uninstall Old NTFS Drivers / 清理旧 NTFS 驱动

存在冲突驱动（如 Tuxera、Paragon、DragonNTFS）需卸载。
Conflicting drivers (e.g., Tuxera, Paragon, DragonNTFS) must be removed。

```bash
sudo rm -rf /Library/Filesystems/ufsd_NTFS.fs
sudo rm -rf /Library/Filesystems/dragonNTFS.fs
sudo rm -rf /Library/Filesystems/tuxeraNTFS.fs
```

检查是否有残留文件：
Check for leftovers:

```bash
ls /Library/Filesystems | grep -i ntfs
```


***

### ❓ Troubleshooting / 常见问题

- **硬盘未检测到**
检查数据线、接口，并用磁盘工具确认硬盘存在。
- **macFUSE 未加载**
用 `kmutil showloaded | grep fuse` 检查，无输出则重新设置恢复模式。
- **权限错误**
用管理员权限（sudo）运行脚本。
- **驱动冲突**
确保卸载所有第三方 NTFS 驱动。

***

### 🔁 Notes / 注意事项

- 每次挂载 NTFS 硬盘都需运行一次脚本。
- 重启后可能要重新挂载硬盘。
- 始终安全退出 NTFS 硬盘，避免数据损坏。

***

如需进一步帮助，请参见仓库主页及 macFUSE 官方文档。
