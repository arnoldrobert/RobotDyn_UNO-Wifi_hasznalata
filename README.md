# RobotDyn_UNO-Wifi_hasznalata

Nagyon sokan panaszkodtak, hogy nem tudják használni ennek a mikrovezérlőnek a Wifijét (ESP-01), vagyis annak beállításait, ezért írtam ezta cikket. A gond ott gyökeredzik, hogy magát az ESP-01 modult nem ismerik a felhasználók. Az ESP -él a firmware -t a GPIO0 láb GND(-) -ra kötésével tehetjük meg. Míg amikor csak használjuk, akkor le kell róla csatlakoztatnunk. Ennél a modulnál kényelmesen egy gomb van erre a célra kialakítva, amit ki-be kapcsolhatunk, attól függően, hogy mit szeretnénk csinálni vele. Én különösen megszerettem ezt a modult, mert az ESP-nek négy ki/be lába van (GPIO16, GPIO12, GPIO04 GPIO02), ami sokszor nagyon jól jön. Továbbá lehetőségem van egyszerre Arduinót és MicroPythont használni ugyanazon a modulon, amit be is szeretnék mutatni.

Használati gyorstalpaló:
1. Ha csak az UNO-t szeretnénk használni billentsük ON felé a 3. és 4. lábat,
2. 
