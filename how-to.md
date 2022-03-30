Powered by Lilisystem@dedicated-1.spielenmitlili.eu on host german-host.io

  

# **Minecraft Server ohne GUI**

Hier einmal alle Befehle zusammenngefasst, die für die Installation von Minecraftserver gebraucht werden welcher ohne grafische Nutzeroberfläche für die Verwaltung auskommen soll.

Ich empfehle eher immer auf das Panel Pterodactyl zu setzen, da dieses eine grafische Verwaltung für den Nutzer bietet wodurch später Updates etc deutlich erleichtert werden. Siehe auch: https://docs.system.lili/installer/minecraft/pterodactyl/how-to.md

Dieser Installer ist für **Version 1.18.X** vorgesehen. Bei anderen Versionen muss gegebenenfalls eine andere Java-Version verwendet werden.

Damit keine Probleme auftreten als **Superuser ("root")** einloggen

### 1. Mit Putty.exe oder anderem Programm via SSH Verbindung mit dem Server aufbauen

### 2. Server updaten

> apt update -y

> apt upgrade -y

### 3. Benötigte Programme installieren, damit der Server laufen kann

> apt install gnupg curl dirmngr nano unzip htop nload -y

### 4. Java installieren

## Bis einschließlich Debian 10

> echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main" | tee /etc/apt/sources.list.d/java.list

> apt install oracle-java17-installer

Sofern nachfragen kommen einfach akzeptieren

## Sofern Debian 11 verwendet wird  

> apt install openjdk-17-jre-headless -y

### 5. Screen installieren um die Konsole auszublenden

> apt install screen -y

### 6. Ordner für unsere Minecraftdateien anlegen

> mkdir minecraft

### 7. Ordner betreten und Minecraft installieren

> cd minecraft

Hier die richtige Minecraftversion auswählen und herunterladen.

Downloadlinks lassen sich auf den **Seiten der jeweiligen Distrubutionen** (z. B. https://papermc.io/) finden.

Empfohlen wird **Paper** da diese Version besonders gut läuft

> wget https://papermc.io/api/v2/projects/paper/versions/1.18.2/builds/271/downloads/paper-1.18.2-271.jar

Dateien anzeigen lassen um den Namen der heruntergeladenen Datei herauszufinden

> ls

### 8. Skripte zum Starten und stoppen des Servers generieren

**Starten**

> nano start.sh

Danach in das offene Fenster folgenden Text eintippen

> screen -AmdS minecraft java -Xms**RAM für den Server zuweisen**M -Xmx**RAM für den Server zuweisen**M -jar /root/minecraft/**Name der heruntergeladenen Datei**

Mit **STRG + O** speichern und mit **ENTER** bestätigen

Mit **STRG + X** verlassen

**Stoppen**

> nano stop.sh

Danach in das offene Fenster folgenden Text eintippen

> screen -r minecraft -X quit

Mit **STRG + O** speichern und mit **ENTER** bestätigen

Mit **STRG + X** verlassen

Start und Stoppdateien ausführbar machen

> chmod +x start.sh
> chmod +x stop.sh

### 9. Die Lizenzbedingungen von Minecraft akzeptieren

> "eula = true" > eula.txt

### 10. Server starten

> ./start.sh

### 11. Minecraft Konsole anzeigen

> screen -r minecraft