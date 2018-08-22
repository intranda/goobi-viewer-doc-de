# 5.1.3 Hauptmenü

Um das Navigationsmenü des Goobi viewer zu konfigurieren, bietet das CMS die Möglichkeit die Menüpunkte festzulegen und Untermenüs zu erstellen.

![](../../.gitbook/assets/cms_hauptmenue.png)

Die Auswahl ist in zwei Spalten aufgeteilt. In der rechten Spalte `Verfügbare Komponenten` werden die verfügbaren Menüpunkte aufgelistet und in der Spalte `Diese Komponenten verwenden`die angezeigten Menüpunkte aufgelistet.  
  
Um Menüpunkte zu den verwendeten hinzuzufügen, müssen diese per Drag-and-Drop von der rechten Spalte in die linke gezogen werden. Die Pfeile neben den Menüpunktnamen stellen die Hierarchieebene des Menüpunkts dar. Es ist möglich, Untermenüs bis zu einer Tiefe von vier Verschachtelungen zu erstellen.

Damit die Einstellungen für das Menü auch greifen, muss nach der Konfiguration noch auf die Schaltfläche `Speichern` geklickt werden.  


Menüeinträge selbst sind KEYs, können also durch Einträge in den lokalen messages Dateien übersetzt werden. Es empfiehlt sich einen Key zu verwenden, der einen kundenspezifischen Präfix aufweist und außerdem in der Oberfläche sofort erkennbar ist, dass dieser String noch übersetzt werden muss. Beispiel:

```text
customer_FOO_menu_search
```

Dieser KEY kann anschließend in den lokalen deutschen und englischen messages Dateien übersetzt werden:

{% code-tabs %}
{% code-tabs-item title="messages\_de.properties" %}
```text
customer_FOO_menu_search=Suchen
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="messages\_en.properties" %}
```text
customer_FOO_menu_search=Search
```
{% endcode-tabs-item %}
{% endcode-tabs %}


