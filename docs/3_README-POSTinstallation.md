> ## Post Installtion:
1. Install Clover/ OpenCore on the main boot EFI paritition to enable boot without the installation media.
2. Please reference my uploaded EFI folder to determine my current bootloader configurations as well as which kexts I am currently using. Note that for CPUFriend, please generate your own DataProvider kexts per different machine specfiications and desired configurations. Use [one-key-cpufriend](https://github.com/stevezhengshiqi/one-key-cpufriend).  
3. Copy the kexts you will be using to their respective directories, per bootloaders:
- Clover: `EFI/Clover/kexts/Other/`
- OpenCore: `EFI/OC/Kexts/`  

*Refer to my uploaded EFI folder for my current kext list.  

5. Refer to the table below for the other post installtion configurations for each particular issue. Some issues are easy to fix, simply requiring a kext installtion or running a script, while others are my involved and require SSDT patching.
6. For those other, more complicated issues, proceed to `5_README-ACPIpatching.md` 

| Feature                              | Status | Dependency                                                   | Remarks                                                      |
| :----------------------------------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| macOS (10.14.x or 10.15.x)           | ✅      | `VirtualSMC.kext`, `Lilu.kext`, Clover  or OpenCore Bootloader             | OpenCore is preferred.                           |
| iMessage/ FaceTime                   | ✅      | Whitelisted Apple ID, Valid SMBIOS                           | [Guide](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/) |
| Siri                                 | ✅      | Apple ID, Working audio recorder                             | Needs `AppleALC`                                             |
| iTunes Video Playback                | ✅      | `WhateverGreen.kext`, Apple ID (*Optional*)                  | -                                                            |
| Sidecar                              | ✅      | iPad with iPadOS 13                                          | Tested with iPad Mini with iPadOS 13.1.2                      |
| WiFi                                 | ✅      | Native with BCM94360CS2. `AirportBrcmFixup` otherwise.                            |                                              |
| Bluetooth                            | ✅      | Native with BCM94360CS2. `BrcmFirmwareRepo.kext`, `BrcmPatchRAM3.kext`, and `BrcmBluetoothInjector.kext` otherwise. | -                                                            |
| Continuty                            | ✅      | Native with BCM94360CS2. `BT4LEContiunityFixup.kext` otherwise. Working Blutetooth and WiFi setup | -                                                            |
| AirDrop                              | ✅      | Native with BCM94360CS2. `BT4LEContiunityFixup.kext` otherwise. Working Blutetooth and WiFi setup | -                                                            |
| TrackPoint                           | ✅      | Patched `VoodooPS2Controller.kext`                           | -                                                            |
| TrackPad                             | ✅      | `VoodooPS2Controller.kext`                                   | -                                                            |
| Built-in Keyboard                    | ✅      | `VoodooPS2Controller.kext`                                   | -                                                            |
| Battery Percentage Indication        | ✅      | `SSDT-OCBAT0-TP_re80_tx70-80_x1c5th-6th_s12017_p51.aml`                                           | Use [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/) |
| CPU Power Management (SpeedShift)    | ✅      | `XCPM` and `CPUFriend.kext`, generate your own CPUFriendDataProvider with [CPUFriendFriend](https://github.com/corpnewt/CPUFriendFriend_ or [one-key-cpufriend](https://github.com/stevezhengshiqi/one-key-cpufriend).                                                      | -                                                            |
| IGPU Power Management                | ✅      | `XCPM`                                                       | -                                                            |
| Filesystem (APFS/HFS+)               | ✅      | Use SATA M.2. SSD or a Compatiable M.2. PCIe SSD             | No NVMe Power Management                                     |
| PCIe Ethernet                        | ✅      | `IntelMausi.kext`                                    | -                                                            |
| AirPort Extreme (Wi-Fi)              | ✅      | Swapping Intel WLAN card with  Dell DW1560                   | -                                                            |
| Audio Recording                      | ✅      | `AppleALC.kext` with Layout ID = 11                          | -                                                            |
| Audio Playback                       | ✅      | `AppleALC.kext` with Layout ID = 11                          | -                                                            |
| Full Graphics Accleration (QE/CI)    | ✅      | `WhateverGreen.kext`                                         | -                                                            |
| Brightness Adjustments    | ✅      | `WhateverGreen.kext` and `SSDT-PNLF-SKL_KBL.aml`                                        | -                                                            |
| Micro SD Card Reader                 | ✅      | Patched `AppleUSBCardReader.kext`                            | -                                                            |
| USB 3.1                              | ✅      | `USBInjectAll.kext` , `SSDT-UAIC.aml`                        | -                                                            |
| DisplayPort on Thunderbolt 3 Dock    | ⚠️      | `SSDT-TB3.aml`, `IOElectrify.kext`                           | The charging Type-C port **does not** support DisplayPort    |
| Thunderbolt 3 Dock (Port Replicator) | ✅      | `SSDT-TB3.aml`, `IOElectrify.kext`                           | -                                                            |
| Thunderbolt 3 Hotplug                | ⚠️      | `SSDT-TB3.aml`, `IOElectrify.kext`                           | The charging Type-C port **does not** support Hotpluging     |
| ThinkPad TB3 Dock (40AC) Ethernet           | ✅      | `AppleRTL815XComposite109.kext`, `AppleRTL815XEthernet109.kext` | [Item page](https://support.lenovo.com/au/en/solutions/acc100356) |
| CalDigit TS3 Plus Dock           | ✅      |  | [Item page](https://www.apple.com/shop/product/HMX12ZM/A/caldigit-ts3-plus-dock) |
| HiDPI *(Optional)*                   | ✅      | [xzhih/one-key-hidpi](https://github.com/xzhih/one-key-hidpi) | Scaling issues post-sleep fixed with AAPL, ig-platform `BAAnWQ==`                 |
| Battery life                         | ✅      | Non-NVME SSD, proper power management setup (CPU Power Management, GPU Power Management) | Drops 10% per hour for light programming tasks               |
| Hibernation                          | ❌      | [DISABLED](https://www.tonymacx86.com/threads/guide-native-power-management-for-laptops.175801/)                                                            | With the developement of acidanthera/HibernationFixup and OpenCore, hibernation may be fixed in the future.                                                    |
| Sierra Wireless EM7455               | ❌      | `Legacy_Sierra_QMI.kext`                                     | No internet                                                  |