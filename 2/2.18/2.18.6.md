# 2.18.6 Weitere Einstellungen

Im Folgenden ist eine Liste von weiteren Sammlungseinstellungen aufgeführt. 

```markup
<collections>
    <collection field=”DC”>
        <displayDepthForSearch>-1</displayDepthForSearch>
        <defaultBrowseIcon>images/collections/collection_tiled_default.jpg</defaultBrowseIcon>
    </collection>
    <redirectToWork>true</redirectToWork>
</collections>
```

| **Option**   | Beschreibung |
| :--- | :--- |
| **collection/displayDepthForSearch** | Maximale Tiefe der hierarchischen Auflistung der Werte des konfigurierten Felds in der erweiterten Suche. Standardwert -1 bedeutet, dass alle Stufen aufgelistet werden.Maximale Tiefe der hierarchischen Auflistung der Werte des konfigurierten Felds in der erweiterten Suche. Standardwert -1 bedeutet, dass alle Stufen aufgelistet werden. |
| **collection/defaultBrowseIcon** | Standard Bild für gekachelte Sammlungen im CMS. Der Pfad ist relative zum Pfad des Themes. |
| **redirectToWork** | Gibt an ob bei einer Sammlung mit nur einem enthaltenen Werk das Werk direkt geöffnet oder eine Suchtrefferliste mit nur einem Werk angezeigt werden soll. Wenn `true` wird das Werk direkt geöffnet. Standard ist `true`. |

