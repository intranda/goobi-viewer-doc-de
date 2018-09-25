# 2.20.1 Konfiguration Inhaltsverzeichnis

Das Inhaltsverzeichnis wird in der `config_viewer.xml` im Element `<toc>` konfiguriert:

```markup
<toc>
    <multiVolumeThumbnailsWidth>50</multiVolumeThumbnailsWidth>
    <multiVolumeThumbnailsHeight>60</multiVolumeThumbnailsHeight>
    <multiVolumeThumbnailsEnabled>true</multiVolumeThumbnailsEnabled>

    <volumeSortFields>
        <template name="_DEFAULT">
            <field order="asc">CURRENTNOSORT</field>
        </template>
        <template name="Periodical" groupBy=“YEAR“>
            <field order="desc">CURRENTNOSORT</field>
        </template>
    </volumeSortFields>

    <labelConfig>
        <template name="_DEFAULT">
            <metadata value=”{DOCSTRCT}{LABEL}”>
                <param type=”field” key=”DOCSTRCT” suffix=”:_SPACE_” />
                <param type=”field” key=”LABEL” />
            </metadata>
        </template>
        <template name="_GROUPS">
            <metadata label="" value="{LABEL}{MD_SERIESDISPLAYORDER}">
                <param type="translatedfield" key="LABEL" />
                <param type="field" key="MD_SERIESDISPLAYORDER" prefix="_SPACE_(" suffix=")" />
            </metadata>
        </template>
    </labelConfig>

    <tocAnchorGroupElementsPerPage>10</tocAnchorGroupElementsPerPage>

    <recordGroupIdentifierFields>
        <field>GROUPID_SERIES</field>
        <field>GROUPID_CONVOLUTE</field>
    </recordGroupIdentifierFields>

    <ancestorIdentifierFields listSiblingRecords="true">
        <field>PI_PARENT</field>
    </ancestorIdentifierFields>

    <useTreeView showDocStructs="_ALL">false</useTreeView>
</toc>
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
      <td style="text-align:left"><b>multiVolumeThumbnailsWidth/Height</b>
      </td>
      <td style="text-align:left">Größe der Thumbnails in der Inhaltsansicht für Anchor-Elemente (mehrbändige
        Werke und Zeitschriften)</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>multiVolumeThumbnailsEnabled</b>
      </td>
      <td style="text-align:left">Auf <code>true</code> setzen, um in der Inhaltsansicht für Anchor-Elemente
        Thumbnails der untergeordneten Werke anzuzeigen</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>volumeSortFields</b>
      </td>
      <td style="text-align:left">Sortierung von Bänden im Inhaltsverzeichnis eines mehrbändigen Werks.
        Hier können über Templates (analog zur Metadaten-Konfiguration) abweichende
        Konfigurationen für bestimmte Anchor-Strukturtypen definiert werden. Ist
        keine spezielle Konfiguration vorhanden, wird das Template <code>&#x201E;_DEFAULT&#x201C;</code> verwendet.
        Das optionale Attribut „groupBy“ gruppiert die Bände in einzelne Blöcke
        nach einem Solr-Metadatenfeld (etwa Jahrgänge einer Zeitschrift). Das hier
        konfigurierte Feld sollte vorzugsweise nicht multivalued sein. Falls die
        Gruppen ebenfalls sortiert werden sollen, muss das konfigurierte Gruppierungsfeld
        auch als Sortierfeld für diese Template konfiguriert sein (das heißt als
        Unterelement <code>&lt;field&gt;</code> innerhalb des Templates). Die definierten <code>&lt;field&gt;</code>-Elemente
        werden in der angegebenen Reihenfolge zur Solr-Query hinzugefügt, das heißt
        es wird primär nach dem Feld im ersten
        <field>-Element sortiert, gleichwertige Treffer untereinander nach dem zweiten,
          etc. Über das optionale Attribut order kann die Sortierung auf Wunsch absteigend
          erfolgen („desc“). Standardwert ist <code>asc</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>labelConfig</b>
      </td>
      <td style="text-align:left">Konfiguration von Labels im Inhaltsverzeichnis. Hier können über Templates
        (analog zur Metadaten-Konfiguration) abweichende Konfigurationen für bestimmte
        Strukturtypen definiert werden. Ist keine spezielle Konfiguration vorhanden,
        wird das Template <code>&#x201E;_DEFAULT&#x201C;</code> verwendet. Das spezielle
        Template "<code>_GROUPS</code>" wird für die Konfiguration des Wurzelelements
        einer abstrakten Gruppe (etwa einer Bandserie) verwendet. Die optionalen
        Attribute "prefix" und "suffix" können hier zusätzlich durch die automatische
        Übersetzung behandelt werden. Hierfür müssen entsprechende Message Keys
        definiert und als Werte dieser Attribute verwendet werden.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>tocAnchorGroupElementsPerPage</b>
      </td>
      <td style="text-align:left">Bei Gesamtwerken und Gruppen mit vielen Bänden kann der Aufbau der Bandauflistung
        sehr lange dauern. Hier gibt es die Möglichkeit, eine Paginierung der Bandauflistung
        einzusetzen und die Anzahl der angezeigten Bände pro Seite auf die hier
        konfigurierte Zahl zu beschränkten. Ist der Wert 0 oder kleiner, ist die
        Paginierung abgeschaltet.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>recordGroupIdentifierFields</b>
      </td>
      <td style="text-align:left">Eine Auflistung von Metadatenfeldern, die zur logischen Gruppierung von
        Werken verwendet werden. Diese fangen in der Regel mit <code>GROUPID_</code> an
        und dienen dazu, Werke, die einen gemeinsamen Feldwert besitzen, als Gruppe
        aufzulisten (auch wenn diese kein gemeinsames Anchor-Dokument besitzen).
        Anwendungsbeispiele sind etwa Bandserien oder Konvolute.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>ancestorIdentifierFields</b>
      </td>
      <td style="text-align:left">
        <p>Diese Liste von Identifier-Feldern dient dazu, Inhaltsverzeichnis-Hierarchien
          aus Werken zu erstellen, die entweder feste gemeinsame übergeordnete Struktur
          (Anchor), oder in einer eher losen Eltern-Kind Beziehung zueinander stehen
          (Related Item). Dabei besitzen die Child-Dokumente jeweil den Identifier
          des Parent-Dokuments im entsprechenden Metadatenfeld. Hinweis: Dieser Mechanismus
          wird auch verwendet, um Bände eines Gesamtwerks (Anchors) aufzulisten.
          Der hierfür benötigte Eintrag <code>&lt;field&gt;PI_PARENT&lt;/field&gt;</code> kann
          konfiguriert werden, wird aber bei Nichtvorhandensein implizit zu dieser
          Liste</p>
        <p>hinzugefügt. Das Attribut listSiblingRecords (wenn auf true gestellt)
          sorgt dafür, dass andere Werke auf gleicher Ebene (z.B. andere Bände desselben
          Gesamtwerks) ebenfalls aufgelistet werden, wenn gerade ein Band geöffnet
          ist.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>useTreeView</b>
      </td>
      <td style="text-align:left">Wenn auf "<code>true</code>" gesetzt, wird das Inhaltsverzeichnis als
        auf- und zuklappbarer Baum dargestellt. Für die Inhaltsverzeichnis-Seite
        kann zusätzlich konfiguriert werden, ob die Baumstruktur für alle oder
        nur für bestimmte Dokumenttypen aktiviert werden soll. Die geschieht mit
        dem Attribut "<code>showDocStructs</code>", mit Semikolon-separierten Dokumenttypen
        (z.B. <code>showDocstructs=&quot;Monograph;Manuscript;PeriodicalVolume&quot;</code>)
        beziehungsweise mit einem Eintrag für alle Typen (<code>showDocstructs=&quot;_ALL&quot;</code>).</td>
    </tr>
  </tbody>
</table>