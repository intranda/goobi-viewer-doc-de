# 2. Goobi viewer Indexer

Der Goobi viewer setzt für die Suche in den Metadaten und Volltexten auf Apache Solr.&#x20;

Um dem Goobi viewer neue Werke bekannt zu machen, müssen diese zunächst indexiert werden. Diese Aufgabe übernimmt der Goobi viewer Indexer. Einmal gestartet überwacht er einen Ordner im Dateisystem, den sogenannten Hotfolder. Über diesen Ordner nimmt er Aufgaben entgegen, zum Beispiel um Werke neu zu indexieren, aber auch um bestehende Werke zu aktualisieren oder zu löschen.

Die Konfiguration findet in der Datei `config_indexer.xml` im Installationspfad des Goobi viewer Indexers statt. Dieser ist üblicherweise `/opt/digiverso/indexer`. Die Konfigurationsmöglichkeiten sind in den folgenden Unterkapiteln näher beschrieben.
