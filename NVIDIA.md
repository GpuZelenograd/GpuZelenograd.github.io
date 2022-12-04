---
pagelang: en-US
title: Old NVIDIA artifacts
pagedescription: Tool to fix old GPUs
redir_js: if (/^RU/i.test(navigator.language)) window.location.href = "/NVIDIARU"
redirect_from:
  - /n
  - /N
  - /nvidia
  - /nVidia
  - /Nvidia
  - /NVidia
---

<br/>

# [🗄️Windows 64-bit (4MB zip)](https://gpuzelenograd.github.io/releases/empty.zip)
# [🐧Linux (4MB tar.xz)](https://gpuzelenograd.github.io/releases/empty.tar.xz)

<br/>
<br/>
<br/>

# User manual

Some preparations need to be done before first plug of artifacting GPU, because otherwise OS may hang during boot. A special boot mode[^bootmode] need to be enabled, it will allow selecting each time between normal boot or safe-mode boot without driver.

To activate it start the "Old NVIDIA artifacts" tool while problematic GPU is not plugged yet, and press "Enable boot without driver" button (it can be under "Prepare without GPU…" submenu)
![e1](photo/e1.png)

After enabling driverless boot mode the instruction for plugging problematoc GPU would be shown
![e2](photo/e2.png)

[^bootmode]: Special boot mode button just tunes builtin OS functionlity. It can be switched back to normal in 4 ways:
    * automatically after the VBIOS search is done
    * manually via the "Disable boot without driver" button
    * manually by running `restore_boot_mode` tool from detail subfolder
    * manually by running `bcdedit /set "{bootmgr}" displaybootmenu yes` (or `systemctl set-default graphical.target` for Linux)


### Stage1 - test VBIOS flash

### Stage2 - more VBIOS flashes

### Completion
... more deatails under construction, [some more screenshots here](https://gpuzelenograd.github.io/NVIDIARU.html?user_manual)

