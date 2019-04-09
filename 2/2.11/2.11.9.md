# 2.11.9 Footer

Unter dem Bild kann ein optionaler Footer angezeigt werden. Der darin enthaltene Text wird wie folgt konfiguriert:

{% code-tabs %}
{% code-tabs-item title="config\_viewer.xml" %}
```markup
<viewer>
     <watermarkTextConfiguration>
           <text>SOLR:MD_COPYRIGHT</text>
           <text>urn</text>
           <text>purl</text>
     </watermarkTextConfiguration>
</viewer>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Die Werte `urn` und `purl` für `<text>` sind reservierte Wörter \(Groß-/Kleinschreibung spielt keine Rolle\).

Werte, die mit `SOLR:` anfangen, gefolgt vom Namen eines existierenden Solr Metadatenfeldes, bewirken, dass das entsprechende Feld im Hauptdokument des Werkes ausgewertet wird - bei Vorhandensein wird dessen Wert in das Watermark geschrieben. Alle anderen Werte werden 1:1 in das Watermark geschrieben. Im letzteren Fall sollte darauf geachtet werden, dass der eingegebene Text nicht zu lang für das Watermark ist. 

Es können in Abhängigkeit des Wertes eines Feldes im Solr Suchindex alternative Footer gerendert werden. Der Eintrag `<watermarkIdField>` kann mehrfach vorkommen. Verwendet für die Bildfooter-ID wird der Wert aus dem ersten Feld, das nicht leer ist. Der Feldname wird wie folgt definiert:

{% code-tabs %}
{% code-tabs-item title="config\_viewer.xml" %}
```markup
<viewer>
    <watermarkIdField>MD_OTHEROWNERINSTITUTION</watermarkIdField>
    <watermarkIdField>DC</watermarkIdField>
</viewer>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Der Inhalt des Feldes kann dann in der `config_imageFooter.xml` ausgelesen werden. Dafür muss die folgende Struktur vorhanden sein:

{% code-tabs %}
{% code-tabs-item title="config\_imageFooter.xml" %}
```markup
<watermarks>
    <watermark id="Wert1" height="50" width="500" color="CCCCCC">
    [...]
    </watermark>
    <watermark id="Wert2" height="50" width="500" color="CCCCCC">
    [...]
    </watermark>
    <watermark id="Wert3" height="50" width="500" color="CCCCCC">
    [...]
    </watermark>
    <watermark id="default" height="50" width="500" color="CCCCCC">
    [...]
    </watermark>
</watermarks>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Der Inhalt des Attributs `id=""` entspricht dabei dem Wert des Indexfeldes, ansonsten greift die Konfiguration mit `id="default"`.

Footer, die für `height` oder `width` einen Wert von 0 haben, werden nicht gerendert.

![Footer unter dem Bild](../../.gitbook/assets/footer.png)

Die `text`-Elemente werden dabei in der angegebenen Reihenfolge auf Machbarkeit überprüft. Im obigen Beispiel wird zuerst überprüft, ob eine URN für das aktuelle Bild existiert. Falls ja, wird die URN in den Footer gerendert, alle anderen Möglichkeiten werden übersprungen. Falls nein, wird das nächste Element ausgewertet \(PURL\). Da die PURL in jedem Fall generiert werden kann, würden alle nachfolgenden `text`-Elemente ignoriert.

