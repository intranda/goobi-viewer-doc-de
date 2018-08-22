# 3.8 Starten und Beenden

Für den Goobi viewer Indexer wurde auf Ihrer Maschine ein Shell-Skript eingerichtet. Zum Starten und Beenden sollte ausschließlich dieses Skript verwendet werden.

#### 3.8.1. Starten des Indexers {#H3.6.1.StartendesIndexers}

Mit dem folgenden Befehl können Sie den Goobi viewer Indexer starten.

```text
systemctl start solrindexer
```

#### 3.8.2. Beenden des Indexers {#H3.6.2.BeendendesIndexers}

Mit dem folgenden Befehl können Sie den Goobi viewer Indexer stoppen.

```text
systemctl stop solrindexer
```

#### 3.8.3. Statusabfrage {#H3.6.3.Statusabfrage}

Mit dem folgenden Kommando können Sie überprüfen, in welchem Status sich der Goobi viewer Indexer gerade befindet:

```text
systemctl status solrindexer
```



