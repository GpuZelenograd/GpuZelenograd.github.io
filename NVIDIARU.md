---
lang: ru-RU
pagelang2: ru
title: Old NVIDIA artifacts
description: Утилита ремонта карт GTX470-780Ti
image: photo/titan-scheme.png
seo:
  type: SoftwareApplication
  name: Old NVIDIA artifacts
redir_js: '{if (!/^RU|en-US/i.test(navigator.language) && !/noredirect/.test(window.location.search)) window.location.replace("/NVIDIA" + window.location.search)}{if (/html$/.test(window.location.pathname) && !/noredirect/.test(window.location.search)) window.location.replace("/NVIDIARU" + window.location.search)}'
hreflangs: <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIA" hreflang="x-default"/> <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIA" hreflang="en"/> <link rel="alternate" href="https://gpuzelenograd.github.io/NVIDIARU" hreflang="ru"/>
json_ld_ext: '"offers":{"@type":"Offer","price":"0","priceCurrency":"USD"},"operatingSystem":"Windows 10 | Linux","applicationCategory":"UtilitiesApplication","applicationSubCategory":"VBIOS tool","aggregateRating":{"@type": "AggregateRating","ratingValue": "4.8","ratingCount":"1211"},"fileSize":"4MB","softwareVersion":"2022.12","interactionCount":{"UserDownloads":"100500"}'
redirect_from:
  - /nvidiaRU
  - /nVidiaRU
  - /NvidiaRU
  - /NVidiaRU
  - /NVIDIAru
  - /nvidiaru
  - /nVidiaru
  - /Nvidiaru
  - /NVidiaru
  - /NVIDIARu
  - /nvidiaRu
  - /nVidiaRu
  - /NvidiaRu
  - /NVidiaRu
---
[&nbsp;&nbsp;&nbsp;`🌐En`](https://gpuzelenograd.github.io/NVIDIA?noredirecten){: style="float: right"}
Old NVIDIA artifacts **2022.12** отключает сбойные блоки GPU. Скачать:
<br>

### [<big><big>**Windows 7-11 64-bit**</big></big>🗄️4MB zip, GTX470-780Ti](https://gpuzelenograd.github.io/releases/Windows_old_nvidia_artifacts-2022.12.zip)
![Titan](photo/titan-scheme.png){: style="float: right; width: 42%;"}
### [<big><big>**Linux**</big></big>🐧4MB tar.xz, GTX645-780Ti](https://gpuzelenograd.github.io/releases/Linux_old_nvidia_artifacts-2022.12.tar.xz)

<br>
Утилита Old NVIDIA artifacts работает с видеокартами поколений Fermi, Kepler и 750Ti. Она может исправить артефакты/отвал/код 43 для некоторых карт, прошивая VBIOS отключающий неисправные блоки. Прошитая видеокарта может использоваться на любом компьютере. Восстановление GTX Titan 6GB также возможно.
<br>
<br>
[Список изменений и прочие загрузки](#changelog)
<br>
<br>
[![VideoManual](photo/video-manual.png)](https://www.youtube.com/watch?v=FAaXGDfH3Ro)

<br>

## Руководство пользователя
Описанные ниже шаги представляют типичное использование утилиты, и благодаря полуавтоматической прошивке укладываются в ~15минут. Для экспертов доступен [неавтоматизированный режим для модификации VBIOS `🌐En`](https://gpuzelenograd.github.io/EXPERT)

Перед подключением проблемной видеокарты необходимо подготовиться, иначе загрузка ОС может зависнуть. Для этого запускаем утилиту и нажимаем кнопку «Включить загрузку без драйвера», может быть в подменю «Подготовка без карты». Это включит [специальный режим загрузки](#bootmode), в котором при каждом старте можно выбрать - грузиться как обычно или зайти в безопасный режим без драйвера

![r1](photo/r1.png)

После его включения отображается инструкция по первой вставке проблемной карты

![r2](photo/r2.png)

Если при подключенной проблемной карте не удаётся загрузить ОС даже без драйвера  - перейдите к разделу [решение проблем](#troubleshootingsect)

## Первая прошивка
При первом запуске с восстанавливаемой картой выполняем тестовую прошивку VBIOS

![r3](photo/r3.png)

После первой прошивки нажимаем «Перезагрузка». Исходный VBIOS на всякий случай автоматически сохраняется в файл

![r4](photo/r4.png)

## Последующие прошивки

После этой и каждой последующей прошивки - необходимо оценить работоспособность карты. При отсутствии артефактов на экране BIOS выбираем обычный запуск с драйвером. Если для видеокарты ещё не стоит драйвер - устанавливаем драйвер NVIDIA 390/391.xx и запускаем какой-нибудь тест. При зависании системы на любом из этапов выполняем перезагрузку в безопасном режиме.

После того как удалось запустить систему - повторно запускаем утилиту и указываем прошла ли карта тест или проблема по-прежнему осталась

![r5](photo/r5.png)
![r6](photo/r6.png)

После нескольких перезагрузок утилита придёт к финальному решению - предложит завершить настройку на найденном оптимальном варианте, или если карта по-прежнему не работает - сообщит что проблема не может быть решена прошивкой. В последнем случае остаётся только выполнить откат VBIOS к исходному соответствующей кнопкой, завершить работу и отключить карту.

## Завершение
Если найден оптимальный вариант прошивки, который работает с драйвером и проходит тест - выбираем "завершить настройку".

![r7](photo/r7.png)

При завершении настройки подобранный VBIOS сохранится в файл и вернётся обычный режим загрузки. В GPU-Z будет видна сокращённая шина памяти:

![r8](photo/r8.png)

### Производительность
При успешном восстановлении уменьшается объём и ширина шины видеопамяти. Для видеокарт с 4мя микросхемами видеопамяти это приводит к довольно сильному падению производительности, но при большом количестве микросхем замедление невелико.

Стандартная 3GB 384bit [780Ti GHz Edition](https://www.techpowerup.com/gpu-specs/gigabyte-gtx-780-ti-ghz-edition.b2682) показывает около [3700 Graphics score](https://www.3dmark.com/search#advanced?test=spy%20P&cpuId=&gpuId=908&gpuCount=1&gpuType=ALL&deviceType=ALL&storageModel=ALL&memoryChannels=0&country=&scoreType=overallScore&hofMode=false&showInvalidResults=false&freeParams=&startDate=2017-01-01&endDate=2100-01-01&minGpuCoreClock=1150&maxGpuCoreClock=1340&minGpuMemClock=&maxGpuMemClock=&minCpuClock=&maxCpuClock=) в тесте TimeSpy. Для сравнения ниже представлены результаты восстановленной 780Ti с шиной 320bit и пары таких карт в режиме SLI:

[**Одна** 780Ti 2.5GB GHz Edition![result 3493](photo/780ti-ghz-3dmarkpreview.png)](https://www.3dmark.com/3dm/88862792)[**SLI 2×**780Ti 2.5GB![result 6111](photo/780ti-sli-3dmarkpreview.png)](https://www.3dmark.com/3dm/88861601)
{: style="column-count:2;text-align: left;"}

### <a id="bootmode">Специальный режим загрузки</a>
Кнопка «Включить загрузку без драйвера» просто изменяет встроенные настройки ОС. Режим можно переключить обратно в обычный несколькими способами:
* автоматически на этапе завершения после окончания поиска VBIOS
* вручную через кнопку «Отключить загрузку без драйвера»
* вручную, запустив от Администратора сценарий `restore_boot_mode` из подпапки detail
* вручную, выполнив от Администратора команду `bcdedit /set "{bootmgr}" displaybootmenu no` (для Linux: `systemctl set-default graphical.target`)

### <a id="troubleshootingsect">Решение проблем</a>
Некоторые проблемные видеокарты могут зависать при загрузке даже во время POST, до загрузки ОС. Часть из таких карт также можно исправить, но для загрузки могут потребоваться различные способы, позволяющие загрузить ОС и выполнить дальнейшую прошивку или откат утилитой «Old NVIDIA artifacts». На некоторых компьютерах через 1 минуту чёрного экрана монитор включатся и загрузка продложается. Если этого не происходит, попробуйте следующие варианты:
* вынув проблемную карту, зайдите в BIOS материнской платы и включите/отключите режим "CSM compatible" (он же non-EFI) режим. Сохраните настройки, выключите компьютер и снова вставьте проблемную видеокарту
* вынув проблемную карту, зайдите в BIOS материнской платы и включите опции «Integrated GPU» или «iGPU Multi-Monitor». Сохраните настройки, выключите компьютер и снова вставьте проблемную видеокарту, но дисплей оставьте подключенным к видеовыходу на материнской плате.
* используйте две дискретных видеокарты: вставьте в ближайший к процессору слот PCIe работающую видеокарту с подключенным дисплеем, а проблемную карту — в другой слот.

При работе с отдельными моделями Asus возникает `Ошибка: Выбранная карта не поддерживает прошивку модифицированных VBIOS`. Для некоторых из них данная проблема может быть решена из командной строки:
* Откройте окно командной строки с правами Администратора
* Выполните `cd` в подпапку "detail", содержающую исполняемый файл "nvflash"
* Запустите команду разрешения записи VBIOS: `nvflash.exe --protectoff`
![protectoff](photo/protectoff.png)

Старые модели карт - GTX470-590 поколения Fermi и [карты Grid поколения Kepler](https://gpuzelenograd.github.io/photo/GridK2-Fixed.png) - используют старые драйвера NVIDIA 3xx и поддерживаются в Windows-версиии приложения, но не в Linux-версии.

### <a id="changelog">Список изменений и прошлые версии</a>

Улучшения в [версии 2022.12](#top):
  * теперь утилита работает в Windows 7 наравне с Windows 10-11
  * исправлена прошиваемость GTX750Ti Asus DirectCU II, GTX760 Asus DirectCU II и некоторых других
  * создание вариаций VBIOS из указанного файла может производиться без прав администратора

#### Архивы версии 2022.11
  * [Windows <i>8</i>-10 64-bit 4MB zip, GTX 470-780Ti](https://gpuzelenograd.github.io/releases/Windows_old_nvidia_artifacts-2022.11.zip)
  * [Linux 4MB tar.xz, GTX <i>645</i>-780Ti](https://gpuzelenograd.github.io/releases/Linux_old_nvidia_artifacts-2022.11.tar.xz)

#### Прочее
  * [Архив c вариантами модификаций VBIOS для референсного исполнения GTX Titan 6GB](https://gpuzelenograd.github.io/releases/NVIDIA-GTX-Titan-6GB_Disable.zip)
