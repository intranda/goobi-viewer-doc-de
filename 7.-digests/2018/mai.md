---
description: 'Goobi viewer Digest: 2018/05'
---

# Mai

Im Mai haben drei Kunden ein Update des Goobi viewers bekommen:

1. Digitale Bibliothek Mecklenburg Vorpommern
2. Digitale Landesbibliothek Berlin
3. eLiechtensteinensia

Stolz sind wir weiter darüber, dass das Grimm-Portal der Universitätsbibliothek Kassel in deren Jahresbericht zur Erwähnung kommt:

* [https://www.uni-kassel.de/ub/fileadmin/datas/ub/dokumente/Jahresbericht\_2017\_WEB.pdf](https://www.uni-kassel.de/ub/fileadmin/datas/ub/dokumente/Jahresbericht_2017_WEB.pdf)

Von den neuen Funktionen her ist der Mai ebenfalls ein sehr produktiver Monat gewesen. Die Entwicklungen im einzelnen:

## Entwicklungen

### SEO

Es wurden erste Schritte unternommen den Goobi viewer im Kontext Suchmaschinenoptimierung zu verbessern. Hierfür wurde die bestehende Funktionalität um eine XML-Sitemap zu generieren auf die  
REST Schnittstelle portiert.

Ebenfalls neu hinzugekommen ist ein automatisch generierter SiteLinks Bereich, der alle neu hinzugekommenen Werke pro Jahr auflistet. 

Für die Unterstützung von Google Scholar wurden HighWire Press Tags mit in die Meta-Tags aufgenommen. In diesem Kontext wurde der Konfigurationsschalter zum automatischen rendern von DublinCore Informationen in den Meta-Tags geändert, so dass diese nun ausgeschaltet sind und den HighWire Press Tags den Vorrang geben.

Es existieren Pläne für die kommenden Monate um im Kontext Suchmaschinenoptimierung weitere Entwicklungen voranzutreiben

### Sprachen und Mehrsprachigkeit

Wir freuen uns, dass der Goobi viewer Core vollständig auf französisch übersetzt wurde!

Der Goobi viewer kann mit mehrsprachigen Metadaten umgehen. Das bedeutet, dass wenn für ein Metadatum mehrere Übersetzungen vorliegen, dann nur die jeweilige Sprache angezeigt werden kannn, in der auch der Rest der Oberfläche gerade angezeigt wird.  
Diese Funktionalität wurde deutlich erweitert, so dass sie nun auch beim Stöbern, bei der Facettierung und bei der Anzeige von Suchtreffern zur Verfügung steht.

### Facettierung

Es wurde eine neue Komponenten für die Facettierung nach Zeit entwickelt. Während vorher nur nach einem Jahr gefiltert werden konnte, ist es nun möglich über eine Slider einen Zeitraum auszuwählen. 

### Gruppierung von Metadaten

In der Metadatenanzeige können nun Metadaten gruppiert angezeigt werden. Dafür kann bei der Definition eines Metadatums das von LIDO Events bekannte type-Attribut verwendet werden. 

### CMS

Eine große Neuerung verbirgt sich im CMS-Backend. Über den neuen Sammlungs-Bereich können Sammlungsnamen und Übersetzungen, beschreibende Texte und Übersetzungen sowie ein Repräsentant und optional eine Verlinkung auf eine CMS Seite definiert werden. Diese neue Funktion ist bereits in den stabilen Master-Branch zurück geflossen und steht mit einem Update zur Verfügung. Unter Umständen müssen für Kundenthemes noch weitere spezifische Anpassungen vorgenommen werden. 

### Sonstiges

* Die Generierung von IIIF Presentation Manifesten aus TEI und CMDI Dokumenten wurde erweitert, so dass nun noch mehr Informationen zur Verfügung stehen.
* Bei den Core-XHTML Dateien wurde verschiedene Funktionalität rund um die Bildanzeige in Komponenten ausgelagert und eine neue viewObject-Seite wurde eingefügt die diese Komponenten einbindet. Dadurch ist es einfacher nicht nur Werks, sondern auch objektbezogene Seiten zu erstellen.
* Das URL-Handling ist nun komplett betriebssystemunabhängig. Der Goobi viewer Core läuft damit unter Linux, Mac und Windows ohne Einschränkungen.

