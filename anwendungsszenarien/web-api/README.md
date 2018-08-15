# 6.7 Web API

{% hint style="warning" %}
Die Web API ist in der jetzigen Form als deprecated markiert und wird durch einen REST Service ersetzt.
{% endhint %}

Die Web API erlaubt es, Informationen zu Werken als JSON-Datensätze über einen einfachen GET-URL-Aufruf zu erhalten. Die Datensätze des Treffersets bestehen jeweils aus statisch definierten, sowie optionalen frei konfigurierbaren Feldern.

Folgende statische Felder sind stets enthalten:

| **id**  | Identifier des Werks  |
| :--- | :--- |
| **title**  | Titels des Werks |
| **dateCreated**  | Importdatum des Werks in den Goobi viewer  |
| **collection**  | Erster Sammlungs-Eintrage für dieses Werk |
| **thumbnailUrl**  | URL zum Thumbnail-Bild des Werkes in \(falls vorhanden\) in der Größe 100x120 px |
| **mediumimage**  | URL zum Thumbnail-Bild des Werkes in \(falls vorhanden\) in der Größe 600x500 px  |
| **url**  | URL zur Bildansicht dieses Werks  |

Details zur Konfiguration weiterer Felder können unter `Fehler! Verweisquelle konnte nicht gefunden werden.`gefunden werden.

