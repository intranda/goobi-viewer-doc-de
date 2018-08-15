# Februar

Im Februar haben die Universitätsbibliothek Kiel und die Landesbibliothek in Liechtenstein ein Update des Goobi viewers erhalten:

* [http://dibiki.ub.uni-kiel.de/viewer/](http://dibiki.ub.uni-kiel.de/viewer/)
* [http://www.eliechtensteinensia.li/viewer/](http://www.eliechtensteinensia.li/viewer/)

## Entwicklungen

### Merklisten

Eine Überarbeitung der Bücherregale in Form von Merklisten ist in diesem Monat in den Goobi viewer master Branch zurück geflossen. Merklisten, die in der Nutzersession gespeichert werden, stehen nun auch nicht angemeldeten Benutzern zur Verfügung. Die Merkliste kann auf Wunsch per Email verschickt werden.

Für angemeldete Benutzer wurde die Bedienführung für Merklisten vereinfacht.

### Emailbenachrichtigung bei gespeicherten Suchen

Bereits seit längerer Zeit können angemeldete Benutzer eine Suche Speichern, um diese zu einem späteren Zeitpunkt wieder aufzurufen. Diese Funktionalität wurde um eine optionale Emailbenachrichtigung bei neuen Suchtreffern erweitert. 

### CMS

Erweiterungen in dem Suchwidget und den CMS-Suchtrefferseiten erlauben nun, dass eine Suche aus einem Subtheme auch auf eine Subtheme-Suchtrefferseite weiterleitet. Mit der Möglichkeit auf der Suchtrefferseite auch eine einschränkende Solr-Query zu definieren existiert damit nun die Möglichkeit in Subthemes eigene gestylte Suchen und Suchtrefferlisten zur Verfügung zu stellen.

Außerdem wurden die beiden Seiten für das Feedback und die Datenschutzerklärung mit dem Piwik Opt-Out Code in das CMS migriert. Dadurch ist es jetzt deutlich komfortabler die bestehenden Texte anzupassen.

Des Weiteren gab es diverse Bugfixes in dem CMS-Bereich.

### API

Die REST-Schnittstelle hat einen neuen Endpoint bekommen, der dabei Hilft bei neuen Suchtreffern eine Email-Benachrichtigung zu versenden.

