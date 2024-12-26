# 1.17 Suche

Die Suche im Goobi viewer erlaubt eine kombinierte Suche sowohl in den Metadaten als auch in den Volltexten. Je nach Auswahl kann eine Suche ebenfalls lediglich auf die Metadaten oder die Volltexte der digitalen Sammlungen eingeschränkt werden. Verknüpfungen von Suchbegriffen, eine Suche mit Rechts- oder Linkstrunkierung oder auch eine Phrasensuche sind ebenfalls realisierbar.

![Einfache Suche](../../../.gitbook/assets/conf_1.17.png)

Abhängig von der Präzision der Suchabfrage und der Anzahl der indexierten Werke können sich sehr viele Suchtreffer ergeben. Diese werden über mehrere Seiten verteilt dargestellt. Dem Nutzer steht ein DropDown Menü zur Verfügung, in der er die Anzahl der pro Seite angezeigten Suchtreffer auswählen kann. Diese Liste kann wie folgt konfiguriert werden:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<search>
    <hitsPerPage>
        <value default="true">10</value>
        <value>25</value>
        <value>50</value>
        <value>100</value>
    </hitsPerPage>
</search>
```
{% endtab %}
{% endtabs %}

Weiter kann konfiguriert bis zu welcher Anzahl Untertreffer automatisch ausgeklappt dargestellt werden und wie viele Untertreffer nachgeladen werden sollen, wenn auf den "Mehr Treffer laden" Link geklickt wird. Dafür sind die Optionen unterhalb von `<childHits />` relevant:

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<search>
    <childHits>
        <initialLoadLimit>5</initialLoadLimit>
        <loadOnExpand>20</loadOnExpand>
    </childHits>
    <displayHitNumbers enabled="false" />
    <fulltextFragmentLength>120</fulltextFragmentLength>
    <hitStyleClass>docstructtype__{record.DOCSTRCT}</hitStyleClass>
</search>
```
{% endtab %}
{% endtabs %}

In dem Element `displayHitNumbers` kann mit dem `enabled` Attribut gesteuert werden, ob die Suchtreffer durchnummeriert angezeigt werden sollen. Standardwert ist false.

Das Element `fulltextFragmentLength` definiert die ungefähre länge der Volltext-Ausschnitte für die Suchtrefferanzeige. Standardwert ist 200.

Im Element `hitStyleClass` kann eine CSS Klasse definiert werden die jedem Suchtreffer zugewiesen wird. Dabei können Variablen nach dem Schema {record.SOLR-FELDNAME} verwendet werden. Der Wert des Solr-Feldes wird dabei - wenn existent - in Kleinbuchstaben umgewandelt und alle Zeichen neben Buchstaben und Zahlen in Unterstriche umgewandelt. Mit der CSS-Klasse ist es möglich unterschiedlichen Suchtreffertypen ein unterschiedliches Styling zu ermöglichen.

Um die Suchbereiche der einfachen Suche zu definieren steht der folgende Konfigurationsblock zur Verfügung. Der Standardwert kann mit dem Attribut `default="true"` gesetzt werden. Existiert dieses nicht, wird automatisch der Wert `filter_ALL` angenommen.

{% tabs %}
{% tab title="config_viewer.xml" %}
```markup
<search>
    <filters>
        <filter default="true">filter_ALL</filter>
        <filter>filter_DEFAULT</filter>
        <filter>filter_FULLTEXT</filter>
        <!-- <filter>filter_NORMDATATERMS</filter> -->
        <!-- <filter>filter_UGCTERMS</filter> -->
        <!-- <filter>filter_SEARCHTERMS_ARCHIVE</filter> -->
        <!-- <filter>filter_CMS_TEXT_ALL</filter> -->
    </filters>
</search>
```
{% endtab %}
{% endtabs %}

Jeder filter-Eintrag erzeugt einen neuen Radiobutton unterhalb der einfachen Suche.

Sind Untertreffer vorhanden kann mit den folgenden beiden Schaltern eingestellt werden ab wann diese angezeigt und wie viele jeweils nachgeladen werden sollen:

{% tabs %}
{% tab title="config_viewer.xml" %}
```xml
<search>
    <childHits>
        <initialLoadLimit>0</initialLoadLimit>
        <loadOnExpand>20</loadOnExpand>
    </childHits>
</search>
```
{% endtab %}
{% endtabs %}
