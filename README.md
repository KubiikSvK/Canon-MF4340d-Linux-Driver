# 🖨️ Canon MF4340d Linux Driver (Jakub Edition)

## 🇨🇿 Česká verze

### 🎯 Účel projektu
Tento projekt vznikl jako praktické řešení pro zprovoznění tiskárny **Canon MF4340d** na moderních verzích Linuxu, zejména Ubuntu 24.04 LTS. Canon neposkytuje aktuální ovladače pro nové distribuce, což znemožňuje běžné použití této tiskárny.

Cílem bylo:

- Zprovoznit tiskárnu připojenou přes **USB na routeru Apple AirPort Extreme** pro **síťové použití**
- Umožnit **nasazení na server**, který by tiskárnu zpřístupnil pro tisk z webových aplikací nebo e-mailu
- Zkompilovat funkční filtr `pstoufr2cpca` ze starších Canon zdrojů
- Vytvořit `.deb` balíček pro snadnou instalaci
- Umožnit bezproblémový tisk přes CUPS bez nutnosti ručních zásahů

Projekt je určen pro domácí i kancelářské prostředí, kde je MF4340d stále funkční, ale chybí podpora ze strany výrobce.

---

### 📦 Popis
Tento repozitář obsahuje ručně zkompilovaný filtr `pstoufr2cpca` pro tiskárnu **Canon MF4340d**, který umožňuje její provoz na moderních distribucích Linuxu.

---

### 🛠️ Sestavení

Balíček byl sestaven na následujícím systému:

- **Distribuce:** Ubuntu 24.04.3 LTS (codename: noble)
- **Kernel:** Linux 6.8.0-79-generic
- **Architektura:** x86_64
- **GCC:** 13.3.0
- **Make:** GNU Make 4.3

#### 🔗 Použité zdroje Canon

Projekt využívá části z oficiálních ovladačů Canon:

- **UFR II/UFRII LT Printer Driver for Linux V6.10**  
  [Canon MF4340d – verze 6.10](https://www.canon-europe.com/support/consumer/products/printers/i-sensys/mf-series/i-sensys-mf4340d.html?type=drivers&detailId=tcm:13-1506758&productTcmUri=tcm:13-726815)  
  → Tato verze byla **nainstalována celá** pomocí dodaného skriptu `install.sh`

- **UFRII/UFRII LT Printer Driver for Linux v3.10**  
  [Canon MF4340d – verze 3.10](https://www.canon-europe.com/support/consumer/products/printers/i-sensys/mf-series/i-sensys-mf4340d.html?type=drivers&detailId=tcm:13-1331911&productTcmUri=tcm:13-726815)  
  → Tato verze byla **ručně rozbalena** a byly z ní **extrahovány zdrojové soubory**:
  - `pstoufr2cpca`
  - `buftool`, `buflist.h`, `libbuftool.a`

Tyto části byly následně zkompilovány a zabaleny do `.deb` balíčku.

---

### 📋 Závislosti

Před instalací se ujistěte, že máte nainstalováno:

```bash
sudo apt update
sudo apt install cups libcups2 libcups2-dev libcupsimage2 libcupsimage2-dev
```

---

### 📥 Instalace ovladače

Pokud nemáte `.deb` balíček lokálně, můžete ho stáhnout pomocí:

```bash
wget https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/releases/download/v1.0/jakub-mf4340d-driver.deb
```

Poté nainstalujte:

```bash
sudo dpkg -i jakub-mf4340d-driver.deb
sudo systemctl restart cups
```

---

### 🖨️ Přidání tiskárny v CUPS

1. Otevřete webové rozhraní CUPS:
   ```
   http://localhost:631
   ```

2. Klikněte na **Administration** → **Add Printer**

3. Přihlaste se jako root (nebo uživatel s oprávněním)

4. Vyberte tiskárnu:
   - Pokud je síťová: zadejte URI ve formátu  
     `socket://<IP_ADRESA_TISKÁRNY>:9100`

5. Vyberte ovladač:
   - **Canon MF4320-4350 UFRII LT**

6. Dokončete nastavení a proveďte testovací tisk

---

### 🧪 Ověření funkčnosti

Pro ruční test filtru:

```bash
/usr/lib/cups/filter/pstoufr2cpca 1 testprinter "" 1 "" testfile.ps > /dev/null
echo $?
```

Sledujte výstup v `/var/log/cups/error_log` pro případné chyby.

---

### 📁 Obsah balíčku

- `pstoufr2cpca`: vlastní CUPS filtr
- `libbuftool.a`, `buflist.h`, `buflist.c`: statická knihovna a hlavičky
- `README.txt`: dokumentace

---

## 🧠 Autor

Projekt vytvořil: **Jakub Kubiik (KubiikSvK)**  
GitHub: [github.com/KubiikSvK](https://github.com/KubiikSvK)  
📧 E-mail: [jvanek23@gmail.com](mailto:jvanek23@gmail.com)

---

## 🐞 Hlášení chyb

Pokud narazíte na chybu, nefunkční filtr nebo problém s kompatibilitou:

- Vytvořte issue přímo zde na GitHubu: [Issues](https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/issues)
- Nebo mě kontaktujte e-mailem: [jvanek23@gmail.com](mailto:jvanek23@gmail.com)

Vaše zpětná vazba pomáhá projekt vylepšovat pro ostatní uživatele.

---

## 📄 Licence

Tento projekt je poskytován „tak jak je“, bez záruky. Používejte na vlastní riziko.

# 🖨️ Canon MF4340d Linux Driver (Jakub Edition)

## 🇬🇧 English Version

### 🎯 Project Purpose
This project was created to provide a working solution for using the **Canon MF4340d** printer on modern Linux distributions, especially Ubuntu 24.04 LTS. Canon does not offer updated drivers for newer systems, making the printer unusable out of the box.

The goals were:

- Enable printing via **USB-connected Canon MF4340d** attached to an **Apple AirPort Extreme router** for **network use**
- Allow **deployment on a server** to support printing from web applications or email
- Compile a functional `pstoufr2cpca` filter from legacy Canon sources
- Package it into a `.deb` installer for easy deployment
- Enable seamless printing via CUPS without manual configuration

This project is intended for home or office environments where the MF4340d is still operational but lacks vendor support.

---

### 📦 Description
This repository contains a manually compiled `pstoufr2cpca` filter for the **Canon MF4340d** printer, enabling it to work on modern Linux distributions.

---

### 🛠️ Build Info

Built on:

- **Distribution:** Ubuntu 24.04.3 LTS (codename: noble)
- **Kernel:** Linux 6.8.0-79-generic
- **Architecture:** x86_64
- **GCC:** 13.3.0
- **Make:** GNU Make 4.3

#### 🔗 Canon Source Drivers Used

This project uses components from official Canon drivers:

- **UFR II/UFRII LT Printer Driver for Linux V6.10**  
  [Canon MF4340d – v6.10](https://www.canon-europe.com/support/consumer/products/printers/i-sensys/mf-series/i-sensys-mf4340d.html?type=drivers&detailId=tcm:13-1506758&productTcmUri=tcm:13-726815)  
  → Fully installed using the provided `install.sh` script

- **UFRII/UFRII LT Printer Driver for Linux v3.10**  
  [Canon MF4340d – v3.10](https://www.canon-europe.com/support/consumer/products/printers/i-sensys/mf-series/i-sensys-mf4340d.html?type=drivers&detailId=tcm:13-1331911&productTcmUri=tcm:13-726815)  
  → Manually unpacked and source files extracted:
  - `pstoufr2cpca`
  - `buftool`, `buflist.h`, `libbuftool.a`

These components were compiled and packaged into the `.deb` installer.

---

### 📋 Dependencies

Before installing, make sure you have:

```bash
sudo apt update
sudo apt install cups libcups2 libcups2-dev libcupsimage2 libcupsimage2-dev
```

Required libraries:

- `libcups.so.2`
- `libavahi-client.so.3`
- `libgnutls.so.30`
- `libdbus-1.so.3`
- `libsystemd.so.0`
- `libz.so.1`
- `libm.so.6`

---

### 📥 Installation

If you don’t have the `.deb` file locally, download it using:

```bash
wget https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/releases/download/v1.0/jakub-mf4340d-driver.deb
```

Then install:

```bash
sudo dpkg -i jakub-mf4340d-driver.deb
sudo systemctl restart cups
```

---

### 🖨️ Printer Setup in CUPS

1. Open the CUPS web interface:
   ```
   http://localhost:631
   ```

2. Go to **Administration** → **Add Printer**

3. Log in as root (or a user with admin rights)

4. Select your printer:
   - For network printers, use URI format  
     `socket://<PRINTER_IP>:9100`

5. Choose driver:
   - **Canon MF4320-4350 UFRII LT**

6. Finish setup and run a test print

---

### 🧪 Manual Filter Test

To manually test the filter:

```bash
/usr/lib/cups/filter/pstoufr2cpca 1 testprinter "" 1 "" testfile.ps > /dev/null
echo $?
```

Check `/var/log/cups/error_log` for any runtime errors.

---

### 📁 Package Contents

- `pstoufr2cpca`: custom CUPS filter
- `libbuftool.a`, `buflist.h`, `buflist.c`: static library and headers
- `README.txt`: documentation

---

## 🧠 Author

Created by: **Jakub Kubiik (KubiikSvK)**  
GitHub: [github.com/KubiikSvK](https://github.com/KubiikSvK)  
📧 Email: [jvanek23@gmail.com](mailto:jvanek23@gmail.com)

---

## 🐞 Bug Reporting

If you encounter a bug, malfunctioning filter, or compatibility issue:

- Open an issue here on GitHub: [Issues](https://github.com/KubiikSvK/Canon-MF4340d-Linux-Driver/issues)
- Or contact me directly via email: [jvanek23@gmail.com](mailto:jvanek23@gmail.com)

Your feedback helps improve the project for others.

---

## 📄 License

This project is provided "as is", without warranty. Use at your own risk.
