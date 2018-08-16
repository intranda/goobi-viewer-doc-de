# 6.4.3 Inhaltstypen

Das CMS-System hat fünf verschiedene Inhaltstypen:

* Text
* Html
* Media \(Bild\)
* Solrquery \(Liste von Werks-Strukturelementen\)
* Pagelist \(Liste von CMS-Seiten\).

Html und Text liegen dabei in mehreren Versionen vor, je eine für jede  Sprache, die im Gobbi viewer konfigurierte wurde. 

Media wiederum besitzt zwei untergeordnete Text-Elemente \(Name und Beschreibung\), die ebenfalls in je einer Ausführung pro Sprache vorliegen; diese werden beim Hochladen von Media-Dateien ins CMS-System festgelegt. 

Solrquery und Pagelist haben den einfachsten Aufbau, jedoch das komplexeste Verhalten, da sie jeweils Listen anderer Objekte liefern.

Die Inhalte aller Inhaltstypen werden auf der Layout-Seite mit der folgenden Notation aufgerufen: 

```text
#{cmsPage.getContent('id')}
```

Hierbei ist zu beachten, dass '`id`', die in der Template-Datei definierte id des Items ist.

Außerdem verfügt jede CMS-Seite über einen Titel und einen Menütitel, die jedoch nicht über das Template gesteuert werden, sondern für jede Seite fest vorgeschrieben sind. Der Menütitel wird nicht auf der Seite selbst angezeigt, sondern dient zur Beschriftung des Links zur CMS-Seite im Navigationsmenü des Goobie viewers. Der Titel kann in der Layout-Datei wie folgt aufgerufen werden:

```text
#{cmsPage.title}
```



Die Typen sind im Folgenden noch einmal genauer beschrieben:

| **Typ**  | Beschreibung |
| :--- | :--- |
| **Titel** | Dies ist ein einfacher Text, der als Titel der Seite dient. |
| **Text**  | Dies ist ein einfacher Text, ohne HTML-Elemente, der beliebig in der Layout-Datei aufgerufen werden kann.  |
| **Html**  | Dies ist ein HTML -Text, der als echtes HTML in die Seite eingebettet wird.  |
| **Media**  | Dies ist eine Bilddatei, die außerhalb des Templates erstellt und mit einer Beschriftung versehen wird.Der Titel einer Media-Datei kann mit `#{cmsPage.getMediaName('media-id')}` aufgerufen werden.Die Beschreibung einer Media-Datei kann mittels `#{cmsPage.getMediaDescription('media-id')}` aufgerufen werden.  |
| **Solrquery**  | Gibt eine Liste von Ergebnissen einer Solr-Anfrage als Java-Objekte zurück. Sie kann nur mit einer entsprechenden Java-Facelets-Syntax verwendet werden. |
| **Pagelist**  | Gibt eine Liste von CMS-Seiten als Java-Objekte zurück, aus denen deren Inhalte analog zu den Inhalten von cmsPage abgerufen werden können. Nur stehen die Elemente der Liste an Stelle von cmsPage. |

