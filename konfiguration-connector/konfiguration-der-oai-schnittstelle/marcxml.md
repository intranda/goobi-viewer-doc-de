# 4.1.7 MARCXML

```markup
<marcxml>
       <enabled>true</enabled>
       <hitsPerToken>10</hitsPerToken>
       <marcStyleSheet>/opt/digiverso/viewer/oai/MODS2MARC21slim.xml</marcStyleSheet>
       <setSpec>
             <field>DC</field>
             <field>DOCSTRCT</field>
       </setSpec>
</marcxml>
```

{% hint style="info" %}
Nur Records, die bei der Indexierung im METS/MODS Format vorlagen, können als MARCXML ausgeliefert werden.
{% endhint %}

| **Option**  | Beschreibung |
| :--- | :--- |
| **enabled** | Aktiviert die Verfügbarkeit des Formats in der OAI-PMH Schnittstelle. Standardwert ist `false`. |
| **hitsPerToken**  | Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Dieser Wert übeschreibt den globalen Standardwert `hitsPerToken` \(siehe [4.1.1.10](hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken)\) für dieses Metadatenformat. Ist kein Wert hier definiert, wird der globale Wert verwendet. |
| **marcStyleSheet**  | Pfad zum MODS2MARC XSLT Stylesheet. Dieses wird für die Auslieferung des MARCXML Formats benötigt |
| **setSpec**  | Konfiguration von Indexfeldern, deren Werte für `setSpec`-Elemente von OAI-Records verwendet werden. Pro Feldkonfiguration wird ein `field`-Element verwendet, und pro gefundenen Wert wird ein `setSpec`-Element generiert. |
