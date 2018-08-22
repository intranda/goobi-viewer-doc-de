# 2.13 Verlinkung bestimmter Strukturtypen auf bestimmte Seitenansichten

Wenn gewünscht, können einzelne Stukturtypen auf fest konfigurierte Seitenansichten verlinkt werden. Möchte man zum Beispiel Mongraphien immer im Inhaltsverzeichnis \(anstatt in der Bildansicht\) und Handschriften in der Metadatenansicht öffnen, kann dies folgendermaßen konfiguriert werden:

```markup
<viewer>
    <docstructTargetPageTypes>
        <_DEFAULT>metadata</_DEFAULT>
        <Monograph>toc</Monograph>
        <Manuscript>toc</Manuscript>
    </docstructTargetPageTypes>
</viewer>
```

In diesem Fall wird die übliche Logik zur Findung der passenden Seitenansicht beim Öffnen des Werks übergangen und die konfigurierte Ansicht verwendet. Ausnahme: Das Werk besitzt eine Übersichtsseite.

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
