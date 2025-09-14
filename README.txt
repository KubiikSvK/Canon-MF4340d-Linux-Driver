Canon MF4340d Linux Driver (Jakub Edition)
==========================================

Verze: 1.0
Autor: Jakub Kubiik (KubiikSvK)
E-mail: jvanek23@gmail.com
GitHub: https://github.com/KubiikSvK

Účel:
------
Tento filtr byl vytvořen pro zprovoznění tiskárny Canon MF4340d na moderních verzích Linuxu,
zejména Ubuntu 24.04 LTS. Cílem bylo umožnit síťový tisk přes USB připojení na routeru Apple AirPort Extreme
a případné nasazení na server pro tisk z webu nebo e-mailu.

Sestavení:
-----------
Filtr pstoufr2cpca byl zkompilován na systému:
- Ubuntu 24.04.3 LTS (noble)
- Kernel: 6.8.0-79-generic
- Architektura: x86_64
- GCC: 13.3.0
- Make: 4.3

Použité zdroje:
---------------
- linux-UFRII-drv-v610-m17n-03.tar.gz (Canon verze 6.10) — nainstalováno pomocí install.sh
- o151en_linux_UFRII_v310.zip (Canon verze 3.10) — ručně rozbaleno, použity zdrojové soubory:
  pstoufr2cpca, buftool, buflist.h, libbuftool.a

Instalace:
----------
1. Nainstalujte závislosti:
   sudo apt install cups libcups2 libcups2-dev libcupsimage2 libcupsimage2-dev

2. Stáhněte balíček:
   wget https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/releases/download/v1.0/jakub-mf4340d-driver.deb

3. Nainstalujte balíček:
   sudo dpkg -i jakub-mf4340d-driver.deb
   sudo systemctl restart cups

4. Přidejte tiskárnu přes CUPS (http://localhost:631):
   - URI: socket://<IP_ADRESA_TISKÁRNY>:9100
   - Ovladač: Canon MF4320-4350 UFRII LT

Test:
-----
Filtr lze otestovat ručně:
   /usr/lib/cups/filter/pstoufr2cpca 1 testprinter "" 1 "" testfile.ps > /dev/null

Chyby sledujte v /var/log/cups/error_log

Kontakt:
--------
Chyby a bugy hlaste prosím přes GitHub Issues nebo e-mailem.
Používejte na vlastní riziko. Žádná záruka.

==============================

Canon MF4340d Linux Driver (Jakub Edition)
==========================================

Version: 1.0
Author: Jakub Kubiik (KubiikSvK)
Email: jvanek23@gmail.com
GitHub: https://github.com/KubiikSvK

Purpose:
--------
This filter was created to enable the Canon MF4340d printer to work on modern Linux distributions,
especially Ubuntu 24.04 LTS. The goal was to allow network printing via USB connected to an Apple AirPort Extreme router,
and optionally deploy the printer on a server for printing from web apps or email.

Build Info:
-----------
The pstoufr2cpca filter was compiled on:
- Ubuntu 24.04.3 LTS (noble)
- Kernel: 6.8.0-79-generic
- Architecture: x86_64
- GCC: 13.3.0
- Make: 4.3

Sources Used:
-------------
- linux-UFRII-drv-v610-m17n-03.tar.gz (Canon v6.10) — installed using install.sh
- o151en_linux_UFRII_v310.zip (Canon v3.10) — manually unpacked, used source files:
  pstoufr2cpca, buftool, buflist.h, libbuftool.a

Installation:
-------------
1. Install dependencies:
   sudo apt install cups libcups2 libcups2-dev libcupsimage2 libcupsimage2-dev

2. Download the package:
   wget https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/releases/download/v1.0/jakub-mf4340d-driver.deb

3. Install the package:
   sudo dpkg -i jakub-mf4340d-driver.deb
   sudo systemctl restart cups

4. Add printer via CUPS (http://localhost:631):
   - URI: socket://<PRINTER_IP>:9100
   - Driver: Canon MF4320-4350 UFRII LT

Testing:
--------
You can test the filter manually:
   /usr/lib/cups/filter/pstoufr2cpca 1 testprinter "" 1 "" testfile.ps > /dev/null

Check errors in /var/log/cups/error_log

Contact:
--------
Please report bugs via GitHub Issues or email.
Use at your own risk. No warranty.