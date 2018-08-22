# 6.7.1 Query

In diesem Modus werden die Datensätze über eine selbst definierte Solr-Query gefiltert.

```text
https://viewer.example.org/viewer/api?action=query&q=DC:varia&count=100&sortField=DATECREATED&sortOrder=desc&jsonFormat=datecentric
```

| **Parameter**  | Beschreibung |
| :--- | :--- |
| **action** | Immer „query“ |
| **q**  | Definition einer Solr Query  |
| **count**  | Optional: Maximale Anzahl der auszuliefernden Datensätze  |
| **sortField**  | Optional \(darf mehrfach vorkommen\): Solr-Sortierfelder für das Trefferset |
| **sortOrder**  | Optional: Sortierungsrichtung der Datensäte für alle Felder aus sortField. Mögliche Werte sind `desc` und `asc`. Standardwert ist `asc`.  |
| **random**  | Optional: Wenn der Wert true ist, werden wird das Trefferset zufallsbasiert sortiert. Standardwert ist `false`.  |
| **jsonFormat**  | Optional: Format des JSON-Arrays. Einziger möglicher Wert ist `datecentric`. In diesem Fall werden die Datensätze nach Ihrem Importdatum gruppiert:  |
