M300 - LB2 Dokumentation Arber Haliti 
===
In diesem Markdown Dokument teile ich meine Erfahrungen und Lernschritte die ich in diesem Modul aufgenommen habe.

## Inhaltsverzeichnis
- [M300 - LB2 Dokumentation Arber Haliti](#m300---lb2-dokumentation-arber-haliti)
  - [Inhaltsverzeichnis](#inhaltsverzeichnis)
- [K1](#k1)
  - [VirtualBox](#virtualbox)
- [K3](#k3)
  - [Vagrant Befehle](#vagrant-befehle)
- [K5](#k5)









K1
======

> [⇧ *Nach oben*](#inhaltsverzeichnis)

## VirtualBox
VirtualBox ist eine Hypervisor Typ 2 Virtualisierungssoftware und benötigt somit ein vorab installiertes Betriebssytem wie Windows oder ein UNIX basiertes Betriebssystem.

1. VirtualBox habe ich auf der [Herstellerwebseite](https://www.virtualbox.org/wiki/Downloads) herunter geladen.
2. Anschliessend habe ich ein Ubuntu 18.04 ISO File von der [Ubuntu Seite](https://ubuntu.com/download) heruntergeladen.
3. VirtualBox starten.
4. Auf "neu" klicken (erstellt neue VM).
5. VM mit folgenden Paramter erstellen
* Name:      `M300_Ubuntu_18.04_desktop`
* Typ:       `Linux`
* Version:   `Ubuntu (64-Bit)`
* Speichergrösse: `2048 MB`
6. Festplatten erzeugen klicken.
   *  Dateipfad:                       `standard`
   *  Dateigrösse:                     `10.00 GB`
   *  Dateityp der Festplatte:         `VMDK (Virtual Maschine Disk)`
   *  Storage on physical hard disk:   `dynamisch alloziert`
7. Disk erzeugen.
8. Unter `ändern` und  `SATA-Controller` auf das CD+Symbol klicken.
9. Unter `Medium auswählen` die zuvor heruntergeladene ISO-Datei anwählen.
10. Die Installations und Konfigurations der VM befolgen und abschliessen.

*Im Terminal wurden dann die folgenden Befehle durchgeführt*
1. Paketliste Updaten falls nötig
   ```Shell 
   $  sudo apt-get update   #Paketlisten des Paketmanagement-Systems "APT" neu einlesen
   
   $  sudo apt-get upgrade   #Installierte Pakete werden wenn möglich auf neuste Versionen aktualisiert

   $  sudo reboot           #System-Neustart durchführen
   ```
2. Synpatic installieren
    ```Shell 
   $  sudo apt-get install synaptic
   ```
3. Nach der Installation nach "Synaptic Package Manager" suchen und diesen starten
4. Im Synaptic Manager nach "Apache" suchen und alle Apache Webserver bezogenen Pakete installieren bzw. anwählen.
5. Anschliessend nach der Installation das System neustarten.
   ```Shell
   $  sudo reboot now
   ```
6. Web-Browser starten und "http://127.0.0.1:80" oder localhost aufrufen. es sollte die standard Apache Webserver seite auftauchen.

## Vagrant
> [⇧ *Nach oben*](#inhaltsverzeichnis)

[Vagrant](https://www.vagrantup.com/downloads.html) von der Hersteller Seite herunterladen und mit den Standardkonfiguration installieren.

*VM erstellen*

1. GitBash öffnen
2. Ordner für VM anlegen
   ´´´Shell
   $ cd C:\Users\arber\M300-Services
   $ mkdir myserver
   ´´´
   Leider ist mir ein Fehler unterlaufen weil ich im M300-Services Ordner nochmals einen Ordner mit dem gleichen Namen erstellt habe das wäre aber nicht nötig gewesen.
3. Vagrant File erzeugen
   ´´´Shell
     $ vagrant init ubuntu/xenial64        #Vagrantfile erzeugen
     $ vagrant up --provider virtualbox    #Virtuelle Maschine erstellen & starten
   ´´´
4. Im Verzeichnis der VM kann man nun mit dem folgendem die VM per SSh erreichen und bedienen.
   ´´´Shell
    $ cd C:\Users\arber\M300-Services\M300-Services\myserver     #Zum Verzeichnis der VM wechseln
    $ vagrant ssh                                                #SSH-Verbindung zur VM aufbauen

     #Anschliessend können ganz normale Bash-Befehle abgesetzt werden:

    $ ls -l /bin  #Bin-Verzeichnis anzeigen
    $ df -h       #Freier Festplattenspeicher
    $ free -m     #Freier Arbeitsspeicher
    ´´´
5. VM über VirtualBox-GUI ausschalten

*VM mit einem bereits abgändertem File*

1. Terminal öffnen
2. In das M300-Verzeichnis wechseln:
    ```Shell
      $ cd C:\Users\arber\M300-Services\M300-Services\myserver
     ```
3. VM erstellen und starten:
    ```Shell
      $ vagrant up
    ``` 
4. Web-Browser starten und "http://127.0.0.1:80" oder localhost aufrufen. es sollte die standard Apache Webserver seite auftauchen.
5. Später habe ich im Ordner `\web` die Hauptseite `index.html` editiert und das Resultat überprüft.
6. Abschliessend habe ich die VM wieder gelöscht:
    ```Shell
      $ vagrant destroy -f
    ```
## Visual Studio Code
> [⇧ *Nach oben*](#inhaltsverzeichnis)

*Kurze Beschreibung meiner Visual Studio Code Installation*

1. Visual Code habe ich von der [Hersteller Webseite](https://code.visualstudio.com/"visualstudio.com")
2. Ich habe folgende Plug-ins installiert
   * Markdown All in One (von Yu Zhang)
   * Vagrant Extension (von Marco Stanzi)
   * vscode-pdf Extension (von tomiko1207)
3. anschliessen Visual Code neu starten
4. ´settings.json´ öffnen
5. Unter dem abscnitt:
    ´´´Shell
     // Configure glob patterns for excluding files and folders. For example, the files 
    explorer decides which files and folders to show or hide based on this setting. 
    Read more about glob patterns here. (...)
    ´´´
6. Folgenden Code einfügen:
    ´´´
    // Konfiguriert die Globmuster zum Ausschließen von Dateien und Ordnern.
 "files.exclude": {
   "**/.git": true,
   "**/.svn": true,
   "**/.hg": true,
   "**/.vagrant": true,
   "**/.DS_Store": true
 },
 ´´´
*Repository Push*
1. VS Code öffnen
2. README.MD bearbeiten 
3. In der linken Leiste das Symbol mit einer "1" aufrufen
4. Unter dem Abschnitt Changes die betroffenen Files bezüglich ihres Changes "stagen" (Stage Changes)
5. Nachricht hinterlegen (Message) und Haken (Commit) setzen
6. Bei den 3 Punkten (...) die Funktion Push aufrufen
7. Warten, bis Dateien vollständig gepusht wurden
8. Anschliessen auf GitHub überpürfen ob alles funktioniert hat. 

## Git-Client & SSH-Key
> [⇧ *Nach oben*](#inhaltsverzeichnis)

Als Git-Client habe ich [GitBash](https://git-scm.com/downloads)

*Nach der Installation habe ich damit angefangen mein Repository zu klonen*

1. GitBash öffnen
2. Git einbinden
   ```Shell
      $ git config --global user.name "<username>"
      $ git config --global user.email "<e-mail>"
    ``` 
*Repository klonen*
1. GitBash öffnen
2. LocalRep erstellen
   ```Shell
      $ cd C:\Users\arber\M300-Services
      $ mkdir MyLocalRep
     ```
3.  Repository klonen
 ```Shell
    $ git clone git@github.com:arber-hal/M300-Services.git

    Cloning into 'M300-Services'...
``` 
4. Repository aktualisieren und Status anzeigen:
    ```Shell
      $ git pull

      Already up to date.
    ```

1. SSH Key erstellen
 ```Shell
      $  ssh-keygen -t rsa -b 4096 -C "arber.haliti@edu.tbz.ch"
 ```
2. Nachdem der SSH Key erstellt wurde muss dieser auf GitHub eingebunden werden
3. Unter "Settings" und "SSH and GPG Keys"
4. SSH Key von "C:\Users\arber\.ssh\id_rsa.pub" hinzufügen
5. Anschliessend in ein Verzeichnis gehen wo eine bereits vorhandene VM ist und mit folgendem Code verbinden:
´´´Shell
vagrant ssh
´´´
K3
======

## Vagrant Befehle

| Befehl                    | Beschreibung                                                      |
| ------------------------- | ----------------------------------------------------------------- | 
| `vagrant init`            | Initialisiert im aktuellen Verzeichnis eine Vagrant-Umgebung und erstellt, falls nicht vorhanden, ein Vagrantfile |
| `vagrant up`              |  Erzeugt und Konfiguriert eine neue Virtuelle Maschine, basierend auf dem Vagrantfile |
| `vagrant ssh`             | Baut eine SSH-Verbindung zur gewünschten VM auf                   |
| `vagrant status`          | Zeigt den aktuellen Status der VM an                              |
| `vagrant port`            | Zeigt die Weitergeleiteten Ports der VM an                        |
| `vagrant halt`            | Stoppt die laufende Virtuelle Maschine                            |
| `vagrant destroy`         | Stoppt die Virtuelle Maschine und zerstört sie.                   |

K5
======

*Was wusste ich schon über VMs und Cloud Funktionen*
Wir haben das Thema Vagrant ganz kurz in einem ÜK angeschnitten wir sind aber nicht weiter auf das Thema Cloud eingegangen also wusste ich am Anfang des Moduls nicht viel über das Thema.

*Reflexion* 
Ich habe vieles neues gelernt was die Cloud Umgebung anbelangt und es lief das ganze Projekt eigentlich ziemlich gut jetzt gegen Schluss hatte ich Probleme mit der VM sie liess sich nicht mehr sauber erstellen und ich konnte den Grund daür nicht herausfinden. Was mir besonders gut gefallen hat und auch spannend war, war die schnelle Konifguration anhand des Vagrant File, das hat mir gezeigt wieviel schneller man eine umgebunge aufbauen könnte wenn man das richtige know-how hätte. 