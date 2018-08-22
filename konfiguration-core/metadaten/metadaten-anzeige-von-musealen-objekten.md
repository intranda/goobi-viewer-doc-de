# 2.19.5 Metadaten-Anzeige von musealen Objekten

Für die Darstellung der Metadaten von musealen Objekten gibt es eine alternative Metadaten-Ansicht. Dabei werden Metadaten direkt unterhalb der Bildanzeige in Reitern gruppiert dargestellt.

![](../../.gitbook/assets/museale_metadaten.png)

Zunächst müssen die auf diese Weise darzustellenden Strukturtypen definiert werden:

```markup
<metadata>
      <museumDocstructTypes>
             <docStruct>Painting</docStruct>
             <docStruct>Sculpture</docStruct>
             <docStruct>Coin</docStruct>
      </museumDocstructTypes>
</metadata>
```

Um die Metadaten nach eigenem Bedarf auf unterschiedliche Reiter zu verteilen, gibt es in der Konfiguration der [Haupt-Metadaten](haupt-metadaten.md) das Attribut `type` im Element `<metadata>`:

```markup
<metadata>
   <mainMetadataList>
         <metadata label="MD_TITLE" value="" type="0">
               <param type="field" key="MD_TITLE" />
         </metadata>
         <metadata label="MD_AUTHOR" value="LINK_WIKIPEDIA" type="0">
               <param type="field" key="MD_AUTHOR" />
               <param type="wikifield" key="MD_AUTHOR" />
         </metadata>
         <metadata label="MD_LOCATION" value="" type="2">
               <param type="field" key="MD_LOCATION" />
         </metadata>
   </mainMetadataList>
</metadata>
```

  

