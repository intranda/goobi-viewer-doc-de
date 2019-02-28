# 2.33.2 IIIF

Der Goobi viewer implementiert die IIIF Presentation API in der Version 2.1.1. Die API wird in dem folgenden Block konfiguriert:

```markup
<webapi>
    <iiif>
        <metadataFields>
            <field>MD_TITLE</field>
            <field>MD_CREATOR</field>
            <field label="OTHERLABEL_PURL">MD_PURL</field>
            <event>Production/MD_EVENTACTOR</event>
            <event>Use/MD_EVENTACTOR</event>
        </metadataFields>
        <descriptionFields>
            <field>MD_CONTENTDESCRIPTION</field>
        </descriptionFields>
        <navDateField>YEAR</navDateField>
        <attribution>iiif_attribution</attribution>
        <logo>dfgviewer_intranda.jpg</logo>
    </iiif>
</webapi>
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
      <td style="text-align:left"><b>metadataFields/field</b>
      </td>
      <td style="text-align:left">Eine Liste mit allen Metadatenfeldern, die im IIIF Presentation Manifest
        ausgegeben werden. Wildcards sind hier erlaubt, zum Beispiel MD_*</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>metadataFields/field[@label]</b>
      </td>
      <td style="text-align:left">Jedes Field-Element kann &#xFC;ber ein optionales <code>label=&quot;&quot;</code> Attribut
        verf&#xFC;gen. Hier kann ein &#xFC;berschreibender message Key definiert
        werden, der dann nur im IIIF Presentation Manifest verwendet wird.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>metadataFields/event</b>
      </td>
      <td style="text-align:left">
        <p>Um Metadaten aus LIDO Events im IIIF Presentation Manifest mit auszugeben
          kann eine Liste an Events definiert werden. In einem Event-Element ist
          der Wert immer EVENTNAME/FELDNAME. Im obigen Beispiel also aus den Events <em>Production</em> und <em>Use</em> das
          Feld MD_EVENTACTOR.</p>
        <p>Auch Events k&#xF6;nnen das optionale <code>label=&quot;&quot;</code> Attribut
          enthalten.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>descriptionFields/field</b>
      </td>
      <td style="text-align:left">Eine Liste mit allen Metadatenfeldern, die eine IIIF Presentation Manifest
        Beschreibung enthalten k&#xF6;nnen. Die Beschreibung wird aus dem ersten
        Feld mit Inhalt bef&#xFC;llt.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>navDateField</b>
      </td>
      <td style="text-align:left">Solr Feld f&#xFC;r die IIIF Presentation navDate Eigenschaft</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>attribution</b>
      </td>
      <td style="text-align:left">Definiert eine message Key, dessen Inhalt als attribution im IIIF Manifest
        angegeben ist.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>logo</b>
      </td>
      <td style="text-align:left">URL zu einem Bild, dass als Logo im IIIF Manifest angegeben ist. Beginnt
        die URL mit http(s), wird sie direkt durchgereicht. Wird hier ein Dateiname
        oder relativer Pfad angegeben, so wird der Pfad relativ ab dem Ordner <code>resources/themes/THEMENAME/images/ </code>gebaut.
        Ist kein Bild definiert, wird der Bildfooter verwendet.</td>
    </tr>
  </tbody>
</table>

Damit die Manifeste von extern eingebunden werden können muss CORS erlaubt sein.

