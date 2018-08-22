# 2.11.5 Externe Bilder

Externe Bilder werden in der Bildanzeige normalerweise direkt an den Client weitergereicht. Manchmal ergibt es aber Sinn, diese durch den ContentServer abrufen und durch den Goobi viewer selbst ausliefern zu lassen. Für diese Funktionalität kann eine Liste mit URLs definiert werden. Trifft eine externe URL auf eines der konfigurierten URLs zu, dann greift die beschriebene Logik:

```markup
<viewer>
    <externalContent>
        <restrictedUrls>
            <url>https?://external/restricted/.*</url>
            <url>https?://external/noaccess/.*\.tif</url>
        </restrictedUrls>
    </externalContent>
</viewer>
```


