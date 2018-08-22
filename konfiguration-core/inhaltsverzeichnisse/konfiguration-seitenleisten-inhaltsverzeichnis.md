# 2.20.2 Konfiguration Seitenleisten-Inhaltsverzeichnis

Das Inhaltsverzeichnis der Seitenleiste wird ähnlich konfiguriert:

```markup
<sidebar>
    <sidebarToc>
        <visible>true</visible>
        <pageNumbersVisible>true</pageNumbersVisible>
        <lengthBeforeCut>60</lengthBeforeCut>
        <useTreeView>false</useTreeView>
        <initialCollapseLevel>2</initialCollapseLevel>
        <collapseLengthThreshold lowestLevelToTest="2">0</collapseLengthThreshold>
    </sidebarToc>
</sidebar>
```

| **Option** | Beschreibung |
| :--- | :--- |
| **visible** | Anzeige dieses Elementes \(true/false\) |
| **pageNumbersVisible** | Anzeige von Seitenzahlen in dieser Ansicht \(true/false\) |
| **lengthBeforeCut** | Maximale Anzahl der Zeichen für jedes Element \(längere Titel können durch Klick auf mehr... angezeigt werden\). |
| **useTreeView** | Darstellung als ausklappbarer Baum |
| **initialCollapseLevel** | Die Hierarchieebene, bis zu der die Ansicht initial zugeklappt wird \(sofern die Konfiguration so angegeben wurde: `<useTreeView>true</useTreeView>`\) |
| **collapseLengthThreshold** | Ist dieser Wert größer als 0, werden alle Elemente, die mehr Kinder haben, als dieser Wert angibt, initial immer zugeklappt. `lowestLevelToTest` gibt die unterste Hierarchieebene an, auf der diese Methode angewandt werden soll. |
