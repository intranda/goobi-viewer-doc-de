# 2.33.2 IIIF

Der Goobi viewer implementiert die IIIF Presentation API in der Version 2.1.1. Die API wird in dem folgenden Block konfiguriert:

```markup
<webapi>
    <iiif>
        <metadataFields>
            <field>MD_TITLE</field>
            <field>MD_CREATOR</field>
        </metadataFields>
        <navDateField>YEAR</navDateField>
        <attribution>iiif_attribution</attribution>
        <logo>dfgviewer_intranda.jpg</logo>
    </iiif>
</webapi>
```

| **Option** | Beschreibung |
| :--- | :--- |
| **metadataFields/field** | Eine Liste mit allen Metadatenfeldern, die im IIIF Presentation Manifest ausgegeben werden. Wildcards sind hier erlaubt, zum Beispiel MD\_\* |
| **navDateField** | Solr Feld für die IIIF Presentation navDate Eigenschaft |
| **attribution** | Definiert eine message Key, dessen Inhalt als attribution im IIIF Manifest angegeben ist. |
| **logo** | URL zu einem Bild, dass als Logo im IIIF Manifest angegeben ist. Beginnt die URL mit http\(s\), wird sie direkt durchgereicht. Wird hier ein Dateiname oder relativer Pfad angegeben, so wird der Pfad relativ ab dem Ordner `resources/themes/THEMENAME/images/` gebaut. Ist kein Bild definiert, wird der Bildfooter verwendet. |



Damit die Manifeste von extern eingebunden werden können muss CORS erlaubt sein.

