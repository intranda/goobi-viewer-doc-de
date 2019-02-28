# 6.5 Normdaten

Im Regelsatz muss bei dem gewünschten Metadatum das Attribut `normdata="true"` aktiviert sein damit die Normdaten im Metadateneditor erfasst werden können:

```markup
<MetadataType type="person" normdata="true">
    <Name>Author</Name>
    <language name="de">Autor</language>
    <language name="en">Author</language>
</MetadataType>
```

Anschließend im Regelsatz für das Metadatum den XPATH-Ausdruck suchen, wohin dieses nach MODS exportiert wird:

```markup
<Metadata>
    <InternalName>Author</InternalName>
    <WriteXPath>./mods:mods/#mods:name[@type='personal'][mods:role/mods:roleTerm="aut"[@authority='marcrelator'][@type='code']]</WriteXPath>
    [...]
```

Jetzt in der Konfigurationsdatei des Goobi viewer Indexers die Felddefinition, in die der XPATH-Ausdruck gemappt wird suchen:

```markup
<MD_AUTHOR>
  <list>
    <item>
      <xpath>
        <list>
          <item>mets:xmlData/mods:mods/mods:name[@type="personal"][mods:role/mods:roleTerm="aut"[@authority='marcrelator'][@type='code']]/mods:displayForm</item>
        </list>
      </xpath>
      <onefield>false</onefield>
      [...]
```

Hier nun sicherstellen, dass dort für Personen die folgende Sektion enthalten ist:

```markup
<groupEntity type="PERSON">
        <field name="MD_VALUE">mods:displayForm</field>
        <field name="MD_DISPLAYFORM">mods:displayForm</field>
        <field name="MD_LINK">@xlink:href</field>
        <field name="MD_CORPORATION">mods:namePart[not(@type)]</field>
        <field name="MD_LASTNAME">mods:namePart[@type="family"]</field>
        <field name="MD_FIRSTNAME">mods:namePart[@type="given"]</field>
        <field name="MD_LIFEPERIOD">mods:namePart[@type="date"]</field>
        <field name="MD_TERMSOFADDRESS">mods:namePart[@type="termsOfAddress"]</field>
        <field name="NORM_URI">@valueURI</field>
</groupEntity>
```

Ein kompletter Eintrag sieht beispielsweise so aus:

```markup
<MD_AUTHOR>
  <list>
    <item>
      <xpath>
        <list>
          <item>mets:xmlData/mods:mods/mods:name[@type="personal"][mods:role/mods:roleTerm="aut"[@authority='marcrelator'][@type='code']]/mods:displayForm</item>
        </list>
      </xpath>
      <onefield>false</onefield>
      <addToDefault>true</addToDefault>
      <groupEntity type="PERSON">
        <field name="MD_VALUE">mods:displayForm</field>
        <field name="MD_DISPLAYFORM">mods:displayForm</field>
        <field name="MD_LINK">@xlink:href</field>
        <field name="MD_CORPORATION">mods:namePart[not(@type)]</field>
        <field name="MD_LASTNAME">mods:namePart[@type="family"]</field>
        <field name="MD_FIRSTNAME">mods:namePart[@type="given"]</field>
        <field name="MD_LIFEPERIOD">mods:namePart[@type="date"]</field>
        <field name="MD_TERMSOFADDRESS">mods:namePart[@type="termsOfAddress"]</field>
        <field name="NORM_URI">@valueURI</field>
      </groupEntity>
      <addUntokenizedVersion>true</addUntokenizedVersion>
    </item>
  </list>
</MD_AUTHOR>
```

Starten Sie nach den Änderungen den Goobi viewer Indexer Prozess neu. Für die Kommandos siehe [Kapitel 3.6. Starten und Beenden](../konfiguration-indexer/starten-und-beenden.md)

Beim Indexieren eines Werkes mit Normdaten sollten nun in der Lodatei Informationen wie nachfolgend angezeigt werden:

```text
[...]
  INFO  2015-04-29 11:25:38,853 (MetadataHelper.java:retrieveNormData:322)
        Retrieving norm data from 'http://d-nb.info/gnd/117395269'...
[...]
```

Für die Anzeige muss nun in der zentrale Konfigurationsdatei des Goobi viewers Core die Definition des Metadatums zur Anzeige die Normdaten auch konfigurieret werden:

```markup
<metadata label="MD_AUTHOR" value="MASTERVALUE_WIKINORM" group="true">
    <param type="field" key="MD_VALUE" />
    <param type="wikipersonfield" key="MD_DISPLAYFORM" />
    <param type="normdatauri" key="NORM_URI" />
</metadata>
```

Sollten zusätzliche Informationen in der Anzeige gewünscht sein, so sind die Parameter entsprechend anzupassen. Dabei darauf achten, dass in den Attributen `value=""` ein neuer KEY definiert wird, der dann in den `messages_*`-Dateien vorhanden ist. Für das obige Beispiel entspricht die Konfiguration innerhalb der Sprachdatei `messages_de.properties`  beispielsweise:

```text
MASTERVALUE_WIKINORM={1} <a href="http://de.wikipedia.org/wiki/{3}" target="_blank"><img src="/viewer/javax.faces.resource/wikipedia.png.xhtml?ln=images/" style="height:16px;" title="Wikipedia" alt="Wikipedia" /></a> {5}
```



