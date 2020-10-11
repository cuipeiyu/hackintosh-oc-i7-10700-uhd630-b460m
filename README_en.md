# hackintosh-oc-i7-10700-uhd630-b460m
 Hackintosh EFI Opencore

## PC

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

## Steps
- Download ``https://www.python.org/ftp/python/3.8.0/python-3.8.0-amd64.exe`` to ``workspace``
- Download SSDTTime``(https://github.com/corpnewt/SSDTTime)`` to ``workspace``
- Download gibMacOS``(https://github.com/corpnewt/gibMacOS)`` to ``workspace``
- Download ProperTree``(https://github.com/corpnewt/ProperTree)`` to ``workspace``
- Download ``https://acpica.org/sites/acpica/files/iasl-win-20200528.zip`` and unzip to ``workspace``
- Download ``http://www.chrysocome.net/downloads/ddrelease64.exe`` to ``workspace/gibMacOS``

<!--  -->
- Setup python-3.8
  - Check ``Add Python 3.8 to PATH`` option

<!--  -->
- Guide ``https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html``

<!--  -->
- Make SSDT

  - Copy ``iasl.exe`` to ``workspace/SSDTTime``

  - Run ``workspace/SSDTTime/SSDTTime.bat``

  - Select ``Dump DSDT``

  - and ``FakeEC``

  - and ``AWAC``

  - and ``USB Reset``

  - The generated file is in ``workspace/SSDTTime/Results``

<!--  -->
- Download recovery image
  - Run ``workspace/gibMacOS/gibMacOS.bat``

  - type ``R`` to toggle Recovery-Only

  - Select one ``Full Install`` tag to download image. print like this

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

  - Copy file path. like this

    ```U:\mac\gibMacOS-master\macOS Downloads\publicrelease\001-51042 - 10.15.7 macOS Catalina\RecoveryHDMetaDmg.pkg```

<!--  -->
- Setup USB flash disk
  - Copy ddrelease64.exe to ``workspace/gibMacOS/Scripts/``
  - Run ``workspace/gibMacOS/MakeInstall.bat``
  - Select your flash disk like ``1O``
    - ``1``: is disk num
    - ``O``: use OpenCore
  - Paste ``RecoveryHDMetaDmg.pkg`` file path
  - Waiting...
