# 5. Konfiguration der Zugriffsbeschränkung

Der Goobi viewer verfügt über die Möglichkeit, bestimmte Aspekte eines Werks unzugänglich bzw. nur bestimmten Kreisen zugänglich zu machen.

Voraussetzung ist das Mitführen von sog. Access Conditions im Quelldokument des Werks \(METS oder LIDO\) als Metadatum. Die entsprechenden Werte müssen anschließend im Solr Index im Feld ACCESSCONDITION stehen:

```markup
<ACCESSCONDITION>
  <list>
      <item>
            <xpath>mets:xmlData/mods:mods/mods:accessCondition[not(@type)]</xpath>
                  <addToDefault>false</addToDefault>
                  <addUntokenizedVersion>false</addUntokenizedVersion>
      </item>
  </list>
</ACCESSCONDITION>
```



