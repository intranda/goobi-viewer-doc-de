# 6.1 Crowdsourcing

Die Konfigurationsdatei `config_crowdsourcing.xml` befindet sich in dem [lokalen Konfigurationsordner](../konfiguration-core/lokale-einstellungen.md) neben den anderen Konfigurationsdateien.Der Pfad dorthin wird in der `config_viewer.xml` definiert und muss den vollen Pfad zur Datei enthalten:

```markup
<crowdsourcing>
     <config>/opt/digiverso/viewer/config/config_crowdsourcing.xml</config>
</crowdsourcing>
```

Die `config_crowdsourcing.xml` ist wie folgt aufgebaut:

```markup
<config>
    <userGeneratedContent>
        <Content type="PERSON">
            <field label="firstname" titleEntry="2"/>
            <field label="lastname" titleEntry="3"/>
            <field label="termsOfAddress" desc="Adelige oder akademische Titel\, etc." titleEntry="1"/>
            <field label="occupation" titleEntry="5" titleFormat="\, {}"/>
            <field label="maidenName" titleEntry="4" titleFormat="\, geb. {}"/>
            <field label="maritalStatus" desc="'ledig'\, 'verlobt'\, 'verheiratet' oder 'geschieden'"/>
            <field label="personIdentifier" desc="Identifier der verwendeten Normdatenbank"  titleFormat="&#8200;[{}]" titleEntry="7"/>
            <field label="references" titleFormat="&#8200;({})" titleEntry="6"/>
            <field label="test " titleFormat="&#8200;({})" titleEntry="7"/>
        </Content>
        <Content type="ADDRESS">
            <field label="street" titleEntry="1"/>
            <field label="district" titleFormat="\, {}" titleEntry="3"/>
            <field label="city" titleEntry="4" titleFormat="\, {}"/>
            <field label="country" titleEntry="5" titleFormat="\, {}"/>
            <field label="coordinateX"/>
            <field label="coordinateY"/>
        </Content>
        <Content type="CORPORATION">
            <field label="title" titleEntry="1"/>
            <field label="address" />
            <field label="corporationIdentifier"/>
        </Content>
        <Content type="COMMENT">
            <field label="text" titleEntry="1"/>
        </Content>
    </userGeneratedContent>
</config>
```

Die vier Content Typen `PERSON`, `ADDRESS`, `CORPORATION` und `COMMENT` \(&lt;Content&gt; Elemente\) sind nicht um weitere Typen erweiterbar. Die verwendbaren Felder \(&lt;field&gt;\) lassen sich aber für jeden Typ beliebig konfigurieren.

| **Attribut** | Beschreibung |
| :--- | :--- |
| **label** | Der sowohl gespeicherte als auch angezeigte Name des Feldes. |
| **titleEntry** | Reihenfolge des Wertes im generierten Titel des Inhaltes. Die Feldwerte werden anhand dieser Zahl sortiert und hintereinander im Titel \(= Ausgabewert des ganzen Inhaltes, zum Beispiel in der Anzeige unter dem Bild\) angezeigt. |
| **titleFormat** | Besondere Formatierung des Wertes im Titel. Der Platzhalter `{}` wird durch den tatsächlichen Wert ersetzt und um die anderen Zeichen in diesem Attribut ergänzt. |
| **desc** | Wird derzeit anscheinend nur in der `toString()` Methode der des Konfigurationselements verwendet. |

Zum Label:  
Der angezeigte Name eines Attributfeldes findet über einen generierten Message-Key statt:

```text
crowdsourcing_contentType<Content type><field label>
```

Die dynamisch verwendeten Zeichenketten beginnen dabei jeweils mit einem Großbuchstaben, alle folgenden Buchstaben sind klein:

```markup
<Content type="PERSON">
       <field label="firstname" titleEntry="2"/>
</Content>
```

Aus dem obigen Eintrag würde folgender Message Key generiert werden:

```text
crowdsourcing_contentTypePersonFirstname
```

