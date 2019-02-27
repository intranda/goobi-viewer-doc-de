# 6.4.3 Inhaltstypen

Im folgenden sind die verschiedenen Inhaltstypen und deren Funktionalität aufgelistet:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Typ</th>
      <th style="text-align:left">Beschreibung</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>TEXT</b> 
      </td>
      <td style="text-align:left">Dies ist ein einfacher Text, ohne HTML-Elemente, der beliebig in der Layout-Datei
        aufgerufen werden kann. Die Texte sind mehrsprachig verfügbar.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>HTML</b> 
      </td>
      <td style="text-align:left">Dies ist ein HTML-Text, der als echtes HTML in die Seite eingebettet wird.
        HTML-Texte sind mehrsprachig verfügbar.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>MEDIA</b> 
      </td>
      <td style="text-align:left">
        <p>Dies ist eine Bilddatei, die außerhalb des Templates erstellt und mit
          einer Beschriftung versehen wird. Folgende Methoden stehen zur Verfügung:</p>
        <ul>
          <li><b>Name: </b><code>#{cmsPage.getMedia(&apos;image&apos;).name}</code>
          </li>
          <li><b>Beschreibung: </b><code>#{cmsPage.getMedia(&apos;image&apos;).description}</code>
          </li>
          <li><b>relative URL: </b><code>#{cmsPage.getMedia(&apos;image&apos;).link}</code>
          </li>
          <li><b>absolute URL: </b><code>#{cmsPage.getMedia(&apos;image&apos;).linkURI}</code>
          </li>
          <li><b>IIIF-URL zu Bild mit Höhe und Breite: <br /></b><code>#{cmsPage.getMedia(&apos;image&apos;).getIconURI(width, height)}</code>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SOLRQUERY</b> 
      </td>
      <td style="text-align:left">Gibt eine Liste von Werks-Strukturelementen einer Solr-Anfrage als Java-Objekte
        zurück. Sie kann nur mit einer entsprechenden JSF verwendet werden.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>PAGELIST</b> 
      </td>
      <td style="text-align:left">Gibt eine Liste von CMS-Seiten als Java-Objekte zurück, aus denen deren
        Inhalte analog zu den Inhalten von cmsPage abgerufen werden können. Nur
        stehen die Elemente der Liste an Stelle von cmsPage.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>COLLECTION</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>TILEGRID</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>TOC</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>RSS</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>SEARCH</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>GLOSSARY</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>COMPONENT</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>TAGS</b>
      </td>
      <td style="text-align:left"><b></b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>METADATA</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>