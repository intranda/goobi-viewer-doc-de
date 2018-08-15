# März

Auch im März haben verschiedene neue Features in den Goobi viewer Einzug gehalten. Sie sind in diesem Monat aber vor allem unter der Haube zu finden.

Gefreut hat uns die Nachricht, dass die UB Kassel nun mit seinen Digitalisaten in der Europeana vertreten ist. Herzlichen Glückwunsch!

* [https://www.europeana.eu/portal/de/search?per\_page=96&q=Universit%C3%A4tsbibliothek+Kassel&qf%5B%5D=Handschrift&view=grid](https://www.europeana.eu/portal/de/search?per_page=96&q=Universit%C3%A4tsbibliothek+Kassel&qf%5B%5D=Handschrift&view=grid)

## Entwicklungen

### IIIF

Eine Entwicklung der größeren Art ist im Kontext IIIF in den Master-Branch zurück geflossen. Hier wurde die Kompatibilität mit der Image API 2.1 sichergestellt auf einem hohen Niveau sichergestellt. Gleichzeitig verwendet der Goobi viewer Core für seine Bildaufrufe grundsätzlich IIIF URLs und Methoden. Diese Entwicklungen und Umstellungen verbessern die Codequalität, Stabilität und Wartbarkeit erheblich.

### Web Annotations

Neu hinzugekommen ist ebenfalls die Unterstützung für Web Annotations. Kommentare, die Benutzern für Bilder eingegeben haben, sind nun über den Standard abrufbar. Er wird als offener Standard von der W3C Annotation Group gepflegt \([https://www.w3.org/annotation/\).](https://www.w3.org/annotation/%29.) Es können einzelne Kommentare, alle Kommentare für eine Seite oder alle Kommentare für ein Werk persistent angesprochen werden. Die Unterstützung von Web Annotations ist ein weiterer Baustein für die Vernetzung der Daten im Digital Hummanities Kontext.

### CMS-Seite für Glossare

Für Goobi workflow wurde ein neues Workflow-Plugin zur Verwaltung von Vokabularien entwickelt. Im Goobi viewer gibt es ein neues CMS-Template, mit denen diese Vokabularien als Glossar dargestellt werden können. Für die Übertragung zwischen Goobi workflow und Goobi viewer steht ein neuer REST API Endpoint zur Verfügung. Über diesen kann das gesamte Glossar vollautomatisch zwischen den beiden Systemen übertragen werden.

### Themes

Bisher war notwendig, dass Themes für den Goobi viewer als kompilierte Jar \(WebFragment\) mit der Applikation gemeinsam ausgeliefert werden. Dieses System entstand bei der Freigabe des intranda viewers als Open Source und der Notwendigkeit, die einzelnen Kundenthemes in unabhängigen Git-Repositories zu migrieren und auszuliefern. Diese technische Abhängigkeit wurde im letzten Monat aufgelöst. Neben der bisherigen steht nun eine weitere Methode zur Verfügung, die es erlaubt das Theme lokal im Verzeichnisbaum liegen zu haben. Dadurch wird gerade die Entwicklung und Pflege des Themes selbst deutlich einfacher und komfortabler.

