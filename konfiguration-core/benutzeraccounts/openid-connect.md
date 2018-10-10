# 2.5.1 OpenID Connect

Der Zugriff mittels OpenID Connect wird wie folgt konfiguriert:

```markup
<user>
    <authenticationProviders>
        <provider type="openId" show="true" name="Google" endpoint="https://accounts.google.com/o/oauth2/auth" clientId="CHANGEME" clientSecret="CHANGEME" image="google.png" />
        <provider type="openId" show="false" name="Facebook" endpoint="https://www.facebook.com/dialog/oauth" clientId="" clientSecret="" image="facebook.png" />
    </authenticationProviders> 
</user>
```

Folgende Parameter sind im `<provider>` Element für den `type="openId"` verfügbar:

| **Attribut** | Beschreibung |
| :--- | :--- |
| **type** | Definiert den Provider-Typ. Der Wert ist in diesem Fall immer `openId`. |
| **show** | Gibt an, ob der Provider auf der Anmeldeseite angezeigt werden soll oder ausgeblendet ist. Standardwert ist `true` |
| **name** | Name des Providers.  |
| **endpoint** | Authentifizierungs-URL des Providers \(vom jeweiligen Provider zu beziehen - bitte die Anweisungen des Providers beachten\) |
| **clientId** | Registrierte ID des Goobi viewers beim jeweiligen Provider. Pro Goobi viewer Installation muss ein neuer Client beim Provider registriert werden. |
| **clientSecret** | Geheimer Schlüssel für die registrierte clientId |
| **image** | Dateiname des angezeigten Provider-spezifischen Bildes |

