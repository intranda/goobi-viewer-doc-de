# 4.1 Konfiguration der OAI-Schnittstelle

In diesem Abschnitt wird die Konfiguration sämtlicher Parameter für die OAI-Schnittstelle detailliert erläutert.

{% hint style="info" %}
Alle aufgelisteten XML-Konfigurationselemente sind relativ zum Wurzelelement &lt;config&gt;.
{% endhint %}

```markup
<identifyTags>
     <repositoryName>OAI Frontend</repositoryName>
     <baseURL>http://localhost:8080/viewer/oai/</baseURL>
     <protocolVersion> 2.0</protocolVersion>
     <adminEmail>support@intranda.com</adminEmail>
     <deletedRecord>transient</deletedRecord>
     <granularity>YYYY-MM-DDThh:mm:ssZ</granularity>
</identifyTags>
```

Die einzelnen Parameter im Überblick

#### 4.1.1. Parameter: repositoryName {#H4.1.1.Parameter:repositoryName}

Dieser Parameter legt den Namen des OAI-Repositories fest.

#### 4.1.2. Parameter: baseURL {#H4.1.2.Parameter:baseURL}

Dieser Parameter definiert diejenige URL, unter der die OAI-Schnittstelle angesprochen werden kann.

#### 4.1.3. Parameter: protocolVersion {#H4.1.3.Parameter:protocolVersion}

Version des OAI Protokolls.

#### 4.1.4. Parameter: adminEmail {#H4.1.4.Parameter:adminEmail}

Kontakt E-Mail Adresse.

#### 4.1.5. deleteRecord {#H4.1.5.deleteRecord}

```text
Werte: no | persistent | transient
```

Angabe, wie mit gelöschten Datensätzen umgegangen wird.

* no - Es werden in der Repository keine Informationen über gelöschte Objekte unterhalten.
* persistent - Informationen über Löschungen werden protokolliert und ohne zeitliche Einschränkung vorgehalten.
* transient - Die Repository kann Informationen über Löschungen enthalten. Die Konsistenz der Informationen sowie das Vorhalten über eine unbestimmte Zeit werden aber nicht garantiert.

#### 4.1.6. Parameter: granularity {#H4.1.6.Parameter:granularity}

Definiert, wie genau mit Zeiten umgegangen wird. Erlaubt sind Datestamps und UTCdatetime.

```markup
<oai-identifier>
     <xmlns>http://www.openarchives.org/OAI/2.0/</xmlns>
     <repositoryIdentifier></repositoryIdentifier>
</oai-identifier>
```

#### 4.1.7. Parameter: xmlns {#H4.1.7.Parameter:xmlns}

Standard Namespace für OAI

#### 4.1.8. Parameter: repositoryIdentier {#H4.1.8.Parameter:repositoryIdentier}

Optionaler Identifier der Repository. Wird als Präfix für Record Identifier verwendet.

```markup
<solr>
      <solrUrl>http://localhost:8080/solr</solrUrl>
      <hitsPerToken>100</hitsPerToken>
      <querySuffix>-DC:restricted</querySuffix>
</solr>
```

#### 4.1.9. solrUrl {#H4.1.9.solrUrl}

URL zur Instanz von Apache Solr. Diese ist in der Regel dieselbe URL, die der Goobi viewer verwendet.

#### 4.1.10.Parameter: hitsPerToken {#H4.1.10.Parameter:hitsPerToken}

Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Standardwert ist `20`.

#### 4.1.10. Parameter: querySuffix {#H4.1.10.Parameter:querySuffix}

Statisches Suffix, das in sämtlichen Solr Queries enthalten sein soll, um etwa bestimmte Dokumente komplett herauszufiltern.

