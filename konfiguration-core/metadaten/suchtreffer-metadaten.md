# 2.19.3 Suchtreffer-Metadaten

Grundsätzlich werden die Metadaten für die Suchtreffer auf die gleiche Weise konfiguriert, wie die Haupt-Metadaten.

```markup
<metadata>
    <searchHitMetadataList>
        <template name="_DEFAULT">
            <metadata label="MD_CREATOR" value="">
                <param type="field" key="MD_CREATOR" />
            </metadata>
            <metadata label="MD_SHELFMARK" value="">
                <param type="field" key="MD_SHELFMARK" />
            </metadata>
            <metadata label="MD_PUBLISHER" value="">
                <param type="field" key="MD_PUBLISHER" />
            </metadata>
            <metadata label="MD_YEARPUBLISH" value="">
                <param type="field" key="MD_YEARPUBLISH" />
            </metadata>
            <metadata label="MD_PLACEPUBLISH" value="">
                <param type="field" key="MD_PLACEPUBLISH" />
            </metadata>
        </template>
        <template name="Chapter">
            <metadata label="" value="SEARCHHIT_DEFAULT1">
                <param type="field" key="MD_CREATORS" suffix=":_SPACE_" dontUseTopstructValue="true" />
                <param type="field" key="LABEL" url="true" />
            </metadata>
            <metadata label="in" value="SEARCHHIT_CHAPTER">
                <param type="anchorfield" key="MD_CREATORS" suffix=":_SPACE_" />
                <param type="anchorfield" key="LABEL" suffix="&lt;br/&gt;" url="true" />
                <param type="topstructfield" key="CURRENTNO" suffix=":_SPACE_" url="true" />
                <param type="topstructfield" key="MD_CREATORS" suffix=":_SPACE_" />
                <param type="topstructfield" key="LABEL" url="true" />
                <param type="topstructfield" key="MD_PLACEPUBLISH" prefix="\,_SPACE_" />
                <param type="topstructfield" key="MD_YEARPUBLISH" prefix="_SPACE_" />
            </metadata>
        </template>
        <displayStructType>true</displayStructType>
        <valueNumber>1</valueNumber>
        <valueLength>40</valueLength>
    </searchHitMetadataList>
</metadata>
```

Das erste Element zeigt die Autoren und den Titel des Kapitels an, das zweite Element die Autoren und den Titel des Gesamtwerks, sowie die Autoren, den Titel, Ort und Jahr der Herausgabe an. Über die Message-Einträge `SEARCHHIT_DEFAULT1`und `SEARCHHIT_CHAPTER`, sowie den nur für Suchtreffer-Metadaten zulässigen Parameter `url`, wird das Layout der Metadaten gesteuert.

Das Ergebnis ist im folgenden Screenshot zu sehen:

![](../../.gitbook/assets/suchtreffer-meta.png)

Bei Suchtreffer-Metadaten sind noch folgende Werte für das Attribut `type` zulässig:

| **Wert** | Beschreibung |
| :--- | :--- |
| **topstructfield** | Wert wird nicht aus dem aktuellen, sondern aus dem obersten Strukturelement des aktuellen Bandes gelesen |
| **anchorfield** | Wert wird nicht aus dem aktuellen Strukturelement, sondern aus dem übergeordneten Gesamtwerk gelesen |

Außerdem sind bei Suchtreffer-Metadaten folgende zusätzliche Attribute verwendbar:

| **Attribut** | Beschreibung |
| :--- | :--- |
| **url** | Wert des Metadatums soll zum zugehörigen Strukturelement verlinken |
| **dontUseTopstructValue** | Beinhaltet das Strukturelement, das zum Suchtreffer gehört, das gewünschte Metadatum nicht, wird normalerweise stattdessen der Wert des Hauptstrukturelements angezeit. Soll dies nicht geschehen, kann dieses Atrribute auf `true` gesetzt werden. |

Für Strukturtypen, die kein eigenes Template haben, wird die Konfiguration auf dem Template DEFAULT verwendet. Falls kein `_DEFAULT` Template definiert ist, werden für diesen Strukturtyp keine Metadaten in der Seitenleiste angezeigt.

Zusätzlich gibt es für die Suchtreffer noch folgende Konfigurationselemente:

| **Option** | Beschreibung |
| :--- | :--- |
| **displayStructType** | Wenn auf false gesetzt, wird der Strukturtyp des Treffers nicht angezeigt. Standardwert ist true. |
| **valueNumber** | Die Anzahl der maximal angezeigten Werte für jeden Feldtyp \(das heißt wenn mehr als ein Wert für das Feld `MD_CREATOR` existiert, und valueNumber den Wert 1 hat, wird nur der erste Wert angezeigt\). Standardwert ist `3`. |
| **valueLength** | Der Platz, der in einer Suchtreffer-Box zur Verfügung steht, ist begrenzt. Dadurch ist es manchmal nötig die Länge der Metadaten-Werte auf eine bestimmte Länge zu trunkieren. Diese Länge wird als die maximale Anzahl der anzuzeigenden Zeichen definiert. Standardwert ist `40` \(in diesem Fall findet keine Trunkierung statt\). |

![](../../.gitbook/assets/suchtreffer-meta-2.png)
