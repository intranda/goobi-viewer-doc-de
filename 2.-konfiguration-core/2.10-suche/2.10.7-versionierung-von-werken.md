# 2.17.9 Versionierung von Werken

Wenn von bestimmten Werken aktualisierte Versionen vorhanden sind, gibt es eine Möglichkeit, dem Benutzer den Versionsverlauf in der Seitenleiste anzuzeigen. Dafür müssen die Werke jeweils den Identifier der Vorgänger- beziehungsweise Nachfolgerversion als Metadazum enthalten. Diese Feldnamen müssen in den Feldern `previousVersionIdentifierField` beziehungsweise `nextVersionIdentifierField` konfiguiert sein. Soll die Version einen expliziten Namen bekommen, muss der Feldname in `versionLabelField` definiert werden.

Enthält ein Werk zum Beispiel einen Vorgänger-Identifier, wird in der Sidebar ein Link für diese ältere Version generiert \(und wenn diese Version wiederum einen Verweis auf einen Vorgänger enthält, wird für diesen ebenfalls ein Link generiert, usw\). Das Konfigurationselement `staticQuerySuffix` enthält eine Solr Subquery die stets an alle Suchanfragen angehangen wird und zusätzliche Filterung ermöglicht. Im unten genannten Beispiel werden alle Werke herausgefiltert, die auf die Query `BOOL_HIDE:true` matchen. Auf diese Weise können Versionen, die nicht auffindbar sein sollen, aus Suchanfragen herausgefiltert werden. Soll etwa nur die aktuelle Version über die Suche, die Sammlungsansicht, etc. auffindbar sein, kann allen anderen Versionen ein bestimmter Metadatenwert vergeben werden, der das Werk als entsprechend diskriminiert. Der Versionsverlauf in der Sidebar wird dadurch nicht beeinträchtigt.

```markup
<search>
    <staticQuerySuffix>AND –BOOL_HIDE:true</staticQuerySuffix>
    <versioning>
        <previousVersionIdentifierField>MD_PREVIOUS_VERSION</previousVersionIdentifierField>
        <nextVersionIdentifierField>MD_NEXT_VERSION</nextVersionIdentifierField>
        <versionLabelField>MD_VERSIONLABEL</versionLabelField>
    </versioning>
</search>
```



