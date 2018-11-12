# 6.7.1 Query

In diesem Modus werden die Datensätze über eine selbst definierte Solr-Query gefiltert.

Über REST:

```text
ttp://kulturerbe-niedersachsen.gbv.de/viewer/rest/records/q/{query}/{sortField}/{sortOrder}/{jsonFormat}/{count}/{offset}/{randomize}/
```

Über Web-API \(deprecated\):

```text
https://viewer.example.org/viewer/api?action=query&q=DC:varia&count=100&sortField=DATECREATED&sortOrder=desc&jsonFormat=datecentric
```

| **Parameter**  | Beschreibung |
| :--- | :--- |
| **action** | Immer „query“ \(nur Web-API\) |
| **q**  | Definition einer Solr Query |
| **count**  | Maximale Anzahl der auszuliefernden Datensätze \(0 für alle\) |
| **offset** | Treffer-Offset \(nur REST; 0 für keinen Offset\) |
| **sortField**  | Optional \(darf mehrfach vorkommen\): Solr-Sortierfelder für das Trefferset \(/-/ für leeren Wert\) |
| **sortOrder**  | Sortierungsrichtung der Datensäte für alle Felder aus sortField. Mögliche Werte ~~sind~~ `desc` und `asc`. Standardwert \(leerer Wert /-/\) ist `asc`.  |
| **random**  | Optional: Wenn der Wert true ist, werden wird das Trefferset zufallsbasiert sortiert. Standardwert ist `false`. \(/-/ für leeren Wert\) |
| **jsonFormat**  | Optional: Format des JSON-Arrays. Einziger möglicher Wert ist `datecentric`. In diesem Fall werden die Datensätze nach Ihrem Importdatum gruppiert. \(/-/ für leeren Wert\) |

