# 3.7 Metadaten

Jedes Metadaten Feld, das im Goobi viewer verwendet werden soll, muss im Goobi viewer Indexer im Konfigurationselement `fields` konfiguriert sein. Hierfür wird das folgende Schema verwendet:

```markup
<fields>
    <PI>
        <list>
            <item>
                <xpath>
                    <list>
                        <item prefix="bibprefix_" suffix="_bibsuffix">mets:xmlData/mods:mods/mods:identifier [@type="ppn" or @type="PPN"]</item>
                        <item>lido:administrativeMetadata/lido:recordWrap/lido:recordID</item>
                    </list>
                </xpath>
                <getnode>first</getnode>
                <addToDefault>true</addToDefault>
                <addUntokenizedVersion>false</addUntokenizedVersion>
            </item>
        </list>
    </PI>
</fields>
```

Dabei trägt das oberste Element jeweils den Namen des Solr Feldes, in das das konfigurierte Metadatum geschrieben werden soll \(hier: `PI`\).

{% hint style="info" %}
Feldkonfigurationen, deren Name nicht mit MD\_ im anfängt, sind größtenteils Pflichtfelder für den Goobi viewer und dürfen nicht entfernt werden!  
Für die Konfiguration von Solr Metadatenfeldern werden Grundkenntnisse in XPath vorausgesetzt. Nähere Details hierzu finden sich beispielsweise unter der folgenden Adresse: [http://de.wikipedia.org/wiki/XPATH](http://de.wikipedia.org/wiki/XPATH)
{% endhint %}

#### 3.7.1 Parameter: item

Diese Elemente enthalten XPath Ausdrücke, unter denen das jeweilige Metadatum zu finden ist. Es werden alle angegeben Ausdrücke überprüft, so dass ein Metadatenfeld \(falls für mehrere Werte zugelassen\) mehrere Werte aus unterschiedlichen XPath Ausdrücken enthalten kann. Im obigen Beispiel ist jeweils ein Ausdruck für METS/MODS sowie für LIDO definiert, das heißt diese Feldkonfiguration ist für beide Formate gültig.

Die Attribute prefix und suffix können optional je ein statisches Prä- beziehungsweise Suffix, das an jeden über den jeweiligen XPath-Ausdruck gefundenen Wert angehängt wird.

Für METS Dokumente kann der Ausdruck entweder relativ zum Element

```markup
<mets:mets>
    <mets:mdWrap MDTYPE=”MODS”>
    [...]
    </mets:mdWrap>
</mets:mets>
```

formuliert werden, zum Beispiel:

```markup
<item>mets:xmlData/mods:mods/mods:identifier[@type="ppn" or @type="PPN"]</item>
```

oder relativ zum obersten Element

```markup
<mets:mets>
    [...]
</mets:mets>
```

```markup
<xpath>mets:amdSec[@ID="AMD"]/mets:rightsMD[@ID="RIGHTS"]/mets:mdWrap[@MDTYPE='OTHER' and @MIMETYPE='text/xml' and @OTHERMDTYPE='DVRIGHTS']/mets:xmlData/dv:rights/dv:ownerContact</xpath>
```

Dabei muss die Variante nicht explizit angegeben werden - der Goobi viewer Indexer überprüft alle konfigurierten Ausdrücke relativ zu beiden Knoten.

Bei LIDO werden die XPath Ausdrücke bei allgemeinen Metadaten relativ zum obersten Element

```markup
<lido:lido>
    [...]
</lido:lido>
```

formuliert, zum Beispiel

```markup
<item>lido:administrativeMetadata/lido:recordWrap/lido:recordID</item>
```

Metadaten von LIDO Events verwenden XPath Ausdrücke relativ zum jeweiligen Event-Element:

```markup
<lido:lido>
     <lido:eventWrap>
          <lido:eventSet>
               <lido:event>
                      ...
               </lido:event>
          </lido:eventSet>
     </lido:eventWrap>
</lido:lido>
```

zum Beispiel:

```markup
<item>lido:eventDate/lido:date/lido:earliestDate</item>
```
