## EM7455/MC7455 - Modem Configuration
### Index
  * [Modem Performance/Specifications](#modem-performancespecifications)
  * [Official Sierra Documents/Firmwares (May require free Sierra account)](#official-sierra-documentsfirmwares-may-require-free-sierra-account)
  * [Which Modem to Buy](#which-modem-to-buy)
  * [Adapters and Antennas](#adapters-and-antennas)
  * [Create Accessible COM Port](#create-accessible-com-port)
  * [Manual Flashing Procedure (Linux)](#manual-flashing-procedure-ubuntu-linux-1804)
  * [Basic Setup](#basic-setup)
  * [Change Modem Identity (Sierra Wireless / Lenovo / Dell)](#change-modem-identity-sierra-wireless--lenovo--dell)
  * [Useful Commands/Info](#useful-commandsinfo)
  * [Connectivity/Router Options](#connectivityrouter-options)
  * [Additional References](#additional-references)

---
### Modem Performance/Specifications
+ The EM7455/MC7455 is a Category 6 LTE modem. It is capable of 300Mbps down and 50Mbps up.
+ Real world, you are unlikely to ever see much more than 230Mbps, even on Sprint Carrier Aggregation of Band 41+41 (40MHz total).
+ **These are my peak results so far (B2+B12, 30MHz total):**

	![Speed Test peak LTE Results](https://www.speedtest.net/result/7472005421.png)
+ Higher speeds will require a modem capable of 3CA (Three Carrier Aggregation) such as the [em7565](https://ltefix.com/shop/sierra-wireless-airprime-cards/sierra-wireless-em7565-cat-12-m-2-modem/)
    + EM7565 allows 3CA of B2+B12+B30 for a total downlink of 40MHz on approximately 60% of AT&T towers (Assuming you are close and have a strong signal).
    + LTEFix now offers the [em7565 pre-flashed to the latest firmware](https://ltefix.com/shop/sierra-wireless-airprime-cards/sierra-wireless-em7565-cat-12-m-2-modem/). If the process of flashing seems daunting, I suggest you purchase through them and pay for the flashing service as you will receive a modem already in a usable state.
    + **These are my peak results so far (B2+B12+B30, 40MHz total):**
    
    ![](http://www.speedtest.net/result/7543436236.png)![](http://www.speedtest.net/result/7545732497.png)
	    
---
### Official Sierra Documents/Firmwares (May require free Sierra account)
+ [Sierra EM7455 Product Page](https://source.sierrawireless.com/devices/em-series/em7455/)
+ [Sierra Wireless AirPrime EM74xx-MC74xx AT Command Reference (PDF)](https://source.sierrawireless.com/~/media/support_downloads/airprime/74xx/4117727_airprime_em74xx-mc74xx_at_command_reference_r3.ashx)
+ [AirPrime - EM7455 - Product Technical Specification (PDF)](https://source.sierrawireless.com/~/media/support_downloads/airprime/74xx/4116236%20airprime%20em7455%20product%20technical%20specification%20r13.ashx)
+ [All firmwares](https://source.sierrawireless.com/resources/airprime/minicard/74xx/airprime-em_mc74xx-approved-fw-packages/)
---
### Which Modem to Buy
+ For every use other than installing in a Lenovo \*70 Series.
    + ~$60 [Dell DW5811e em7455](https://www.ebay.com/sch/i.html?_from=R40&_nkw=DW5811e&_sacat=0&LH_BIN=1&_sop=15)
    + This model supports Bands 29 and 30, unlike the Lenovo.
    + When purchasing the Dell, I would recommend you get a production model. Engineering Samples will sometimes contain an early (SWI9X30C_00.08.02.00) firmware that can be a royal pain to flash due to `AT!BOOTHOLD` not being implemented.
    
    ![](https://i.imgur.com/Q9JdEIe.png)

+ For use in a [ThinkPad L470, L570, P51, P51s, P70, P71, T470, T470p, T470s, T570, TP25, X270](https://support.lenovo.com/cy/en/solutions/acc100362)
    + [~$90 EM7455 module (4XC0M95181 / 01AX746)](https://www.ebay.com/sch/i.html?_from=R40&_nkw=%284XC0M95181%2C01AX746%29&_sacat=0&LH_BIN=1&_sop=15)
    + This is required due to a Lenovo Firmware lock. If you get the less expensive 4XC0L59128, your T470 will not recognize it when installed in the WWAN slot.
    + Specs: https://download.lenovo.com/pccbbs/options_iso/tp_em7455_4g_lte_4xc0m95181.pdf
    
+ ~~For use in a [ThinkPad T460, T460s, T460p, T560, X260, X1 Carbon, L460, P50, P70](https://pcsupport.lenovo.com/cy/en/accessories/acc100290)~~
    + ~~[~$70 EM7455 module (4XC0L59128 / 00JT542):](https://www.ebay.com/sch/i.html?_from=R40&_nkw=%284XC0L59128%2C00JT542%2Clenovo+em7455%29&_sacat=0&LH_BIN=1&_sop=15)~~
    + ~~Specs: https://download.lenovo.com/pccbbs/options_iso/tp_em7455_4gltem_4xc0l59128.pdf~~
    + Do not waste your money on the Lenovo EM7455 (4XC0L59128 / 00JT542). It lacks Bands 29 and 30. If you get the Dell, you can change its identity according to my instructions and it will work in a Lenovo \*60 series. I currently have a DW5811e in my T460s.
---
### Adapters and Antennas
![](https://i.imgur.com/LjpCXCi.jpg)
+ **Get USB adapter with SIM slot for modem**
    + $26, shipped from Texas. Includes small 3dBi antennas.
        + [USB To NGFF M.2 Key B Adapter Enclosure With SIM Card Slot](https://ltefix.com/shop/pcie-m-2/usb-to-ngff-m-2-key-b-adapter-enclosure/)
+ **If you are at the edge of coverage and need something better, look for 700-2700 MHz antennas with SMA connectors.**
	+ Buy some [$0.75 SMA Female To RP-SMA Male Adapters](https://www.ebay.com/itm/RP-SMA-Male-Plug-to-SMA-Female-Jack-Straight-RF-Coax-Adapter-Convertor-Connector/181974337700) if you buy antennas, just to be sure you can use what you get.
		+ SMA vs RP-SMA, [learn the difference](https://www.getfpv.com/rf-rp-sma-male-to-sma-female-adapter.html)
	+ Log-Periodic antennas offer excellent gain for a low cost and small footprint.
		+ [$29 698-2700MHz Yagi Radome 9dBi-11dBi 4G LTE Directional Antenna](https://ltefix.com/shop/antennas/outdoor-antennas/698-2700mhz-yagi-radome-9dbi-11dbi-4g-lte-directional-antenna/)
	+ Omni-Antennas can boost overall signal if you already have decent service and just want great service.
		+ While not explicitly tuned to Band 12/13/17, a pair of [2.4GHz 9dBi RP-SMA Antennas](https://www.ebay.com/itm/2-4GHz-9dBi-RP-SMA-Male-Connector-Tilt-Swivel-Wireless-WiFi-Router-Antenna-O9W4/253375536787) will provide a nice signal boost.
		
---
### Create Accessible COM Port
##### My [Automated Flashing of the EM7455/MC7455 with a Ubuntu Linux 18.04 LiveCD](https://www.ttl.one/2018/07/sierra-wireless-lte-autoflashing-em74xx.html) script will complete this task.

+ Option 1: Use my [automatic script to do all configuration](https://github.com/danielewood/sierra-wireless-modems/blob/master/autoflash-7455.sh). This will change any of the Dell/Lenovo/Generic modems to Generic MBIM with AT ports and update the firmware to the newest version. 
    + WARNING: Only for use with an external USB enclosure.
    + Create a Bootable LiveCD/LiveUSB Ubuntu 18.04
    + Run my script, follow on screen instructions.
+ Option 2: [Sierra Wireless MC7455 | EM7455 -- AT! Command Guide](https://ltehacks.com/viewtopic.php?t=33)
    + Use Putty instead of the Huawei program
+ Option 3: [Sierra Wireless EM7455: How to enable COM ports](https://zukota.com/sierra-wireless-em7455-how-to-enable-com-ports/)
    + Use Rufus to write the Ubuntu image, if it asks, use `dd` mode.		

---
### Manual Flashing Procedure (Ubuntu Linux 18.04)
1. Install libqmi-utils version 1.20 (It is not yet in the main repositories)
    + `wget http://security.ubuntu.com/ubuntu/pool/universe/libq/libqmi/libqmi-utils_1.20.0-1ubuntu1_amd64.deb`
    + `dpkg -i libqmi-utils_1.20.0-1ubuntu1_amd64.deb`
    + `wget http://security.ubuntu.com/ubuntu/pool/main/libq/libqmi/libqmi-glib5_1.20.0-1ubuntu1_amd64.deb`
    + `dpkg -i libqmi-glib5_1.20.0-1ubuntu1_amd64.deb`
    + `wget http://security.ubuntu.com/ubuntu/pool/main/libq/libqmi/libqmi-proxy_1.20.0-1ubuntu1_amd64.deb`
    + `dpkg -i libqmi-proxy_1.20.0-1ubuntu1_amd64.deb`
    + `wget http://security.ubuntu.com/ubuntu/pool/universe/libq/libqmi/libqmi-utils_1.20.0-1ubuntu1_amd64.deb`
    + `dpkg -i libqmi-utils_1.20.0-1ubuntu1_amd64.deb`
2. Get the [latest firmware bundle](#official-sierra-documentsfirmwares-may-require-free-sierra-account) from Sierra Wireless.
    + `curl -o SWI9X30C_02.30.01.01_Generic_002.045_000.zip -L https://source.sierrawireless.com/~/media/support_downloads/airprime/74xx/fw/02_30_01_01/7455/swi9x30c_02.30.01.01_generic_002.045_000.ashx`
3. Extract firmware CWE and NVU.
    `unzip SWI9X30C_02.30.01.01_Generic_002.045_000.zip`
4. Stop Modem Manager
    `systemctl stop ModemManager`
5. Flash firmware
    ```
    deviceid=`lsusb | grep -i -E '1199:9071|1199:9079|413C:81B6' | awk '{print $6}'`
    qmi-firmware-update --update -d "$deviceid" SWI9X30C_02.30.01.01.cwe SWI9X30C_02.30.01.01_GENERIC_002.045_000.nvu
    ```
6. Modem will reset with new firmware and carrier profile.

---
### Basic Setup
##### My [Automated Flashing of the EM7455/MC7455 with a Ubuntu Linux 18.04 LiveCD](https://www.ttl.one/2018/07/sierra-wireless-lte-autoflashing-em74xx.html) script will complete this task.
1. Enable Advanced Commands:
    + `AT!ENTERCND="A710"`
2. Set preferred image to GENERIC (Will error if Generic does not exist)
    + `AT!IMPREF="GENERIC"`
3. Set Interface bitmask to 0000100D (diag,nmea,modem,mbim). [This is the same as USBCOMP=8](https://zukota.com/sierra-wireless-em7455-how-to-enable-com-ports/).
    + `AT!USBCOMP=1,1,0000100D`
4. Set LTE Only (Disables UMTS/HSDPA/3G fallback, which you probably dont want)
    + `AT!SELRAT=06`
5. Set Modem to use all available bands (Dont hide any bands)
    + `AT!BAND=00`
6. Save settings and reboot modem to apply
    + `AT!RESET`


### EM7565 Basic Setup
1. Enable Advanced Commands:
    + `AT!ENTERCND="A710"`
2. Set preferred image to GENERIC (Will error if Generic does not exist)
    + `AT!IMPREF="GENERIC"`
3. Set Interface bitmask to 0000100D (diag,nmea,modem,mbim).
    + `AT!USBCOMP=1,3,0000100D`
4. Set LTE Only (Disables UMTS/HSDPA/3G fallback, which you probably dont want)
    + `AT!SELRAT=06`
5. Set Modem to use all available LTE bands (Dont hide any bands)
    + `AT!BAND=00`
    + `AT!BAND=09`
6. Save settings and reboot modem to apply
    + `AT!RESET`
---
### EM7565 ROOter Setup
#### For GoldenOrb 2017-12-15 Release
+ Run the following AT commands to set to LTE only, and set the USB Composition to something that works with ROOter.
```
AT!ENTERCND="A710"
AT!BAND=00
AT!BAND=09
AT!SELRAT=06
AT!USBCOMP=1,3,100D
AT!RESET
```
+ Run the following from SSH:
```
# Replace hooks for AirCard 340U (if you use a 340U, use PID 9041 as your sacrificial PID):
sed -i 's/ 9051 / 9091 /g' /usr/lib/rooter/connect/create_connect.sh
# Insert PID for EM7455 on every boot:
sed -i '$s%^exit 0%echo "1199 9091" > /sys/bus/usb-serial/drivers/option1/new_id\nexit 0\n%' /etc/rc.local
# Insert PID for EM7455 on immediately:
echo "1199 9091" > /sys/bus/usb-serial/drivers/option1/new_id
```
---
### Change Modem Identity (Sierra Wireless / Lenovo / Dell)
##### My [Automated Flashing of the EM7455/MC7455 with a Ubuntu Linux 18.04 LiveCD](https://www.ttl.one/2018/07/sierra-wireless-lte-autoflashing-em74xx.html) script will complete this task.

1. Enable Terminal Echo
    ```
    ATE1
    ```
2. Enable Advanced Commands:
    ```
    AT!ENTERCND="A710"
    ```
3. Record current settings so you can revert if needed.
    ```
    AT!USBVID?
    AT!USBPID?
    AT!USBPRODUCT?
    AT!PRIID?
    ```
    Note the Carrier PRI, we'll use that below.
    ```
    Carrier PRI: 9999999_9904609_SWI9X30C_02.24.05.06_00_GENERIC_002.026_000
    PRI Part Number: 9904609
    Revision: 002.026
    Customer: Generic-Laptop
    ```
4. Change Modem Identity (Generic, Lenovo, or Dell)
    Change Modem into a Generic Sierra Wireless em7455/mc7455
    ```
    AT!USBVID=1199
    AT!USBPID=9071,9070
    AT!USBPRODUCT="EM7455"
    AT!PRIID="9904609","002.026","Generic-Laptop"
    ```
    Change Modem into a Lenovo em7455/mc7455 (Use this if installing in a Lenovo)
    ```
    AT!USBVID=1199
    AT!USBPID=9079,9078
    AT!USBPRODUCT="Sierra Wireless EM7455 Qualcomm Snapdragon X7 LTE-A"
    AT!PRIID="9904609","002.026","Lenovo-Storm"
    ```
    Change Modem into a Dell DW5811e em7455/mc7455
    ```
    AT!USBVID=413C
    AT!USBPID=81B6,81B5
    AT!USBPRODUCT="Dell Wireless 5811e Gobi(TM)4G LTE Mobile Broadband Card"
    AT!PRIID="9904609","002.026","DELL"
    ```
5. Save settings and reboot modem to apply
    ```
    AT!RESET
    ```
---
### Flash using Sierra Wireless Linux Flashing Tool (fwdwl-lite)
+ [Moved to dedicated page](https://github.com/danielewood/sierra-wireless-modems/blob/master/Sierra-Linux-QMI-SDK.md).
---
### Flash modem stuck in QDLoader mode using qmi-firmware-update
+ For qmi-firmware-update does not work with the 75xx series. [Use this procedure instead](https://github.com/danielewood/sierra-wireless-modems/blob/master/Sierra-Linux-QMI-SDK.md#em7565-stuck-in-qdloader).
```
deviceid=`lsusb | grep -i -E '1199:9070|1199:9078|413C:81B5' | awk '{print $6}'`
qmi-firmware-update --update-qdl -d "$deviceid" SWI9X30C_02.24.05.06.cwe SWI9X30C_02.24.05.06_GENERIC_002.026_000.nvu
```

---
### Useful Commands/Info
Enable Terminal Echo
```
ATE1
```
---
Enable Advanced Commands:
```
AT!ENTERCND="A710"
```
---
Clear all Carrier Preferences/Firmwares other than current(You will want to flash the modem after this):
```
AT!IMAGE?
AT!IMAGE=0
AT!RESET
```
AT!IMAGE=?
```
AT!IMAGE=<op>[,<type>[,<slot>[,"<build_id>","<unique_id>"]]]
op   - 0:delete 1:list 2:get max num images
type - 0:FW 1:CONFIG
slot - FW slot index - none implies all slots
AT!IMAGE?[<op>[,<type>]]
```
Selectively Clear Firmwares:
+ Example: Delete (0), FW (0), Slot (3)

```
AT!ENTERCND="A710"
AT!IMAGE=0,0,3
AT!RESET
```
---
Clear all changes and restore to (Lenovo/Sierra) factory settings:
```
AT!ENTERCND="A710"
AT!RMARESET=1
AT!RESET
```
Clear all changes and restore to (Dell) factory settings:
```
AT!ENTERCND="A710"
AT!NVRESTORE=0
AT!RESET
```
---
[Lock LTE Bands](https://ltehacks.com/viewtopic.php?t=33) (Pick one)
```
AT!BAND=10,"B2 (1900)",0,0000000000000002
AT!BAND=10,"B4 (1700/2100)",0,0000000000000008
AT!BAND=10,"B5 (850)",0,0000000000000010
AT!BAND=10,"B12 (700)",0,0000000000000800
AT!BAND=10,"B2B4",0,000000000000000A
AT!BAND=10,"B2B4B5B12",0,000000000000081A
````
Set Band Lock:
```
AT!BAND=10
```
Clear Band Lock:
```
AT!BAND=00
```
---
`AT!LTEINFO?`
```
!LTEINFO: 
Serving:   EARFCN MCC MNC   TAC      CID Bd D U SNR PCI  RSRQ   RSRP   RSSI RXLV
              800 310 410 35666 0A14666A  2 5 5  22 404 -14.1  -79.6  -45.5 --

IntraFreq:                                          PCI  RSRQ   RSRP   RSSI RXLV
                                                    404 -14.1  -79.6  -45.5 --
                                                    402 -20.0  -89.3  -57.6 --

InterFreq: EARFCN ThresholdLow ThresholdHi Priority PCI  RSRQ   RSRP   RSSI RXLV
             5110            0           0        0 272 -12.1  -80.9  -50.6   0
```
---
Show available Carrier Aggregations for your modem:
```
AT!LTECA?
Hardware:
LTEB1: B8, 
LTEB2: B2, B5, B12, B13, B29, 
LTEB3: B7, B20, 
LTEB4: B4, B5, B12, B13, B29, 
LTEB5: B2, B4, B30, 
LTEB7: B3, B7, B20, 
LTEB8: B1, 
LTEB12: B2, B4, B30, 
LTEB13: B2, B4, 
LTEB20: B3, B7, 
LTEB25: 
LTEB26: 
LTEB29: 
LTEB30: B5, B12, B29, 
LTEB41: B41,

Permitted Bands:
Empty

Prune_ca_combos:
Empty

AT!LTECA=?
!LTECA=<flag>
<flag>: 0 – disable CA
	1 – enable CA
```
---
`AT!GSTATUS?`
```
!GSTATUS: 
Current Time:  22016		Temperature: 40
Reset Counter: 1		Mode:        ONLINE         
System mode:   LTE        	PS state:    Attached     
LTE band:      B2     		LTE bw:      20 MHz  
LTE Rx chan:   800		LTE Tx chan: 18800
LTE CA state:  ACTIVE      		LTE Scell band:B12    
LTE Scell bw:10 MHz  		LTE Scell chan:5110
EMM state:     Registered     	Normal Service 
RRC state:     RRC Connected  
IMS reg state: No Srv  		

PCC RxM RSSI:  -45		RSRP (dBm):  -81
PCC RxD RSSI:  -44		RSRP (dBm):  -79
SCC RxM RSSI:  -52		RSRP (dBm):  -83
SCC RxD RSSI:  -51		RSRP (dBm):  -81
Tx Power:      15		TAC:         8C65 (35666)
RSRQ (dB):     -14.0		Cell ID:     0A14666A (169106666)
SINR (dB):     23.8
```
---
```
AT!HWID?
Revision: 0.5
```
---
### Connectivity/Router Options
+ Windows 10 will block Hotspot/ICS mode, you cannot use Windows 10's ICS with this setup.
+ Linux doesn't care, it will happily route packets all day long. 
+ If you want a dead-simple setup:
    + Get a [router from this list](https://www.ofmodemsandmen.com/routers.html)
    + Install [ROOter (AKA LEDE/OpenWRT)](https://www.ofmodemsandmen.com/firmware.html)
    + Punch in the APN "broadband"
    + Done
    
    ![](https://i.imgur.com/Gd0s1kJ.png)

---
### Free Over-the-Air Updates
+ [Sierra AirVantage FOTA](https://source.sierrawireless.com/airvantage/fota/)
    + Use your name as Business Name
+ Get Modem FSN + IMEI with `ATI`
+ [Change Modem Settings](https://source.sierrawireless.com/airvantage/av/reference/register/howtos/configure-FXT-GL-AirPrime-ForAV/)
    + `AT+WDSC=3,x`(x being the frequency of connection in minutes)
    + `AT+WDSS=1,1` (Sends initial heartbeat immediately)

---
### Additional References: 

+ Must tape over USB3 pins on MC74XX:
    + https://techship.com/faq/sierra-wireless-mc74-series-module-is-not-detected-by-the-operating-system/
+ Sierra Wireless MC7455 | EM7455 -- AT! Command Guide
    + https://ltehacks.com/viewtopic.php?t=33
+ Routers Supported by ROOter
    + https://www.ofmodemsandmen.com/routers.html
+ BPlus USB 3.0 Enclosure for M2 B Key with SIM
    + http://www.hwtools.net/Adapter/USB3M2%20Series.html#Web-shop- 
+ ROOter development thread
    + http://forums.whirlpool.net.au/archive/2689577
+ Zukota on enabling COM ports
    + https://zukota.com/sierra-wireless-em7455-how-to-enable-com-ports/
+ ROOter Sierra FAQ
    + http://whirlpool.net.au/wiki/sierra_advanced
+ Interesting AT Command Utility GUI, have not tried it.
    + http://m2msupport.net/m2msupport/download-at-command-tester/
+ Mikrotik specific: 
    + http://whirlpool.net.au/wiki/wiki_rooter_pg5
+ pfSense (QMI, wont work without successful decode of engineer mode)
    + https://forum.netgate.com/topic/110135/sierra-wireless-airprime-em7455-support/5
+ Engineer Mode Decoder
    + https://github.com/bkerler/SierraWirelessGen
    + https://forum.sierrawireless.com/t/em7455-deactivate-low-power-mode/8620/15
+ Ubuntu fix apt-get on LiveCD
    + https://askubuntu.com/questions/378558/unable-to-locate-package-while-trying-to-install-packages-with-apt#481355
+ ROOTer enable fcc auth with QMI command
    + Todo: Lookup sending AT Commands with uqmi
    + `/lib/netifd/proto/mbim.sh: uqmi $DBG -m -d $device --fcc-auth`
+ Using uqmi commands:
    + http://tiebing.blogspot.com/2015/03/linux-running-4g-lte-modem.html
+ Git Repo for uqmi
    + https://git.openwrt.org/project/uqmi.git
+ MC7700 flashing by Mork
    + http://whrl.pl/Rfbxjc
+ SpeedFusion connection bonding with VPS
    + http://whrl.pl/Re9nIw
+ Long Range Custom Yagi Setups
    + https://ltehacks.com/viewtopic.php?f=24&t=71
+ LTE Modulations, Bandwidths, and Datarates:
    + https://frankrayal.com/2011/06/27/lte-peak-capacity/
+ Understanding LTE Signal Strength Values
    + http://usatcorp.com/faqs/understanding-lte-signal-strength-values/
   
