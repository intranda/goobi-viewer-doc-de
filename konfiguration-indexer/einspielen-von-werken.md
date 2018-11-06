# 3.9 Einspielen von Werken

Um ein Werk zu indexieren, müssen die gewünschten XML-Dateien \(zum Beispiel im METS/MODS, LIDO oder TEI Format\) im Hotfolder platziert werden. Zusätzlich können folgende Ordner mit abgelegt werden, die bei der Indexierung ebenfalls berücksichtigt werden:

```text
/<Dateiname>_media/*.* (Medien: Bilder, Video und Audio)
/<Dateiname>_txt/*.txt (Plain-Text Volltexte)
/<Dateiname>_alto/*.xml (ALTO XML)
/<Dateiname>_xml/*.xml (ABBYY XML)
/<Dateiname>_pdf/*.pdf (vorgerenderte PDF-Seiten)
/<Dateiname>_src/*.* (Dateien, die direkt zum Download angeboten werden sollen)
```

Die Ordner müssen dabei den Dateinamen der zu indexierenden XML-Datei tragen \(ohne deren Erweiterung, aber mit dem entsprechenden Suffix\).  
Beispiel:

```text
/opt/digiverso/viewer/hotfolder/PPN123456789.xml
/opt/digiverso/viewer/hotfolder/PPN123456789_media/
/opt/digiverso/viewer/hotfolder/PPN123456789_txt/
/opt/digiverso/viewer/hotfolder/PPN123456789_wc/
```

{% hint style="info" %}
Dateinamen in Ordnern müssen jeweils den Dateinamen des entsprechenden Datei im Medienordner tragen, zum Beispiel für das Bild 00000001.tif heißt die Volltextdatei 00000001.txt.
{% endhint %}

{% hint style="info" %}
Da der Goobi viewer Indexer sofort anfängt zu indexieren, sobald eine XML-Datei gefunden wird, könnte die Indexierung abgeschlossen sein, bevor die Datenordner fertig kopiert wurden. In dem Fall werden die Ordner nicht berücksichtigt und verbleiben im Hotfolder. Darum sollten METS und LIDO Dateien erst in den Hotfolder kopiert werden, wenn das Kopieren der dazugehörigen Datenordner abgeschlossen ist.
{% endhint %}

Falls nicht Goobi workflow für das Exportieren von Daten in den Hotfolder verwendet wird, ist darauf zu achten, dass die Konfiguration die oben beschriebenen Anforderungen erfüllt.

