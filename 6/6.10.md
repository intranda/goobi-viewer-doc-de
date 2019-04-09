# 6.10 Leeren des Solr Suchindex

Manchmal kann es während der Entwicklung notwendig sein, den gesamten Solr Suchindex zu leeren. Dafür müssen alle Werke ohne Rückstände aus dem Goobi viewer gelöscht werden. Zum Abschluss steht dann eine Optimierung des Solr-Index an. Auf der Linux Kommandozeile kann diese Aufgabe wie folgt gelöst werden:

```text
cd /opt/digiverso/viewer/indexed_mets/
for i in *.xml; do echo touch ../hotfolder/${i/.xml/.purge}; done
curl "http://localhost:8080/solr/update?optimize=true&waitFlush=false"
```



