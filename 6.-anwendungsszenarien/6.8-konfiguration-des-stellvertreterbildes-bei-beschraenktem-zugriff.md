# 6.8 Konfiguration des Stellvertreterbildes bei beschränktem Zugriff

Sofern im Goobi viewer die Bildanzeige durch eine Access Condition verhindert ist, wird ein Stellvertreterbild angezeigt.

Der Pfad zu diesem Bild ist in der messages Datei über den folgenden Key konfiguriert: 

```text
noImage_accessDenied
```

Der Standardeintrag ist wie folgt:

```text
noImage_accessDenied=<img src\=“/viewer/resources/images/access_denied.png” />
```



Der Key kann in den lokalen messages Dateien überschrieben werden. Dadurch können individuelle Bilder oder Texte angezeigt werden die pro Sprache unterschiedlich sind.

