# 4.1.5 METS

```markup
<mets>
     <enabled>true</enabled>
     <hitsPerToken>10</hitsPerToken>
     <metsDirectory>/opt/digiverso/viewer/indexed_mets/</metsDirectory>´
     <setSpec>
          <field>DC</field>
          <field>DOCSTRCT</field>
     </setSpec>
</mets>
```

{% hint style="info" %}
Nur Records, die bei der Indexierung im METS/MODS Format vorlagen, können als METS ausgeliefert werden.
{% endhint %}

| **Option**  | Beschreibung |
| :--- | :--- |
| **enabled** | Aktiviert die Verfügbarkeit des Formats in der OAI-PMH Schnittstelle. Standardwert ist `false`. |
| **hitsPerToken**  | Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Dieser Wert übeschreibt den globalen Standardwert `hitsPerToken` \(siehe [4.1.1.10](hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken)\) für dieses Metadatenformat. Ist kein Wert hier definiert, wird der globale Wert verwendet. |
| **metsDirectory**  | Pfad zum METS Ordner des Goobi viewers. Dieser wird für die Auslieferung des METS Formats benötigt. |
| **setSpec**  | Konfiguration von Indexfeldern, deren Werte für `setSpec`-Elemente von OAI-Records verwendet werden. Pro Feldkonfiguration wird ein `field-Element` verwendet, und pro gefundenen Wert wird ein `setSpec`-Element generiert. |

