# 6.4.2 Einstellungen im Goobi viewer

Das Metadatum `viewerSubTheme` wird innerhalb des Solr Index in ein eigenständiges Feld geschrieben. Dafür muss in der Konfigurationsdatei solr\_indexerconfig.xml folgende Felddefinition hinzugefügt werden:

```markup
<MD_VIEWERSUBTHEME>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:extension/intranda:intranda/intranda:viewersubtheme</xpath>
            <addToDefault>false</addToDefault>
            <addUntokenizedVersion>false</addUntokenizedVersion>
        </item>
    </list>
</MD_VIEWERSUBTHEME>
```



Im Goobi viewer Core muss folgende Anpassung für die korrekte Auswertung vorgenommen werden:

```markup
<viewer>
    <theme subTheme="true" 
           mainTheme="my-theme" 
           discriminatorField="my-subtheme"
           autoswutch="true"
           addFilterQuery="false"
           filterQueryVisible="false"></theme>
</viewer>
```

In der Datei `template.html` wird nun nach dem custom css folgender Block hinzugefügt:

```markup
<!-- SUBTHEME CSS -->
<h:panelGroup rendered="#{navigationHelper.subThemeDiscriminatorValue != null and navigationHelper.subThemeDiscriminatorValue != '-'}">
    <link type="text/css" rel="stylesheet" href="#{request.contextPath}/resources/themes/#{navigationHelper.theme}/css/dist/#{navigationHelper.subThemeDiscriminatorValue}.min.css" />
</h:panelGroup>

```

Für jedes Subtheme gibt es eine eigene CSS-Datei, dass eigene CSS-Definitionen für dieses Theme enthält. Über die Reihenfolge des Einbindens in der Datei `template.html` kann in dieser subthemespezifischen Datei jeder Wert der globalen Datei `viewer.css` oder themespezifischen Datei `custom.min.css` mit subthemeeigenen Werten überschrieben werden.

