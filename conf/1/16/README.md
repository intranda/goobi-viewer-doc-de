# 1.16 Theme

Falls Ihr Goobi viewer mit einem eigenen Theme installiert wurde, ist das dazugehörige Name in folgendem Konfigurationselement enthalten:

{% tabs %}
{% tab title="config\_viewer.xml" %}
```markup
<viewer>
    <theme mainTheme="reference" discriminatorField="" />
</viewer>
```
{% endtab %}
{% endtabs %}

Das Attribut `mainTheme` enthält den Namen des Themes, in dem obigen Beispiel den Wert `reference`. Dieser muss dem Ordnernamen entsprechen, in dem die Theme-Dateien liegen.

Das optionale Attribut `discriminatorField` enthält dabei den Namen des Solr-Feldes, anhand dessen die Werke erkannt werden, für die abweichendes CSS verwendet werden sollen.

{% hint style="info" %}
Grundsätzlich wird der Goobi viewer mit nur einem Theme ausgeliefert. Bei Änderungen der Theme-Definition auf einen ungültigen Wert, werden leere Seiten angezeigt.
{% endhint %}

