# 1. Core Changelog

## Allgemein

Zum Update des Goobi viewer Indexers auf die neuste Version immer die folgenden Kommandos benutzen:

```
mkdir /root/BACKUP/$(date -I)

systemctl stop solrindexer
mv /opt/digiverso/indexer/solrIndexer.jar /root/BACKUP/$(date -I)
wget -O /opt/digiverso/indexer/solrIndexer.jar https://github.com/intranda/goobi-viewer-indexer/releases/latest/download/solrIndexer.jar
systemctl start solrindexer
```

## 21.10-SNAPSHOT

### Goobi viewer Core

#### Stopwords

Der Tomcat Prozess darf die `stopwords.txt` Datei im Solr Kontext nicht lesen. Aus diesem Grund muss die dort vorliegende Datei an einen anderen Ort kopiert werden. Der Pfad in der globalen Konfigurationsdatei wird mit dem Update automatisch angepasst.

```
cp /opt/digiverso/solr/solr/server/solr/configsets/goobiviewer/conf/lang/stopwords.txt /opt/digiverso/viewer/config/
```

#### Metsresolver wird zu Sourcefile

Der Link zu den Quelldateien wird nun anders aus der Konfigurationsdatei ausgelesen. Dafür wird die Einstellung unter **urls/metadata/mets** umbenannt zu **sourcefile** und auch die URL muss angepasst werden:

```xml
<!-- ALT -->
<urls>
    <metadata>
        <mets>https://viewer.example.org/viewer/oai?verb=GetRecord&amp;metadataPrefix=mets&amp;identifier=</mets>
    </metadata>
</urls>


<!-- NEU -->
<urls>
    <metadata>
         <sourcefile>https://viewer.example.org/viewer/sourcefile?id=</sourcefile>
    </metadata>
</urls>
```

#### Archivkonfiguration

Weiter wurde die Konfiguration für die Archivansicht umgestellt. Im Bereich urls/basex entfällt die Unterteilung nach URL und Datenbank, sondern es wird nur noch die URL angegeben.

Neu eingeführt wird weiter der Konfigurationsbereich \<archives />. Die Sektion metadata/basexMetadataList wird dorthin als metadataList verschoben.&#x20;

```xml
<!-- ALT -->
<urls>
    <!--
    <basex>
        <url>https://basex.example.org/basex/</url>
        <defaultDatabase>Example - EAD_FILENAME.XML</defaultDatabase>
    </basex>
    -->
</urls>

<metadata>
    <basexMetadataList />
</metadata>


<!-- NEU -->
<urls>
    <basex>https://basex.example.org/basex/</basex>
</urls>

<archives enabled="false">
    <metadataList />
</archives>
```

{% hint style="info" %}
Für die Funktionalität zur Auswahl eines Archivbestandes muss die neue Datei [findDB.xq](https://raw.githubusercontent.com/intranda/goobi-plugin-administration-archive-management/master/plugin/src/main/resources/findDb.xq) im webapps Verzeichnis der baseX Installation vorliegen
{% endhint %}

### Goobi viewer Connector

Die Integration des Connectors wurde geändert und wird nun als direkte Abhängigkeit des Themes mit installiert. Eine vorhandene Installation der M2M.war muss zurückgebaut werden. Alle weiteren Einstellungen bleiben so erhalten wie sie sind.

```
mkdir -p /root/BACKUP/$(date -I)
systemctl stop tomcat9
mv /var/lib/tomcat9/webapps/M2M* /root/BACKUP/$(date -I)
mv /etc/tomcat9/Catalina/localhost/M2M.xml /root/BACKUP/$(date -I)
systemctl start tomcat9

vim /etc/apache2/sites-enabled/VIEWER.EXAMPLE.ORG.conf
```

Anschließend ist die `pom.xml` des Themes anzupassen damit der Connector als neue Abhängigkeit mit aufgenommen wird:

```xml
<!-- NEU -->
    <dependency>
        <groupId>io.goobi.viewer</groupId>
        <artifactId>viewer-connector</artifactId>
        <version>21.10-SNAPSHOT</version>
    </dependency>

<!-- ANPASSEN IM maven-dependency-plugin -->
<excludeArtifactIds>viewer-core,viewer-connector</excludeArtifactIds>
<excludes>MANIFEST.MF,**/pom.*,install/,docker/,**/*.class,web-fragment.xml</excludes>
```

{% hint style="warning" %}
Der Goobi viewer Connector verwendet jetzt die selben Zugriffslizenzen wie der Goobi viewer Core. Sollten vorher welche im Abschnitt solr/restrictions in der config\_oai.xml definiert worden sein müssen diese bei einem Update geprüft werden.
{% endhint %}

## 21.09

### Cronjobs

Für den automatischen Pull sollte der reguläre Ausdruck am Ende des minütlichen Cronjobs überprüft werden. Dieser muss gegebebenfalls analog zum folgenden angepasst werden:

```bash
## These two scripts pull the theme git repository regulary. The @daily part is only 
## a reminder for the 1-minute schedule
#*/1 *       * * *   root    cd /opt/digiverso/viewer/themes/goobi-viewer-theme-reference; git pull | grep -v -e "Already up.to.date." -e "Bereits aktuell."
#@daily              root    echo "Please look at the git checkout interval for the Goobi viewer theme" | mail -s "Reference: Theme repository is checked out every minute" admin@intranda.com 

```

### Apache

In der `robots.txt` sollten die folgenden drei Zeilen hinzugefügt werden:

```
Disallow: /viewer/login/
Disallow: /viewer/crowd/
Disallow: /viewer/error/
```

### Goobi viewer Core

Der Splitting Character hat sich geändert und aus einem Komma wurde ein Semikolon. Deswegen muss - sofern vorhanden - in der lokalen `config_viewer.xml` unter viewer/zoomXXXView/tileSize/scaleFactors aus einem `,` ein `;` gemacht werden:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<!-- Beispiel Alt -->
<scaleFactors>1,32</scaleFactors>

<!-- Beispiel Neu -->
<scaleFactors>1;32</scaleFactors>
```
{% endtab %}
{% endtabs %}

### Goobi viewer Connector

Durch die Umstellung auf commons-configuration2 musste der Elementname `<xmlns>` in der Konfigurationsdatei zu `<namespace>` umbenannt werden. Die lokale Konfigurationsdatei muss geprüft und gegebenenfalls angepasst werden:

{% tabs %}
{% tab title="config_oai.xml" %}
```markup
<!-- ALT -->
<oai-identifier>
    <xmlns>http://www.openarchives.org/OAI/2.0/</xmlns>
</oai-identifier>

<!-- -->
<oai-identifier>
    <namespace>http://www.openarchives.org/OAI/2.0/</namespace>
</oai-identifier>
```
{% endtab %}
{% endtabs %}

## 21.08

### pom.xml und Jenkinsfile im Theme

Der Goobi viewer verwendet jetzt Java 11 als Abhängigkeit. Dafür muss die `pom.xml` des Themes geprüft werden.&#x20;

Zuerst sollten die Maven Plugins aktualisiert werden:

```
mvn versions:display-plugin-updates
```

Anschließend muss die das Compiler Plugin eine neue Version übergeben bekommen. Dafür eine Zeile in dem `<properties />` Block am Anfang der Datei ersetzten und die explizite Definition von source und target Version bei der Konfiguration des maven-compiler-plugins am Ende der Datei entfernen:

{% tabs %}
{% tab title="pom.xml" %}
```markup
<!-- ALT -->
<jdk.version>1.8</jdk.version>

<!-- NEU -->
<maven.compiler.release>11</maven.compiler.release>

<!-- LÖSCHEN -->
<configuration>
    <source>${jdk.version}</source>
    <target>${jdk.version}</target>
</configuration>
```
{% endtab %}
{% endtabs %}

Außerdem muss die Jenkinsfile geprüft werden und dort das für den build verwendete Docker image auf `maven:3-jdk-11` geändert werden.

### Tomcat

Auf dem Server ist zu prüfen, dass der `tomcat-lib` Ordner nicht mehr als `PreResources` eingebunden ist:

* [ ] /etc/tomcat9/Catalina/localhost/**viewer.xml**

Weiter bitte sicherstellen, dass Java 11 genutzt wird. Dafür verifizieren, dass für den Tomcat 9 kein alternatives `JAVA_HOME` gesetzt ist:

* [ ] /etc/default/**tomcat9**

### Goobi viewer Core

Sofern in der `normdatamap.properties` Datei keine individuellen Einstellungen gemacht wurden, zum Beispiel für Provenienzen, kann die Datei gelöscht werden damit neue Standardwerte für die Indexierung von Koordinaten aus GND Normdatensätzen greifen.

Außerdem wurde in der Konfigurationsdatei viel aufgeräumt und eine einheitliche Terminologie und Schreibweise für die Aktivierung und Anzeige von Funktionen eingeführt. Dafür wurden die Attribute `visible`, `display`, `show` oder `use` genauso wie potentielle Unterelemente wie `<enabled>true</enabled>` alle auf das Attribut `enabled="true"` vereinheitlicht. Die lokale Konfigurationsdatei muss hier zwingend geprüft und mit der globalen abgeglichen werden. Alle Änderungen hier in der Anleitung aufzulisten wäre deutlich zu aufwendig, hier aber ein paar Beispiele:

```markup
<!-- ALT -->
<user>
    <userRegistrationEnabled>true</userRegistrationEnabled>
</user>

<calendar>
    <enabled>true</enabled>
</calendar>

<sidebar>
    <toc>
        <visible>true</visible>
    </toc>
    <sidebarRssFeed display="true" />
    <sidebarWidgetDownloads visible="true" />
</sidebar>

<!-- NEU -->
<user>
    <registration enabled="true" />
</user>
<calendar enabled="true" />

<sidebar>
    <toc enabled="true" />
    <sidebarRssFeed enabled="true" />
    <sidebarWidgetDownloads enabled="true" />
</sidebar>
```

### Goobi viewer Indexer

Der Schalter `<getchilds />` wurde umbenannt zu `<getchildren />`. Die Änderung muss in der Konfigurationsdatei nachgezogen werden:

```
mkdir /root/BACKUP/$(date -I)
cp /opt/digiverso/indexer/solr_indexerconfig.xml /root/BACKUP/$(date -I)
sed 's|getchilds|getchildren|g' -i /opt/digiverso/indexer/solr_indexerconfig.xml
```

Weiter muss sichergestellt sein, dass das Konfigurationselement `<viewerUrl />` auf die externe URL und nicht auf localhost zeigt, da ansonsten bei der Indexierung von in METS Dateien verlinkten ALTO Dateien versucht wird die Daten von sich selbst herunterzuladen.

Mit der internen Umstellung der Art- und Weise des Einlesens der Konfigurationsdatei kann auf den Platzhalter `#SPACE#` für ein Leerzeichen verzichtet werden und Leerzeichen werden direkt deklariert. Bei einem Update ist zu prüfen, ob der Platzhalter in der Konfigurationsdatei verwendet wird und wenn ja ist dieser anzupassen. Dafür kommt auf der Ebene des `<item />` ein Eintrag hinzu und der bisherige Platzhalter wird durch ein Leerzeichen ersetzt.

```markup
<!-- Alt -->
<MD_TESTFIELD>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:test</xpath>
            <onefield separator="#SPACE#,#SPACE#">true</onefield>
            <replace string="stringToReplace1#SPACE#">replace1#SPACE#</replace>
            <geoJSONSource separator="#SPACE#/#SPACE#">mods:coordinates/point</geoJSONSource>
        </item>
    </list>
</MD_TESTFIELD>

<!-- Neu -->
<MD_TESTFIELD>
    <list>
        <item xml:space="preserve">
            <xpath>mets:xmlData/mods:mods/mods:test</xpath>
            <onefield separator=" , ">true</onefield>
            <replace string="stringToReplace1 ">replace1 </replace>
            <geoJSONSource separator=" / ">mods:coordinates/point</geoJSONSource>
        </item>
    </list>
</MD_TESTFIELD>
```

### Goobi viewer Connector

Die Installation der OAI und SRU Schnittstelle wird vereinfacht. Dafür sind die folgenden Schritte auszuführen:

```
mkdir /root/BACKUP/$(date -I)
systemctl stop tomcat9
mv /etc/tomcat9/Catalina/localhost/M2M.xml /root/BACKUP/$(date -I)
mv /opt/digiverso/viewer/bin/ /root/BACKUP/$(date -I)
mv /var/lib/tomcat9/webapps/M2M* /root/BACKUP/$(date -I)
wget -O /tmp/M2M.war https://github.com/intranda/goobi-viewer-connector/releases/latest/download/M2M.war
mv /tmp/M2M.war /var/lib/tomcat9/webapps/M2M.war
systemctl start tomcat9
```

## 21.07

### Goobi viewer Core

In der Konfigurationsdatei wurde der Block für die Kommentare und die Facettierung umbenannt und muss von der Benennung und der Syntax angepasst werden:

```markup
<!-- ALT -->
<userComments>
    <enabled>true</enabled>
    <conditionalQuery>DC:varia</conditionalQuery>
    <notificationEmailAddress>user@example.org</notificationEmailAddress>
</userComments>

<!-- NEU -->
<comments enabled="true">
    <condition>DC:varia</condition>
    <notificationEmailAddress>user@example.org</notificationEmailAddress>
</comments>
```

```markup
<!-- Alt -->
<search>
    <drillDown>
        <field>YEAR</field>
        <geoField>WKT_COORDS</geoField>
        <field initialElementNumber="3" sortOrder="alphabetical_asc">MD_LANGUAGE</field>
    </drillDown>
</search>

<!-- Neu -->
<search>
    <facets>
        <field>YEAR</field>
        <geoField>WKT_COORDS</geoField>
        <field initialElementNumber="3" sortOrder="alphabetical_asc">MD_LANGUAGE</field>
    </facets>
</search>
```

Außerdem kann der Feedbackempfänger jetzt optional aus eine Liste ausgewählt werden. Dafür muss die Struktur in der Konfigurationsdatei ebenfalls angepasst werden:

```markup
<!-- Alt -->
<feedbackEmailAddress>viewer@example.org</feedbackEmailAddress>

<!-- Neu -->
<feedbackEmailAddressList>
    <address label="Contact" default="true">viewer@example.org</address>
</feedbackEmailAddressList>
```

Sofern das Feld `DATECREATED` für die Anzeige konfiguriert ist muss der Parameter vom Typ `field` auf `millisfield` geändert werden:

```markup
<!-- Alt -->
<metadata label="DATECREATED">
    <param type="field" key="DATECREATED"/>
</metadata>

<!-- Neu -->
<metadata label="DATECREATED">
    <param type="millisfield" key="DATECREATED"/>
</metadata>
```

Die Konfigurationsoption urls/contentServer wird nicht mehr verwenden und kann aus der lokalen `config_viewer.xml` entfernt werden:

```markup
<!-- DELETE THIS LINES -->
<!-- contentServer: relative path to contentServer from the Goobi viewer context -->
<contentServer external="false">/</contentServer>
```

Nach dem Update ist zu prüfen welche Identifier als Zitierlinks angezeigt werden sollen (URN, DOI, Handle, ...) und die Anzeige bei Bedarf anzupassen und zu ergänzen.

## 21.0.6

### Goobi viewer Core

Die folgenden drei SQL Statements ausführen. Wenn beim letzten ein Fehler auftritt muss dieser vorher manuell geprüft und korrigiert werden.

```sql
ALTER TABLE bookshelves MODIFY share_key VARCHAR(64);
ALTER TABLE bookshelves ADD CONSTRAINT share_key_unique UNIQUE(share_key);
ALTER TABLE `cms_collections` ADD UNIQUE `solr_field_solr_value_unique`(`solr_field`, `solr_value`);
```

## 21.05

### Goobi viewer Core

Die Anzeige für die Anzahl der Bände ist nicht mehr hart im Quelltext verankert sondern konfigurierbar. Sofern eine lokale Konfiguration für die `<titleBarMetadataList />` und die `<searchHitMetadataList />` existieren muss der folgende Abschnitt hinzugefügt werden:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<!-- Number of volumes for anchors -->
<metadata label="numVolumes">
    <param type="field" key="NUMVOLUMES" />
</metadata>
```
{% endtab %}
{% endtabs %}

Um bei indexierten Geokoordinaten die Facettierung auf einer Karte anzuzeigen ist in einen eventuell vorhandenen lokalen Abschnitt `<drillDown />` in der lokalen Konfigurationsdatei der folgende Eintrag hinzuzufügen:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<geoField>WKT_COORDS</geoField>
```
{% endtab %}
{% endtabs %}

## 21.04

### Goobi viewer Core

Der Schalter `<unconditionalImageAccessMaxWidth />` wurde umbenannt zu `<thumbnailImageAccessMaxWidth />` und muss - sofern vorhanden - auch in der lokalen Konfigurationsdatei umbenannt werden:

```
mkdir /root/BACKUP/$(date -I)
cp /opt/digiverso/viewer/config/config_viewer.xml /root/BACKUP/$(date -I)
sed 's|unconditionalImageAccesMaxWidth|thumbnailImageAccessMaxWidth|g' -i /opt/digiverso/viewer/config/config_viewer.xml
```

Der Schalter `<doublePageMode />` wurden umbenannt zu `<doublePageNavigation />` und das Unterelement `<enabled />`  in ein Attribut verschoben. Die lokale Konfigurationsdatei ist zu prüfen und gegebenenfalls anzupassen:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<!-- ALT -->
<doublePageMode>
    <enabled>true</enabled>
</doublePageMode>

<!-- NEU -->
<doublePageNavigation enabled="true" />
```
{% endtab %}
{% endtabs %}

Für die Steuerung des Bildzooms und Bild-Downloads stehen neue **Funktionen** zur Verfügung. Diese **werden nicht automatisch hinzugefügt**.

{% hint style="warning" %}
Bei einem Update auf die Version 21.04 müssen die im Backend konfigurierten Zugriffslizenzen und Rechte geprüft und die neuen Rechte explizit hinzugefügt werden!
{% endhint %}

### Goobi viewer Indexer

Prüfen, ob bei Indexierfehlern eine E-Mail versendet wird und dieses gegebenenfalls nachkonfigurieren:

{% tabs %}
{% tab title="solr_indexerconfig.xml" %}
```markup
<init>
    <email>
        <recipients>mail@example.org</recipients>
        <smtpServer>127.0.0.1</smtpServer>
        <smtpUser></smtpUser>
        <smtpPassword></smtpPassword>
        <smtpSenderAddress>do-not-reply@viewer.example.org</smtpSenderAddress>
        <smtpSenderName>Goobi viewer Indexer</smtpSenderName>
        <smtpSecurity>NONE</smtpSecurity>
    </email>
</init>
```
{% endtab %}
{% endtabs %}

### Goobi viewer Connector

Bei einem Update ist die Sektion mit den `<sets />` zu prüfen, ob die ausgegebenen Ergebnisse mit der Intention der konfigurierten Einträge übereinstimmt. Dabei ist ein besonderes Augenmerk auf Solr-Queries mit den Feldern `DC` und `DOCSTRCT` zu richten. Da diese Felder in alle Solr-Docs eines Datensatzes geschrieben werden müssen sie eventuell mit `+(ISWORK:true ISANCHOR:true)` weiter eingeschränkt werden.

## 21.03

### Apache

Es ist aufgefallen, dass die `robots.txt` einen erstaunlich starken Einfluss auf die Suchmaschinen hat. Deswegen ist zu prüfen, ob sie existiert, darauf zugegriffen werden kann und sinnvolle Werte inklusive der Sitemap enthalten sind. \
Bei den Werten muss vor allem darauf geachtet werden, ob der Goobi viewer mit einem /viewer/ Präfix deployt ist oder nicht.

```
User-agent: *
Disallow: /viewer/content*action=pdf
Disallow: /viewer/rest/pdf/*
Disallow: /viewer/api/v1/records/*/pdf/
Disallow: /viewer/search/
Disallow: /viewer/tags/
Disallow: /viewer/term/
Disallow: /viewer/oai
Disallow: /viewer/nextHit/
Disallow: /viewer/prevHit/

#Sitemap: http://VIEWER.EXAMPLE.ORG/viewer/sitemap_index.xml

Crawl-delay: 10
```

### Goobi viewer Core

#### Umbenennung der mainMetadataList

Bibliographische Daten können jetzt auf mehrere Seiten aufgeteilt werden. Dafür wurde der Bereich `<mainMetadataList />` in der Konfigurationsdatei umbenannt zu `<metadataView index="0" />`. Bei dem Update muss das in der lokalen `config_viewer.xml `ebenfalls erfolgen:

```
mkdir /root/BACKUP/$(date -I)
cd /opt/digiverso/viewer/config/
cp config_viewer.xml /root/BACKUP/$(date -I)
sed -e 's|<mainMetadataList>|<metadataView index="0">|g' -e 's|</mainMetadataList>|</metadataView>|g' -i config_viewer.xml
```

Außerdem ist zu prüfen ob in den lokalen messages Dateien individuelle Namen für einzelne Blöcke vergeben wurden. Wenn ja sind diese Anzupassen, denn das Namensschema dafür hat sich verändert. Aus `metadataTab0` für die Überschrift des ersten Metadatenblocks (`type="0"`) wurde `metadataTab_0_0`, der neue Infix zeigt das `index="0"` Attribut an.&#x20;

Wenn das folgende Kommando eine Ausgabe liefert muss eine Anpassung erfolgen:

```
grep -i metadataTab /opt/digiverso/viewer/config/messages_*.properties
```

#### Liebe für die Metadatenkonfiguration

Um die Anzeige der Metadaten auf der Seite "Bibliographische Daten" ein bisschen intuitiver zu gestalten sind die folgenden Änderungen vorzunehmen:

1. Alle Vorkommnisse von `DOCSTRCT` aufteilen in `DOCSTRCT_TOP` und `DOCSTRCT_SUB`
2. Bei den Feldern `DOCSTRCT_TOP` und `DC` im `<param />` Element das Attribut `topstructOnly="true"` ergänzen. Das führt dazu, dass der Publikationstyp und die Sammlung nur in den Metadaten des Publikationstyps selbst sichtbar sind.
3. Bei den Feldern `MD_TITLE` und `DOCSTRCT_SUB` das Attribut `hideIfOnlyMetadataField="true"` ergänzen. Das führt dazu, dass keine fast leeren Blöcke nur mit Titel und Strukturelement sichtbar sind.

```markup
<metadata label="MD_TITLE" hideIfOnlyMetadataField="true">
    <param type="field" key="MD_TITLE"/>
</metadata>
<metadata label="DOCSTRCT_TOP">
    <param type="translatedfield" key="DOCSTRCT_TOP" topstructOnly="true"/>
</metadata>
<metadata label="DOCSTRCT_SUB" hideIfOnlyMetadataField="true">
    <param type="translatedfield" key="DOCSTRCT_SUB"/>
</metadata>
<metadata label="DC">
    <param type="translatedfield" key="DC" topstructOnly="true"/>
</metadata>
```

### Goobi viewer Connector

Um sicherzustellen, dass bei der Dublin Core Ausgabe die Sammlungsnamen korrekt übersetzt werden, muss in der lokalen `config_oai.xml` der `<oaiFolder />` auf den config Ordner des Goobi viewer Core zeigen:

```
cd /opt/digiverso/viewer/config/
grep oaiFolder config_oai.xml
mkdir /root/BACKUP/$(date -I)
cp config_oai.xml /root/BACKUP/$(date -I)
sed 's|<oaiFolder>/opt/digiverso/viewer/oai/</oaiFolder>|<oaiFolder>/opt/digiverso/viewer/config/</oaiFolder>|g' -i config_oai.xml
```

## 21.02

### Apache

Damit die IIIF Manifeste ebenfalls gzip Komprimiert ausgeliefert werden muss der folgende Output Filter zusätzlich in dem Abschnitt für mod\_deflate hinzugefügt werden:

```
AddOutputFilterByType DEFLATE application/json
```

Anschließend den Dienst neu starten:

```
systemctl restart apache2
```

### Goobi viewer Core

Die Konfiguration des Beschreibungstextes für das Widget "Zitieren und Nachnutzen" ist vereinfacht worden. Es muss die lokale Konfigurationsdatei nach einer abweichenden Konfiguration geprüft und bei Bedarf der Message-Key für den Text in das neue Attribut `introductionText` verschoben werden:

```markup
<!-- ALT -->
<sidebarWidgetUsage display="true">
    <licenseText>
        <metadata label="MD_LICENSETEXT" value="MASTERVALUE_LICENSETEXT">
            <param type="field" key="LABEL" />
        </metadata>
    </licenseText>


<!-- NEU -->
<sidebarWidgetUsage display="true" introductionText="MASTERVALUE_LICENSETEXT" />
```

{% hint style="warning" %}
Durch die Refaktorisierung der Sammlungsauflistung muss in Themes, die die Gruppierung von Suchtreffern verwenden, das Gruppierfeld neu gesetzt werden.
{% endhint %}

Im selben Widget sind die Konfigurationsoptionen `<displayLinkToJpegImage />` und `<displayLinkToMasterImage />` durch den neuen Block `<downloadOptions><option>...` ersetzt worden. Die lokale Konfigurationsdatei muss auf vom vorherigen Standard abweichende Einträge geprüft und dann auf das neue Format migriert werden.&#x20;

```markup
<!-- ALT -->
<page>
    <displayLinkToJpegImage maxSize="2000">true</displayLinkToJpegImage>
    <displayLinkToMasterImage maxSize="max">true</displayLinkToMasterImage>
</page>


<!-- NEU -->
<page>
    <downloadOptions>
        <option label="label__download_option_preview_150" format="jpg" boxSizeInPixel="150" />
        <option label="label__download_option_small_1024" format="jpg" boxSizeInPixel="1024" />
        <option label="label__download_option_medium_2048" format="jpg" boxSizeInPixel="2048" />
        <option label="label__download_option_large_4096" format="jpg" boxSizeInPixel="4096" />
        <option label="Master" format="MASTER" boxSizeInPixel="max"/>
    </downloadOptions>
</page>
```

### Goobi viewer Indexer

{% hint style="warning" %}
Bitte vorsichtshalber die Version 21.02 des Goobi viewer Indexers nicht mit LIDO Datensätzen verwenden.
{% endhint %}

## 21.01

### Cron

In der Goobi viewer Cronjob Datei müssen verschiedene Aufrufe angepasst werden. Das betrifft die Aufrufe zur Sitemap Generierung und zur Suchtrefferbenachrichtigung wie auch den Pfad zu dem Solr optimize Kommando.

```markup
## This REST call triggers the email notification about new search hits for users...

<!-- ALT -->
42 8,12,17  * * *   root    curl -s http://localhost:8080/rest/search/sendnotifications/?token=TOKEN


<!-- NEU -->
42 8,12,17  * * *   root    curl -s -H "Content-Type: application/json" -H "token:TOKEN" -d '{"type":"NOTIFY_SEARCH_UPDATE"}' http://localhost:8080/viewer/api/v1/tasks/ 1>/dev/null
```

```markup
## This REST call creates an XML sitemap for the Goobi viewer instance...

<!-- ALT -->
18 1     * * *   root    curl -s -X POST -H "Content-Type: application/json" -d '{}' "https://viewer.example.org/viewer/rest/sitemap/update/?token=TOKEN" 1>/dev/null

<!-- NEU -->
18 1     * * *   root    curl -s -H "Content-Type: application/json" -H "token:TOKEN" -d '{"type":"UPDATE_SITEMAP"}' http://localhost:8080/viewer/api/v1/tasks/ 1>/dev/null
```

```markup
## Optimize the Solr search index once a month

<!-- ALT -->
@monthly            root    curl -s http://localhost:8983/solr/update?optimize=true&waitFlush=false

<!-- NEU -->
@monthly            root    curl -s http://localhost:8983/solr/collection1/update?optimize=true&waitFlush=false
```

### Solr

Der Dienst soll auf localhost eingeschränkt und die Garbage Collector Optionen für eine verbesserte Performance angepasst werden.&#x20;

```bash
patch /etc/default/solr.in.sh << "EOF"
@@ -46,19 +46,19 @@
 #  -XX:+PrintGCDateStamps -XX:+PrintGCTimeStamps -XX:+PrintTenuringDistribution -XX:+PrintGCApplicationStoppedTime"
 
 # These GC settings have shown to work well for a number of common Solr workloads
-#GC_TUNE=" \
-#-XX:SurvivorRatio=4 \
-#-XX:TargetSurvivorRatio=90 \
-#-XX:MaxTenuringThreshold=8 \
-#-XX:+UseConcMarkSweepGC \
-#-XX:ConcGCThreads=4 -XX:ParallelGCThreads=4 \
-#-XX:+CMSScavengeBeforeRemark \
-#-XX:PretenureSizeThreshold=64m \
-#-XX:+UseCMSInitiatingOccupancyOnly \
-#-XX:CMSInitiatingOccupancyFraction=50 \
-#-XX:CMSMaxAbortablePrecleanTime=6000 \
-#-XX:+CMSParallelRemarkEnabled \
-#-XX:+ParallelRefProcEnabled \
+GC_TUNE=" \
+-XX:SurvivorRatio=4 \
+-XX:TargetSurvivorRatio=90 \
+-XX:MaxTenuringThreshold=8 \
+-XX:+UseConcMarkSweepGC \
+-XX:ConcGCThreads=4 -XX:ParallelGCThreads=4 \
+-XX:+CMSScavengeBeforeRemark \
+-XX:PretenureSizeThreshold=64m \
+-XX:+UseCMSInitiatingOccupancyOnly \
+-XX:CMSInitiatingOccupancyFraction=50 \
+-XX:CMSMaxAbortablePrecleanTime=6000 \
+-XX:+CMSParallelRemarkEnabled \
+-XX:+ParallelRefProcEnabled"
 #-XX:-OmitStackTraceInFastThrow  etc.
 
 # Set the ZooKeeper connection string if using an external ZooKeeper ensemble
@@ -232,3 +232,4 @@
 LOG4J_PROPS="/opt/digiverso/solr/log4j2.xml"
 SOLR_LOGS_DIR="/opt/digiverso/solr/logs"
 SOLR_PORT="8983"
+SOLR_OPTS="$SOLR_OPTS -Djetty.host=127.0.0.1"
EOF
```

Außerdem den Gesamtspeicher der virtuellen Maschine prüfen und gegebenenfalls die Zuweisung zwischen Tomcat und Solr Dienst anpassen.

### Goobi viewer Core

In der lokalen config\_viewer.xml muss die URL zur REST API angepasst werden:

```markup
<!-- ALT -->
<rest>https://viewer.example.org/viewer/rest/</rest>

<!-- NEU -->
<rest>https://viewer.example.org/viewer/api/v1/</rest>
```

### Goobi viewer Indexer

Um die Sortierung von Bänden flexibler zu gestalten sowie das Stöbern nach Named Entity Werten zu ermöglichen muss das Solr Schema aktualisiert werden. Das kann mit den folgenden Zeilen erfolgen:

```bash
mkdir /root/BACKUP/$(date -I)
cp /opt/digiverso/solr/solr/server/solr/configsets/goobiviewer/conf/schema.xml /root/BACKUP/$(date -I)
wget -O /opt/digiverso/solr/solr/server/solr/configsets/goobiviewer/conf/schema.xml https://raw.githubusercontent.com/intranda/goobi-viewer-indexer/master/goobi-viewer-indexer/src/main/resources/other/schema.xml
chown solr. /opt/digiverso/solr/solr/server/solr/configsets/goobiviewer/conf/schema.xml
cd /opt/digiverso/solr/solr/
sudo -u solr bin/solr zk upconfig -n goobiviewer -d server/solr/configsets/goobiviewer/
curl "http://localhost:8983/solr/admin/collections?action=RELOAD&name=collection1&wt=xml"
```

{% hint style="warning" %}
Der Datenbestand muss anschließend neu indexiert werden. Andernfalls kann es zu Fehlermeldungen in der Benutzeroberfläche kommen wenn das Feld `CURRENTNOSORT` vermischt als Datentyp INT und LONG im Solr Index vorhanden ist.
{% endhint %}

##
