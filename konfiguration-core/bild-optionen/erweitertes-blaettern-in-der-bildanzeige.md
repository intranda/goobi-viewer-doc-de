# 2.11.1 Erweitertes Blättern in der Bildanzeige

Zusätzlich zu den üblichen Blätterfunktionen in der Bildanzeige, können weitere Schaltflächen per Konfiguration hinzufügt werden, um mehrere Seiten auf einmal zu blättern. Dazu dient der folgende Konfigurationsblock:

```markup
<viewer>
    <pageBrowse>
        <enabled>false</enabled>
        <pageBrowseStep>0</pageBrowseStep>
        <pageBrowseStep>5</pageBrowseStep>
        <pageBrowseStep>10</pageBrowseStep>
    </pageBrowse>
</viewer>
```

Das Element `<enabled>` schaltet die zusätzlichen Schaltflächen in der Bildanzeige an oder aus. Die Elemente `<pageBrowseStep>` legen jeweils eine Schrittgröße fest, wobei Schrittgrößen von 0 ignoriert werden. In der obigen Beispielkonfiguration wird eine Schaltfläche zum Blättern um 5 und eine zum Blättern von 10 Seiten gleichzeitig angezeigt. Mehr als drei Elemente `<pageBrowseStep>` werden nicht ausgewertet.
