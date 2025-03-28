# RobotDyn_UNO+Wifi_hasznalata

Nagyon sokan panaszkodnak arra, hogy nem tudják használni ennek a mikrovezérlőnek a Wifijét (ESP-03), vagyis annak beállításait, ezért írtam ezt a cikket. A gond ott gyökerezik, hogy magát az ESP modult nem ismerik a felhasználók. Ennél a modulnál a firmware-t a GPIO0 láb GND(-)-ra kötésével tehetjük meg. Míg amikor csak használjuk, le kell róla csatlakoztatnunk. Ennél a modulnál kényelmesen egy gomb van erre a célra kialakítva, amit ki-be kapcsolhatunk, attól függően, hogy mit szeretnénk csinálni. Én különösen megszerettem ezt a modult, mert az ESP moduljának öt ki/be lába van (GPIO16, GPIO12, GPIO04 GPIO02, GPIO0), ami sokszor nagyon jól jön. Továbbá lehetőség van egyszerre Arduinot és MicroPythont használni ugyanazon a modulon.
A firmware ráírására szükség lesz az esptool.py alkalmazásra, amit innen tudsz letölteni: https://github.com/espressif/esptool és a Pythonra, mert nélküle nem lehet használni az esptool.py-t, amit pedig innen tölthető le:https://www.python.org/downloads/ .
> Használati gyorstalpaló:

1. Ha csak az UNO-t szeretnénk használni billentsük ON felé a 3. és 4. gombot, a többit pedig az OFF felé,
2. Amikor a firmware-t szeretnénk ráírni az ESP -re az 5., 6., 7. és a 8. gombot ON felé, a többit OFF irányába,

A parancssorban (promtban) az esptool.py segítségével írassuk ki az ESP paramétereit a következő paranccsal: **"esptool.py flash_id"**. 

Valami ehhez hasonlót kell, hogy kiírjon:
```
C:\Users\petof>esptool.py flash_id
esptool.py v3.0-dev
Found 1 serial ports
Serial port COM4
Connecting....
Detecting chip type... ESP8266
Chip is ESP8266EX
Features: WiFi
Crystal is 26MHz
MAC: 60:01:94:0c:dc:1b
Uploading stub...
Running stub...
Stub running...
Manufacturer: c8
Device: 4014
Detected flash size: 1MB
Hard resetting via RTS pin...
```
Ki-be kapcsoljuk minden parancs között a modult. Most törölnünk kell a flash-t a következő paranccsal: **"esptool.py erase_flash"** .
Utána töltsük le az aktuális firmware-t a hivatalos ESPRESSIF oldaláról: https://www.espressif.com/en/support/download/at , vagy az én repozitomból: https://github.com/arnoldrobert/Flash-ESP-01-firmware/raw/master/v1.3.0.2_AT_Firmware.bin , és írjuk rá az ESP-re a következő paranccsal: **"esptool.py --port COM4 --baud 74880 --no-stub write_flash -fs 1MB -fm qio 0x0 v1.3.0.2_AT_Firmware.bin"** .

3. Ha csak az AT parancsokat szeretnénk próbálgatni, akkor 5. és 6. gombot ON felé, a többit OFF irányba kapcsoljuk.
Nyissunk meg egy üres Arduino file-t, állítsuk be a COM portot, majd lépjünk a Serial Monitorba, a baud-ot tegyük 115200 -ra, és írjuk a be következő parancsot: **"AT+GMR"** . Használhatunk más UART-ot támogató serial monitort a soros kommunikációra pl. a PuTTY-t is.

Ezt fogja kiírni:
```
AT+GMR

AT version:0.40.0.0(Aug  8 2015 14:45:58)
SDK version:1.3.0
Ai-Thinker Technology Co.,Ltd.
Build:1.3.0.2 Sep 11 2015 11:48:04
OK
```
Innen tudod az AT parancsokat letölteni: https://www.espressif.com/sites/default/files/documentation/4a-esp8266_at_instruction_set_en.pdf .

4. Amikor az Arduinoval szeretnénk vezérelni az ESP-t akkor 3. és 4. gombot ON felé, a többit OFF irányba kapcsoljuk. A modulon lévő ESP lábak közül keressük meg a Tx és az Rx-et. Ezeket majd a programban megadott Arduino digitális lábakhoz kell kötni. A Tx lábat közvetlenül csatlakoztathatjuk az Arduino digitális lábára, mig az Rx-et feszültségosztón kersztül csatlakoztassuk, mivel az Arduino 5V-ot míg az ESP 3.3V-ot használ. A feszültségosztó kapcsolási rajza a file-ok között van. Ezen az oldalon magyarázattal és Arduino kóddal találtok példákat: http://allaboutee.com/2015/01/02/esp8266-arduino-led-control-from-webpage/ .

> MicroPython firmware ráírása az ESP-re.

A második lépést kell megismételni: az esptool.py segítségével törölni kell a flash-t **"esptool.py erase_flash"**, majd ráírni az új MicroPython firmware-t, amit innen lehet letölteni http://micropython.org/download#esp8266 , a következő paranccsal: **"esptool.py --port COM4 --baud 74880 --no-stub write_flash -fs 1MB -fm qio 0x0 esp8266-20190529-v1.11.bin"** .
