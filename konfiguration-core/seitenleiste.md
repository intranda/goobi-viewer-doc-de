# 2.23 Seitenleiste

Folgende Elemente schalten Links in der Seitenleiste zu den verschiedenen Arten der Werksansicht an beziehungsweise ab \(Standardwert ist jeweils `true`\):

```markup
<sidebar>
     <overview>
           <visible>true</visible>
           <condition>DC:abc</condition>
     </overview>
     <page>
           <visible>true</visible>
     </page>
     <toc>
           <visible>true</visible>
     </toc>
     <thumbs>
           <visible>true</visible>
     </thumbs>
     <searchInItem>
          <visible>true</visible>
     </searchInItem>
     <metadata>
           <visible>true</visible>
           <showEventMetadata>true</showEventMetadata>
     </metadata>
     <fulltext>
           <visible>true</visible>
     </fulltext>
     <dfg>
           <visible>true</visible>
     </dfg>

     <opac>
           <visible>true</visible>
     </opac>
</sidebar>
```

| **Option** | Beschreibung |
| :--- | :--- |
| overview/visible | Schaltet die Anzeige von Werks-Übersichtsseiten global ein oder aus |
| **overview/condition** | Optionale Solr Subquery. Werke, die von dieser Query erfasst werden, bekommen grundsätzlich eine Übersichtsseite angezeigt \(falls overview/visible auf true steht\). Hat das Werk keine eigene Übersichtsseiten-Konfiguration im Index, wird eine Standardkonfiguration verwendet \(es muss sich hierfür eine Default-Konfigurationsdatei mit dem Namen overviewpage.default.xml im lokalen Konfigurationsordner, dessen Pfad unter configFolder eingetragen ist, befinden\). |
| **page/visible** | Bild-/Video-/Audio |
| **toc/visible** | Sichtbarkeit des Links zum Inhaltsverzeichnis in der Werks-Navigation. Achtung: dies ist nicht das Seitenleisten-Inhaltsverzeichnis, hierfür siehe `sidebarToc`. |
| **thumbs/visible** | Seitenvorschau \(Thumbnails\) |
| **searchInItem/visible** | Suche im Werk |
| **metadata/visible** | Metadaten / Bibliographische Daten |
| **metadata/showEventMetadata** | Metadaten aus allen LIDO Events |
| **fulltext/visible** | Volltext |
| **dfg/visible** | Link zum DFG-Viewer |
| **opac/visible** | Link zum OPAC |

![Konfiguration im Widget Ansicht in der Seitenleiste ](../.gitbook/assets/seitenleiste%20%281%29.png)

Innerhalb dieser Sektion wird in der Konfigurationsdatei auch das Seitenleisten-Inhaltsverzeichnis konfiguriert. Aufgrund der thematischen Nähe, ist es in [Kapitel  2.20.2](inhaltsverzeichnisse/konfiguration-seitenleisten-inhaltsverzeichnis.md) beschrieben.
