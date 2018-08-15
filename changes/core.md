# 9.1 Core

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

