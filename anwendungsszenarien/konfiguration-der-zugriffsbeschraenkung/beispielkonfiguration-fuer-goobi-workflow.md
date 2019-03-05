# 6.8.3 Beispielkonfiguration für Goobi workflow

Um eine Lizenz in Goobi workflow zu konfigurieren muss als erstes ein Metadatum dafür existieren.

Dieses Metadatum muss dann in allen Strukturelementen freigeschaltet sein, die potentiell mit einer Zugriffslizenz belegt werden sollen. In der Regel bieten sich dafür vor allem die Dokumententypen wie Monographien, Zeitschriften, Karten etc. an. Es kann aber auch für Unterstrukturelemente Sinn ergeben, wenn zum Beispiel eine Zeitschrift gesperrt, aber ein Artikel daraus als Open Access freigegeben werden soll. Wichtig ist das Metadatum nicht mehr als einmal zu erlauben.

{% code-tabs %}
{% code-tabs-item title="/opt/digiverso/goobi/rulesets/ruleset.xml" %}
```markup
<MetadataType>
    <Name>AccessLicense</Name>
    <language name="de">Zugriffslizenz</language>
    <language name="en">License</language>
</MetadataType>

[...]

<metadata num="1o">AccessLicense</metadata>

[...]

<Metadata>
    <InternalName>AccessLicense</InternalName>
    <WriteXPath>./mods:mods/#mods:accessCondition[@type='use and reproduction']</WriteXPath>
</Metadata>

```
{% endcode-tabs-item %}
{% endcode-tabs %}



Um zu verhindern, dass in Goobi workflow im Metadateneditor für die Zugriffslizenz ein Freitextfeld  angezeigt wird, und dadurch potentiell fehleranfällig verschiedene Schreibweisen des gleichen Wertes eingetragen werden, kann dort in der `goobi_metadataDisplayRules.xml` ein DropDown Menü mit möglichen Werten definiert werden:

{% code-tabs %}
{% code-tabs-item title="/opt/digiverso/goobi/config/goobi\_metadataDisplayRules.xml" %}
```markup
<select1 ref="AccessLicense">
    <item selected="true">
        <label>Open Access</label>
        <value></value>
    </item>
    <item selected="false">
        <label>Lesesaal</label>
        <value>license_readingRoom</value>
    </item>
    <item selected="false">
        <label>Mitarbeiternetz</label>
        <value>license_internalEmployeeNetwork</value>
    </item>
    <item selected="false">
        <label>Virtueller Campus</label>
        <value>license_virtualCampus</value>
    </item>
</select1>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
Wir empfehlen den internen werten der Zugriffsbeschränkungen einen sprechenden Präfix wie in dem Beispiel license\_ vorzustellen. Das erleichtert später die Zuordnung im Goobi viewer Backend.
{% endhint %}
