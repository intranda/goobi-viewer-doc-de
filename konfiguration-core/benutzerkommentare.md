# 2.27 Benutzerkommentare

Authentifizierte Benutzer können zu einzelnen Seiten Kommentare hinterlassen. Die Funktionalität kann mit dem `<enabled>` Element global an- und abgestellt werden. Zusätzlich ist es möglich die Kommentarfunktion auf Werke einzuschränken, die eine definierte Bedingung erfüllen. Diese Bedingung wird als Solr query im `<conditionalQuery>` Element definiert. Sollen ein oder mehrere E-Mailadresse bei einem neuen Kommentar benachrichtigt werden können diese mit dem wiederholbaren Element `<notificationEmailAddress>` konfiguriert werden.

```markup
<userComments>
    <enabled>true</enabled>
    <conditionalQuery>DC:varia</conditionalQuery>
    <notificationEmailAddress>user@example.org</notificationEmailAddress>
</userComments>
```

