# 3.2 Verzeichnisse

Für den Betrieb muss für den Goobi viewer Indexer eine Reihe von Ordnern konfiguriert werden, aus denen Dateien gelesen beziehungsweise in denen Dateien abgelegt werden können. Bei Nichtvorhandensein bestimmter Ordner werden diese automatisch angelegt, die Pfadkonfigurationen dürfen allerdings nicht fehlen.

```markup
<init>
     <hotFolder>/opt/digiverso/viewer/hotfolder/</hotFolder>
     <tempFolder>/opt/digiverso/indexer/temp/</tempFolder>
     <viewerHome>/opt/digiverso/viewer/</viewerHome>
     <dataRepositories>
          <enabled>false</enabled>
          <dataRepositoriesHome>/opt/digiverso/viewer/data</dataRepositoriesHome>
          <maxRecords>10000</maxRecords>
          <dataRepository>1</dataRepository>
          [...]
     </dataRepositories>
     <mediaFolder>media</mediaFolder>
     <pyramidTiffFolder>ptif</pyramidTiffFolder>
     <altoFolder>alto</altoFolder>
     <fulltextFolder>fulltext</fulltextFolder>
     <fulltextCrowdsourcingFolder>fulltext_crowd</fulltextCrowdsourcingFolder>
     <wcFolder>wc</wcFolder>
     <pagePdfFolder>pdf</pagePdfFolder>
     <sourceContentFolder>source</sourceContentFolder>
     <userGeneratedContentFolder>ugc</userGeneratedContentFolder>
     <mixFolder>mix</mixFolder>
     <indexedMets>indexed_mets</indexedMets>
     <indexedLido>indexed_lido</indexedLido>
     <successFolder>/opt/digiverso/viewer/success/</successFolder>
     <updatedMets>/opt/digiverso/viewer/updated_mets/</updatedMets>
     <deletedMets>/opt/digiverso/viewer/deleted_mets/</deletedMets>
     <errorMets>/opt/digiverso/viewer/error_mets/</errorMets>
     <origLido>/opt/digiverso/viewer/orig_lido/</origLido>
</init>
```

#### 3.2.1 Parameter: hotFolder

In diesem Ordner werden zu indexierende Inhalte abgelegt \(etwa durch Goobi\). Der Ordner wird vom Goobi viewer Indexer in kurzen Zeitabständen auf neue XML Dateien überprüft. Wenn neue Dateien gefunden werden, werden diese \(falls ein unterstütztes Datenformat vorliegt\) nacheinander indexiert und aus dem Hotfolder entfernt.

#### 3.2.2 Parameter: tempFolder

Ordner für temporäre Dateien.

#### 3.2.3 Parameter: viewerHome

Basispfad des Goobi viewers.

#### 3.2.4 Parameter: dataRepositories/enabled

Aktiviert die Aufteilung von Werksdaten \(Medien, XML, Volltexte, etc.\) auf mehrere Datenrepositories. Dadurch kann die Datenmenge pro Ordner auf eine Bestimmte Anzahl begrenzt werden.

#### 3.2.5 Parameter: dataRepositories/dataRepositoriesHome

Ordner, relativ zu dem die einzelnen Repository-Ordner gesucht beziehungsweise angelegt werden.

#### 3.2.6 Parameter: dataRepositories/maxRecords

Anzahl der Werke, die eine Datenrepository maximal enthalten darf. Standardwert ist `10000`.

#### 3.2.7 Parameter: dataRepositories/dataRepository

Dieses Element darf beliebig oft existieren und definiert die einzelnen Datenrepositories. Der eingetragene Name darf allerdings jeweils nur einmal vorkommen. Ordner mit dem eingetragenen Wert als Namen werden unterhalb von `dataRepositoriesHome` gesucht beziehungsweise bei Nichtvorhandensein angelegt \(das heißt der eingetragene Wert darf nur Zeichen enthalten, die das zugrundeliegende Dateisystem erlaubt\). Unterhalb des jeweiligen Ordners befindet sich jeweils eine komplette Ordnerstruktur für Mediendateien, XML, Volltexte etc. \(diese werden ebenfalls automatisch angelegt\).

#### 3.2.8 Parameter: mediaFolder

Dieser Ordner dient als Ablage für etwaige Mediendateien \(Bilder, Video und Audio\) eines indexerten Objekts. Diese werden jeweils in einem Unterordner abgelegt, der den Identifier des jeweiligen Objekts als Namen trägt. Die Mediendateien müssen stets vorliegen, da sie aus diesem Ordner in den Goobi viewer geladen werden. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.9 Parameter: pyramidTiffFolder

Dieser Ordner enthält zusätzlich zu regulären Bildern, die im mediaFolder liegen, gegebenenfalls gekachelte Pyramiden-TIFF Dateien. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.10 Parameter: altoFolder

In diesem Ordner werden ALTO XML Dateien abgelegt. Diese enthalten detaillierte OCR Ergebnisse und können sowohl für die Extraktion von Volltexten als auch von Wortkoordinaten verwendet werden. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.11 Parameter: altoCrowdsourcingFolder

Dieser Ordner enthält ebenfalls ALTO XML Dateien. Diese stammen allerdings aus den Crowdsourcing Funktionen des Goobi viewers. Diese werden beim Indexieren bevorzugt verwendet, das heißt wenn für eine Seite ein ALTO Dokument aus dem Crowdsourcing vorhanden ist, wird dieses indexiert, und nicht das Dokument aus dem OCR.

#### 3.2.12 Parameter: fulltextFolder

Hier werden die \(plaintext\) Volltext Dateien nach dem Indexieren abgelegt. Die jeweils in einem Unterordner abgelegt werden, der den Identifier des jeweiligen Objekts als Namen trägt. Sie sind zwar nicht für den Betrieb des Goobi viewers erforderlich \(die Volltexte werden vollständig indexiert\), allerdings können sie für eine evtl. Reindexierung eines Objekts  
wiederverwendet werden \(für den Fall, dass kein Volltext Ordner im Hotfolder gefunden wird, sucht der Goobi viewer Indexer nach einem bereits vorhandenen Volltext Ordner aus früherer Indexierung\).  
Folgendes ist dabei zu beachten: Ist für eine Seite zusätzlich ein ALTO Dokument vorhanden, wird dieses bevorzugt für die Indexierung von Volltexten verwendet.  
Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu `viewerHome` \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.13 Parameter: fulltextCrowsourcingFolder

Dieser Ordner enthält ebenfalls einfache Volltext Dateien. Diese stammen allerdings aus den Crowdsourcing Funktionen des Goobi viewers. Diese werden beim Indexieren bevorzugt verwendet, das heißt wenn für eine Seite ein Volltext Dokument aus dem Crowdsourcing vorhanden ist, wird dieses indexiert, und nicht das Dokument aus dem OCR.

#### 3.2.14 Parameter: wcFolder

Hier werden die TEI Wortkoordinaten Dateien nach dem Indexieren abgelegt. Diese werden jeweils in einem Unterordner abgelegt, der den Identifier des jeweiligen Objekts als Namen trägt. Sie sind zwar nicht für den Betrieb des Goobi viewers erforderlich \(die Wortkoordinaten werden vollständig indexiert\), allerdings können sie für eine evtl. Reindexierung eines Objekts wiederverwendet werden \(für den Fall, dass kein Wortkoordinaten Ordner im Hotfolder gefunden wird, sucht der Goobi viewer Indexer nach einem bereits vorhandenen Wortkoordinaten Ordner aus früherer Indexierung\).  
Folgendes ist dabei zu beachten: Ist für eine Seite zusätzlich ein ALTO Dokument vorhanden, wird dieses bevorzugt für die Generierung von Wortkoordinaten verwendet.  
Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.15 Parameter: pagePdfFolder

Hier werden vorgerenderte PDF Dateien für die einzelnen Seiten des Objekts nach dem Indexieren abgelegt. Diese werden jeweils in einem Unterordner abgelegt, der den Identifier des jeweiligen Objekts als Namen trägt. Bei Vorhandensein dieser Dateien kann für das betreffende Objekt die Generierung von PDF Dokumenten erheblich beschleunigt werden. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.16 Parameter: sourceContentFolder

Hier werden Dateien abgelegt, die für das Objekt zum direkten Download angeboten werden sollen \(zum Beispiel Born Digital Materialien\) abgelegt. Diese werden jeweils in einem Unterordner abgelegt, der den Identifier des jeweiligen Objekts als Namen trägt. Für jede Datei, die hier liegt, wird für das betreffende Objekt jeweils ein Download Link angezeigt. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.17 Parameter: userGeneratedContentFolder

Hier werden XML Dokumente abgelegt, die nutzergenerierte Inhalte aus den Crowdsourcing Funktionen des Goobi viewers stammen. Diese werden für die Anzeige und die Suchbarkeit dieser Inhalte im normalen Betrieb verwendet. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.18 Parameter: Parameter: mixFolder

Hier werden die MIX Dateien \(technische Informationen über die Bilder des Objekts\) nach dem Indexieren abgelegt. Diese werden jeweils in einem Unterordner abgelegt, der den Identifier des jeweiligen Objekts als Namen trägt. Sie sind zwar nicht für den Betrieb des Goobi viewers erforderlich \(relevante MIX Daten werden indexiert\), allerdings können sie für eine evtl. Reindexierung eines Objekts wiederverwendet werden \(für den Fall, dass kein MIX Ordner im Hotfolder gefunden wird, sucht der Goobi viewer Indexer nach einem bereits vorhandenen MIX Ordner aus früherer Indexierung\). Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.19 Parameter: indexedMets

Hier werden die METS Dateien nach dem Indexieren abgelegt. Sie sind nicht für den allgemeinen Betrieb des Goobi viewers erforderlich, müssen allerdings vorliegen, falls ein Dokument über den METS Resolver angefordert wird. Dieser Ordner wird relativ zu dataRepositoriesHome \(bei `dataRepositories/enabled = true`\) beziehungsweise zu viewerHome \(bei `dataRepositories/enabled = false`\) gesucht beziehungsweise angelegt. Aus diesem Grund darf der Wert nur den Namen und keinen absoluten Pfad enthalten.

#### 3.2.20 Parameter: indexedLido

Hier werden die LIDO Dateien von Einzelobjekten nach dem Indexieren abgelegt. Sie sind nicht für den allgemeinen Betrieb des Goobi viewers erforderlich, müssen allerdings vorliegen, falls ein Dokument über den LIDO Resolver angefordert wird.

#### 3.2.21 Parameter: updatedMets

Wird eine METS oder LIDO Datei reindexiert, wird die vorherige Version dieser Datei hier archiviert. Dabei wird an den Dateinamen der Zeitstempel der jeweiligen Reindexierung angehängt.

{% hint style="info" %}
Für den Goobi viewer besitzt dieser Ordner keine Relevanz, muss aber dennoch existieren.
{% endhint %}

#### 3.2.22 Parameter: deletedMets

Wird ein Objekt aus dem Index gelöscht, wird die betreffende METS beziehungsweise LIDO Datei hier abgelegt.

{% hint style="info" %}
Für den Goobi viewer besitzt dieser Ordner keine Relevanz, muss aber dennoch existieren.
{% endhint %}

#### 3.2.23 Parameter: successFolder

Hier werden Dateien abgelegt, die dazu dienen, Goobi eine erfolgreiche Indexierung zu signalisieren. Anhand dieser Dateien erfährt Goobi den Ausgang der Indexierung eines Vorgangs und meldet diesen dem Benutzer.

{% hint style="info" %}
Für den Goobi viewer besitzt dieser Ordner keine Relevanz, muss aber dennoch existieren.
{% endhint %}

#### 3.2.24 Parameter: errorMets

Scheitert die Indexierung eines Objekts, wird die betreffende METS beziehungsweise LIDO Datei hier abgelegt. Zusätzlich wird die Fehlermeldung, die der Goobi viewer Indexer generiert, in eine Logdatei geschrieben und ebenfalls dort abgelegt. Anhand dieser Dateien erfährt Goobi den Ausgang der Indexierung eines Vorgangs und meldet diesen dem Benutzer.

{% hint style="info" %}
Für den Goobi viewer besitzt dieser Ordner keine Relevanz, muss aber dennoch existieren.
{% endhint %}

#### 3.2.25 Parameter: origLido

Hier werden die originalen LIDO Dateien, so wie sie im Hotfolder vorgefunden werden, abgelegt. Diese können u.U. Tausende von Objekten enthalten, die zunächst in einzelne LIDO Datensätze aufgespalten werden \(siehe 3.1.13\). Die originalen Dateien sind für den Betrieb nicht notwendig und dienen nur der Archivierung.

{% hint style="info" %}
Für den Goobi viewer besitzt dieser Ordner keine Relevanz, muss aber dennoch existieren.
{% endhint %}

