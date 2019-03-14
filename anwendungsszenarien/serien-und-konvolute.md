# 6.2 Serien und Konvolute

Der Goobi viewer kann - unabhängig von Gesamtwerks- und Kollektionszugehörigkeit - Gruppen von mehreren voneinander unabhängigen Werken abbilden und diese als eine logische, navigierbare Einheit darstellen. Eine solche logische Einheit kann zum Beispiel ein Sammelband sein.

Die Erkennung dieser Gruppen erfolgt anhand von Indexfeldern, deren Name mit `GROUPID_` beginnen \(zum Beispiel `GROUPID_CONVOLUTE`\) und deren Wert bei mehreren Werken übereinstimmt. So gehören alle Werke, die den Wert `GROUPID_CONVOLUTE:12345` haben, zur Gruppe `12345`, Werke mit einem anderen Werk zu einer anderen Gruppe.

Die Reihenfolge des Werkes innerhalb einer Gruppe wird durch Indexfelder mit dem Präfix `GROUPORDER_` bestimmt. Hinter dem Präfix muss das Indexfeld so heißen, wie das dazugehörige Felder mit der `Gruppen-ID`, im o.g. Beispiel also `GROUPORDER_CONVOLUTE`. Der Wert muss dabei eine Ganzzahl sein. Ein Werk mit `GROUPORDER_CONVOLUTE:34` stünde also in der Auflistung vor einem Werk, das den Wert `GROUPORDER_CONVOLUTE:98` hat.

Die Indexfelder müssen in der Konfigurationsdatei des Goobi viewer Indexers für entsprechende MODS Ausdrücke konfiguriert werden. Besitzen die Felder die genannten Präfixe, werden sie automatisch entsprechend behandelt.

Das Datenmodell des Goobi viewers sieht außerdem vor, dass Werke beliebig vielen Gruppen angehören können.

Beispiel für die Konfiguration in einem Goobi workflow Regelsatz:

{% code-tabs %}
{% code-tabs-item title="/opt/digiverso/goobi/rulesets/ruleset.xml" %}
```markup
<MetadataType>
    <Name>Convolute</Name>
    <language name="de">Konvolut</language>
    <language name="en">Convolute</language>
</MetadataType>
<MetadataType>
    <Name>ConvoluteNr</Name>
    <language name="de">Konvolut-Nr</language>
    <language name="en">Convolute Nr</language>
</MetadataType>

[...]

<metadata num="1o">Convolute</metadata>
<metadata num="1o">ConvoluteNr</metadata>

[...]

<Metadata>
    <InternalName>Convolute</InternalName>
    <WriteXPath>./mods:mods/mods:note[@type='convoluteid']</WriteXPath>
</Metadata>
<Metadata>
    <InternalName>ConvoluteNr</InternalName>
    <WriteXPath>./mods:mods/mods:note[@type='convoluteorder']</WriteXPath>
</Metadata>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Beispiel für das Mapping und Indexieren in der Goobi viewer Indexer Konfigurationsdatei:

{% code-tabs %}
{% code-tabs-item title="/opt/digiverso/indexer/solr\_indexerconfig.xml" %}
```markup
<GROUPID_CONVOLUTE>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:note[@type='convoluteid']</xpath>
            <addToDefault>true</addToDefault>
            <addUntokenizedVersion>false</addUntokenizedVersion>
        </item>
    </list>
</GROUPID_CONVOLUTE>
<GROUPORDER_CONVOLUTE>
    <list>
        <item>
            <xpath>mets:xmlData/mods:mods/mods:note[@type='convoluteorder']</xpath>
            <addUntokenizedVersion>false</addUntokenizedVersion>
        </item>
    </list>
</GROUPORDER_CONVOLUTE>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Beispiel für die Freischaltung in dem Goobi viewer Core:

{% code-tabs %}
{% code-tabs-item title="/opt/digiverso/viewer/config/config\_viewer.xml" %}
```markup
<toc>
	<recordGroupIdentifierFields>
		<field>GROUPID_CONVOLUTE</field>
	</recordGroupIdentifierFields>
</toc>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Anhand der als Gruppen-Identifier definierter Felder werden im Inhaltsverzeichnis die durch die Gruppenzugehörigkeit entstandenen Hierarchien abgebildet. Der Teil des Feldnamens hinter `GROUPID_` bildet dabei eine konkrete Gruppe ab \(hier: `CONVOLUTE`\). Über das Feld `GROUPORDER_CONVOLUTE` wird dabei die Reihenfolge des Werks innerhalb der Gruppe definiert und entsprechend im Inhaltsverzeichnis verwendet.

