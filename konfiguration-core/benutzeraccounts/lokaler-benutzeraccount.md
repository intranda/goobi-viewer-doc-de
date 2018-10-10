# 2.5.2 lokaler Benutzeraccount

Der Zugriff über einen Goobi viewer internen Benutzeraccount wird wie folgt konfiguriert:

```markup
<user>
    <authenticationProviders>
        <provider type="local" show="true" name="Goobi viewer"/>
    </authenticationProviders> 
</user>
```

Folgende Parameter sind im `<provider>` Element für den `type="local"` verfügbar:

| **Attribut** | Beschreibung |
| :--- | :--- |
| **type** | Definiert den Provider-Typ. Der Wert ist in diesem Fall immer `local`. |
| **show** | Gibt an, ob der Provider auf der Anmeldeseite angezeigt werden soll oder ausgeblendet ist. Standardwert ist `true` |
| **name** | Name des Providers.  |

Für die Registrierung eines lokalen Benutzeraccounts, wie auch für anderweitigen Mailversand muss ein Mailserver konfiguriert werden. Die Konfiguration dafür ist wie folgt:

```markup
<user>
    <smtpServer>localhost</smtpServer>
    <smtpUser></smtpUser>
    <smtpPassword></smtpServer>
    <smtpSenderAddress>do-not-reply@goobi-viewer.example.org</smtpSenderAddress>
    <smtpSenderName>Goobi viewer</smtpSenderName>
    <feedbackEmailAddress>feedback@example.org</feedbackEmailAddress>
</user>
```

| Option | Beschreibung |
| :--- | :--- |
| **smtpServer** | SMTP Server für den Mailversand |
| **smtpUser** | Benutzername zur Authentifizierung an dem SMTP Server |
| **smtpPassword** | Passwort zur Authentifizierung an dem SMTP Server |
| **smtpSenderAddress** | Die dem Empfänger angezeigte Senderadresse |
| **smtpSenderName** | Der dem Empfänger angezeigte Sendername |
| **smtpSecurity** | Verschlüsselungsart für den Mailversand. Mögliche Werte sind: `NONE`, `SSL` und `STARTTLS`. Standardwert ist `NONE`. |
| **feedbackEmailAddress** | Empfängeradresse für Benutzerfeedback |

{% hint style="info" %}
Die im Beispiel angegebene Konfiguration versendet über einen lokalen Dienst \(zum Beispiel Postfix\), der auf dem gleichen Server installiert sein muss, wie der Goobi viewer selbst.
{% endhint %}

