# 2.17.4 Timeline

Der Goobi viewer bietet mit der Jahressuche einen Einstieg in die Inhalte, der analog zu dem Kalendereinstieg funktioniert. Die Jahressuche kann in der folgenden Sektion konfiguriert werden:

```markup
<search>
    <timeline>
        <enabled>true</enabled>
        <startyear>1500</startyear>
        <endyear>2013</endyear>
        <hits>108</hits>
    </timeline>
</search>
```

Der Schalter `<enabled>` schaltet die Jahressuche an- oder ab. Mögliche Werte für `startyear` und `endyear` sind ganze Jahre \(auch Minus\) sowie für Startjahr weiter der Wert MIN und für Endjahr der Wert MAX. Bei MIN wird das kleinste verfügbare Jahr aus dem Index als Startwert genommen, bei MAX das größte Verfügbare als Endjahr. In `hits` wird die Anzahl der Treffer für die [Zeitleiste](../../anwendungsszenarien/web-api/timeline.md) definiert. Auch hier ist MAX als Wert erlaubt.

