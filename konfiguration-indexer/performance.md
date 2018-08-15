# 3.3 Performance

```markup
<performance>
    <metsFileSizeThreshold>10485760</metsFileSizeThreshold>
    <dataFolderSizeThreshold>157286400</dataFolderSizeThreshold>
    <autoOptimize>false</autoOptimize>
    <threads>4</threads>
</performance>
```

####  3.3.1 Parameter: metsFileSizeThreshold {#H3.1.5.Parameter:metsFileSizeThreshold}

Größenangabe einer METS Datei in Bytes, ab der ein alternatives Schreibverfahren in den Solr Index angewendet werden soll, um Speicherüberläufe bei sehr großen Werken zu vermeiden. Standardwert ist `10485760`.

#### 3.3.2 Parameter: dataFolderSizeThreshold {#H3.1.6.Parameter:dataFolderSizeThreshold}

Größenangabe eines beliebigen Datenordners in Bytes, ab der ein alternatives Schreibverfahren in den Solr Index angewendet werden soll, um Speicherüberläufe bei sehr großen Werken zu vermeiden. Standardwert ist `157286400`.

#### 3.3.3 Parameter: autoOptimize {#H3.1.7.Parameter:autoOptimize}

Automatische Optimierung des Solr Indexes nach jeder Indexierung. Wird ein Dokument aus dem Solr Index gelöscht, so wird dieses zunächst nur als gelöscht markiert und verbleibt ansonsten im Index. Eine Optimierung des Indexes entfernt solche als gelöscht markierte Dokumente vollständig, um den Index zu verkleinern, und führt weitere Defragmentierungsmaßnahmen durch. Dies dient der Verbesserung der Performanz. Da die Optimierung eine ressourcenintensive Operation ist, sollte sie im Normalfall nur sporadisch ausgeführt werden. Standardwert ist `false`.

Sollte dieses Verhalten gewünscht sein, muss dieses Konfigurationselement auf `false` gesetzt werden. Standardwert ist `true`.

#### 3.3.4 Parameter: threads

Ist der Wert höher als 1, werden Page-Dokumente in parallelen Threads generiert. Der Standardwert ist `1`.

