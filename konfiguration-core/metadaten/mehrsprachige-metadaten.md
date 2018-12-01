# 2.19.10 mehrsprachige Metadaten

Der Goobi viewer unterstützt mehrsprachige Metadaten. Diese sind mit dem Suffix \_LANG\_XX im Indexfeld gekennzeichnet wobei XX durch den Sprachkürzel ersetzt werden muss. Hier ein Beispiel für ein dreisprachiges Titelfeld:

```markup
<MD_TITLE_LANG_FR>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:titleInfo/mods:title[@lang="fre"]</xpath>
            <addToDefault>true</addToDefault>
            <addSortField>true</addSortField>
            <replace string="&lt;ns&gt;"></replace>
            <replace string="&lt;/ns&gt;"></replace>
            <replace string="&lt;&lt;"></replace>
            <replace string="&gt;&gt;"></replace>
            <replace string="¬"></replace>
        </item>
    </list>
</MD_TITLE_LANG_FR>
<MD_TITLE_LANG_DE>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:titleInfo/mods:title[@lang="ger"]</xpath>
            <addToDefault>true</addToDefault>
            <addSortField>true</addSortField>
            <replace string="&lt;ns&gt;"></replace>
            <replace string="&lt;/ns&gt;"></replace>
            <replace string="&lt;&lt;"></replace>
            <replace string="&gt;&gt;"></replace>
            <replace string="¬"></replace>
        </item>
    </list>
</MD_TITLE_LANG_DE>
<MD_TITLE_LANG_EN>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:titleInfo/mods:title[@lang="eng"]</xpath>
            <addToDefault>true</addToDefault>
            <addSortField>true</addSortField>
            <replace string="&lt;ns&gt;"></replace>
            <replace string="&lt;/ns&gt;"></replace>
            <replace string="&lt;&lt;"></replace>
            <replace string="&gt;&gt;"></replace>
            <replace string="¬"></replace>
        </item>
    </list>
</MD_TITLE_LANG_EN>
```

Die Felder können alle gleichwertig nebeneinander in den folgenden Abschnitten konfiguriert werden:

* [2.17.1 Sortierung](../suche/sortierung.md) \(`search/sorting/luceneField`\)
* [2.17.2 Facettierung](../suche/facettierung.md) \(`search/drillDown/field`\)
* [2.19.1 Haupt-Metadaten](haupt-metadaten.md) \(`metadata/mainMetadataList/metadata`\)
* [2.19.3 Suchtreffer-Metadaten](suchtreffer-metadaten.md) \(`metadata/searchHitMetadataList/metadata`\)
* [2.19.7 Stöbern](stoebern.md) \(`metadata/browsingMenu/luceneField`\)
* [2.20.1 Konfiguration Inhaltsverzeichnis](../inhaltsverzeichnisse/konfiguration-inhaltsverzeichnis.md) \(`toc/labelConfig/template/metadata/param`\)

Der Goobi viewer erkennt die mehrsprachigen Felder automatisch und zeigt - sofern der in [Abschnitt 2.15 ](../sprachumschaltung-bei-mehrsprachigen-metadaten.md)beschriebene Schalter auf `true` steht - nur die Sprache der aktuellen Benutzeroberfläche an.

