# 6.6.2 Count

In diesem Modus werden die Datensätze ebenfalls über eine selbst definierte Solr-Query gefiltert, allerdings wird hier nur die Anzahl der gefundenen Treffer zurückgegeben.

Über REST:

```text
https://viewer.example.org/viewer/rest/records/count/DC:varia/
```

Über Web-API Servlet \(deprecated\):

```text
https://viewer.example.org/viewer/api?action=count&q=DC:varia
```

| **Parameter**  | Beschreibung |
| :--- | :--- |
| **action** | Immer „count“ |
| **q**  | Definition einer eigenen Solr |

