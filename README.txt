Jakub MF4340d Driver v1.0
--------------------------
Tento balíček obsahuje ručně zkompilovaný filtr pstoufr2cpca pro tiskárnu Canon MF4340d.

Systém: Ubuntu 24.04
Postup:
- Kompilace z cndrvcups-lb + cndrvcups-common-3.40
- Připojení buflist.h, buftool.c, buflist.c
- Vytvoření libbuftool.a
- Linkování s libcups

Instalace:
sudo dpkg -i jakub-mf4340d-driver.deb
sudo systemctl restart cups

Přidání tiskárny:
- URI: socket://IP_ADRESA_TISKÁRNY:9100
- Ovladač: Canon MF4320-4350 UFRII LT
