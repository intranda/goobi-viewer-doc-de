# 2.24 Navigation und Anzeige

Folgende Elemente schalten unterschiedliche Elemente beziehungsweise Funktionen des Goobi viewers an oder ab \(Standardwert ist jeweils `true`\):

```markup
<webGuiDisplay>
    <collectionBrowsing>true</collectionBrowsing>
    <userAccountNavigation>true</userAccountNavigation>
    <displayTagCloudNavigation>true</displayTagCloudNavigation>
    <displayTagCloudStartpage>true</displayTagCloudStartpage>
    <displaySearchResultNavigation>true</displaySearchResultNavigation>
    <displayBreadcrumbs>true</displayBreadcrumbs>
    <breadcrumsClipping>50</breadcrumsClipping>
    <displayTitleBreadcrumbs maxTitleLength="40" includeAnchor="false">false</displayTitleBreadcrumbs>
    <displayTitlePURL>true</displayTitlePURL>
    <displayMetadataPageLinkBlock>true</displayMetadataPageLinkBlock>
    <displayStatistics>true</displayStatistics>
    <displayTimeMatrix>false</displayTimeMatrix>
</webGuiDisplay>
```

| **Option** | Beschreibung |
| :--- | :--- |
| **collectionBrowsing** | Seite mit der Auflistung der Sammlungen |
| **userAccountNavigation** | Login Seite für Nutzer |
| **displayTagCloudNavigation** | Link zur Tag Cloud Seite \(nur mobile Ansicht\) |
| **displayTagCloudStartpage** | Tag Cloud auf der Startseite |
| **displaySearchResultNavigation** | Blätterfunktion zum nächsten/vorherigen Suchtreffer |
| **displayBreadcrumbs** | Breadcrumb Nagivation |
| **displayMetadataPageLinkBlock** | Links auf der Metadaten Seite \(METS/LIDO, MARCXML, DC, OPAC, PDF, ...\) |
| **breadcrumbsClipping** | Maximale Anzahl von Zeichen, die ein Breadcrumb-Eintrag eines Werktitels haben kann |
| **displayStatistics** | Link zur Statistikseite \(nur mobile Ansicht\). Standardwert ist `true`. |
| **displayTimeMatrix** | Link zur Zeitmatrix \(zweidimensionale Zeitleiste; nur mobile Ansicht\). Standardwert ist `false`. |
| **displayTitlePURL** | Steht dieses Element auf `false`, wird in der Komponente title.xhtml die PURL zur aktuellen Seite nicht angezeigt, unabhängig von der Einstellung, die die aufrufende Seite übergibt. Standardwert ist `true`. |

