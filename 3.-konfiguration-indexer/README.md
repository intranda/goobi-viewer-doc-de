# 3. Konfiguration Indexer

Der Goobi viewer setzt für die Suche in den deskriptiven Metadaten sowie in den Volltexten die Suchmaschine Apache Solr ein, die intern auf der Suchengine Apache Lucene basiert. 

Um dem Goobi viewer neue Objekte bekannt und damit in einer Suche findbar zu machen, müssen diese Objekte zunächst durch einen Indexierprozess laufen. Dieser findet mit Hilfe des Goobi viewer Indexers statt, dessen Konfiguration im Folgenden detailliert erläutert wird.

Die Konfiguration findet in der Datei `solr_indexerconfig.xml` im Installationspfad des Goobi viewer Indexers statt. Dieser ist üblicherweise `/opt/digiverso/indexer`.  


