# 2.18.7 Strukturelement-Whitelist

Standardmäßig werden für Suchqueries ohne konkrete Suchbegriffe \(etwa Sammlungsauflistung, RSS-Generierung, etc.\) selbständige Werke sowie Gesamtwerke \(Anchor\) ausgeliefert, was durch die folgende Query konfiguriert ist.

```markup
<search>
    <docstrctWhitelistFilterQuery>(ISWORK:true ISANCHOR:true) -IDDOC_PARENT:*</docstrctWhitelistFilterQuery>
</search>
```

Sollen etwa weitere Dokumenttypen aufgelistet werden \(z.B. Zeitschriftenbände\), muss diese Query entsprechend erweitert werden:

```markup
<search>
    <docstrctWhitelistFilterQuery>((ISWORK:true ISANCHOR:true) -IDDOC_PARENT:*) (+DOCTYPE:DOCSTRCT +DOCSTRCT:PeriodicalVolume)</docstrctWhitelistFilterQuery>
</search>
```

