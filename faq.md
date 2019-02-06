# 7. FAQ

## Wie kann ich herausfinden wie alt mein Goobi viewer ist?

Im Quelltext der Seite befindet sich ganz am Anfang im meta-Tag bei dem das Attribut name=""version" gesetzt ist. Der Inhalt von dem Attribut content gibt Auskunft über das Alter der Codebasis

```markup
<meta name="version" content="Goobi viewer-3.2-20180719-5b53620" />
```

"**Goobi viewer**" ist der Produktname, "**3.2**" die interne Versionsnummer. "**20180719**" entspricht dem Datum, wann der Goobi viewer kompiliert wurde. "**5b53620**" sind die ersten sieben Zeichen des Git-Commit-Hashs der für die Kompilierung verwendet wurde. 

Das Datum ist ein guter, erster Indikator. Nach dem Git-Commit-Hash kann zum Beispiel auf GitHub gesucht werden um herauszufinden auf welchem Stand die Applikation genau ist. 



## Wie kann ich meinen gesamten Datenbestand neu indexieren?

Für die Neuindexierung des gesamten Datenbestandes muss der Inhalt des [indexed\_mets](konfiguration-indexer/verzeichnisse.md#3-2-18-parameter-indexedmets) Ordners in den [hotfolder](konfiguration-indexer/verzeichnisse.md#3-2-1-parameter-hotfolder) kopiert werden:

```bash
cp /opt/digiverso/viewer/indexed_mets/*.xml /opt/digiverso/viewer/hotfolder/
```

{% hint style="warning" %}
Vor dem Kopieren muss darauf geachtet werden, dass der Hotfolder leer ist damit keine potentiell korrigierten Werke mit einer älteren Version aus dem indexed\_mets Ordner überschrieben werden.
{% endhint %}

## Welche Webbrowser werden vom Goobi viewer unterstützt?

Der Goobi viewer unterstützt alle alle sogenannten "Evergreen Browser". Das sind die aktuellen Versionen von [Google Chrome](https://www.google.com/chrome/), [Firefox](http://www.mozilla.org/firefox/), [Safari](http://www.apple.com/safari/) und [Microsoft Edge](https://www.microsoft.com/en-us/windows/microsoft-edge).

Ältere Versionen, insbesondere der Internet Explorer 11 werden seit Mitte Juli 2018 nicht mehr offiziell unterstützt.

