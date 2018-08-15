# 2.15. Sprachumschaltung bei mehrsprachigen Metadaten

Metadaten können in verschiedenen Sprachen vorliegen, siehe [Kapitel 2.19.9](metadaten/mehrsprachige-metadaten.md). Wenn der Goobi viewer beim Wechsel der Sprache in der Benutzeroberfläche auch die Sprache der angezeigten Metadaten wechseln soll, dann muss der folgende Schalter auf `true` gesetzt werden:

```markup
<viewer>
    <useViewerLocaleAsRecordLanguage>false</useViewerLocaleAsRecordLanguage>
</viewer>
```



