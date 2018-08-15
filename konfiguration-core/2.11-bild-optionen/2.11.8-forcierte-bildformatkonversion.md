# 2.11.8 Forcierte Bildformatkonversion

Die folgende Option erlaubt es, sofern auf `true` gesetzt, die Auslieferung aller Bilder als JPEG zu forcieren \(unabhängig vom Ausgangsformat\). Andernfalls wird der ContentServer versuchen, das optimale Format für die Ausgabe im Webbrowser selbst zu ermitteln \(zum Beispiel PNG für PNG oder JPEG für TIFF/JPEG\). Standardwert ist `false`.

```markup
<viewer>
    <forceJpegConversion>true</forceJpegConversion>
</viewer>
```

