# 2.12 individuelle Seitentypen

In dem URL Schema der Links des Goobi viewers gibt es feststehende Namen für verschiedene Seitentypen. Die Bildanzeige befindet sich zum Beispiel immer unter /image/ und die Suche unter /search/. Um hier eigene Namen zu vergeben und die Standardwerte zu überschreiben gibt es den folgenden Konfigurationsblock:

```markup
<viewer>
    <pageTypes>
        <viewObject>objekt</viewObject>
        <viewImage>objekt</viewImage>
        <search>suche</search>
        <!-- <viewToc></viewToc> -->
        <!-- <viewThumbs></viewThumbs> -->
        <!-- <viewMetadata></viewMetadata> -->
        <!-- <viewFulltext></viewFulltext> -->
        <!-- <term></term> -->
        <!-- <browse></browse> -->
        <!-- <viewFullscreen></viewFullscreen> -->
        <!-- <sites></sites> -->
    </pageTypes>
</viewer>
```



