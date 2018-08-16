# 4.1.9 Goobi viewer Übersichtsseiten

```markup
<iv_overviewpage>
     <enabled>true</enabled>
     <hitsPerToken>100</hitsPerToken>
</iv_overviewpage>
```

| **Option**  | Beschreibung |
| :--- | :--- |
| **enabled** | Aktiviert die Verfügbarkeit des Formats in der OAI-PMH Schnittstelle. Standardwert ist `false`. |
| **hitsPerToken**  | Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Dieser Wert übeschreibt den globalen Standardwert `hitsPerToken` \(siehe [4.1.1.10](hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken)\) für dieses Metadatenformat. Ist kein Wert hier definiert, wird der globale Wert verwendet. |

