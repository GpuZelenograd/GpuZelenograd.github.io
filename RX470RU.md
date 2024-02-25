---
title: VBIOS для RX470-580
description: Нюансы различных производителей
redirect_from:
  - /Rx470RU
  - /rx470RU
  - /RX470Ru
  - /Rx470Ru
  - /rx470Ru
  - /RX470ru
  - /Rx470ru
  - /rx470ru
---
# Подбор подходящего VBIOS для RX470-580
Данные заметки представлены в ознакомительных целях. Мы не оказываем услуги подбора VBIOS и не принимаем карты RX470-580 в ремонт.

Наиболе актуальная версия публикуется GpuZelenograd в [https://gpuzelenograd.github.io/RX470RU](https://gpuzelenograd.github.io/RX470RU)

### На что обращать внимание при выборе VBIOS на TechPowerup

 * Наличие в списке поддерживаемых типов памяти - той памяти, которая фактически стоит на видеокарте
 * Совпадения порядка и количества видеовыходов. Если карта майнинговая и видеовыходов мало - допускается чтоб в VBIOS их было больше чем по факту. В каких биосах какие видеовыходы про многие VBIOS написано в разделе ниже
 * Совпадение модели ШИМ. В каких биосах какая ШИМ про многие VBIOS написано в разделе ниже
 * Соответствие TDP указанного в techpowerup  и количества фаз
    * Если на карте 5-6 фаз, то TDP должен быть более 100W, иначе карта будет неадекватно снижать частоту
    * Если на карте 4 фазы, то TDP должен быть менее 100W, иначе карта сгорит
    * Также после прошивки VBIOS следует проверить что под нагрузкой реально активируются все фазы, такую несовместимость заранее предсказать проблематично 
 * Отсутствие редактирования от майнеров. 99% биосов без красной плашки Unverified являются не редактированными (очень редко бывает исключения). Но и среди "Unverified" тоже много нормальных VBIOS. Как правило это можно проверить по 2 критериям:
     * в строчках Memory Timings не должно быть соседних строк с одинаковыми (скопированными значениями).
     * частоты памяти и GPU должны соответствовать заявленным на сайте производителя, майнеры могли делать частоты как выше, так и ниже.
 * Частоту GPU Clock (максимальную). Попытка поставить на RX470 биос от быстрой 580 с частотой 1411 MHz приведёт к случайным вылетам приложений.
 * Частоту памяти (максимальную). Если микросхемы памяти не спроектированы для работы на 2000Mhz, использовать их на 2000Mhz не рекомендуется. Заводские частоты 8Gbit-чипов:
     * Samsung
         * суффикс -HC22: 2000-2250Mhz
         * суффикс -HC25: 2000Mhz
         * суффикс -HC28: 1750Mhz
         * суффикс -HC03: 1500Mhz
     * Hynix
         * суффикс -R4C: 2000Mhz
         * суффикс -R2C/R0C: 1750Mhz
         * суффикс -T2C: 1500Mhz
     * Micron
         * D9TCB (A-die), D9VVR(B-die): 2000Mhz
         * D9SXD (A-die), D9VVQ(B-die), D9TRV(A-die), D9SSX(A-die): 1750Mhz
         * D9SXC (A-die), D9VVW(B-die), D9TRZ(A-die): 1500Mhz
         * D9XDL - 4Gbit-чип, 1500Mhz
 * И только в самую последнюю очередь имеет смысл обращать внимание на то - какая карта 470/480/570 (она же 580-2048sp)/580(она же 590_GME)
     * Все биосы будут исправно работать со всеми чипами, единственный недочёт - использование биоса от 470/570 на 480/580 приведёт к тому что будут задействоваться только 2048 шейдерных блоков из 2304 доступных.


# Способы поиска в базе TechPowerup
В зависимости от ситуации могут использоваться разные способы поиска. Некоторые из них предоставлены самим TechPowerup, некоторые через Google


### Только по subvendor
По subvendor id (нужное значение гуглится по скриншотам GPU-Z) - например для XFX=1682. Ищем в 3 вариациях, подставляя это код в URL

 * [Официальные Биосы techpowerup: https://www.techpowerup.com/vgabios/?did=1002-67DF-1682-](https://www.techpowerup.com/vgabios/?did=1002-67DF-1682-)
 * [Непроверенные биосы: https://www.techpowerup.com/vgabios/?architecture=Uploads&did=1002-67DF-1682-](https://www.techpowerup.com/vgabios/?architecture=Uploads&did=1002-67DF-1682-)
 * [Непроверенные биосы на ребрендинг (580 2048SP и 590 GME): https://www.techpowerup.com/vgabios/?architecture=Uploads&did=1002-6FDF-1682-](https://www.techpowerup.com/vgabios/?architecture=Uploads&did=1002-6FDF-1682-)

Однако, многие VBIOS используют subvendor id=1002 (код AMD) что не позволяет найти VBIOS по subvendor

### По поддерживаемой памяти и частоте

Тут можно искать через google и применять дополнительную фильтрацию. Вот например запрос только официальных VBIOS под микрон B-die на частоту 1750Mhz с исключением биосов с автодетектом памяти (чтоб нашлись только те где один вариант без автодетекта)

`67DF MT51J256M32HFB -autodetect -unverified "1750 MHz Temperature" site:techpowerup.com` [ссылка-пример](https://www.google.com/search?filter=0&q=67DF+MT51J256M32HFB+-autodetect+-unverified+%221750+MHz+Temperature%22+site%3Atechpowerup.com)

А вот под Samsung FС на картах Sapphire (код subvendor 1DA2) на частоту 2000 Mhz:

`67DF 1DA2 K4G80325FC "2000 MHz Temperature" site:techpowerup.com` [ссылка-пример](https://www.google.com/search?filter=0&q=67DF+1DA2+K4G80325FC+%222000+MHz+Temperature%22+site%3Atechpowerup.com)

### По уникальному идентификатору (у многих вендоров начинается на 113)
В списках по производителям ниже многие VBIOS представлены просто их идентификатором без ссылки. Чтоб скачать такой биос опять же используем google 

`"113-D0090101-100" -unverified site:techpowerup.com` [ссылка-пример](https://www.google.com/search?filter=0&q=%22113-D0090101-100%22+-unverified+site%3Atechpowerup.com)

Если среди официальных не нашлось - убираем фильтрацию по unverified.

`"GV-RX570GAMING-8GD/FH0/0A9D" site:techpowerup.com` [ссылка-пример](https://www.google.com/search?filter=0&q=%22GV-RX570GAMING-8GD%2FFH0%2F0A9D%22+site%3Atechpowerup.com)

# Нюансы по производитлям карт - ШИМы и видеовыходы

## Reference-карты (турбины Sapphire и другие с идентичным текстолитом)
ШИМ: IR3567B, 4-6 фаз
Видеовыходы: 1 HDMI с нижнего краю, опционально DVI параллельно ему вторым рядом и 3 DP в том же ряду что HDMI. На майнинговых бывает отсутствие подмножества - бывает что есть только DVI или из 3х шт DP оставлен 1. Такие отличия как правило не отражаются в VBIOS, и на совместимость не влияют.

480 Reference 2000MHz 8GB (0B37
* 110W Samsung-B - 113-D0090101-100 D0090101.100

470 Reference (Sapphire platinum E349)
* 92W Micron-A - 113-349P8-UM1 349P0EMG.U41


## Asus
На всех картах имеет уникальное сочетание ШИМа и видеовыходов, которое не встречается у других производителей. Соответственно не пытайтесь использовать VBIOS Asus для других производителей, и наоборот.

[Большинство нужных VBIOS ASUS представлено тут](https://www.techpowerup.com/vgabios/?did=1002-67DF-1043--)

#### карты Expedition/LED на шимке ASP1106 
Под карты Expedition/LED на шимке ASP1106 и память Samsung FB идёт вот этот VBIOS
[67DFHB.15.50.2.1.AS56](https://www.techpowerup.com/vgabios/206012/206012)

Также он является диагностическим - у него пониженные требования к ШИМ-контроллеру для старта и некоторые платы с неисправными ШИМ-контроллерами других моделей, зависающие на инициализации - с ним дают картинку в windows через некоторые видеовыходы;
это позволяет сделать предположение об исправности чипа; полноценно работать не будет, т.к. ШИМка всё же не та

## Sapphire
Все модели кроме reference-турбины имеют видеовыходы отличающиеся от reference, "2 HDMI под DVI, 2 DP сбоку", поэтому тут тоже - нет совместимости с другими вендорами.
Конкретная модель карты Sapphire написана на наклейке вида "E3??". ШИМка IR3567B/NCP81022 и количество фаз представлено в списке ниже в соответствии с этим номером.
В биосе этот же номер представлен как последние 4 цифры идентификатора устройства, после 1DA2

#### E343, NCP81022 4-phase 6pin сверху, расположение питания ближе к видеовыходaм, как Reference
Sapphire 570 Pulse Mini ITX 1750Mhz 8GB (E343)
* 120W Samsung-B - 113-D00036-S01 343L05S7.S01
* 120W Micron-B/H5GQ8H24MJR - 113-D00035-S02 343L0507.S02

#### E347, IR3567B 8pin сбоку (необычное), 4-5-6 фаз по распайке
Sapphire 470 nitro+ **2000Mhz** 8GB (E347) - даже если фаз 5 - продолжают работать только 4.
* 110W Samsung-B - 113-1E3470U.S61 347P06SU.S61
* 130W Samsung-B - 113-1E3470U.O4W 347P06SU.O4W

Sapphire 480 nitro+/nitro+ OC 2000Mhz 8GB (E347) - vbios активирует 5фазный режим при старте
* 140W Samsung-B - 113-2E3472U.O54 347X06SU.O54 (на 1306Mhz)
* 145W Samsung-B - 113-2E3470U.S5X 347X06SU.S5X (более старая вариация S52, на 1306Mhz - O5Y)
* 150W Samsung-B - 113-2E3470U.X5W 347X06SU.X5W (и более старые вариации X4L, X51)
* 150W H5GC8H24MJR - 113-2E3470U.X6N 347X06HU.X6N

Sapphire 570 1750Mhz
* 125W Micron-A/H5GQ8H24MJR 113-3E3470U-S47 347L060U.S47 (activates 5 phases)

Sapphire 470D(?) 1650Mhz 8GB (E350), NCP81022 4-phase
* 95W Samsung-B - 113-350P58G-U41 350P0ESI.U41 (и более новая вариация U44)

470D **4GB** (A019)
* 100W - 113-3E353AU-O4J 353D05SU.O4J

#### E350, 6pin сбоку, GPRO 8200 IR3567B 5-phase
* 85W Samsung 113-350P58G

#### E353, 8pin сверху, NCP81022 4-phase DrMos
бывает quad

Sapphire 470 nitro 1750Mhz 8GB (E353) + подходит под pulse rx570
* 128W H5GQ8H24MJR - 113-WE353GU-M7F 353P06HU.M7F
* 128W Samsung-B/Micron-A - 113-2E353BU.O50 353P060U.O50 - под переделку, + подходит под pulse rx570
* 122W Micron-B - 113-WE3534U-M9J 353P6MBU.M9J

Sapphire 480 nitro OC **1750Mhz** 8GB (E353)
* 142W Samsung-B/Micron-A - 113-1E353FU.O50 353X060U.O50

Sapphire 570 Pulse 1750Mhz 8GB (E353)
* 135W Micron-B/H5GQ8H24MJR - 113-5E353BU-O6G 353L6MHU.O6G
* 135W Samsung-B/H5GQ8H24MJR - 113-5E353BU-O4G 353L6SHU.O4G
* 135W H5GC8H24AJR_PARTNER_SAPPHIRE - 113-2E353WU-O6K 353L6HAJ.O6K

Sapphire 580 Pulse 2000Mhz 8GB (E353)
* 155W Samsung-B/H5GC8H24AJR_PARTNER_SAPPHIRE - 113-4E353WU-O67 353Y6HAJ.O67
* 155W Micron-B - 113-4E353BU-O50 353Y6MBU.O50
* 155W Samsung-B/H5GQ8H24MJR - 113-4E353BU-O4E 353Y060U.O4E
* 155W H5GQ8H24MJR - 113-4E3531U-O4V 353Y06HU.O4V - прошивка этого в rx570 даёт revision E7 у которого 32CU

Sapphire 590 GME 2000Mhz 8GB (E353)
* 160W Samsung-C/H5GC8H24AJR_PARTNER_SAPPHIRE 113-4E353GU-S80 353GHASC.S80

#### E366, 6pin + 8pin сверху, NCP81022 6-phase
Sapphire 570 nitro+ 1750Mhz 8GB (E366)
* 135W H5GQ8H24MJR - 113-2E366DU-S4U 366L06HU.S4U
* 135W Micron-B - 113-2E366DU-S5U 366L6MBU.S5U
* 135W Samsung-B/Micron-A - 113-2E366DU-S4L 366L060U.S4L
* 160W H5GQ8H24MJR - 113-2E366AU-X56 366L06HU.X56
* 160W Micron-B - 113-2E366AU-X5T 366L6MBU.X5T
* 160W Samsung-B/Micron-A - 113-2E366AU-X4Z 366L060U.X4Z - под переделку. Прошивка этого в 580 чип - даёт rev от 570.

Sapphire 580 nitro+ 2000Mhz 8GB (E366)
* 160W Micron-B - 113-1E366CU-S5S 366Y6MBU.S5S
* 160W Samsung-B/H5GQ8H24MJR - 113-1E366CU-S52 366Y060U.S52
* 160W Micron-A - 113-1E366CU-S5Q 366Y06MU.S5Q (возможно низкий хешрейт при тех же частотах, причины не очень ясны)
* 175W Micron-B - 113-1E3660U-O5R 366Y6MBU.O5R
* 175W Samsung-B/H5GQ8H24MJR - 113-1E3660U-O51 366Y060U.O51 (есть боле старый 113-3E366DU-S4Y 366R060U.S4Y)
* 175W Micron-A - 113-1E3660U-O5P 366Y06MU.O5P под переделку
* 175W Samsung-C - 113-1E3660U-O69 366Y6SFC.O69
* 175W Samsung-B/H5GC8H24AJR_PARTNER_SAPPHIRE - 113-1E3664U-O65 366Y6HAJ.O65
* 185W Samsung-B/H5GQ8H24MJR - 113-SE366AU-Z45 366R060U.Z45

Sapphire 580 **2100Mhz** 8GB (E366)
* 183W Micron-B - 113-BE366EU-Z48 366R6MBU.Z48
* 183W Samsung-B/H5GQ8H24MJR - 113-BE366EU-Z46 366R060U.Z46

Sapphire 590 GME 2000Mhz 8GB (E366)
* 180W Samsung-C/H5GQ8H24MJR - 113-1E366GU-O40 366G6SFC.O40

Sapphire 590 2000Mhz 8GB (E366)
* 175W Micron-B - 113-4E3664U-S6B 366U6MBU.S6B
* 175W H5GQ8H24MJR - 113-4E3661U-S6J 366U6HYU.S6J
* 175W Samsung-C - 113-4E3661U-S6R 366U6SFC.S6R

Sapphire 590 **2100Mhz** 8GB (E366)
* 185W Micron-B - 113-4E3661U-X6A 366U6MBU.X6A
* 185W H5GQ8H24MJR - 113-4E3661U-X6I 366U6HYU.X6I
* 185W Samsung-B - 113-4E3661U-X6M 366U6S0U.X6M

#### E382 - reference 570 с турбиной?

#### E387, 8pin сверху, IR3567B 4phase
существует текстолит под quad bios

Sapphire 590 Pulse 2000Mhz 8GB (E387)
* 175W Samsung-B - 113-5E3874U-S4R 387U6S0U.S4R
* 175W Samsung-B - 113-5E3874U-S4T 387U6S0U.S4T - отличий мало: в имени папки в заголовке и ucCKSVOffsetandDisable

Sapphire 580 Pulse 2000Mhz 8GB (E387)
* 155W Micron-B - 113-1E3870U-O49 387Y6MBU.O49
* 155W Samsung-B/H5GQ8H24MJR 113-1E3870U-O45 387Y6SHU.O45
* 155W Samsung-B/H5GQ8H24MJR 113-1E3870U-O4B 387Y6SHU.O4B

Sapphire 570 Pulse 1750Mhz 8GB (E387)
* 138W Micron-B - 113-2E3870U-O4J 387L6MBU.O4J

Возможно её VBIOS 387E:
* 122W, 1750Mhz Samsung-B/H5GC8H24MJR 113-WE3874U.M3E 387P6SHU.M3E (возможно есть более новый 387P6SHU.M4E)
* 75W(silent mode 1000Mhz), 1750Mhz Samsung-B/H5GC8H24MJR 113-WE3874U.M5E 387P6SHU.M5E
* 122W, 1750Mhz Micron-B 113-WE3870U.M3C 387P6MBU.M3C (возможно есть более холодный 113-WE3870U.M5C)

#### E388, 8pin сверху, NCP81022 4-phase Driver + DualMosfet
VBIOS from E353
E388 - [470 Quad Firmware, 4phase NCP81022, 1x8pin, DVI-only. D9VVR Аналог E353?](https://www.techpowerup.com/forums/threads/sapphire-rx-470-8gb-e388-bios.279773/)

#### E391, короткая, 8pin сверху - ncp81022, 4 фазы (S88-3E391-001JC)
* 580 2048sp, 146W, 1750Mhz Samsung-C 113-339101S-U13 391L36SC.U13

#### E396 (299-FE396-000CF)
??

## MSI, V341
Некоторые модели имеют видеовыходы отличающиеся от reference, "2 HDMI под DVI, 2 DP сбоку", поэтому тут тоже - нет совместимости с другими вендорами.
Конкретная модель карты MSI написана на текстолите как версия X.X после V341 VER. ШИМка IR3567B/up9505 и нестандартные нюансы видеовыходов представлено в списке ниже в соответствии с этим номером.
В биосе этот же номер представлен как последние 2 цифры после 341 в текстовой строке, начинающейся со 113. Строка отображается второй в резделе BIOS Internals в techpowerup. Т.е. 113-V34122 соответствует ver2.2. 


* V341 ver1.1,ver1.2 ШИМ IR3567B, но в отличии от reference оба порта под DVI-выходом, это HDMI (как на sapphire)
* V341 ver1.3,ver1.4 ШИМ up9505, 2HDMI как на sapphire
    * для 1.3 Samsung-B/H5GQ8H24MJR MS-V34113-F1, 113-MSITV341MH.613
    * для 1.4 Samsung-B/H5GQ8H24MJR/Micron-B "113-MSITV341MH.840" "113-MSITV341MH.841" - отличаются только EFI-частью
* V341 ver2.0,ver2.1 просто удлинённый Reference, ШИМ IR3567B, видеовыходы стандартные
* V341 ver2.2 ШИМ up9505, видеовыходы стандартные 
* V341 ver3.0 ШИМ ir35201, 2 HDMI (как на sapphire) - ни с чем не совместим (580 Gaming+, 180W, 2x8 PIN)
* V809-2258,V809-3428,V809-2657 - идентичны Reference


## Gigabyte
Самые сложные карты, ШИМки бывают up9505p и ir3567b, как отличить по биосу непонятно, надо следить что все фазы активировались в нагрузке.
Ниже частичная попытка классификации VBIOS для  Rx 570 Ganing

* GV-RX570GAMING-8GD/FF0/0AC5    125W 1750Mhz MT51J256M32HFB в биосе не прописано наличие DVI
* GV-RX570GAMING-8GD/FX0/078B     90W 1750Mhz K4G80325FB
* GV-RX570GAMING-8GD/FI1/0A2B    125W 1750Mhz H5GC8H24AJR_MI_PARTNER_GBT
* GV-RX570GAMING-8GD/FH0/0A9D    125W 1750Mhz MT51J256M32HFB - not activate IR phases, maybe desogned for up9505p
* GV-RX570GAMING-8GD/FA0/078E     90W 1750Mhz H5GQ8H24MJR_MI_PARTNER_GBT
* GV-RX570GAMING-8GD/F90/0757     90W 1750Mhz MT51J256M32HFB
* GV-RX570GAMING-8GD/F80/0753     90W 1750Mhz MT51J256M32HFB
* GV-RX570GAMING-8GD/F1/0763      90W 1750Mhz MT51J256M32HFB
* GV-RX570GAMING-8GD-MI/F80/073F  90W 1750Mhz MT51J256M32HF
* GV-RX570GAMING-8GD-MI/F7?/0739  90W 1750Mhz MT51J256M32HF(MI_PARTNER_GBT) activates 6 IR phases, MTP becomes like GV-RX570AORUS-4G
* GV-RX570GAMING-8GD-MI/F6*/0705  90W 1750Mhz MT51J256M32HFB
* GV-RX570GAMING-8GD-MI/F20/072F  90W 1750Mhz H5GC8H24MJR
* GV-RX570GAMING-8GD-MI/F11/072E  90W 1750Mhz K4G80325FB_MI_PARTNER_GBT
* GV-RX570GAMING-8GD-MI/F*/0704   90W 1750Mhz MT51J256M32HFB (TIC33423)

## Powercolor/Dataland
ШИМка всегда ir3567B, видеовыходы в биосе всегда стандартные. Для 6-фазных карт на ir3567B c Micron/Samsung рекомендуется VBIOS
* [RX580 2048SP GDDR5 256Mx32 8G J0112JAY.MLC 2019](https://www.techpowerup.com/vgabios/207832/207832) - 1310/1750Mhz 6phase ir3567B activates

## XFX/HIS
На картах с малым TDP ШИМка ncp81022, на картах с большим TDP шимка ir3567B.
* ncp81022 4 фазы + MT51J256M32HF/K4G80325FB: [113-47185MSF1-W91](https://www.techpowerup.com/vgabios/202074/202074)


## Прочее со всякой киатайщины
* 570-mic8g.bi - 125W micronA 1750. Fan 1500RPM by default. 6phase ir3567B activates
* rx58mt8gf2   - 145W micronA 1244/1750, rx580  -dont boot on ir3567B
* MIC400.BIN   - 120W micronA - no ir3567B phase activatin

## device ids из inf-файлов (пока не структурировано)
```
	(?? no driver) 1002-67DF-BDBD-A14C-C0 Blackmagic Radeon Pro 580 8 GB
	"Radeon RX 580 Series"         PCI\VEN_1002&DEV_67DF&REV_C1 HP/ASUS RX 580 Mobile, мало VBIOS
	"Radeon RX 570 Series"         PCI\VEN_1002&DEV_67DF&REV_C2 нет VBIOS
	"Radeon RX 580 Series"         PCI\VEN_1002&DEV_67DF&REV_C3 REF-вариант 580 для HP L39869-001, мало VBIOS
	"Radeon (TM) RX 480 Graphics"  PCI\VEN_1002&DEV_67DF&REV_C4 Dell RX 580 Mobile, 1 VBIOS (also C4 on basic rx480 with zeroes in VBIOS)
	"Radeon (TM) RX 470 Graphics"  PCI\VEN_1002&DEV_67DF&REV_C5 Dell RX 570 Mobile, мало VBIOS
	"Radeon RX 570 Series"         PCI\VEN_1002&DEV_67DF&REV_C6 нет VBIOS
	"Radeon (TM) RX 480 Graphics"  PCI\VEN_1002&DEV_67DF&REV_C7 много VBIOS, стандарная 480
	"Radeon (TM) RX 470 Graphics"  PCI\VEN_1002&DEV_67DF&REV_CF много VBIOS, стандарная 470
	"Radeon(TM) RX 470 Graphics"   PCI\VEN_1002&DEV_67DF&REV_D7 нет VBIOS
	"Radeon RX 470 Series"         PCI\VEN_1002&DEV_67DF&REV_E0 нет VBIOS
	"Radeon RX 590 Series"         PCI\VEN_1002&DEV_67DF&REV_E1 много VBIOS, стандарная 590
	"Radeon RX 590 Series"         PCI\VEN_1002&DEV_67DF&REV_E3 нет VBIOS
	"Radeon RX 580 Series"         PCI\VEN_1002&DEV_67DF&REV_E7 много VBIOS, стандарная 580
	"Radeon RX 570 Series"         PCI\VEN_1002&DEV_67DF&REV_EF много VBIOS, стандарная 570
	"Radeon RX 470 Series"         PCI\VEN_1002&DEV_67DF&REV_FF мало VBIOS 470D -> 560XT
	"Radeon RX P30PH"              PCI\VEN_1002&DEV_67DF&REV_F7 нет VBIOS

Vendors overriding in windows inf: 0x1028 (DELL), 0x103C (HP->Asus)
Asus 0533 - Asus mining led overrides 570 -> Asus 470 (4g & 8g (?))
Asus 0539 - 570 -> Asus 470 (?)
MSI  341E - 470->570 (Armor AC 4g & 8g(?))
PowerColor 560 - 470 -> 560 XT (4g)
XFX  9566 -   470 -> 560 XT
Sapphire A353-470 -> 560 XT (4g)
Sapphire A396-470 -> 560 XT (4g)
Sapphire F353-570 -> 580 -2048SP (4g)

Прошивка может сделать 6FDF из 67DF. Для 6FDF:
	"AMD Radeon RX590 GME"         PCI\VEN_1002&DEV_6FDF&REV_E7 стандарная 580 с прошивкой(?)
	"AMD Radeon RX 580 2048SP"     PCI\VEN_1002&DEV_6FDF&REV_EF, стандарная 570 с прошивкой
```