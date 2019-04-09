# 2.13 Öffnen bestimmter Dokumententypen in alternativen Seitenansichten

Es ist möglich bestimmte Dokumententypen in alternativen Seitenansichten zu öffnen. Sollen zum Beispiel Zeitungen und Zeitungsbände immer in der Kalenderansicht \(anstelle der Bildanzeige\) geöffnet werden, kann dies folgendermaßen konfiguriert werden:

```markup
<viewer>
    <docstructTargetPageTypes>
        <Newspaper>calendar</Newspaper>
        <NewspaperVolume>calendar</NewspaperVolume>
        <MultiVolumeWork>toc</MultiVolumeWork>
        <Periodical>toc</Periodical>
    </docstructTargetPageTypes>
</viewer>
```

In diesem Fall wird die übliche Logik zur Findung der passenden Seitenansicht beim Öffnen des Werks übergangen und die konfigurierte Ansicht verwendet. Ausnahme: Das Werk besitzt eine Übersichtsseite, dann wird diese geöffnet.

Optional kann außerdem unter `_DEFAULT` die Standardansicht für alle Strukturtypen festgelegt werden. Diese wird verwendet, wenn keine explizite Konfiguration für den betreffenden Strukturtyp existiert. Besitzt das Werk eine Übersichtsseite, wird auch hier auf die Übersichtsseite verlinkt und nicht auf die konfigurierte Ansicht.

Folgende Ansichten sind möglich:

* image
* toc
* thumbs
* preview
* metadata
* fulltext
* overview
* fullscreen
* calendar

