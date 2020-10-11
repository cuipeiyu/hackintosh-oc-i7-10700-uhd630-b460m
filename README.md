# hackintosh-oc-i7-10700-uhd630-b460m
 Hackintosh EFI Opencore

## 硬件清单

- Intel Core i7-10700 @ 2.90GHz
  - Comet Lake
  - 8C/16T
- Gigabyte B460M AORUS ELITE
  - Intel UHD Graphics 630 128MB
- Kingston DDR4 32GB(16GB × 2) 2666MHz
- Samsung SSD 970 EVO 500GB (m.2)
- Intel Ethernet Connection (12) I219-V
  - ``https://bitbucket.org/RehabMan/os-x-intel-network/downloads/``
- Realtek @ Intel High Definition Audio control
- HID keyboard + HID-compliant mouse

## 步骤
- 下载 ``https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64.exe`` 到 ``workspace``
- 下载 SSDTTime``(https://github.com/corpnewt/SSDTTime)`` 到 ``workspace``
- 下载 gibMacOS``(https://github.com/corpnewt/gibMacOS)`` 到 ``workspace``
- 下载 ProperTree``(https://github.com/corpnewt/ProperTree)`` 到 ``workspace``
- 下载 ``https://acpica.org/sites/acpica/files/iasl-win-20200528.zip`` 并解压到 ``workspace``
- 下载 ``http://www.chrysocome.net/downloads/ddrelease64.exe`` 到 ``workspace/gibMacOS``

<!--  -->
- 安装 python-3.8
  - 勾选 ``Add Python 3.8 to PATH``

- 安装 7z

<!--  -->
- OpenCore 手册 ``https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html``

<!--  -->
- 生成 SSDT

  - 复制 ``iasl.exe`` t到o ``workspace/SSDTTime``

  - 运行 ``workspace/SSDTTime/SSDTTime.bat``

  - 选择 ``Dump DSDT``

  - 选择 ``FakeEC``

  - 选择 ``AWAC``

  - 选择 ``USB Reset``

  - 文件生成在 ``workspace/SSDTTime/Results`` 目录下

<!--  -->
- 下载恢复镜像
  - 运行 ``workspace/gibMacOS/gibMacOS.bat``

  - 输入 ``R`` 切换到仅恢复模式

  - 选择一个含 ``Full Install`` 标签的（建议使用最新的版本）输出像这样:

    ```
    #######################################################
    #                 Downloaded 1 of 1                   #
    #######################################################

    Succeeded:
      RecoveryHDMetaDmg.pkg

    Failed:
      None

    Files saved to:
      U:\mac\gibMacOS-master\macOS Downloads\publicrelease\001-51042 - 10.15.7 macOS Catalina

    Press [enter] to return...
    ```

  - 根据输出内容复制文件路径。像这样:
    ```U:\mac\gibMacOS-master\macOS Downloads\publicrelease\001-51042 - 10.15.7 macOS Catalina\RecoveryHDMetaDmg.pkg```

<!--  -->
- 插入U盘 （将会清空&格式化U盘）
  - 复制 ``ddrelease64.exe`` 文件到 ``workspace/gibMacOS/Scripts/`` 目录下
  - 运行 ``workspace/gibMacOS/MakeInstall.bat``
  - 根据U盘选择。像这样: ``1O``
    - ``1``: 指U盘序号
    - ``O``: 使用 ``OpenCore`` 默认联网下载最新
  - 根据提示 输入 ``y`` 格式化U盘
  - 粘贴 ``RecoveryHDMetaDmg.pkg`` 文件路径
  - 等待完成...

- 一些驱动下载
  ``https://github.com/acidanthera/AppleALC/releases/`` DEBUG + RELEASE
  ``https://github.com/acidanthera/VirtualSMC/releases/`` DEBUG + RELEASE
  ``https://github.com/acidanthera/NVMeFix/releases/`` DEBUG + RELEASE
  ``https://github.com/acidanthera/Lilu/releases/`` DEBUG + RELEASE
  ``https://github.com/acidanthera/WhateverGreen/releases/`` DEBUG + RELEASE
  ``https://github.com/acidanthera/IntelMausi/releases/`` DEBUG + RELEASE

## 主板设置

### Disable
- Fast Boot
- Secure Boot
- Serial/COM Port
- Parallel Port
- VT-d (can be enabled if you set DisableIoMapper to YES)
- CSM
- Thunderbolt(For initial install, as Thunderbolt can cause issues if not setup correctly)
- Intel SGX
- Intel Platform Trust
- CFG Lock (MSR 0xE2 write protection)
  (This must be off, if you can't find the option then enable both AppleCpuPmCfgLock and AppleXcpmCfgLock under Kernel -> Quirks. Your hack will not boot with CFG-Lock enabled)

### Enable
- VT-x
- Above 4G decoding
- Hyper-Threading
- Execute Disable Bit
- EHCI/XHCI Hand-off
- OS type: Windows 8.1/10 UEFI Mode
- DVMT Pre-Allocated(iGPU Memory): 64MB
- SATA Mode: AHCI
