# 2.22 Resolver

Ihr Goobi viewer bietet Resolver an, um Werke über einen Identifier \(PI\), eine URN beziehungsweise einen selbstdefinierten Identifier zu öffnen. 

* **Identifier:** `https://viewer.example.org/viewer/piresolver?id=PPN123456789`
* **URN:**  `https://viewer.example.org/viewer/resolver?urn=urn:nbn:de:hebis:66:fuldig-1946`
* **Benutzerdefiniert:** `https://viewer.example.org/viewer/resolver?identifier=ZDB001023124&field=ALLEGROID`

Mangels Notwendigkeit sind die für das Resolving verwendeten Felder und Parameter nicht mehr konfigurierbar.

Die folgenden Optionen steuern die URL-Weiterleitung beim Öffnen des gefundenen Werkes:

```markup
<urnresolver>
    <doRedirectInsteadofForward>false</doRedirectInsteadofForward>
</urnresolver>
```

| **Option** | Beschreibung |
| :--- | :--- |
| **doRedirectInsteadOfForward** | Wenn true, wird beim Resolving ein HTTP Redirect statt Forward ausgeführt. |

Des Weiteren gibt es die Möglichkeit, die Quelldatei eines Werkes direkt zu öffnen. Je nachdem, ob das Werk aus METS oder LIDO stammt, wird ein anderer Resolver verwendet:

* METS: `https://viewer.example.org/viewer/metsresolver?id=PPN123456789`
* LIDO: `https://viewer.example.org/viewer/lidoresolver?id=PPN123456789`

