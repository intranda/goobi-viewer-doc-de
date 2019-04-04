# 9.1 Core changes

## 2019-03-29

Aktualisierung des Goobi viewer Indexers und Anpassen der Konfigurationsdatei `solr_indexerconfig.xml`. Wenn das Metadatum `MD_SERIESTITLE` existiert muss dieses in `MD_TITLE_SERIES` umbenannt werden. Siehe dazu auch den letzten Abschnitt in [Kapitel 6.2](../anwendungsszenarien/serien-und-konvolute.md).

Außerdem kann aus der lokalen `config_viewer.xml` die Definition der Klassifikationen aus dem CMS-Bereich gelöscht werden \(config/cms/classifications\). Die Werte werden inzwischen in der Datenbank vorgehalten.

Durch die Refaktorisierung des Medien-Bereichs sind einige Funktionen von dort an andere Stelle gewandert. Zum Beispiel auch die Zuweisung einer Bild-Datei zu einer Sammlung. Dieser Umzug muss manuell gemacht werden. Dafür ist vor dem Update folgendes SQL auszuführen:

```sql
SELECT cms_media_item_id, file_name, collection, collection_name, collection_field FROM cms_media_items WHERE collection=1;
```

Die Query liefert eine Liste aller Medien-Objekte die berücksichtigt werden müssen. Für jedes muss im CMS-Backend eine neue Sammlung angelegt werden mit `collection_field` als Sammlungsfeld und `collection_name` als Sammlungsname. Das Bild muss anhand der `id` oder des Dateinamens identifiziert werden.

## 2019-02-14

Die Übersichtsseiten-Funktionalität wurde zugunsten einer CMS-Erweiterung entfernt. Mit dem Update des Cores muss zwingend auch der Goobi viewer Indexer und das Solr-Schema aktualisiert werden.

In der Konfigurationsdatei des Goobi viewer Indexers den Eintrag für den `overviewFolder` entfernen und für einen `cmsFolder` hinzufügen:

{% code-tabs %}
{% code-tabs-item title="solr\_indexerconfig.xml" %}
```markup
<!--overviewFolder>overview</overviewFolder-->
<cmsFolder>cms</cmsFolder>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Außerdem den Ordner im Dateisystem anlegen:

```bash
mkdir /opt/digiverso/viewer/cms/
chown tomcat8:tomcat8 /opt/digiverso/viewer/cms/
```

Nun folgendes SQL Statement ausführen um sicherzustellen, dass der Zeichensatz der CMS-Zieltabelle korrekt ist und die Migration nicht fehlschlägt:

```sql
ALTER TABLE cms_content_items CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Ob die Migration ausgeführt werden muss, kann in der Datenbank geprüft werden:

```sql
SELECT COUNT(*) FROM overview_pages,overview_page_updates;
```

Um dann bereits angelegte Übersichtsseiten aller Werke ins CMS zu migrieren, den folgenden Aufruf einmalig ausführen:

```text
https://viewer.example.org/viewer/tools?action=migrateOverviewPages
```

Am Ende kann der overview Ordner aus dem Dateisystem auch in das Backup verschoben werden.

## 2018-12-19

Der Goobi viewer Indexer und das dazugehörige Schema müssen aktualisiert und der Datenbestand neu indexiert werden damit die Bildmaße als WIDTH und HEIGHT in den Solr Suchindex geschrieben werden. 

## 2018-12-17

Für die neue Facettierung nach Strukturelementen muss der Goobi viewer Indexer auf die Version 3.2.20181214 und das Solr-Schema auf 20181214 aktualisiert und der Datenbestand neu indexiert werden. 

Außerdem muss in der lokalen config\_viewer.xml geprüft werden, ob das Feld `DOCSTRCT` zur Facettierung konfiguriert ist. Wenn ja ist dieses durch die neuen beiden Feldnamen `DOCSTRCT_TOP` und `DOCSTRCT_SUB` zu ersetzen.

```markup
<search>
    <drillDown>
        <!--field initialElementNumber="3">DOCSTRCT</field-->
        <field initialElementNumber="3">DOCSTRCT_TOP</field>
        <field initialElementNumber="3">DOCSTRCT_SUB</field>
    </drillDown>
</search>
```



## 2018-11-19

Eine Änderung in der Darstellung von Normdaten-Buttons erfordert eine Umkonfigurierung aller Installationen, die Normdaten anzeigen.

Der Type für NORM\_URI lautet nicht mehr `field` sondern neu `normdatauri` und kann als Parameter an beliebige Stelle platziert werden. So können Normdaten-Buttons auch zwischen anderen Parametern gerendert werden, anstatt wie bisher nur ganz am Ende. 

{% code-tabs %}
{% code-tabs-item title="config\_viewer.xml" %}
```markup
<metadata label="MD_AUTHOR" value="MASTERVALUE_WIKINORM" group="true">
    <param type="field" key="MD_VALUE"/>
    <param type="wikipersonfield" key="MD_VALUE"/>
    <param type="normdatauri" key="NORM_URI" />
</metadata>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Für den Normdaten-Button muss ein eigener Platzhalter \(hier: `{5}`\) definiert werden: 

{% code-tabs %}
{% code-tabs-item title="messages\_de.properties" %}
```text
MASTERVALUE_WIKINORM={1} <a href="http://de.wikipedia.org/wiki/{3}" target="_blank" title="Wikipedia" alt="Wikipedia" data-trigger="hover" data-placement="top" data-toggle="tooltip"><i class="fa fa-wikipedia-w" aria-hidden="true"></i></a> {5}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Außerdem die folgende Datei unter /opt/digiverso/viewer/config/ ablegen:

{% code-tabs %}
{% code-tabs-item title="normdatamap.properties" %}
```text
001=NORM_IDENTIFIER_ZLB
0247_a=URI
035__(DE-101)=NORM_IDENTIFIER_ZLB
1001_a=NORM_NAME
1001_d=NORM_LIFEPERIOD
1001_q=NORM_SEX
4001_a=NORM_ALTNAME
5000_4\:beza=NORM_ACQUAINTANCE
5000_4\:bezav:VD-16\ Mitverf.=NORM_COAUTHOR
5001_4\:beza=NORM_ACQUAINTANCE
5001_4\:bezav:Mitschu\u0308ler=NORM_CLASSMATE
5001_4\:bezav:VD-16\ Mitverf.=NORM_COAUTHOR
5001_4\:bezf=NORM_RELATIVE
5001_4\:bezfv:Vater=NORM_FATHER
5001_4\:bezfv:Vorfahren=NORM_ANCESTOR
5001_4\:saml=NORM_COLLECTOR
5102_4\:besi=NORM_OWNER
5102_4\:bete=NORM_CONTRIBUTOR
530_04\:rela=NORM_RELATIONSHIP
548__4\:datl=NORM_LIFEPERIOD
548__4\:dats=NORM_PRODUCTIONPERIOD
548__4\:datw=NORM_WORKPERIOD
548__4\:datx=NORM_LIFEPERIODEXACT
550__4\:stud=NORM_EDUCATION
550__4\:beru=NORM_PROFESSION
550__4\:obin=NORM_OBIN
551__4\:ortg=NORM_PLACEOFBIRTH
551__4\:ortu=NORM_PLACEOFEDUCATION
551__4\:orts=NORM_PLACEOFDEATH
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 2018-10-25

Die folgenden beiden Feldeinträge sollen in der Konfigurationsdatei des Goobi viewer Indexers ergänzt werden:

{% code-tabs %}
{% code-tabs-item title="solr\_indexerconfig.xml" %}
```markup
<MD_PROCESSID>
    <list>
        <item>
            <xpath>@OBJID</xpath>
            <addToDefault>false</addToDefault>
            <addUntokenizedVersion>false</addUntokenizedVersion>
        </item>
    </list>
</MD_PROCESSID>

<BOOL_CONTAINSIMAGE>
    <list>
        <item>
            <xpath>string(boolean(mets:fileSec/mets:fileGrp[@USE="PRESENTATION"]))</xpath>
            <addToDefault>false</addToDefault>
            <addSortField>true</addSortField>
        </item>
    </list>
</BOOL_CONTAINSIMAGE>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 2018-10-19

Der Goobi viewer Indexer muss aktualisiert und der Datenbestand neu indexiert werden um sicherzustellen, dass keine falschen Suchtreffer angezeigt werden.

## 2018-10-09

In der `config_viewer.xml` muss der Block `<openIdConnect>` umbenannt werden in `<authenticationProviders>`. Sein Attribut `show`wandert in die einzelnen enthaltenen `<provider>` Einträge. Der Default-Wert für `show` ist dabei `true.` Alle `<provider>` Einträge mit Namen `Google` und `Facebook` müssen zusätzlich das Attribut `type="openId"` bekommen. Die Anmeldung über lokale Viewer-Nutzeraccounts muss als separater `<provider>` eingetragen werden:

```markup
<provider type="local" show="true" name="Goobi viewer"/>
```

Eine typische komplette Konfiguration sieht dann so aus:

```markup
<authenticationProviders>
    <provider type="openId" show="true" name="Google" endpoint="https://accounts.google.com/o/oauth2/auth" clientId="CHANGEME" clientSecret="CHANGEME" image="google.png" />
    <provider type="openId" show="false" name="Facebook" endpoint="https://www.facebook.com/dialog/oauth" clientId="CHANGEME" clientSecret="CHANGEME" image="facebook.png" />
    <provider type="local" show="true" name="Goobi viewer"/>
</authenticationProviders>
```

Siehe auch Sektion [5.2 Benutzeraccounts](../konfiguration-core/benutzeraccounts/).

## 2018-09-10

Da sich bei der Suchtreffer- und Sammlungsanzeige in der URL die Position geändert hat an dem die Einschränkung angezeigt ist muss eine Weiterleitung eingerichtet werden, damit externe Verlinkungen weiterhin funktionieren. Dafür kann zum Beispiel im Apache das folgende Snippet verwendet werden:

```text
## Redirect collection facetting to new URL destination
ProxyPassMatch ^/viewer/browse/DC(.*)/-/([0-9]+)/-/-/$ !
RedirectMatch 301 ^/viewer/browse/DC(.*)/-/([0-9]+)/-/-/$ /viewer/browse/-/$2/-/DC$1/

ProxyPassMatch ^/viewer/search/DC(.*)/-/([0-9]+)/-/-/$ !
RedirectMatch 301 ^/viewer/search/DC(.*)/-/([0-9]+)/-/-/$ /viewer/search/-/-/$2/-/DC$1/

ProxyPassMatch ^/viewer/search/(.*)/-/([0-9]+)/-/-/$ !
RedirectMatch 301 ^/viewer/search/(.*)/-/([0-9]+)/-/-/$ /viewer/search/-/-/$2/-/DC:$1/
```

## 2018-09-06

Bestehende Cronjobs für den Goobi viewer sind zu prüfen und in die Datei `/etc/cron.d/intranda-goobiviewer` zusammenzuführen. Eine Vorlage für so eine Datei ist wie folgt:

{% code-tabs %}
{% code-tabs-item title="/etc/cron.d/intranda-monitoring" %}
```text
PATH=/usr/bin:/bin:/usr/sbin/
MAILTO=support@intranda.com

#
# Regular cron jobs for the Goobi viewer
#

## This REST call triggers the email notification about new search hits for users, 
## that enabled notifications for saved searches
42 8,12,17  * * *   root    curl -s http://localhost:8080/viewer/rest/search/sendnotifications/?token=fc375cda-0908-405b-ad7a-1fc5ba638662

## This REST call creates an XML sitemap for the Goobi viewer instance. Please always 
## call it on it's external URL because otherwise the protocol (http/https) might not 
## be detected correctly
18 1        * * *   root    curl -s -X POST -H "Content-Type: application/json" -d '{}' "https://viewer.example.org/viewer/rest/sitemap/update/?token=fc375cda-0908-405b-ad7a-1fc5ba638662" 1>/dev/null

## This two scripts pull the theme git repository regulary. The @daily part is only 
## a reminder for the 1-minute schedule
*/1 *       * * *   root    cd /opt/digiverso/viewer/themes/goobi-viewer-theme-reference; git pull | grep -v "Already up-to-date." 
@daily              root    echo "Please look at the git checkout interval for the Goobi viewer theme" | mail -s "Reference: Theme repository is checked out every minute" do-not-reply@example.org

## Optimize the Solr search index once a month
@monthly            root    curl -s "http://localhost:8080/solr/update?optimize=true&waitFlush=false"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Der Token muss erst generiert und dann in der lokalen config\_viewer.xml konfiguriert werden:

```bash
cat /proc/sys/kernel/random/uuid
```

{% code-tabs %}
{% code-tabs-item title="config\_viewer.xml" %}
```markup
<webapi>
    <authorization>
        <token>fc375cda-0908-405b-ad7a-1fc5ba638662</token>
    </authorization>
</webapi>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 2018-08-17

Wenn das Crowdsourcing Modul installiert ist, muss aus dessen Konfigurationsdatei `config_viewer-module-crowdsourcing.xml` der folgende Block entfernt werden:

```markup
<viewImage>
    <url>resources/components/viewImageUserGeneratedContent.xhtml</url>
</viewImage>
```

## 2018-06-21

Bei der [Facettierung](../konfiguration-core/suche/facettierung.md) dürfen die konfigurierten Feldnamen nicht mehr mit FACET\_ starten, sondern müssen mit MD\_ beginnen.

## 2018-05-28

Optional: Extrahiertes Theme einbinden. Siehe dazu Kapitel [2.16.1](../konfiguration-core/theme/externe-themes.md)

## 2018-05-08

Damit die vom Goobi viewer generierten [IIIF Presentation Manifeste](../konfiguration-core/web-api/iiif.md) von extern funktionieren, muss CORS erlaubt werde. Dafür das Headers Modul im Apache aktivieren sofern noch nicht geschehen:

```text
a2enmod headers
```

In dem oder in den vhosts folgendes Snippet einfügen:

```text
## CORS for IIIF
Header set Access-Control-Allow-Origin "*"
```

Anschließend den Apache neu starten:

```text
systemctl restart apache2
```

Außerdem muss der Goobi viewer Indexer aktualisiert und der Datenbestand neu indexiert werden. Hintergrund ist, dass für die Generierung der IIIF Manifeste die Bildgrößen verfügbar sein müssen. Stehen diese im Solr Suchindex ist die Generierung der Manifeste deutlich schneller als wenn dafür jedes Bild einzeln gelesen werden muss.

