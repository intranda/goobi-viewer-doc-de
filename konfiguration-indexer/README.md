# 3. Konfiguration Indexer

Der Goobi viewer setzt für die Suche in den Metadaten und Volltexten auf Apache Solr. 

Um dem Goobi viewer neue Werke bekannt zu machen, müssen diese zunächst indexiert werden. Diese Aufgabe übernimmt der Goobi viewer Indexer. Einmal gestartet überwacht er einen Ordner im Dateisystem, den sogenannten Hotfolder. Dort abgelegte Dateien werden gemäß der vorliegenden Konfiguration abgearbeitet und indexiert. 

Die Konfiguration findet in der Datei `solr_indexerconfig.xml` im Installationspfad des Goobi viewer Indexers statt. Dieser ist üblicherweise `/opt/digiverso/indexer`. Die Konfigurationsmöglichkeiten sind im folgenden erläutert.

