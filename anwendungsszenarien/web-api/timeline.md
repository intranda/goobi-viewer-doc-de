# 6.7.3 Timeline

Im Zeitleisten-Modus eine zufällige Auswahl an Datensätzen für einer Darstellung in einer Zeitleiste beziehungsweise Zeitmatrix ausgeliefert.

```text
https://viewer.example.org/viewer/api?action=timeline&startDate=1900&endDate=2000 &count=100
```

| **action**  | Immer „timeline“  |
| :--- | :--- |
| **startDate / endDate**  | Jahreszahlen von-bis, aus der Datensätze ausgeliefert werden sollen  |
| **q**  | Definition einer eigenen Solr Query, ersetzt `startDate` / `endDate`  |
| **count**  | Optional: Maximale Anzahl der auszuliefernden Datensätze  |

