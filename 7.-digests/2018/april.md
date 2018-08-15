# April

Der Monat April war von zwei Hauptthemenbereichen geprägt 

1. Implementierung der IIIF Presentation API.
2. Bugfixing und Refaktorisieren

Zu der IIIF Presentation API gleich mehr als erster Punkt unter den Entwicklungen. Zum Thema Bugfixing und Refaktorisieren ein paar Hintergrundeinblicke am Ende dieses Digests.

## Entwicklungen

### IIIF

Wärend wir im letzten Monat über die IIF Image API und deren Kompatibilität zur Version 2.1 berichtet haben können wir diesen Monat vermelden, dass der Goobi viewer kompatibel zu der IIIF Presentation API 2.1.1 ist. Dabei ist es egal, ob die Ursprungsdokumente im METS/MODS, LIDO, TEI, EAD oder weiterem Format vorliegen. Sobald diese durch den Goobi viewer selbst angezeigt werden können, also die Metadaten von dem Goobi viewer Indexer indexiert und im Solr Suchindex gespeichert wurden, werden auch automatisch IIIF Presentation Manifest Dateien generiert.

Ein Download-Link für das Manifest eines Werkes oder Objektes steht oberhalb der Bildanzeige zur Verfügung. Für Entwickler stehen weitere Methoden zur Verfügung, um die URLs zu den verschiedenen Manifesten in eigene Anzeigen einbinden zu können:

* [https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/javadoc/de/intranda/digiverso/presentation/controller/imaging/IIIFPresentationAPIHandler.html](https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/javadoc/de/intranda/digiverso/presentation/controller/imaging/IIIFPresentationAPIHandler.html)

Die Anzeige der Manifeste kann dann zum Beispiel im Mirador oder im UniversalViewer erfolgen.

### CMS

Im CMS bestent nun die Möglichkeit einzelne Seiten mit Werken zu verknüpfen. Damit kann innerhalb der Werksanzeige automatisch auf die entsprechende Seite verlinkt werden.

Weiter können die URLs zu hochgeladenen Medien einfach kopiert werden. Das erleichtert die Arbeit vor allem, wenn diese Medien dann im Texten auf CMS Seiten weiter verwendet werden sollen.

### Resolver

Dem METS und LIDO Resolver können nun auch URNs übergeben werden. Vorher war es auf die Werksidentifier wie PPNs oder AC-Nummern beschränkt.

## Entwicklerdokumentation

Für Entwickler wird das Javadoc wie auch das JSDoc automatisch bei jedem Commit generiert und auf Github Pages veröffentlicht. Die Dkumentationen stehen unter den folgenden Adressen zur Verfügung:

* Javadoc: [https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/javadoc/index.html](https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/javadoc/index.html)
* JSDoc:   [https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/jsdoc/index.html](https://intranda.github.io/goobi-viewer-core/goobi-viewer-core/doc/jsdoc/index.html)

Die URLs sind ebenfalls in der README.md von Goobi viewer Core zu finden.

## Bugfixing und Refaktorisieren

In der Softwareentwicklung gibt es immer wieder Programmierfehler. Diese werden "Bugs" genannt, Korrekturen sind "Bugfixes". Bugs gibt es von ganz unterschiedlicher Art. Beispiele sind Syntaxfehler \(eine Klammer geht auf, aber nicht wieder zu\), Schleifen die sich nie wieder beenden oder Dateien die gelesen aber dann nie wieder geschlossen werden. 

Es gibt aber auch Funktionalität die ab einem gewissen Punkt nicht mehr gut skaliert. Hat eine digitale Bibliothek 10, 100, 1000 oder 10.000 eindeutige Besucher pro Tag, die ganz unterschiedlich lange mit dem Datenbestand arbeiten? Eine Datenbankabfrage die bei 100 Besuchern innerhalb von wenigen Millisekunden bearbeitet wird, kann bei 10.000 Besuchern und mehrfachen parallelen Abfragen dann auf einmal einige Sekunden dauern. Hier wird es schwieriger zu definieren, ob es sich dabei um einen Fehler handelt, oder um eine neue Anforderung die vor einigen Jahren noch nicht existierte.

Für uns im Goobi viewer Team ist es immer wichtig etwas nachstellen zu können. Wenn ein Entwickler ein Verhalten bei sich in der Entwicklungsumgebung reproduzieren kann, dann können wir auch daran arbeiten dieses zu Verändern. Die Lösung ist dann ganz unterschiedlich und die Zeit die dort hinein fließt lässt sich nicht in Quelltext ablesen. Manchmal dauert es über einen Tag ein Verhalten nachzustellen, einige Stunden um dieses zu verstehen und dann noch einmal mehrere Stunden um verschiedene Lösungsansätze auszuprobieren. Am Ende ist es dann manchmal nur eine Zeile Code die anders ist. 

Wir im Goobi viewer Team arbeiten mit verschiedenen Hilfen, die uns erlauben Fehler in der Entwicklung schnell zu erkennen und zu beheben. Diese sind vor allem technischer Natur, aber eines unserer Hilfsmittel ist die sogenannte "Refaktorisierung". Dieser Prozess beschreibt das Aufräumen von Quelltext bei gleichbleibender Funktionalität. Er führt dazu, dass der Code übersichtlich bleibt oder einfacher zu verstehen ist. Dafür nehmen nehmen wir uns immer wieder Zeit. Jeden Monat ein bisschen. Diese Arbeiten sind nach außen hin nicht sichtbar, es gibt keine neuen Features, Buttons, Anzeigen etc. Sie sind aber für die kontinuierliche Weiterentwicklung des Goobi viewers sehr wichtig. 

