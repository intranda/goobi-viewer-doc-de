# August

Der August war ebenfalls noch durch die Sommerferien geprägt. Neben diversen kleineren Bugfixes hat es an zwei Bereichen Feature-Entwicklungen gegeben.

## Entwicklungen

### Crowdsourcing

In dem Crowdsourcing erfasste nutzergenerierte Inhalte, also Informationen, die auf dem Bild markiert und mit Metadaten versehen wurden, werden nun für die Anzeige im Werk vollständig aus dem Solr Index gelesen. Dadurch ist die Anzeige unabhängig von dem Crowdsourcing Modul selbst. Bisher war das nur für die Volltexte und Transkriptionen der Fall. Diese Anpassung erlaubt die Ergebnisse nutzergenerierter Inhalte über mehrere Instanzen zu teilen, sofern sie den selben Solr Index nutzen.

### SEO

Das Thema Suchmaschinenoptimierung geht weiter und die bestehden Funktionalität wurde weiter ausgebaut. Bei den HighWire Press Tags wie auch den DublinCore Tags wurde noch einmal Hand angelegt um mehr Metadaten auszugeben und sie im DublinCore Format auch noch spezifischer auszuzeichnen.

Die auf der Seite Sitelinks aufgelisteten Werke verweisen nun immer auf die Seite mit den Bibliographischen Daten.

Ebenfalls wurde viel an der Generierung der Sitemap gearbeitet, damit diese auch mit großen Datenbeständen gut skaliert. In die Sitemap werden folgende Seiten aufgenommen:

* alle CMS Seiten
* pro Werk:
  * die Seite mit dem ersten Bild beziehungsweise dem Repräsentanten
  * die Seite "Bibliographische Daten"
  * die Seite "Inhaltsverzeichnis"
  * alle Seiten mit Volltext

Die Generierung der Sitemap erfolgt über einen Aufruf der REST Schnittstelle. Dafür steht der folgende Endpoint zur Verfügung:

* /rest/sitemap/update/

Damit die Suchmaschinen die Reihenfolge von Seiten besser verstehen, wurden auf Werksseiten mit Paginator um `rel="next"`- und `rel="prev"`-Links im Header ergänzt.

### Cronjob

Es gibt bestimmte Aufgaben, die im Goobi viewer regelmäßig stattfinden sollen. Diese wurden zusammengetragen und in eine Cron-Datei zusammengefasst. Eine Vorlage dafür befindet sich in der [Updateanleitung](../../9/9.1.md#2018-09-06).

