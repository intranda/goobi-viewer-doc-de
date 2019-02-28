# 6.6.4 Normdaten

Die Web API bietet die Möglichkeit, Anfragen an den intranda Normdaten-Service beziehungsweise  GND abzuschicken, und die Normdatensätze als JSON-Objekte zu erhalten.

```text
https://viewer.example.org/viewer/api?action=normdata&url=http%3A%2F%2Fd-nb.info%2Fgnd%2F123524652&lang=de
```

| **Parameter**  | Beschreibung |
| :--- | :--- |
| **action** | Immer „normdata“ |
| **url**  | Escapte URL zum intranda Normdaten-Service oder GND |
| **lang**  | Optional: Sprache, in der die Labels der Normdatenfelder zurückgegeben werden sollen. Standardwert ist die Systemsprache des Servers. |

