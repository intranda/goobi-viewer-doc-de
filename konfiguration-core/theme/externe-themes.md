# 2.16.1 externe Themes

Das Theme für den Goobi viewer liegt standardmäßig in der kompilierten Applikation. Es kann aber auch extrahiert außerhalb des Applikationskontextes liegen, zum Beispiel als ausgechecktes Git-Repository.

Dafür muss als Unterelement des Theme-Eintrages noch ein rootPath mit dem absoluten Pfad bis zu dem Themes-Ordner definiert werden:

```markup
<viewer>
    <theme subTheme="true" 
           mainTheme="intranda" 
           discriminatorField="DC" 
           autoSwitch="false"
           addFilterQuery="false" 
           filterQueryVisible="false" >
        <rootPath>/opt/digiverso/viewer/themes/MYTHEMENAME/src/META-INF/resources/resources/themes/</rootPath>
    </theme>
</viewer>
```

Dieser Pfad muss außerdem im Context der Applikation als PreRessource definiert sein:

```markup
<Context>
    <Resources>
        <PreResources 
            className="org.apache.catalina.webresources.DirResourceSet"
            base="/opt/digiverso/viewer/themes/MYTHEMENAME/src/META-INF/resources/resources/themes"
            webAppMount="/resources/themes" />
    </Resources>
</Context>
```

