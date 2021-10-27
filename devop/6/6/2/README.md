# 6.6.2 CSS und Javascript

## Allgemein

Für die Verwaltung der vom Goobi viewer verwendeten CSS und Javascript Abhängigkeiten wird eine Kombination aus NPM und Grunt verwendet. Sie werden in der `package.json` verwaltet.

## Vorbereitungen

Bei einer neuen Installation muss sichergestellt sein, dass `npm` und die `grunt-cli` installiert sind:

```
sudo apt install npm
sudo npm install -g grunt-cli
```

Danach können die Abhängigkeiten erstmalig mit dem folgenden Kommando heruntergeladen werden:

```
npm install
```

## Updates prüfen

Mit dem folgenden Kommando kann überprüft werden ob Patches für installierte Abhängigkeiten vorliegen:

```
npm outdated
```

Liegt für die Abhängigkeit ein Update vor, so wird dieses wie folgt angezeigt:

```
Package                Current  Wanted  Latest  Location
leaflet.markercluster    1.5.1   1.5.3   1.5.3  global
```

Liegt kein Update vor, ist die Ausgabe leer.

## Updates installieren

### Patch-Releases

npm ist so konfiguriert, dass nur Patch-Versionen installierter Abhängigkeiten eingespielt werden.

Nach einem Update müssen die aktualisierten Pakete aus dem `node_modules` Verzeichnis in den Goobi viewer Core kopiert werden:

```
# Abhängigkeit aktualisieren
npm update PAKETNAME

# Pakete in den Goobi viewer Core kopieren
grunt copyDeps [--verbose]
```

### Major- und Minor Releases

{% hint style="info" %}
Es sollte vor einem Update geprüft werden, ob bei der Verwendung bestimmter Pakete Besonderheiten zu beachten sind. Angaben dazu befinden sich in der Unterseite 6.6.2.1.&#x20;
{% endhint %}

Für die Installation von Major- oder Minor Releases muss diese explizit in der `package.json` in dem Abschnitt _dependencies_ angepasst werden. Dies ist hier exemplarisch mit einem Update von TinyMCE 5.9.1 auf 5.10.0 gezeigt:

#### **Anzeigen des Updates**

```
npm outdated tinymce
Package  Current  Wanted  Latest  Location              Depended by
tinymce    5.9.2   5.9.2  5.10.0  node_modules/tinymce  goobi-viewer-core
```

#### **Aktualisieren der package.json**

{% code title="package.json" %}
```
/* ALT */
  "dependencies": { 
    "tinymce": "~5.9.1" 
  } 


/* NEU */
  "dependencies": { 
    "tinymce": "~5.10.0" 
  } 
```
{% endcode %}

#### **Installieren der neuen Library**

```
npm install
```

#### **Übernahme in den Goobi viewer Core**

```
grunt copyDeps
```

## Abhängigkeit hinzufügen

Um eine neue Abhängigkeit hinzuzufügen muss folgendes passieren:

#### Installation der neuen Abhängigkeit

```
npm install [<@scope>/]PAKETNAME
```

#### Anpassen des SemVer-Präfix in der package.json

npm installiert neue Pakete standardmäßig mit dem `^` Prefix. Dieses muss manuell zur Tilde `~`  geändert werden, um nur Patch-Versions zu aktualisieren.

{% code title="package.json" %}
```
/* ALT */
  "dependencies": { 
    "PAKETNAME": "^4.0.0" 
  } 


/* NEU */
  "dependencies": { 
    "PAKETNAME": "~4.0.0" 
  } 
```
{% endcode %}

#### Hinzufügen von Pfaddefinition in copyDeps Task

Damit die Dateien korrekt kopiert werden müssen in der `grunt/copyPaths.js` die entsprechenden Pfaddefinitionen hinzugefügt werden.

#### **Übernahme in den Goobi viewer Core**

```
grunt copyDeps
```
