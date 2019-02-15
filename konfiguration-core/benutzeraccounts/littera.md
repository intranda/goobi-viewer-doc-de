# 2.5.5 Littera

Die Authentifizierung gegen einen Littera web.OPAC über externauth wird wie folgt konfiguriert:

```markup
<user>
    <authenticationProviders>
        <provider type="userPassword" show="false" name="littera" endpoint="https://littera.example.org/externauth" image="littera.png"/>
    </authenticationProviders> 
</user>
```

Folgende Parameter sind im `<provider>` Element für den `type="userPassword"` mit dem `name="littera"` verfügbar:

| **Attribut** | Beschreibung |
| :--- | :--- |
| **type** | Definiert den Provider-Typ. Der Wert ist in diesem Fall immer `userPasword`. |
| **show** | Gibt an, ob der Provider auf der Anmeldeseite angezeigt werden soll oder ausgeblendet ist. Standardwert ist `true` |
| **name** | Name des Providers, in diesem Fall immer `littera` |
| **endpoint** | Authentifizierungs-URL des Providers \(vom jeweiligen Provider zu beziehen - bitte die Anweisungen des Providers beachten\) |
| **image** | Dateiname des angezeigten Provider-spezifischen Bildes |
| **timeout** | Definiert in Millisekunden den maximalen Zeitraum wie lange auf eine Antwort vom Server gewartet werden soll, bevor die Anmeldung fehlschlägt. |

