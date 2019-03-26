# Dezember

Das Jahr neigt sich dem Ende entgegen und wir blicken mit Stolz auf die vergangenen 12 Monate Goobi viewer Entwicklung zurück. An dieser Stelle auch noch einmal an herzliches Dankeschön an alle Anwender, die sich auch in diesem Jahr wieder so konstruktiv in die Entwicklung eingebracht haben!

Wir freuen uns im Dezember über zwei neue Goobi viewer Instanzen. Das Landesmuseum für Vorgeschichte Halle \(Saale\) hat Ihre Instanz zum Projektabschluss der Öffentlichkeit präsentiert:

{% embed url="https://twitter.com/MuseumHalle/status/1069632260675158017" %}

Der Goobi viewer ist unter der Adresse [https://digital-heritage.landesmuseum-vorgeschichte.de](https://digital-heritage.landesmuseum-vorgeschichte.de) zu finden.

Außerdem freuen wir uns über die Eröffnung des Chester Beatty Goobi viewers durch die irische Kultusministerin Josepha Madigan: 

{% embed url="https://twitter.com/CBL\_Dublin/status/1070280473920880640" %}

Die Instanz ist befindet sich unter der URL [https://viewer.cbl.ie](https://viewer.cbl.ie)

Ein Update hat die [digitale Landesbibliothek Oberösterreich](https://digi.landesbibliothek.at) bekommen.

Stellvertretend für die Goobi Community treten wir im Kontext [IIIF](https://iiif.io) auch in der Öffentlichkeit stärker in Erscheinung. So ist der Goobi viewer mit seinen unterstützten APIs im letzten IIIF Newsletter erwähnt: 

* [https://iiif.io/news/2018/12/19/newsletter/\#goobi-viewer-implements-the-iiif-image-and-presentation-apis](https://iiif.io/news/2018/12/19/newsletter/#goobi-viewer-implements-the-iiif-image-and-presentation-apis)

Bevor es jetzt mit der Beschreibung der Entwicklungen losgeht noch ein letzter Punkt: Wir wurden gebeten auf Änderungen die bestehende Funktionalitäten verändern besonders hinzuweisen. Diese Änderungen werden wir hier im Digest mit einem Warnhinweis versehen und bei der Ankündigung im Community Forum auch gleich mit erwähnen.

Ausschlaggebend war der Wegfall der docStructWhiteList die eine Auswirkung auf die aufgelisteten Werke innerhalb einer Sammlung haben kann, wenn zum Beispiel nicht nur Zeitschriften, sondern auch die enthaltenen Zeitschriftenbände angezeigt werden sollen. Das ist seit der Änderung nicht mehr möglich. Wir arbeiten daran hier einerseits für viele Nutzern eine Vereinfachung hinzubekommen, andererseits aber an Flexibilität nichts einzubüßen.

{% hint style="warning" %}
So wird in Zukunft auf eine bestehende Funktionalität hingewiesen die sich geändert hat.
{% endhint %}

## Entwicklungen

### SEO

Die Suchmaschinenoptimierung ist auch im Dezember weiter vorangeschritten. Diesen Monat wurden zwei Dinge umgesetzt. Such- und Tagcloudseiten werden nun mit einem "noindex" meta-Tag ausgegeben. Diese direktive war vorher bereits durch die robots.txt gesetzt, wird aber durch den meta-Tag im HTML verbindlicher.

Zweitens werden nun kanonische Links über den URN- oder PI- \(PPN, EPN, ...\) -resolver als kanonisch gekennzeichnet. Dadurch können Suchmaschinen gleiche Seiten, die über alternative URLs zur Verfügung stehen besser verstehen und Dubletten vermeiden.

### Crowdsourcing

Es gibt nun einen neuen TEI-Export der ermöglicht Transkriptionen aus dem Crowdsourcing als TEI zu exportieren. Als kleines Addon werden auch ALTO Ergebnisse zu TEI konvertiert. Der Download steht entweder für das ganze Werk oder für die angezeigte Seite zur Verfügung und ist im neuen Widget "Zitieren und Nachnutzen" zu finden.

### Widget mit Lizenz und Nutzungshinweisen

Das bereits im November vorgestellte neue Widget "Zitieren und Nachnutzen" wurde noch einmal deutlich erweitert. Neu hinzugekommen ist vor allem die Möglichkeit gleich einen Zitierlink für das Werk oder die Seite zu kopieren. Weiter wurden aus der Oberfläche die verschiedenen Möglichkeiten der Verlinkung und des Downloads zusammengetragen und in dem neuen Widget konzentriert. Das beinhaltet zum Beispiel die Downloadmöglichkeiten unterhalb der Seite "Bibliographische Daten", die Verlinkung zum Katalog oder zum DFG-Viewer aus der Seitenleiste oder die Downloadoptionen oberhalb des Titels und in der aufgeklappten Überschrift.

Das Widget wird standardmäßig in der Seitenleiste angezeigt.

![Erweitertes Widget zum &quot;Zitieren und Nachnutzen&quot;](../../.gitbook/assets/screenshot-viewer-demo01.intranda.com-2018.12.20-16-24-03.png)

{% hint style="warning" %}
Achtung: Es wurden die Downloadmöglichkeiten auf der Seite "Bibliographische Daten" oder oberhalb des Werkes entfernt und in das neue Widget "Zitieren und Nachnutzen" verschoben.
{% endhint %}

### CMS

Es gibt ein neues CMS-Template um die einfache- und die erweiterte Suchseite über das CMS abzubilden. Dabei ist es in der Seite möglich auszuwählen welcher Suchtyp angezeigt und ob bei einer leeren Suche automatisch alle Werke oder keine Werke angezeigt werden sollen. Das Template steht im Core zur Verfügung.

### Facettierung nach Strukturelementen

Es ist ab sofort möglich nicht nur nach Dokumententypen \(Monographie, Karte, Akte, Musikalie, ...\) zu facettieren, sondern in den gefundenen Werken auch nach den enthaltenen Strukturelementen \(Kapitel, Abbildung, Tabelle, Lebenslauf, ...\). Dafür muss nicht nur der Goobi viewer Core selbst, sondern auch das Solr-Schema und der Goobi viewer Indexer aktualisiert sowie der Datenbestand neu indexiert werden. Anschließend gibt es die neuen Felder `DOCSTRCT_TOP` und `DOCSTRCT_SUB` die für die Facettierung wie auch die erweiterte Suchmaske konfiguriert werden können.

![Suchtreffer und Facettierung nach Sammlung, Dokument- und neu: Strukturtyp](../../.gitbook/assets/bildschirmfoto-vom-2018-12-20-16-35-16.png)

Siehe dazu auch die [Hinweise für Administratoren bei den Core changes am 2018-12-17](../../changes/core.md#2018-12-17) sowie das aktualisierte [Kapitel 2.17.2](../../konfiguration-core/suche/facettierung.md) in der Dokumentation.

### Authentifizierung gegen Aleph X-Services

Neu hinzugekommen ist die Möglichkeit die Benutzerauthentifizierung auch gegen einen Aleph X-Service laufen zu lassen. Dafür wurde ein neuer Authenticationprovider für bor\_auth implementiert. Siehe auch [Kapitel 2.5.4]()

### optional automatische Phrasensuche

Bei der Suche in bestimmten Feldern, zum Beispiel der Signatur, möchte man automatisch eine Phrasensuche haben und keine enthaltenen Übereinstimmungen. Dafür gibt es nun in der erweiterten Suche das Attribut `untokenizeForPhraseSearch="true"`, siehe auch [Kapitel 2.17.3](../../konfiguration-core/suche/erweiterte-suche.md)

### automatisches Öffnen eines Werkes bei nur einem Werk in einer Sammlung

Ist in einer digitalen Sammlung nur ein Werk vorhanden wurde dieses standardmäßig geöffnet. Das Verhalten ist jetzt konfigurierbar und wenn ausgestellt wird eine Suchtrefferliste mit einem Werk angezeigt, siehe auch[ Kapitel 2.18.6](../../konfiguration-core/digitale-kollektionen/weitere-einstellungen.md)

### Performanceverbesserung bei Inhaltsverzeichnissen

Der Goobi viewer hat die Möglichkeit bestimmte Strukturelemente mit Zugriffbeschränkungen für den PDF-Download zu versehen. Die Rechteprüfung führte bei Werken mit vielen Strukturelementen \(in dem gemeldeten Fall waren es 1700\) zu Performanceeinbußen. Der Code wurde optimiert und die Rechte werden nicht mehr für jedes Strukturelement einzeln sondern einmal konzentriert für alle abgefragt. Dadurch konnte die Generierzeit für das Inhaltsverzeichnis mehr als halbiert werden.

