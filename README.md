# RobotDyn_UNO-Wifi_hasznalata

Nagyon sokan panaszkodnak, hogy nem tudják használni ennek a mikrovezérlőnek a Wifijét (ESP-03), vagyis annak beállításait, ezért írtam ezta cikket. A gond ott gyökeredzik, hogy magát az ESP modult nem ismerik a felhasználók. Ennél a modulnál a firmware -t a GPIO0 láb GND(-) -ra kötésével tehetjük meg. Míg amikor csak használjuk, le kell róla csatlakoztatnunk. Ennél a modulnál kényelmesen egy gomb van erre a célra kialakítva, amit ki-be kapcsolhatunk, attól függően, hogy mit szeretnénk csinálni. Én különösen megszerettem ezt a modult, mert az ESP moduljának öt ki/be lába van (GPIO16, GPIO12, GPIO04 GPIO02, GPIO0), ami sokszor nagyon jól jön. Továbbá lehetőség van egyszerre Arduinót és MicroPythont használni ugyanazon a modulon.
A firmware ráírására szükség lesz az esptool.py alkalmazásra, amit innen tudsz letölteni: https://github.com/espressif/esptool és a Pythonra, mert nélküle nem lehet használni az esptool.py -t, amit pedig innen tölthető le:https://www.python.org/downloads/ .
> Használati gyorstalpaló:

1. Ha csak az UNO-t szeretnénk használni billentsük ON felé a 3. és 4. gombot, a többit pedig az OFF felé,
2. Amikor a firmware-t szeretnénk ráírni az ESP -re az 5., 6., 7. és a 8. gombot ON felé, a többit OFF irányába,
A parancssorban (promtban) az esptool.py segitségével írassuk ki az ESP paramétereit a következő paranccsal: **"esptool.py flash_id"**. 

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
Utána töltsük le a az aktuális firmware-t a hivatalos ESPRESSIF oldaláról: https://www.espressif.com/en/support/download/at , vagy az én repoziomból: https://github.com/arnoldrobert/Flash-ESP-01-firmware/raw/master/v1.3.0.2_AT_Firmware.bin .

3. Ha csak az AT parancsokat szeretnénk próbálgatni, akkor 6. és 7. gombot ON felé, a többit OFF irányba,
4. Az Arduinoval szeretnénk vezérelni az ESP -t akkor 3., 4., 5. és 6. gombot ON felé, a többit OFF irányba,
5. Végül ha csak a wifit szeretnénk használni akkor az 1. és 2. gombot ON felé, a többit kikapcsolni.
