# 2.11.3 Konfiguration der Bildanzeige

Für die Bildanzeige kommt OpenSeadragon basierend auf der IIIF Image API zum Einsatz. Für die Anzeige existiert ein eigener Konfigurationsblock, im Abschnitt `<viewer>`

Viewer, die das Crowdsourcing-Modul nutzen, können die Bildanzeige dort unter `<zoomCrowdsourcingView>` separat konfigurieren, sofern gewünscht.

Der Konfigurationsblock hat folgende Form:

```markup
<viewer>
    <zoomImageView tileImage="true" footerHeight="50">
        <scale>300</scale>
        <scale>900</scale>
        <scale>1800</scale>
        <scale>3200</scale>
        <tileSize>
            <scaleFactors>1,32,64</scaleFactors>
            <size>512</size>
        </tileSize>
    </zoomImageView>
</viewer>
```

Die einzelnen Konfigurationsparameter werden im Folgenden erklärt:

| **Option** | Beschreibung |
| :--- | :--- |
| **tileImage** | Legt fest, ob das Bild als ganzes oder gekachelt angezeigt werden soll. Für die gekachelte |
| **footerHeight** | Die absolute Höhe des Footers in Pixeln. Um den Footer ganz auszuschalten, kann man hier einen Wert von „0“ eingeben. |
| **scale** | Diese Konfiguration wird nur für tileImage=“false“ berücksichtigt. Dann gibt sie die Breite des angezeigten Bildes in Pixeln an. Dies ist nicht die Breite der Bildanzeige, die im html-code gestgelegt wird, sondern die Größe des Bildes, das zur Anzeige geladen wird.Diese Konfiguration ist beliebig wiederholbar, um das Bild in verschiedenen Auflösungen anzuzeigen. Größere Versionen des Bildes beim Zoomen der Bildanzeige werden nachgeladen.  |
| **tileSize** | Diese Konfiguration wird nur für tileImage=“true“ berücksichtigt. Sie besteht aus zwei Teilkonfigurationen: scaleFactors und size.  |

`scaleFactors` ist eine Komma-separierte Liste von Skalierungsfaktoren, um die die Kacheln für die Anzeige verkleinert werden. Werden zum Beispiel die Faktoren 1 und 32 angegeben, werden erst Kacheln angezeigt, die das Bild in der Verkleinerung 1/32 anzeigen. Beim Heranzoomen werden diese Kacheln ersetzt durch solche, die das Bild in voller Auflösung zeigen. Es ist üblich, aber nicht zwingend erforderlich, in Zweierpotenzen zu skalieren. Diese Werte sind jedoch nur Richtlinien für die zugrundeliegende OpenSeadragon Implementierung, die in der Regel mehrere Vergrößerungen zwischen den angegebenen Werten verwendet.

`size` bestimmt die Größe der einzelnen Kacheln in Pixeln. Welchen Ausschnitt des tatsächlichen Bildes sie dabei abbilden, hängt von dem verwendeten `scaleFactor` ab. Bei einem `scaleFactor` von 4 und einer size von 512, wird ein 2048 mal 2048 Pixel großer Ausschnitt des Originalbildes pro Kachel angezeigt.

Diese Konfiguration ist beliebig wiederholbar, wenn man verschiedene Kachelgrößen verwenden möchte.

