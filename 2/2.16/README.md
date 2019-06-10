# 2.16 Theme

Falls Ihr Goobi viewer mit einem eigenen Theme installiert wurde, ist das dazugehörige Name in folgendem Konfigurationselement enthalten:

{% code-tabs %}
{% code-tabs-item title="config\_viewer.xml" %}
```markup
<viewer>
    <theme subTheme="true"
           mainTheme="reference"
           discriminatorField=""
           autoSwitch="true"
           addFilterQuery="false"
           filterQueryVisible="false" />
</viewer>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Das Attribut `mainTheme` enthält den Namen des Themes. Dieser muss dem Ordnernamen entsprechen, in dem die Theme-Dateien liegen.

Optional können für bestimmte Werke alternative Themes zugeschaltet werden. Dafür muss das Attribut `subtheme` auf `true` stehen.

Das Attribut `discriminatorField` enthält dabei den Namen des Indexfelds, anhand dessen die Werke erkannt werden, für die abweichende Theme verwendet werden sollen. Im obigen Beispiel ist es die digitale Kollektion. Die Umschaltung in ein Subtheme bewirkt auch, dass alle Suchanfragen über den gesetzten Wertes des `discriminatorField` konfigurierten Feldes gefiltert werden, solange man sich in dieser Ansicht befindet, um die Navigation sowohl visuell als auch datenmäßig etwa auf eine bestimmte Region oder Institution zu fokussieren. Steht das Attribut `filterQueryVisible` auf `true` \(Standardwert `false`\), wird die Filter-Query mit in die URL geschrieben, damit eine gefilterte Suchanfrage bequem über die URL weitergegeben werden kann.

Über das Attribut `autoSwitch` \(Standardwert `true`\) kann bestimmt werden, ob beim Öffnen eines Werks, das den entsprechenden Wert des in `discriminatorField` konfigurierten Feldes besitzt, automatisch in das entsprechende Subtheme mit Suchfilter gewechselt werden soll. Ist dieser Schalter deaktiviert, muss ein Subtheme explizit \(zum Beispiel über ein Menü\) eingeschaltet werden.

{% hint style="info" %}
Grundsätzlich wird der Goobi viewer mit nur einem Theme ausgeliefert. Bei Änderungen der Theme-Definition auf einen ungültigen Wert, werden leere Seiten angezeigt.
{% endhint %}

