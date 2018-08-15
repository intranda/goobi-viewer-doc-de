# 4.1.6 LIDO

```markup
<lido>
     <enabled>true</enabled>
     <hitsPerToken>10</hitsPerToken>
     <lidoDirectory>/opt/digiverso/viewer/indexed_mets/</lidoDirectory>
     <setSpec>
            <field>DC</field>
            <field>DOCSTRCT</field>
     </setSpec>
</lido>
```

{% hint style="info" %}
Nur Records, die bei der Indexierung im LIDO Format vorlagen, können als LIDO ausgeliefert werden.
{% endhint %}

| **enabled**  | Aktiviert die Verfügbarkeit des Formats in der OAI-PMH Schnittstelle. Standardwert ist `false`. |
| :--- | :--- |
| **hitsPerToken**  | Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Dieser Wert übeschreibt den globalen Standardwert `hitsPerToken` \(siehe [4.1.1.10](hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken)\) für dieses Metadatenformat. Ist kein Wert hier definiert, wird der globale Wert verwendet. |
| **lidoDirectory**  | Pfad zum LIDO Ordner des Goobi viewers. Dieser wird für die Auslieferung des LIDO Formats benötigt. |
| **setSpec**  | Konfiguration von Indexfeldern, deren Werte für `setSpec`-Elemente von OAI-Records verwendet werden. Pro Feldkonfiguration wird ein `field`-Element verwendet, und pro gefundenen Wert wird ein `setSpec`-Element generiert. |

