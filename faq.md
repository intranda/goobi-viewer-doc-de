# 7. FAQ

## Wie kann ich herausfinden wie alt mein Goobi viewer ist?

Im Quelltext der Seite befindet sich ganz am Anfang im meta-Tag bei dem das Attribut name=""version" gesetzt ist. Der Inhalt von dem Attribut content gibt Auskunft über das Alter der Codebasis

```markup
<meta name="version" content="Goobi viewer-3.2-20180719-5b53620" />
```

"**Goobi viewer**" ist der Produktname, "**3.2**" die interne Versionsnummer. "**20180719**" entspricht dem Datum, wann der Goobi viewer kompiliert wurde. "**5b53620**" sind die ersten sieben Zeichen des Git-Commit-Hashs der für die Kompilierung verwendet wurde. 

Das Datum ist ein guter, erster Indikator. Nach dem Git-Commit-Hash kann zum Beispiel auf GitHub gesucht werden um herauszufinden auf welchem Stand die Applikation genau ist. 





