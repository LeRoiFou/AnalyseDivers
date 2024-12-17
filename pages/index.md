<p class="titlecss"> Société ABC<br>
Analyse sur les marchandises - exercice 2023 </p>

<br>

<!-- Données préalables requêtées -->

<!-- Au niveau des ventes -->

```sql accounts707
select
    EcritureDate
    , sum(Credit) - sum(Debit) as Montant
from accounts.VentesMses707_2023
group by EcritureDate
order by Montant desc
```

```sql average707
select
    avg(Montant)
from ${accounts707}
```

<!-- Au niveau des achats -->

```sql accounts607
select
    EcritureDate
    , sum(Debit) - sum(Credit) as Montant
from accounts.AchatsMses607_2023
group by EcritureDate
order by Montant desc
```

```sql average607
select
    avg(Montant)
from ${accounts607}
```

<!-- Au niveau des résultats -->

```sql result
select
    Intitule
    , month(EcritureDate) as Mois
    , sum(Credit) - sum(Debit) as Montant
from accounts.VentesMses707_2023
group by
    Intitule
    , Mois
union
select
    Intitule
    , month(EcritureDate) as Mois
    , sum(Credit) - sum(Debit) as Montant
from accounts.AchatsMses607_2023
group by
    Intitule
    , Mois
```

# 1. 1er semestre 2023

## Ventes

```sql account707sem1
select
    EcritureDate
    , sum(Credit) - sum(Debit) as Montant
from accounts.VentesMses707_2023
where date_part('month', EcritureDate) in(1, 2, 3, 4, 5, 6)
group by EcritureDate
```

<LineChart
    data={account707sem1}
    x=EcritureDate
    y=Montant
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#0000cc"/>
<ReferenceArea yMin=60000 yMax=119999 color='#0080ff'/>
<ReferenceArea yMin=0 yMax=59999 color='#00ffff'/>
<ReferenceLine y=90700 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-04" y=41550 label='Le + bas' labelPosition=left color=info/>
<ReferencePoint x="2023-04-26" y=139380 label='Le + haut' labelPosition=left color=info/>
</LineChart>

## Achats

```sql account607sem1
select
    EcritureDate
    , sum(Debit) - sum(Credit) as Montant
from accounts.AchatsMses607_2023
where date_part('month', EcritureDate) in(1, 2, 3, 4, 5, 6)
group by EcritureDate
```

<LineChart
    data={account607sem1}
    x=EcritureDate
    y=Montant
    lineColor='#990000'
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#cc0000"/>
<ReferenceArea yMin=60000 yMax=119999 color='#cc6600'/>
<ReferenceArea yMin=0 yMax=59999 color='#cccc00'/>
<ReferenceLine y=89300 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-28" y=33000 label='Le + bas' labelPosition=left color=negative/>
<ReferencePoint x="2023-05-31" y=144500 label='Le + haut' labelPosition=left color=negative/>
</LineChart>

## Résultats au 1er semestre

```sql resultsem1
select
    Intitule
    , sum(Montant) as Montant
from ${result}
where Mois in(1, 2, 3, 4, 5, 6)
group by Intitule
```

<DataTable data={resultsem1} totalRow=true>
    <Column id=Intitule align=center totalAgg=Resultat/>
    <Column id=Montant align=center totalAgg=sum fmt='#,##0.00,"K" "€"'/>
</DataTable>

# 2. 2ème semestre 2023

## Ventes

```sql account707sem2
select
    EcritureDate
    , sum(Credit) - sum(Debit) as Montant
from accounts.VentesMses707_2023
where date_part('month', EcritureDate) in(7, 8, 9, 10, 11, 12)
group by EcritureDate
```

<LineChart
    data={account707sem2}
    x=EcritureDate
    y=Montant
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#0000cc"/>
<ReferenceArea yMin=60000 yMax=119999 color='#0080ff'/>
<ReferenceArea yMin=0 yMax=59999 color='#00ffff'/>
<ReferenceLine y=90700 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-04" y=41550 label='Le + bas' labelPosition=left color=info/>
<ReferencePoint x="2023-04-26" y=139380 label='Le + haut' labelPosition=left color=info/>
</LineChart>

## Achats

```sql account607sem2
select
    EcritureDate
    , sum(Debit) - sum(Credit) as Montant
from accounts.AchatsMses607_2023
where date_part('month', EcritureDate) in(7, 8, 9, 10, 11, 12)
group by EcritureDate
```

<LineChart
    data={account607sem2}
    x=EcritureDate
    y=Montant
    lineColor='#990000'
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#cc0000"/>
<ReferenceArea yMin=60000 yMax=119999 color='#cc6600'/>
<ReferenceArea yMin=0 yMax=59999 color='#cccc00'/>
<ReferenceLine y=89300 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-28" y=33000 label='Le + bas' labelPosition=left color=negative/>
<ReferencePoint x="2023-05-31" y=144500 label='Le + haut' labelPosition=left color=negative/>
</LineChart>

## Résultats au 2ème semestre

```sql resultsem2
select
    Intitule
    , sum(Montant) as Montant
from ${result}
where Mois in(7, 8, 9, 10, 11, 12)
group by Intitule
```

<DataTable data={resultsem2} totalRow=true>
    <Column id=Intitule align=center totalAgg=Resultat/>
    <Column id=Montant align=center totalAgg=sum fmt='#,##0.00,"K" "€"'/>
</DataTable>

<!-- Saut de page -->
<div style="page-break-after: always;"></div>

# 3. Données annuelles

```sql resultyear
select
    Intitule
    , sum(Montant) as Montant
from ${result}
group by Intitule
```

<DataTable data={resultyear} totalRow=true>
    <Column id=Intitule align=center totalAgg=Resultat/>
    <Column id=Montant align=center totalAgg=sum fmt='#,##0.00,"K" "€"'/>
</DataTable>

# 4. Top 10

## Ventes

```sql accounts707top10
select
    EcritureDate
    , Montant
from ${accounts707}
limit 10
```

<DataTable data={accounts707top10} totalRow=true sort=Montant>
    <Column id=EcritureDate title=Date align=center totalAgg="Montant moyen de ces ventes" fmt='dd/mm/yyyy'/>
    <Column id=Montant align=center totalAgg=mean contentType=colorscale colorScale=info fmt='#,##0.00,"K" "€"'/>
</DataTable>

## Achats

```sql accounts607top10
select
    EcritureDate
    , Montant
from ${accounts607}
limit 10
```

<DataTable data={accounts607top10} totalRow=true sort=Montant>
    <Column id=EcritureDate title=Date align=center totalAgg="Montant moyen de ces achats" fmt='dd/mm/yyyy'/>
    <Column id=Montant align=center totalAgg=mean contentType=colorscale colorScale=negative fmt='#,##0.00,"K" "€"'/>
</DataTable>

<!-- **********************************\*\*\******************************** -->
<!-- ********************** STYLE OPERE SOUS FORMAT CSS ******************** -->
<!-- *********************************************************************** -->
<style>
    .titlecss {
        text-align:center;
        font-weight: bolder;
        color: rgb(38, 108, 165);
        font-size: 20px;
        text-transform: uppercase;
        padding: 10px;
        border: 2px black solid;
    }
</style>
