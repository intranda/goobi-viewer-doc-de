# 4.1.1 Hauptkonfiguration

{% hint style="info" %}
Alle aufgelisteten XML-Konfigurationselemente sind relativ zum Wurzelelement 
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

#### 4.1.1.1 Parameter: repositoryName <a id="H4.1.1.Parameter:repositoryName"></a>

Dieser Parameter legt den Namen des OAI-Repositories fest.

#### 4.1.1.2 Parameter: baseURL <a id="H4.1.2.Parameter:baseURL"></a>

Dieser Parameter definiert diejenige URL, unter der die OAI-Schnittstelle angesprochen werden kann.

#### 4.1.1.3 Parameter: protocolVersion <a id="H4.1.3.Parameter:protocolVersion"></a>

Version des OAI Protokolls.

#### 4.1.1.4 Parameter: adminEmail <a id="H4.1.4.Parameter:adminEmail"></a>

Kontakt E-Mail Adresse.

#### 4.1.1.5 deleteRecord <a id="H4.1.5.deleteRecord"></a>

```text
Werte: no | persistent | transient
```

Angabe, wie mit gelöschten Datensätzen umgegangen wird.

* no - Es werden in der Repository keine Informationen über gelöschte Werke unterhalten.
* persistent - Informationen über Löschungen werden protokolliert und ohne zeitliche Einschränkung vorgehalten.
* transient - Die Repository kann Informationen über Löschungen enthalten. Die Konsistenz der Informationen sowie das Vorhalten über eine unbestimmte Zeit werden aber nicht garantiert.

#### 4.1.1.6 Parameter: granularity <a id="H4.1.6.Parameter:granularity"></a>

Definiert, wie genau mit Zeiten umgegangen wird. Erlaubt sind Datestamps und UTCdatetime.

```markup
<oai-identifier>
    <xmlns>http://www.openarchives.org/OAI/2.0/</xmlns>
    <repositoryIdentifier></repositoryIdentifier>
</oai-identifier>
```

#### 4.1.1.7 Parameter: xmlns <a id="H4.1.7.Parameter:xmlns"></a>

Standard Namespace für OAI

#### 4.1.1.8 Parameter: repositoryIdentier <a id="H4.1.8.Parameter:repositoryIdentier"></a>

Optionaler Identifier der Repository. Wird als Präfix für Record Identifier verwendet.

```markup
<solr>
    <solrUrl>http://localhost:8080/solr</solrUrl>
    <hitsPerToken>100</hitsPerToken>
    <querySuffix>-DC:restricted</querySuffix>
    <restrictions>
        <!-- <restriction field="ACCESSCONDITION">restricted1</restriction> -->
        <!-- <restriction field="ACCESSCONDITION" conditions="-MDNUM_PUBLICRELEASEYEAR:[* TO NOW/YEAR]">restricted2</licenseType> -->
    </restrictions>
</solr>
```

#### 4.1.1.9 solrUrl <a id="H4.1.9.solrUrl"></a>

URL zur Instanz von Apache Solr. Diese ist in der Regel dieselbe URL, die der Goobi viewer verwendet.

#### 4.1.1.10 Parameter: hitsPerToken <a id="H4.1.10.Parameter:hitsPerToken"></a>

Anzahl der Records, die Solr maximal bei einer Anfrage \(Seite/Token\) zurückgibt. Standardwert ist `20`.

#### 4.1.1.11 Parameter: querySuffix <a id="H4.1.10.Parameter:querySuffix"></a>

Statisches Suffix, das in sämtlichen Solr Queries enthalten sein soll, um etwa bestimmte Dokumente komplett herauszufiltern.

#### 4.1.1.12 **Parameter restrictions/restriction**

Hier besteht die Möglichkeit Zugriffsbeschränkungen zu konfigurieren, analog zu denen im Goobi viewer Core.   
In Beispiel 1 werden alle Werte herausgefiltert, bei denen im Solr Feld `ACCESSCONDITION` der Wert `restricted1` steht.   
In Beispiel 2 ist gezeigt, wie eine zusätzliche Bedingung im Attribut `conditions` angegeben werden kann. Analog zur Konfiguration der [Moving Wall](../../anwendungsszenarien/moving-wall.md) werden hier Werke nur dann herausgefiltert, wenn im Feld `ACCESSCONDITION` der Wert `restricted2` steht und zusätzlich im Feld `MDNUM_PUBLICRELEASEYEAR` ein Wert kleiner als das aktuelle Jahr enthalten ist.

