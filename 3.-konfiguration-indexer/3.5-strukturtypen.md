# 3.5 Strukturtypen

Strukturtypen können im Index automatisch durch andere ersetzt werden, falls dies so gewünscht ist. Dazu werden diese Strukturelemente in die folgende Konfigurationsliste eingetragen:  


```markup
<docstructmapping>
    <useDefaultDocstruct>false</useDefaultDocstruct>
        <list>
            <_default>OtherDocStrct</_default>
            <Gemälde>Painting</Gemälde>
            <Münze>Coin</Münze>
    </list>
</docstructmapping>
```

Das Element `_defaul`t enthält den Standard-Strukturtyp \(siehe unten\). Alle anderen Einträge definieren Muster, nach denen Strukturtypen ersetzt werden sollen. Dabei enthält der Name des XML-Elements den ursprünglichen Namen des Strukturtyps. Der Inhalt des XML-Elements enthält die Zeichenkette, durch die der ursprüngliche Name ersetzt werden soll. Im obigen Beispiel wird der Strukturtyp `Münze durch Coin` ersetzt.

Das Konfigurationselement `useDefaultDocstruct` bestimmt, wie mit Strukturtypen umgegangen wird, die in der Konfigurationsdatei nicht explizit gemappt sind. Bei `true` wird der Strukturtyp durch den Standard-Strukturtyp \(`<_default>`\) ersetzt. Bei `false` wird das Strukturelement so übernommen, wie es ist \(allerdings werden Leerzeichen durch Unterstriche ersetzt\).  


