# 2.28 CMS

Das CMS-Modul des Goobi viewers wird im Elementblock `<cms>` konfiguriert.

```markup
<cms>
    <enabled>true</enabled>
    <useCustomNavBar>true</useCustomNavBar>
    <mediaFolder>cms_media</mediaFolder>
    <mediaDisplayWidth>400</mediaDisplayWidth>
</cms>
```

| **Option** | Beschreibung |
| :--- | :--- |
| **enabled** | Schaltet CMS-Funktionen grundsätzlich ein beziehungsweise ab. Ist Ihr Goobi viewer ohne CMS-Funktionen installiert worden, hat dieses Konfigurationselement keine Funktion. Standardwerst ist false. |
| **useCustomNavBar** | Die CMS-Funktionen des Goobi viewers bieten die Möglichkeit, das Haupt-Navigationsmenü anzupassen, etwa dort um selbst erstellte CMS-Seiten zu integrieren. Damit das angepasste Navigationsmenü verwendet wird, muss dieser schalter auf `true` stehen. Standardwert ist `false`. |
| **mediaFolder** | Ordner, in dem für die CMS-Seiten hochgeladenen Mediendateien \(zum Beispiel Bilder\) abgelegt werden. Der Ordner wird relative zum Root-Datenorder des Goobi viewers erwartet \(typischerweise `/opt/digiverso/viewer`\). Standardwert ist `cms_media`. |
| **mediaDisplayWidth** | Definiert die Breite in Pixeln, in der CMS-Medien standardmäßig dargestellt werden: in CMS-Templates, im TileGrid oder als Repräsentant einer Sammlung. |



