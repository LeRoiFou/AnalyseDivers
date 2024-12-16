<p class="titlecss"> Société ABC<br>
Analyse financière - divers </p>

<br>

# 1. Analyse des achats de l'exercice 2023

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

<LineChart
    data={accounts607}
    x=EcritureDate
    y=Montant
    lineColor='#990000'
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#cc0000"/>
<ReferenceArea yMin=60000 yMax=119999 color='#cc6600'/>
<ReferenceArea yMin=0 yMax=59999 color='#cccc00'/>
<ReferenceLine y=89300 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-28" y=33000 label='Le + bas' labelPosition=left/>
<ReferencePoint x="2023-05-31" y=144500 label='Le + haut' labelPosition=left/>
</LineChart>

```sql accounts607top5
select
    EcritureDate
    , Montant
from ${accounts607}
limit 5
```

<DataTable data={accounts607top5} totalRow=true>
    <Column id=EcritureDate title='Date des 5 plus gros achats' align=center totalAgg="Montant moyen des achats" fmt='dd/mm/yyyy'/>
    <Column id=Montant align=center totalAgg=mean contentType=colorscale colorScale=negative fmt='#,##0.00,"K" "€"'/>
</DataTable>

<!-- Saut de page -->
<div style="page-break-after: always;"></div>

# 2. Analyse des ventes de l'exercice 2023

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

<LineChart
    data={accounts707}
    x=EcritureDate
    y=Montant
    chartAreaHeight=250
    xGridlines=true>
<ReferenceArea yMin=120000 color="#0000cc"/>
<ReferenceArea yMin=60000 yMax=119999 color='#0080ff'/>
<ReferenceArea yMin=0 yMax=59999 color='#00ffff'/>
<ReferenceLine y=90700 hideValue labelPosition="aboveStart" color=alert/>
<ReferencePoint x="2023-10-04" y=41550 label='Le + bas' labelPosition=left/>
<ReferencePoint x="2023-04-26" y=139380 label='Le + haut' labelPosition=left/>
</LineChart>

```sql accounts707top5
select
    EcritureDate
    , Montant
from ${accounts707}
limit 5
```

<DataTable data={accounts707top5} totalRow=true>
    <Column id=EcritureDate title='Date des 5 plus gros CAHT' align=center totalAgg="CAHT moyen" fmt='dd/mm/yyyy'/>
    <Column id=Montant align=center totalAgg=mean contentType=colorscale colorScale=info fmt='#,##0.00,"K" "€"'/>
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
