# K530 Firmware Reverse Engineering

This project is to reverse engineer the Redragon Draconic / K530 to get QMK running on it.
Use this information at your own risk. I'm not liable if you break something.

## Keyboard

* [Vendor Page](https://www.redragonzone.com/products/draconic-k530)
* [Firmware Download](https://cdn.shopify.com/s/files/1/2695/9506/files/Redragon_K530_Keyboard_f42e1632-df58-43b9-9b82-98bf6b4884d7.zip?v=1623053136)

![00000IMG_00000_BURST20210611194314804_COVER](https://user-images.githubusercontent.com/24465803/121808341-574a9680-cc2e-11eb-851e-3b0cd4b353b9.jpg)



## Tasks

- [x] Identify MCU `VS11K09A-1` / `Sonix SN32F248BF`
- [X] Find data sheet [VS11K09A-1](http://evision.net.cn/include/upload/kind/file/20190413/20190413174647_5965.pdf) / [Sonix SN32F248B](http://www.sonix.com.tw/files/1/9BB2674D32FB0D70E050007F01007532)
- [ ] Find SDK and dev tools
- [ ] Get SWD working
- [ ] Ability to flash firmware
- [ ] Get origional firmware
- [ ] Enable SWD in current firmware
- [ ] Get QMK firmware working
    - [ ] Basic keyboard functionality [Build Tools](https://docs.qmk.fm/#/getting_started_build_tools)
    - [ ] RGB Leds and animations `VSPW01` [RGB Matrix](https://docs.qmk.fm/#/feature_rgb_matrix)
    - [ ] Bluetooth `PAR2801QN-GHVC` [docs](https://docs.qmk.fm/#/feature_bluetooth)
- [ ] Dump origional bootloader

## Chips

* Main MCU - EVision [VS11K09A-1](http://evision.net.cn/include/upload/kind/file/20190413/20190413174647_5965.pdf), Seems to be based on the [Sonix SN32F248BF](http://www.sonix.com.tw/files/1/9BB2674D32FB0D70E050007F01007532)
* Bluetooth - ~!TON~ PXI Pixart PAR2801QN-GHVC
    * [FCC Doc](https://fccid.io/2AIPB-PAJ2801UA-40/User-Manual/Users-Manual-3083972) 
    * [PAR2801QN-GHVC](https://en.sziton.com/wp-content/uploads/datasheets/module/PAR2801-Q32P-datasheet-v1.2.pdf)
* ~LED driver~ Charging Chip - EVision [VSPW01](http://www.evision.net.cn/include/upload/kind/file/20190413/20190413175237_5340.pdf)

## LEDs

They seem to be driven by GPIO and transistors.
- [ ] Figure out pin map and matrix
- [ ] Caps lock LED

## Bluetooth

Appears to be an another ARM Cortex M0 MCU with UART and GPIO.
- [ ] SWD debugging
- [ ] Pin map to main MCU

## Extract default dk63 firmware.hex
1. Download [Resource Hacker](http://www.angusj.com/resourcehacker/) (Not sure of a mac or linux variant)
2. Download [Firmware Update tool](https://kmovetech.com/DIERYA%20&%20Kemove%20Wired%20mode%20firmware%20update.rar)
3. Extract the Firmware .rar and open the .exe in RH
4. Look for `RCData 4000:0`, this is the hex file of the firmware
5. Right click on `4000:0` and choose `Save Resource to BIN file`
6. Save the firmware so it can be examined or uplodaded.

## Firmware Flash
1. Download the USB MCU ISP [tool](http://www.sonix.com.tw/files/1/8226BAA772296B66E050007F010014EB)
2. Open the program and click load file.
3. Select `SN32F4xB` and then the firmware file.
4. The VID should alread be `0C45` and enter `766B` for the PID.
5. Click Start
6. Profit!

## Links
### Analyzing Keyboard Firmware
- https://mrexodia.github.io/reversing/2019/09/28/Analyzing-keyboard-firmware-part-1
- https://mrexodia.github.io/reversing/2019/09/28/Analyzing-keyboard-firmware-part-2
- https://mrexodia.github.io/reversing/2019/09/28/Analyzing-keyboard-firmware-part-3
