# 2.5.1 OpenID Connect

Der Zugriff mittels OpenID Connect wird wie folgt konfiguriert:

```markup
<user>
    <openIdConnect show="true">
        <provider name="Google" endpoint="https://accounts.google.com/o/oauth2/auth" clientId="CHANGEME" clientSecret="CHANGEME" image="google.png" />
        <provider name="Facebook" endpoint="https://www.facebook.com/dialog/oauth" clientId="" clientSecret="" image="facebook.png" />
    </openIdConnect> 
</user>
```

Über das Attribut `show` kann die OpenID Connect Funktionalität separat ein- beziehungsweise abgeschaltet werden.  
Darüber hinaus können zusätzliche OpenID Connect Provider \(ausstellende Institutionen\) über neue `<provider>` Elemente definiert werden:

| **name** | Angezeigter Provider Name |
| :--- | :--- |
| **url endpoint** | Authentifizierungs-URL des Providers \(vom jeweiligen Provider zu beziehen - bitte die Anweisungen des Providers beachten\) |
| **useTextField** | Wenn true, wird der Nutzer zunächst aufgefordert, einen Nutzernamen einzugeben \(erforderlich für manche OpenID Provider\) |
| **clientId** | Registrierte ID des Goobi viewers beim jeweiligen Provider. Pro Goobi viewer Installation muss ein neuer Client beim Provider registriert werden. |
| **clientSecret** | Geheimer Schlüssel für die registrierte clientId |
| **image** | Dateiname des angezeigten Provider-spezifischen Bildes |

