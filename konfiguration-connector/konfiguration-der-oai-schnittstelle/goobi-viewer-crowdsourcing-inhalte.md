# 4.1.10 Goobi viewer Crowdsourcing-Inhalte

```markup
<iv_crowdsourcing>
     <enabled>true</enabled>
     <hitsPerToken>10</hitsPerToken>
</iv_crowdsourcing>
```

| **Option**  | Beschreibung |
| :--- | :--- |
| **enabled** | Aktiviert die Verfügbarkeit des Formats in der OAI-PMH Schnittstelle. Standardwert ist `false`. |
| **hitsPerToken**  | Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Dieser Wert übeschreibt den globalen Standardwert `hitsPerToken` \(siehe [4.1.1.10](hauptkonfiguration.md#H4.1.10.Parameter:hitsPerToken)\) für dieses Metadatenformat. Ist kein Wert hier definiert, wird der globale Wert verwendet. |


