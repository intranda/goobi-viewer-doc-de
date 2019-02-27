# 6.4.1 Dateistruktur

Ein CMS-Template ist eine Layout-Vorlage für eine durch das CMS-System des Goobi viewers definierbare Webseite. Es definiert die HTML-Struktur sowie die möglichen einfügbaren Inhalte der Seite.

Ein Template wird durch drei Dateien definiert :

| **Datei** | Beschreibung |
| :--- | :--- |
| **Template** | Eine XML-Datei, die die Beschreibung des Templates, sowie eine Liste aller möglichen Inhalte enthält. Sie verweist außerdem auf die anderen für das Template verwendeten Dateien, und ist damit das Kernstück der Template-Definition |
| **Layout** | Eine XHTML-Datei, die die HTML-Struktur der Seite vorgibt, in welche die vom Benutzer definierten Inhalte eingebettet werden. |
| **Icon** | Eine Bilddatei, die eine einfache graphische Repräsentation des Templates darstellt. Das Bild muss quadratische Abmessungen haben, und ist üblicherweise eine 128x128px große PNG-Datei. |

Alle Dateien müssen im Unterverzeichnis `/cms/templates/` des Theme-Ordners des aktiven Goobi viewer Themes im webapp Verzeichnis des Servers liegen, also zum Beispiel:

```text
/var/lib/tomcat8/webapps/viewer/resources/themes/reference/cms/templates
```

Dieses Verzeichnis wird im Folgenden als Template-Verzeichnis bezeichnet. Direkt in diesem Verzeichnis liegen die Template-Dateien. Die Layout-Dateien liegen im Unterordner `/views/` des Template-Verzeichnisses, die Template-Icons im Unterordner `/icons/`.

Die Namen der Layout- und Icon-Dateien werden in der Template-Datei definiert; der einfachen Zuordnung halber sollten alle Dateien jedoch denselben Dateinamen \(mit unterschiedlichem Suffix\) haben.

