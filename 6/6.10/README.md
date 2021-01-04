# 6.10 REST API

Die REST API erlaubt es, Informationen zu Werken als JSON-Datensätze über einen einfachen GET-URL-Aufruf zu erhalten. Die Datensätze des Treffersets bestehen jeweils aus statisch definierten, sowie optionalen frei konfigurierbaren Feldern.

Folgende statische Felder sind stets enthalten:

| **Feldname**  | Inhalt |
| :--- | :--- |
| **id** | Identifier des Werks |
| **title**  | Titels des Werks |
| **dateCreated**  | Importdatum des Werks in den Goobi viewer  |
| **collection**  | Erster Sammlungs-Eintrage für dieses Werk |
| **thumbnailUrl**  | URL zum Thumbnail-Bild des Werkes in \(falls vorhanden\) in der Größe 100x120px |
| **mediumimage**  | URL zum Thumbnail-Bild des Werkes in \(falls vorhanden\) in der Größe 600x500px  |
| **url**  | URL zur Bildansicht dieses Werks  |

