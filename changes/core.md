# 9.1 Core

## 2018-09-10

Da sich bei der Suchtreffer- und Sammlungsanzeige in der URL die Position geändert hat an dem die Einschränkung angezeigt ist muss eine Weiterleitung eingerichtet werden, damit externe Verlinkungen weiterhin funktionieren. Dafür kann zum Beispiel im Apache das folgende Snippet verwendet werden:

```text
## Redirect collection facetting to new URL destination
ProxyPassMatch ^/viewer/browse/DC(.*)/-/([0-9]+)/-/-/$ !
RedirectMatch 301 ^/viewer/browse/DC(.*)/-/([0-9]+)/-/-/$ /viewer/browse/-/$2/-/DC$1/

ProxyPassMatch ^/viewer/search/DC(.*)/-/([0-9]+)/-/-/$ !
RedirectMatch 301 ^/viewer/search/DC(.*)/-/([0-9]+)/-/-/$ /viewer/search/-/-/$2/-/DC$1/
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
42 8,12,17  * * *   root    curl -s http://localhost:8080/viewer/rest/search/sendnotifications/?token=6326390c-b19f-11e8-a99c-08606e6a464a

## This REST call creates an XML sitemap for the Goobi viewer instance. Please always 
## call it on it's external URL because otherwise the protocol (http/https) might not 
## be detected correctly
18 1        * * *   root    curl -s -X POST -H "Content-Type: application/json" -d '{}' "https://viewer.example.org/viewer/rest/sitemap/update/?token=6326390c-b19f-11e8-a99c-08606e6a464a" 1>/dev/null

## This two scripts pull the theme git repository regulary. The @daily part is only 
## a reminder for the 1-minute schedule
*/1 *       * * *   root    cd /opt/digiverso/viewer/themes/goobi-viewer-theme-reference; git pull | grep -v "Already up-to-date." 
@daily              root    echo "Please look at the git checkout interval for the Goobi viewer theme" | mail -s "Reference: Theme repository is checked out every minute" do-not-reply@example.org

## Optimize the Solr search index once a month
@monthly            root    curl -s http://localhost:8080/solr/update?optimize=true&waitFlush=false

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

