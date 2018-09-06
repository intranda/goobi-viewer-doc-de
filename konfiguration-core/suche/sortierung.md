# 2.17.1 Sortierung

Die Sortierung der Suchtrefferliste lässt sich folgendermaßen konfigurieren.

```markup
<search>
     <sorting>
           <enabled>true</enabled>
           <defaultSortField>DATECREATED</defaultSortField>
           <luceneField>SORT_CREATOR</luceneField>
           <luceneField>SORT_TITLE</luceneField>
           <luceneField>SORT_YEARPUBLISH</luceneField>
     </sorting>
</search>
```

Über das Element `<enabled>` lässt sich die Sortierung komplett abschalten \(Standardwert ist `true`\). Über die Elemente `<luceneField>` werden die Solr Felder definiert, nach denen die Sortierung vorgenommen werden kann. Die Reihenfolge der Auflistung entspricht dabei der angezeigten Reihenfolge. Soll ein Sortierfeld sofort bei der Erstsuche verwendet werden, bevor der Benutzer eine explizite Sortierung ausgewählt hat, kann dieses im Element `<defaultSortField>` definiert werden.

{% hint style="warning" %}
Die zur Sortierung verwendeten Felder dürfen keine Felder mit mehrfachen Werten sein \(das heißt in ihrer Deklaration in /opt/digiverso/viewer/apache-solr/collection1/conf/schema.xml darf das Attribut multiValued nicht den Wert true haben\).
{% endhint %}

