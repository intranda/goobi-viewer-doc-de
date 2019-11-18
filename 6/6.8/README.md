# 6.8 Konfiguration der Zugriffsbeschränkung

Der Goobi viewer unterstützt die Möglichkeit, bestimmte Aspekte eines Werks unzugänglich beziehungsweise nur bestimmten Kreisen zugänglich zu machen.

Voraussetzung ist das Mitführen von sogenannten Access Conditions im Quelldokument des Werks als Metadatum. Die entsprechenden Werte müssen im Solr Index im das Feld ACCESSCONDITION gemappt werden:

{% code title="solr\_indexerconfig.xml" %}
```markup
<ACCESSCONDITION>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:accessCondition[@type='restriction on access']</xpath>
            <addToDefault>false</addToDefault>
            <addUntokenizedVersion>false</addUntokenizedVersion>
        </item>
    </list>
</ACCESSCONDITION>
```
{% endcode %}



