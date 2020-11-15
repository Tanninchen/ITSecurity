# ITSecurity
## Anleitung 

### Root Zertifikat erstellen

Root Zertififikat mit zugehörigen privaten schlüssel ertsellen erstellen ->
openssl genrsa -out myRoot.key 4096 

dann das eigentliche Zertifikat ->
openssl req -x509 -new -nodes -key myRoot.key -sha256 -days 3650  -out myRoot.crt

checken ob das Zertifkat rihtig erstell wurde ->  openssl x509 -in myRoot.crt -text -noout  
 
 
### Installation des Zertifikats
 
 Zertifikat in entsprechenen Zertifikatsspeicher kopiert werden. ->
 
 sudo mkdir /usr/local/share/ca-certificates/extra
sudo cp myRoot.crt \/usr/local/share/ca-certificates/extra/myRoot.crt
sudo update-ca-certificates

### Zertifikat für eine /Sub)Domain erstellen

1. privater Schlüssel und ein CSR erstellt.
 -> Konfigurationsdatei mit notwendigen Daten erstellen.
 openssl req -new -sha256 -nodes \    
            -out test.example.csr \    
            -newkey rsa:2048 -keyout test.example.key \    
            -config test.example.csr.cnf
Server-Zertifikat erstellen -> weitere Konfigurationsdatei erstellt 

2. aus dem CSR wird mit Hilfe des Stammzertifikates ein Zertifikat für die Domäne erstellt
3. dieses Zertifikat kann anschließend zb im Web Server konfiguriert werden.


### Apache Webserver für https konfigurieren
apache WebServer neu starten
Zertifikat erstellen
/etc/apache2/sites-available/default-ssl.conf 
-> Virtuelen Host anlegen , editieren und Zertifikate einfügen

chainFIle anlegen ->
