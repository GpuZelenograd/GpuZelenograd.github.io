---
title: Old NVIDIA artifacts
description: Tool to fix GTX470-780Ti GPUs
image: photo/titan-scheme.png
seo:
  type: SoftwareApplication
  name: Old NVIDIA artifacts
redir_js: if (/^RU/i.test(navigator.language) && !/noredirect/.test(window.location.search)) window.location.replace("/NVIDIARU" + window.location.search)
hreflangs: <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIA" hreflang="x-default"/> <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIA" hreflang="en"/> <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIARU" hreflang="ru"/>
json_ld_ext: '"offers":{"@type":"Offer","price":"0","priceCurrency":"USD"},"operatingSystem":"Windows 10 | Linux","applicationCategory":"UtilitiesApplication","applicationSubCategory":"VBIOS tool","aggregateRating":{"@type": "AggregateRating","ratingValue": "4.8","ratingCount":"1211"},"fileSize":"4MB","softwareVersion":"2022.12","interactionCount":{"UserDownloads":"100500"}'
redirect_from:
  - /n
  - /N
  - /nvidia
  - /nVidia
  - /Nvidia
  - /NVidia
---

Old NVIDIA artifacts **2022.12** disables bad blocks to fix GPU artifacting. Download:
<br>

### [<big><big>**Windows 7-10 64-bit**</big></big>🗄️4MB zip, GTX470-780Ti](https://gpuzelenograd.github.io/releases/Windows_old_nvidia_artifacts-2022.12.zip)
![Titan](photo/titan-scheme.png){: style="float: right; width: 42%;"}
### [<big><big>**Linux**</big></big>🐧4MB tar.xz, GTX645-780Ti](https://gpuzelenograd.github.io/releases/Linux_old_nvidia_artifacts-2022.12.tar.xz)

<br>
Old NVIDIA artifacts utility works with Fermi, Kepler and 750Ti gpus. It can fix some  artifacting GPUs by flashing VBIOS that disable malfunctioning GPU parts. Fixed GPUS can be used in any computer. GTX Titan 6GB is also supported
<br>
<br>
[Changelog and misc downloads](#changelog)
<br>
<br>
Thanks to all researchers for modded BIOSes, they were very helpful during development!
<br>

## User manual

Prepare your system for malfunctioning GPU otherwise your system may hang during OS boot:  start the utility while faulty GPU is not plugged yet

![e1](photo/e1.png)

* click "Enable boot without driver" ([special boot mode](#bootmode) where you can select between regular boot and safe mode without video driver)
* follow instructions on your screen

![e2](photo/e2.png)

if you can't boot your system with faulty GPU even in safe mode, then check [Troubleshooting](#troubleshootingsect)

## First flash
Click "Flash testing VBIOS"

![e3](photo/e3.png)

Original VBIOS automatically got saved at this point, click "Reboot"

![e4](photo/e4.png)


## Next flashes
If the system boots fine and there are NO artifacts on the screen:
* install compatible NVIDIA driver, like 390/391.xx
* run any *short* benchmark
* start the utility again, select "Activate more blocks and reboot"

![e5](photo/e5.png)

If there are artifacts or boot/benchmark problems - select "Flash fixing VBIOS and reboot"

![e6](photo/e6.png)

Continue until the utility will find an optimal and stable VBIOS. If your GPU still shows some artifacts then it can not be fixed by this utility.

## Last stage
If the utility have found optimal and stable VBIOS and GPU have completed any benchmark - start the utility and select "Complete configuring", this will save modified VBIOS and return your system to normal boot mode

![e7](photo/e7.png)

You can run GPU-Z and check your current "bus width" and "memory size"

![e8](photo/e8.png)

### Performance
If modification succeeds, the GPU memory size and bus width reduces. For GPUs with only 4 memory chips the performance drop is significant, but for cards with a lot of chips the difference is quite small. The 3GB 384bit [780Ti GHz Edition](https://www.techpowerup.com/gpu-specs/gigabyte-gtx-780-ti-ghz-edition.b2682) has a [~3700 average TimeSpy Graphics score](https://www.3dmark.com/search#advanced?test=spy%20P&cpuId=&gpuId=908&gpuCount=1&gpuType=ALL&deviceType=ALL&storageModel=ALL&memoryChannels=0&country=&scoreType=overallScore&hofMode=false&showInvalidResults=false&freeParams=&startDate=2017-01-01&endDate=2100-01-01&minGpuCoreClock=1150&maxGpuCoreClock=1340&minGpuMemClock=&maxGpuMemClock=&minCpuClock=&maxCpuClock=).

Here are results for a 780Ti with 320bit bus left after fix, and a SLIed pair of such cards:

[**Single** 2.5GB 780Ti GHz Edition![result 3493](photo/780ti-ghz-3dmarkpreview.png)](https://www.3dmark.com/3dm/88862792)[**SLI 2x** 2.5GB 320bit 780Ti![result 6111](photo/780ti-sli-3dmarkpreview.png)](https://www.3dmark.com/3dm/88861601)
{: style="column-count:2;text-align: left;"}

### <a id="bootmode">Special boot mode</a>
"Enable boot without driver" button just tunes built-in OS functionality to let you enter safe mode without video driver. To reverse it try one of this:
* successfully complete VBIOS modification (will be applied automatically)
* manually via the "Disable boot without driver" button
* manually by launching as Administrator `restore_boot_mode` tool from detail subfolder
* manually by running as Administrator `bcdedit /set "{bootmgr}" displaybootmenu no` (for Linux: `systemctl set-default graphical.target`)

### <a id="troubleshootingsect">Troubleshooting</a>
Some of faulty GPUS may hang even during POST and don't make it to safe mode. Some of them *can* be fixed, but may require several workarounds to be able to boot the OS and be flashed with the "Old NVIDIA artifacts" tool. Try following:
* enable or disable CSM-compatible-with-non-EFI mode in motherboard BIOS
* enable "Integrated GPU" or "iGPU Multi-Monitor" in motherboard BIOS and attach display to the motherboard
* use two discrete GPUs: plug the working GPU with display attached into the PCIe slot closest to CPU and plug the faulty card in another slot.


### <a id="changelog">Changelog and misc downloads</a>

[Version 2022.12](#top) improvements:
  * now works on Windows7 (Windows10 as well)
  * fixed flashing GTX750Ti Asus DirectCU II, GTX760 Asus DirectCU II and some others
  * generating modded VBIOSes from a given file can be done without admin rights

#### Older 2022.11 downloads
  * [Windows <i>8</i>-10 64-bit 4MB zip, GTX 470-780Ti](https://gpuzelenograd.github.io/releases/Windows_old_nvidia_artifacts-2022.11.zip)
  * [Linux 4MB tar.xz, GTX <i>645</i>-780Ti](https://gpuzelenograd.github.io/releases/Linux_old_nvidia_artifacts-2022.11.tar.xz)

#### Misc
  * [modified VBIOS variants for reference edition GTX Titan 6GB](https://gpuzelenograd.github.io/releases/NVIDIA-GTX-Titan-6GB_Disable.zip)