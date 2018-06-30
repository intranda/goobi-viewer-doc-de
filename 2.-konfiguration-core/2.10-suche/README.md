# 2.17 Suche

Die Suche im Goobi viewer erlaubt eine kombinierte Suche sowohl in den Metadaten als auch in den Volltexten. Je nach Auswahl kann eine Suche ebenfalls lediglich auf die Metadaten oder die Volltexte der digitalen Sammlungen eingeschränkt werden. Verknüpfungen von Suchbegriffen, eine Suche mit Rechts- oder Linkstrunkierung oder auch eine Phrasensuche sind ebenfalls realisierbar.

![Einfache Suche](../../.gitbook/assets/suche%20%281%29.png)

Abhängig von der Präzision der Suchabfrage und der Anzahl der indexierten Werke können sich hunderte beziehungsweise tausende Suchtreffer ergeben, die auf einer über mehrere Seiten verteilten Suchtrefferliste angezeigt werden. Die Anzahl der pro Seite angezeigten Suchtreffer kann über das folgende Element konfiguriert werden \(der Standardwert ist 10\):

```markup
<search>
    <hitsPerPage>10</hitsPerPage>
    <fulltextFragmentLength>120</fulltextFragmentLength>
</search>
```

Das Element `fulltextFragmentLength` definiert die ungefähre länge der Volltext-Ausschnitte für die Suchtrefferanzeige. Standardwert ist 200.

Um die Suchbereiche der einfachen Suche zu definieren steht der folgende Konfigurationsblock zur Verfügung:

```markup
<search>
    <filters>
        <filter>filter_ALL</filter>
        <filter>filter_DEFAULT</filter>
        <filter>filter_FULLTEXT</filter>
        <!-- <filter>filter_NORMDATATERMS</filter> -->
        <!-- <filter>filter_UGCTERMS</filter> -->
        <!-- <filter>filter_OVERVIEWPAGE</filter> -->
    </filters>
</search>
```

Jeder filter-Eintrag erzeugt einen neuen Radiobutton unterhalb der einfachen Suche.

