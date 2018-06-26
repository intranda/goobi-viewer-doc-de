# 2.10. Suche

Die Suche im Goobi viewer erlaubt eine kombinierte Suche sowohl in den Metadaten als auch in den Volltexten. Je nach Auswahl kann eine Suche ebenfalls lediglich auf die Metadaten oder die Volltexte der digitalen Sammlungen eingeschränkt werden. Verknüpfungen von Suchbegriffen, eine Suche mit Rechts- oder Linkstrunkierung oder auch eine Phrasensuche sind ebenfalls realisierbar.

![](../../.gitbook/assets/suche.png)

Abhängig von der Präzision der Suchabfrage und der Anzahl der indizierten Objekte können sich hunderte bzw. tausende Suchtreffer ergeben, die auf einer über mehrere Seiten verteilten Suchtrefferliste angezeigt werden. Die Anzahl der pro Seite angezeigten Suchtreffer kann über das folgende Element konfiguriert werden \(der Standardwert ist 10\):

```markup
<search>
    <hitsPerPage>10</hitsPerPage>
    <fulltextFragmentLength>200</fulltextFragmentLength>
</search> 
```

Das Element `fulltextFragmentLength` definiert die ungefähre länge der Volltext-Ausschnitte für die Suchtrefferanzeige. Standarfwert ist 200.

