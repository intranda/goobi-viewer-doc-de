# 8.6 Entwicklungsumgebung

## Einleitung

Die folgende Anleitung für die Einrichtung einer Entwicklungsumgebung wurde für Ubuntu Linux geschrieben und ist analog auf andere Betriebssysteme übertragbar. Sie ist als Schritt für Schritt Anleitung von oben nach unten geschrieben, das bedeutet, dass Einstellungen und Konfigurationen aufeinander aufbauen. Wird die Reihenfolge nicht eingehalten, können unter Umständen unerwünschte Effekte auftreten.

## Vorbereitung

Im Homeverzeichnis einen Ordner `Entwicklungsumgebung`anlegen:

```text
mkdir ~/Entwicklungsumgebung
```

## Download

Die folgenden Pakete herunterladen und entpacken:

* [Eclipse IDE for Enterprise Java Developers](https://www.eclipse.org/downloads/packages/)
* [Apache Tomcat 8.5](https://tomcat.apache.org/download-80.cgi)

Eclipse wird in dem Ordner `Entwicklungsumgebung/Eclipse` abgelegt und der Tomcat unter `Entwicklungsumgebung/Tomcat/8.5.XX`

Danach im Verzeichnis `Entwicklungsumgebung/Eclipse` die folgende Datei ablegen:

{% tabs %}
{% tab title="config\_viewer.xml" %}
```markup
<?xml version="1.0" encoding="UTF-8" ?>
<config>
    <configFolder>/opt/digiverso/viewer/config/</configFolder>
</config>
```
{% endtab %}
{% endtabs %}

## Verzeichnisstruktur anlegen

Der Goobi viewer benötigt die folgende Ordnerstruktur und darin Lese- und Schreibrechte:

```text
/opt
    |_ /digiverso	
        |_ /logs
        |_ /viewer
            |_ /cache
            |_ /cms_media
            |_ /config

```

Das kann unter Linux mit dem folgenden Kommando angelegt werden:

```bash
mkdir -p /opt/digiverso/{logs,viewer/{cache,cms_media,config}}
chown -R "$(logname)." /opt/digiverso
```

Anschließend die folgende lokale Konfigurationsdatei erzeugen. In dieser können dann alle lokalen Einstellungen hinterlegt werden:

```markup
<?xml version="1.0" encoding="UTF-8" ?>
<config>
        <configFolder>/opt/digiverso/viewer/config/</configFolder>

        <viewer>
                <theme subTheme="false" mainTheme="reference" discriminatorField="" autoSwitch="true" addFilterQuery="false" filterQueryVisible="false" />
        </viewer>
</config>
```

## MySQL

Der Goobi viewer benötigt eine lokale Datenbank. Die Installation und Einrichtung erfolgt mit den folgenden Befehlen:

```bash
apt install mariadb-server
```

```bash
mysql -e "CREATE DATABASE viewer;
CREATE USER 'viewer'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON viewer.* TO 'viewer'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;"
```

## Eclipse einrichten

Die folgenden Schritte beschreiben die Einrichtung von Eclipse

### Workspace 

Der Workspace soll als Unterordner von `Entwicklungsumgebung` angelegt werden, also zum Beispiel `Entwicklungsumgebung/eclipse-workspace` 

### Welcome Screen

In dem Welcome Screen unten rechts die Checkbox **Always show Welcome at start up** deaktivieren und den Welcome Screen danach schließen.

### Allgemeine Einstellungen

Folgende allgemeine Einstellungen in Eclipse vornehmen. 

1. Fehlermeldungen beim Kompilieren des Goobi viewers abschalten: `Window ->  Preferences ->  Java ->  Compiler ->  Building ->  Build path problems ->  Circular dependencies = Warning`
2. GIT Staging abschalten:   `Window ->  Preferences ->  Team ->  Git ->  Committing -> "Use Staging View to commit instead of Commit Dialog" deaktivieren`
3. Textfile Encoding

   `Window ->   
   Preferences ->   
   General ->   
   Workspace ->   
   Text file encoding ->   
   Other: UTF-8`

### Git Repositories klonen

Es müssen drei Git-Repositories importiert werden: Core, Core-Config und ein Theme. In diesem Beispiel das Reference-Theme. Dafür wie folgt vorgehen.

Im Menü folgendes auswählen:

* File -&gt; Import
* In dem sich öffnenden Dialogfeld im Ordner **Git** den Eintrag **Projects from Git** auswählen und Next klicken.
*  **Clone URI** wählen und `Next` klicken. 
* Als URI die folgende URL eingeben und `Next` klicken: `https://github.com/intranda/goobi-viewer-core.git`. 
* Als Branch nur den **master** auswählen und `Next` klicken. 
* Als Verzeichnis in das geklont werden soll `Entwicklungsumgebung/git/goobi-viewer-core` eintragen und `Next` klicken. 
* Das klonen dauert nun ein wenig. Anschließend den Dialog mit einem Klick auf `Next` und `Finish` abschließen.  

Den gleichen Weg auch für die folgenden beiden URIs durchführen:

* `https://github.com/intranda/goobi-viewer-core-config.git`
* `https://github.com/intranda/goobi-viewer-theme-reference.git`

### Maven

Im Project Explorer nun mit einem rechten Mausklick auf das Projekt `goobi-viewer-theme-reference` das Kontexmenü öffnen und dort `Run As -> Maven install` wählen. 

Anschließend für das selbe Projekt das Kontextmenü erneut öffnen und `Maven -> Update Project...` wählen. Dort in "Available Maven Codebases" die anderen beiden Projekte ebenfalls auswählen und mit `OK` bestätigen.

### Tomcat Einbindung

Der Tomcat wird in Eclipse eingebunden. Dafür im Menü folgendes auswählen:

* Window -&gt; Show View -&gt; Servers

Anschließend im unteren Bildschirmbereich auf den folgenden Link klicken`No servers are available. Click this link to create a new server...` 

In dem sich öffnenden Dialogfeld im Ordner **Apache** den Eintrag **Tomcat v8.5 Server** auswählen, als **Server name** `Apache Tomcat v8.5` eingeben und `Next` klicken. Bei dem **Tomcat installation directory** den Pfad zu `Entwicklungsumgebung/Tomcat/8.5.XX` hinterlegen und die Einstellungen mit `Finish` übernehmen.

Im Project Explorer auf der Linken Seite ist nun ein neuer Eintrag "Servers" zu sehen. Dort die folgende Datei editieren: 

* `Servers/Tomcat v8.5-config/context.xml`

Innerhalb von `<Context />` den folgenden Eintrag hinzufügen:

{% tabs %}
{% tab title="context.xml" %}
```markup
<Resource 
    name="viewer"
    auth="Container"
    factory="org.apache.tomcat.jdbc.pool.DataSourceFactory"
    type="javax.sql.DataSource"
    driverClassName="org.mariadb.jdbc.Driver"
    username="viewer"
    password="password"
    maxActive="100" 
    maxIdle="30" 
    minIdle="4"
    maxWait="10000" 
    testOnBorrow="true" 
    testWhileIdle="true"
    validationQuery="SELECT SQL_NO_CACHE 1"
    removeAbandoned="true" 
    removeAbandonedTimeout="120" 
    url="jdbc:mysql://localhost:3306/viewer?characterEncoding=UTF-8&amp;autoReconnect=true&amp;autoReconnectForPools=true" />
```
{% endtab %}
{% endtabs %}

### Applikation einmalig starten

Der Goobi viewer wird nun einmalig im Tomcat ausgeführt. Dabei werden zum Beispiel Datenbanktabellen angelegt und es sind anschließend auch weitere Konfigurationsmöglichkeiten in Eclipse vorhanden.

Zum Starten im Projekt Explorer auf das Projekt **goobi-viewer-theme-reference** mit einem rechten Mausklick das Kontextmenü öffnen und `Run as -> Run on Server` auswählen. In dem sich öffnenden Dialog dann  `Tomcat v.8.5 Server` auswählen und mit einem Klick auf `Finish` bestätigen.

Sobald die Applikation einmalig deployt wurde den Tomcat wieder stoppen

### Tomcat Konfiguration

Nun wieder den Server View aufrufen `Window > Show View Servers` und per Doppelklick auf den Tomcat v8.5 Server die Einstellungen aufrufen. 

In der ersten offenen Registerkarte "Overview" in dem Bereich "Timeouts" bei **Start \(in seconds\)** den Wert `80` setzen. Dann die Registerkarte "Modules" öffnen, auf "Edit" klicken und die Checkbox bei **Auto reloading enabled** entfernen. Damit wird ein Neustart des Servers bei Dateiänderungen verhindert.

Die Einstellungen mit der Tastenkombination Strg+S speichern und die Einstellungsmaske schließen.

### Benutzeraccount anlegen

Um sich später im Goobi viewer Backend anmelden zu können muss ein Benutzeraccount angelegt werden. Mit dem folgenden Kommando wird ein Testaccount mit dem Benutzernamen `goobi@intranda.com` und dem Passwort `viewer` in die Datenbank eingefügt:

```bash
mysql -e 'USE viewer;
INSERT INTO users (active,email,password_hash,score,superuser) VALUES (1,"goobi@intranda.com","$2a$10$Z5GTNKND9ZbuHt0ayDh0Remblc7pKUNlqbcoCxaNgKza05fLtkuYO",0,1);'
```

## Frontend Entwickler

Die Entwicklung am Theme und Styling erfordert aufgrund der Projektstruktur weitere Einstellungen

### NPM und Grunt

Für den LESS- und JS-Compiler ist die Installation von npm und grunt notwendig. Dafür die folgenden beiden Pakete auf der Kommandozeile installieren:

```bash
sudo apt install npm grunt
```

Anschließend in Eclipse in dem Project Explorer bei dem goobi-viewer-theme-reference einen **rechten Mausklick** auf die Datei `package.json` ausführen und dort `Run as -> npm install` wählen.

Damit die mit Grunt erstellten statischen Resourcen direkt im tomcat landen, muss noch eine Konfigurationsdatei im home-Verzeichnis des Nutzers angelegt werden, in der hinterlegt ist, wo der tomcat liegt. Diese Datei wird unter folgendem Pfad erwartet:

```bash
~/.config/grunt_userconfig.json
```

In dieser Datei wird nur der Pfad zum webapps-Verzeichnis des tomcat konfiguriert. Der Inhalt sieht folgendermaßen aus, es muss nur der Platzhalter \[USERNAME\] ersetzt werden:

```javascript
{
    "tomcat_dir": "/home/[USERNAME]/Entwicklungsumgebung/Tomcat/8.5.XX/wtpwebapps/"
}
```

Nun einen **rechten Mausklick** auf die Datei `Gruntfile.js` ausführen und dort `Run as -> Grunt Task` wählen.

Änderungen in den LESS und JavaScript Dateien werden nun direkt kompiliert und stehen als aktualisierte min-Dateien zur Verfügung. 

## Backend Entwickler

Die Entwicklung am Java Backend erfordert in der Regel bei jeder neu kompilierten Klasse ein Neuladen des Tomcats mit den neuen Binaries. Um dieses zu verhindern kann der HotSwapAgent eingesetzt werden. Die Einrichtung ist in den folgenden Schritten beschrieben

### HotSwapAgent

Die neuste hotswap-agent.jar von der folgenden Adresse herunterladen und in dem Ordner `~/Entwicklungsumgebung/` speichern:

* [https://github.com/HotswapProjects/HotswapAgent/releases](https://github.com/HotswapProjects/HotswapAgent/releases)

### TravaOpenJDK

Das TravaOpenJDK für Linux herunterladen, entpacken und in dem Ordner `~/Entwicklungsumgebung/Java/` abspeichern:

* [https://github.com/TravaOpenJDK/trava-jdk-8-dcevm/releases](https://github.com/TravaOpenJDK/trava-jdk-8-dcevm/releases)

### Eclipse Konfiguration

In Eclipse muss das JDK als Standard JRE konfiguriert werden:

1. Einstellungen öffnen `Window -> Preferences -> Java -> Installed JREs`
2. Neues JRE hinzufügen `Add`
3. Die Dialogfelder mit den folgenden Einstellungen übernehmen: `Standard VM -> JRE home: Entwicklungsumgebung/Java/java8-openjdk-dcevm-linux/dcevm8u232b09  Finish`
4. Das neue JRE in dem noch offenen Einstellungsdialog auswählen und mit einem Klick auf `Apply and Close` übernehmen.

### Tomcat Konfiguration

In Eclipse im Menü folgendes auswählen:

* Window -&gt; Show View -&gt; Servers

Dann im unteren Bereich per Doppelklick auf `Apache Tomcat v8.5` die Einstellungen öffnen. In dem Bereich `General Information` auf den Link `Open launch configuration` klicken und in dem sich öffnenden Konfigurationsdialog in den Reiter `Arguments` wechseln.

In der Textbox für die VM arguments die folgende Zeile anfügen und die Platzhalter für \[USERNAME\] und \[VERSION\] den eigenen Gegebenheiten anpassen:

```bash
-javaagent:/home/[USERNAME]/Entwicklungsumgebung/hotswap-agent-[VERSION].jar
```

Die Einstellungen mit einem Klick auf den `OK` Button übernehmen.

Danach auf der noch offenen Einstellungsseite in dem Bereich `Publishing` die Option `Automatically  publish when resources change` auswählen. Als letztes muss noch in den tomcat-Einstellungen der Tab `Modules` geöffnet werden - dieser befindet sich am unteren Rand der tomcat-Einstellungen. Dort das Modul für den viewer auswählen, auf `Edit...` klicken und den Haken bei `Auto reloading enabled` entfernen. Auf OK klicken. die Änderungen mit Strg+S Speichern und die Tomcat Einstellungen danach schließen. 

### Anmerkung zur Benutzung

Der **Tomcat** muss im **Debug-Modus** gestartet werden. Ansonsten funktioniert das class-Reloading nicht.

