# 6.7.2 Count

In diesem Modus werden die Datensätze ebenfalls über eine selbst definierte Solr-Query gefiltert, allerdings wird hier nur die Anzahl der gefundenen Treffer zurückgegeben.

```text
https://viewer.example.org/viewer/api?action=count&q=DC:varia
```

| **Parameter**  | Beschreibung |
| :--- | :--- |
| **action** | Immer „count“ |
| **q**  | Definition einer eigenen Solr |

