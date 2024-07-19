This is documenting my experience trying to fix my keyboard.

# The Problem
I decided that the new HP Keyboard I bought was too big for me to carry all the way to Pune and decided the small compact one that we bought in 2017 would do. Before coming here, I checked if it was working by changing the batteries which had rusted the contacts and pressing a few keys. When the key strokes were detected, I thought everything is fine. It was not, Today, I tried to use it and when I pressed `e` it printed `ce\` when I pressed `i` it returned `i<return>`. Return means enter. Same with a few other keys. It prints `lo` if I press `l` while holding `a`. It is so bizarre. There's no rhyme or reason to it. 

# Origin of the Problem
I thought the reason for this problem was the update button I pressed in the firmware section of Pop's settings. I had done this the previous night and got a weird error I didn't remember because of which I had assumed that the update had failed. Maybe it hadn't. This was my hypothesis.

# My Procedure

My initial searches led me to a tool `fwupd`. The command for it is `fwupdmgr`

> [!note] This is what the firmware setting in the pop settings uses under the hood

[Can I downgrade Logitech K375s keyboard firmware? And is there a way to backup the current firmware on the keyboard before I do so?](https://github.com/fwupd/fwupd/issues/2044)
This was one of the first results. 

```
fwupdmgr --show-all-devices get-devices
```
This command was going to  be used a lot. It lists all the devices connected along with their details like firmware and flags etc

This is my output for the command

```
HP OMEN Laptop 15-en0xxx
│
├─AMD Ryzen 5 4600H with Radeon Graphics:
│ │   Device ID:          4bde70ba4e39b28f9eab1628f9dd6e6244c03027
│ │   Current version:    0x08600103
│ │   Vendor:             Advanced Micro Devices, Inc.
│ │   GUIDs:              b9a2dd81-159e-5537-a7db-e7101d164d3f ← cpu
│ │                       997104da-ec11-5e04-9d94-ac5501fbf609 ← CPUID\PRO_0&FAM_17
│ │                       1f2e0c2f-e078-5fcb-a8de-f78eff9a470a ← CPUID\PRO_0&FAM_17&MOD_60
│ │                       5fd5eb41-dd4a-5742-8448-861eaaa61cf8 ← CPUID\PRO_0&FAM_17&MOD_60&STP_1
│ │   Device Flags:       • Internal device
│ │ 
│ ├─GPIO controller:
│ │     Device ID:        f685512aa07369c9e77742acef941d779d31e766
│ │     GUID:             37b440a9-2473-5087-a39b-db84f32a8ed8 ← GPIO\ID_AMDI0030:00
│ │   
│ ├─Graphics Processing Unit (GPU):
│ │     Device ID:        e32966e41f54b47823eef28bd8b4bd9e1018b923
│ │     Current version:  113-RENOIR-026
│ │     Vendor:           Advanced Micro Devices, Inc. [AMD/ATI] (PCI:0x1002)
│ │     GUIDs:            5e44bedb-3951-52b5-a3dc-4adcac9d2ef7 ← PCI\VEN_1002&DEV_1636
│ │                       4f62f09b-2b5e-5ab8-9d46-b309ebca0a64 ← PCI\VEN_1002&DEV_1636&REV_C7
│ │                       dacb5f1a-7c34-539d-9ff7-2ce6e8a9f3af ← PCI\VEN_1002&DEV_1636&SUBSYS_103C8786
│ │                       65c40014-d6d7-5583-9081-103479a4f754 ← PCI\VEN_1002&DEV_1636&SUBSYS_103C8786&REV_C7
│ │     Device Flags:     • Internal device
│ │   
│ └─Secure Processor:
│       Device ID:        c54ab0237d7a8db8c717b68e0be78e4374a2a079
│       Vendor:           Advanced Micro Devices, Inc. (PCI:0x1022)
│       GUIDs:            0e8dc554-a0a2-51fb-b439-1eb72b14ec38 ← PCI\VEN_1022&DEV_15DF
│                         1adad2a8-21d1-5354-ae84-b68876203f50 ← PCI\VEN_1022&DEV_15DF&REV_00
│                         55963292-c886-55db-8816-985b30e4a8dc ← PCI\VEN_1022&DEV_15DF&SUBSYS_103C8786
│                         9f95f002-f7b7-5ec4-a5fa-b3e0a3bc0f55 ← PCI\VEN_1022&DEV_15DF&SUBSYS_103C8786&REV_00
│       Device Flags:     • Internal device
│     
├─KINGSTON SNV2S500G:
│     Device ID:          310f45f1f223064b5c16bf6dff31146755a64480
│     Summary:            NVM Express solid state drive
│     Current version:    SBI02102
│     Vendor:             Kingston Technology Company, Inc. (NVME:0x2646)
│     Serial Number:      50026B7282DAA145
│     GUIDs:              f4fb8601-d321-52b2-ab3f-a15451ef9042 ← NVME\VEN_2646&DEV_5017
│                         3860890e-40a7-5dc3-ace7-b25350b8025a ← NVME\VEN_2646&DEV_5017&REV_03
│                         9c6b23e3-a908-5e05-883b-c3b185db2f39 ← NVME\VEN_2646&DEV_5017&SUBSYS_26465017
│                         3042fb19-79ec-5156-8f74-95ab420e249d ← NVME\VEN_2646&DEV_5017&SUBSYS_26465017&REV_03
│                         ec4538de-b8bf-535c-9bf3-dfe16be87018 ← KINGSTON SNV2S500G
│     Device Flags:       • Internal device
│                         • Updatable
│                         • System requires external power source
│                         • Needs shutdown after installation
│                         • Device is usable for the duration of the update
│   
├─System Firmware:
│     Device ID:          a45df35ac0e948ee180fe216a5f703f32dda163f
│     Summary:            UEFI ESRT device
│     Current version:    252116992
│     Minimum Version:    252116992
│     Vendor:             HP (DMI:AMI)
│     Update State:       Success
│     GUIDs:              11bdf49e-a358-424a-873c-a115a02fe66a
│                         230c8b18-8d9b-53ec-838b-6cfc0383493a ← main-system-firmware
│     Device Flags:       • Internal device
│                         • Updatable
│                         • System requires external power source
│                         • Needs a reboot after installation
│                         • Cryptographic hash verification is available
│                         • Device is usable for the duration of the update
│   
├─TPM:
│     Device ID:          c6a80ac3a22083423992a3cb15018989f37834d6
│     Summary:            TPM 2.0 Device
│     Current version:    3.41.0.5
│     Vendor:             Advanced Micro Devices, Inc. (TPM:AMD)
│     GUIDs:              ff71992e-52f7-5eea-94ef-883e56e034c6 ← system-tpm
│                         9305de1c-1e12-5665-81c4-37f8e51219b8 ← TPM\VEN_AMD&DEV_0001
│                         78a291ae-b499-5b0f-8f1d-74e1fefd0b1c ← TPM\VEN_AMD&MOD_AMD
│                         65a3fced-b423-563f-8098-bf5c329fc063 ← TPM\VEN_AMD&DEV_0001&VER_2.0
│                         5e704f0d-83cb-5364-8384-f46d725a23b8 ← TPM\VEN_AMD&MOD_AMD&VER_2.0
│     Device Flags:       • Internal device
│   
├─TU116M [GeForce GTX 1660 Ti Mobile]:
│     Device ID:          ce4c74a5188d5b9cdb1e72ed32dad2d313c1c999
│     Current version:    a1
│     Vendor:             NVIDIA Corporation (PCI:0x10DE, PCI:0x1022)
│     GUIDs:              06dce33a-0e57-5628-a4e8-89c236211c44 ← PCI\VEN_10DE&DEV_2191
│                         2d31e8c0-a4f5-5c44-a3ae-41985f5a0ab7 ← PCI\VEN_10DE&DEV_2191&REV_A1
│                         d21e2ebb-f8b1-503d-bdf9-6c04236e38ce ← PCI\VEN_10DE&DEV_2191&SUBSYS_103C8786
│                         5c7e9d3a-d7c8-56de-82e4-ac8edf208321 ← PCI\VEN_10DE&DEV_2191&SUBSYS_103C8786&REV_A1
│                         8f3f2d84-79db-5a32-a553-72b06bd850f5 ← PCI\VEN_1022&DEV_1633
│                         52bf1581-2e1a-5888-9d2f-6237292ebc62 ← PCI\VEN_1022&DEV_1633&REV_00
│                         27f245f3-99ff-5b03-b949-bd6dfec31ddb ← PCI\VEN_1022&DEV_1633&SUBSYS_10221453
│                         616e2475-e699-59ca-8148-e748ef0d8eff ← PCI\VEN_1022&DEV_1633&SUBSYS_10221453&REV_00
│     Device Flags:       • Internal device
│                         • Cryptographic hash verification is available
│   
├─Unifying Receiver:
│     Device ID:          fd51eca49fafd1d90624f3af006c4b98c05c6867
│     Summary:            Miniaturised USB wireless receiver
│     Current version:    RQR24.05_B0029
│     Bootloader Version: BOT03.01_B0008
│     Vendor:             HIDRAW:0x046D|USB:0x046D
│     Install Duration:   30 seconds
│     GUIDs:              cc4cbfa9-bf9d-540b-b92b-172ce31013c1
│                         279ed287-3607-549e-bacc-f873bb9838c4 ← HIDRAW\VEN_046D&DEV_C52B
│                         fcf55bf5-767b-51ce-9c17-f6f538c4ee9f ← HIDRAW\VEN_046D&DEV_C52B&REV_00
│     Device Flags:       • Updatable
│                         • Supported on remote server
│                         • Unsigned Payload
│   
└─WDC PC SN730 SDBPNTY-512G-1006:
      Device ID:          0fba4a8bedba53076fc9b147655e59455bc25a87
      Summary:            NVM Express solid state drive
      Current version:    HPS2
      Vendor:             Sandisk Corp (NVME:0x15B7)
      Serial Number:      20317C805060
      GUIDs:              fccbb6ea-e20e-58ad-bf8a-7fb7d43ff4c2 ← NVME\VEN_15B7&DEV_5006
                          a39943dd-3afb-54f8-b110-c5a21f071200 ← NVME\VEN_15B7&DEV_5006&REV_00
                          12c86995-0b90-5ec5-98f3-7a6ed4ca50e0 ← NVME\VEN_15B7&DEV_5006&SUBSYS_15B75006
                          7b974856-317d-5538-a915-de0a6353750f ← NVME\VEN_15B7&DEV_5006&SUBSYS_15B75006&REV_00
                          430b96d5-8289-5250-a02c-2f0ec84e7f09 ← WDC PC SN730 SDBPNTY-512G-1006
      Device Flags:       • Internal device
                          • Updatable
                          • System requires external power source
                          • Needs a reboot after installation
                          • Device is usable for the duration of the update
```
We are interested in the Unifying Receiver Part

I also found this github repo with all the firmware code for logitech devices
[fw_updates](https://github.com/Logitech/fw_updates/)

Note that the Current Version of the Firmware on the Unifying Receiver is RQR24.*

> [!note] There were multiple steps and dead ends before I found this repo. I tried to install updates through logitech's firmware update tool for windows. Had to go to windows for that. I have quite a few software installed there now that I don't need.

I tried all the commands that the user had tried in the github issue I linked above. 
```
fwupdmgr downgrade fd51eca49fafd1d90624f3af006c4b98c05c6867
fwupdmgr get-updates fd51eca49fafd1d90624f3af006c4b98c05c6867
fwupdmgr activate fd51eca49fafd1d90624f3af006c4b98c05c6867
```

None of them worked.
With the downgrade command, I was getting two options for the firmware I want to get back to. The current one was `RQR24.10_B0036`
I had the option of `RQR24.05_B0029` and `RQR24.07_B0030`

Both of them would send the receiver into bootloader mode and fail the update. I had to unplug and replug it. I don't know if that worked. Sometimes, I would press update in Pop settings. Again to get back. It got back to the old state of \*36 firmware and wonky keys. 

One of the commands in the above github issue was `fwupdmgr install ~/Downloads/66924773f5ff849c0e26b2bd4ff4fdbb228a895d-Logitech-K370s_K375s-MPK03.02_B0009.cab 7d8aa8eabc1c6bd74a385396092abd8d0f7f9f85`

Then, I looked more into fw_updates repo. All the firmware packages had a folder called `lvfs` inside them. inside that, there was a Makefile. I used the command
```
make all
```

Now, I had the .cab file.

running
```
fwupdmgr install ./Logitech-Unifying-RQR24.03_B0027.cab fd51eca49fafd1d90624f3af006c4b98c05c6867
```

Would result in the error
```
failed to update_detach using unifying: failed to detach to bootloader: failed to send: failed to write: wrote -1 of 7
```

Then I found another github issue and a merge request
https://github.com/fwupd/fwupd/commit/ddfc72db5610f54f589358cac9c29323f70745ab
https://github.com/fwupd/fwupd/issues/1183
which said that when the bootloader is activated and reboots, it loses connection with fwupd and this makes it think that the operation has failed. Then we have to run the same command again to complete the installation.

I ran the same command again but the device was not being detected at all after this partial update. Or so I thought. I was being detected along with bootloader active, it had a different uuid. I ran the install command with that new uuid to complete the flashing process.
```
fwupdmgr install ./Logitech-Unifying-RQR24.03_B0027.cab 84d0e3f2a0f8b2328f7995767b23ebb40494723f --allow-older
```

This finally updated the firmware of the reciever.