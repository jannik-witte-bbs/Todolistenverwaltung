### Projektdokumentation: Einrichten eines Linux-Servers

#### 1. Netzwerkkonfiguration für eine statische IP-Adresse

- **Ziel:** Konfiguration einer statischen IP-Adresse auf dem Raspberry Pi.
- **Datei bearbeiten:** `/etc/dhcpcd.conf`
- **Befehl:** `sudo nano /etc/dhcpcd.conf`
- **Hinzugefügte Konfiguration:**

  ```plaintext
  interface eth0
  static ip_address=192.168.1.100/24
  static routers=192.168.1.1
  static domain_name_servers=192.168.1.1 8.8.8.8
  ```

- **Dienst neu starten:** `sudo service dhcpcd restart`

#### 2. Benutzerkonfiguration

- **Benutzer hinzufügen:** `willi` und `fernzugriff`
- **Befehle:**

  ```bash
  sudo adduser willi
  sudo adduser fernzugriff
  sudo usermod -aG sudo fernzugriff
  ```

#### 3. SSH-Dienst konfigurieren

- **Paketinstallation:** `sudo apt-get install openssh-server`
- **Konfigurationsdatei bearbeiten:** `sudo nano /etc/ssh/sshd_config`
- **Wichtige Änderungen:**

  ```plaintext
  PermitRootLogin no
  AllowUsers fernzugriff
  ```

- **Dienst neu starten:** `sudo systemctl restart ssh`

#### 4. Docker Installation und Test

- **Notwendige Pakete installieren:**

  ```bash
  sudo apt-get install apt-transport-https ca-certificates curl gnupg software-properties-common
  ```

- **Docker GPG-Schlüssel und Repository hinzufügen:**

  ```bash
  curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
  echo "deb [arch=armhf signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  sudo apt-get update
  sudo apt-get install docker-ce docker-ce-cli containerd.io
  ```

- **Docker Test:**

  ```bash
  docker run hello-world
  ```

### Zusätzliche Schritte

- **Überprüfen der Installation:**

  - **Docker-Version:** `docker --version`
  - **Docker-Dienststatus:** `sudo systemctl status docker`

Diese Dokumentation enthält alle wesentlichen Schritte und Befehle, die zur Einrichtung deines Projekts erforderlich sind. Sie bietet eine gute Grundlage für deine Projektdokumentation. Solltest du weitere Details hinzufügen oder anpassen wollen, lass es mich wissen!
