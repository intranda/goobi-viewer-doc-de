# 4.1.3 Dublin Core

```markup
<oai_dc>
     <enabled>true</enabled>
     <hitsPerToken>100</hitsPerToken>
     <fields>
          <field name="title" valueSource="MD_TITLE" defaultValue="" />
          <field name="creator" valueSource="MD_CREATOR" multivalued="true" />
          <field name="subject" prefix="collection" valueSource="DC" multivalued="true" />
          <field name="publisher" valueSource="MD_PUBLISHER" useTopstructValueIfNoneFound="true" />
          <field name="date" valueSource="MD_YEARPUBLISH" suffix="A.D. " useTopstructValueIfNoneFound="true" />
          <field name="type" valueSource="DOCSTRCT" translated="true" />
          <field name="type" defaultValue="Text" />
          <field name="format" defaultValue="image/jpeg" />
          <field name="format" defaultValue="application/pdf" />
          <field name="identifier" valueSource="#AUTO#" />
          <field name="source" valueSource="#AUTO#" />
          <field name="rights" valueSource="#AUTO#"/>
     </fields>
     <setSpec>
          <field>DC</field>
          <field>DOCSTRCT</field>
     </setSpec>
</oai_dc>
```

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Option</b>
      </th>
      <th style="text-align:left">Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>enabled</b>
      </td>
      <td style="text-align:left">Aktiviert die Verf&#xFC;gbarkeit des Formats in der OAI-PMH Schnittstelle.
        Standardwert ist <code>false</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>hitsPerToken</b>
      </td>
      <td style="text-align:left">Anzahl der Records, die Solr maximal bei einer Anfrage (Seite/Token) zur&#xFC;ckgibt.
        Dieser Wert &#xFC;berschreibt den globalen Standardwert <code>hitsPerToken</code> (siehe
        <a
        href="hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken">4.1.1.10</a>) f&#xFC;r dieses Metadatenformat. Ist kein Wert hier definiert,
          wird der globale Wert verwendet.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>fields</b>
      </td>
      <td style="text-align:left">
        <p>Konfiguration der ausgelieferten Metadatenfelder f&#xFC;r dieses Format.
          Jedes field-Element entpricht einem Eintrag im Record. Folgende Attribute
          sind m&#xF6;glich:</p>
        <ul>
          <li><b>name</b> &#x2013; Name des Dublin Core Feldes (aus &#x201E;title&#x201C;
            wird etwa <code>&lt;dc:title&gt;</code>). Dies ist ein Pflicht-Attribut,
            und sollte einen validen Namen nach Dublin Core Spezifikation enthalten.</li>
          <li><b>valueSource</b> &#x2013; Solr-Feld, aus dem der Wert f&#xFC;r dieses
            Feld gelesen wird. F&#xFC;r die Felder <code>identifier</code>, <code>source</code> und <code>rights</code> kann
            auch der Wert <code>AUTO</code> eingetragen werden, wobei dann im Programm
            fest definierte Algorithmen zur Wertermittlung eingesetzt werden.</li>
          <li><b>translated</b> &#x2013; Wenn true, wird der Wert &#xFC;ber messages.properties
            &#xFC;bersetzt (in die Sprache, die unter <code>&lt;defaultLocale&gt;</code> konfiguriert
            ist. Standardwert ist <code>false</code>
          </li>
          <li><b>multivalued</b> &#x2013; Wenn dieses Attribut vorhanden ist und den
            Wert <code>true</code> besitzt, wird f&#xFC;r jeden gefundenen Wert des in <code>valueSource</code> definierten
            Solr-Feldes ein Dublin Core Element erzeugt.</li>
          <li><b>useTopstructValueIfNoneFound</b> &#x2013; Wenn im aktuellen Strukturelement
            kein Wert f&#xFC;r das im Attribut valueSource definiertes Feld gefunden
            wird, kann optional der Wert des obersten Strukturelements verwendet werden,
            wenn dieses Attribut vorhanden ist und den Wert <code>true</code> besitzt.
            Dies ist n&#xFC;tzlich, wenn zus&#xE4;tzliche, untergeordnete Strukturelemente
            als Records ausgeliefert werden.</li>
          <li><b>defaultValue</b> &#x2013; Definierbarer statischer Wert. Der Wert wird
            nur eingetragen, wenn kein Wert aus der Konfiguration in <code>valueSource</code> ermittelt
            werden konnte.</li>
          <li><b>prefix / suffix</b> &#x2013; Optionales vor beziehungsweise hinter den
            Wert gestelltes Pr&#xE4;- beziehungsweise Suffix. Der Wert dieser Attribute
            wird automatisch &#xFC;bersetzt, falls es einen gleichnamingen Message
            Key gibt.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>setSpec</b>
      </td>
      <td style="text-align:left">Konfiguration von Indexfeldern, deren Werte f&#xFC;r <code>setSpec</code>-Elemente
        von OAI-Records verwendet werden. Pro Feldkonfiguration wird ein <code>field</code>-Element
        verwendet, und pro gefundenen Wert wird ein <code>setSpec</code>-Element
        generiert.</td>
    </tr>
  </tbody>
</table>