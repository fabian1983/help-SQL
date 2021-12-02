https://awesomeopensource.com/project/qianguyihao/Web

# help-SQL

---
titel: 05-Algemene opdrachten voor MySQL-database
publiceren: waar
---

<ArticleTopAd></ArticleTopAd>



## Enkele eenvoudige commando's van MySQL

We kunnen databases en tabellen maken in Navicat Premium-software en vervolgens query-opdrachten invoeren om gegevens op te vragen. Selecteer de menubalk "Query -> New Query -> Enter sql command -> Run", het effect is als volgt:

![](https://github.com/qianguyihao/Web/blob/master/img/20200417_1750.png)

We kunnen de opdrachtregel ook rechtstreeks in de terminal invoeren om te werken.

Merk op dat bij het uitvoeren van de sql-opdracht in de Mac-terminal, `;` (puntkomma in Engels formaat) moet worden toegevoegd aan het einde van de opdracht. Het effect is als volgt:

![](https://github.com/qianguyihao/Web/blob/master/img/20200417_1700.png)

Enkele eenvoudige opdrachten van de MySQL-opdrachtregel zijn als volgt.

**Voer de opdrachtregel in als root**:

```
mysql -u root -p
```

**Controleer welke databases er zijn**:

``` sql
databases tonen;
```

**Kies om de opgegeven database in te voeren**:

``` sql
gebruik xxx_database;

# Voorbeeld
gebruik qianguyihao_database;
```

**Controleer in de huidige database welke tabellen er zijn**:

``` sql
SHOW tables;
```

**In de huidige database alle gegevens van de opgegeven tabel opvragen**:

``` sql
SELECTEER * FROM xxx_table;

# Voorbeeld
SELECTEER * FROM qianguyihao_student_table
```

**Verwijder de opgegeven tabel**:

``` sql
tafel laten vallen xxx;

# Voorbeeld
laat tafel vallen qianguyihao_student_table;
```

**Verwijder de opgegeven database**:

``` sql
drop database qianguyihao_student_table;
```

**Een database maken**:

``` sql
database maken qianguyihao_database2;
```

## waar voorwaardelijke zoekopdracht

Gebruik de `where`-component om de gegevens in de tabel te filteren, en rijen met het resultaat true verschijnen in de queryresultaten.

Het syntaxisformaat is als volgt:

``` sql
SELECT * FROM tabelnaam WHERE voorwaarde;
```

Hoe schrijf je in het bovenstaande grammaticale formaat specifiek 'voorwaarde'? Hiervoor kunnen veel situaties zijn. Laten we verder lezen.

### Vergelijkingsoperatoren

-`=` is gelijk aan
-`>` is groter dan
-`>=` groter dan of gelijk aan
-`<` is kleiner dan
-`<=` kleiner dan of gelijk aan
-`!=`: Niet gelijk
-`leeftijd> 20`: gegevens opvragen waarvan de leeftijd hoger is dan 30

**Voorbeeld**:

``` sql
# Vraag gegevens op waarvan de leeftijd groter is dan 20
SELECTEER * VAN qianguyihao_table WHERE leeftijd> 20;
```

### Logische operators

-AND

-OR

-NOT

**Voorbeeld**:

``` sql
# Vraag de gegevens op van leeftijd tussen 20 en 30
SELECTEER * VAN qianguyihao_table WHERE leeftijd TUSSEN 20 EN 30;

```

### Bereikquery

-'in' betekent in een niet-continu bereik.

-`tussen ... AND ...` betekent in een continu bereik

Bijvoorbeeld:

``` sql
# Vraag de gegevens op waarvan de naam Qiangu One of Xu Song is
SELECTEER * FROM qianguyihao_table WHERE naam IN ['Qianguyihao','Xu Song'];

SELECTEER * FROM qianguyihao_table WHERE leeftijd BETWEEN 20 AND 30;
```

### Vage vraag

-`vind ik leuk`
  -`%` betekent een willekeurig aantal tekens
  -`_` betekent een willekeurig karakter

Voorbeelden van `%`-symbolen:

``` sql
# Querygegevens die de twee woorden "front end" in de titel bevatten (er kan inhoud zijn voor en na de twee woorden "front end")
selecteer * van qianguyihao_table WHERE `title` zoals "%Frontend%";

# Vraag de gegevens op waarvan de titel begint met "Front End"
selecteer * van qianguyihao_table WHERE `title` zoals "Frontend%";

```

Voorbeelden van `_` symbolen:

``` sql
# Zoek in de titel, de zoekvoorwaarde is: er zijn ten minste vijf tekens in de titel en van deze vijf tekens moeten de eerste twee tekens beginnen met "Qiangu".
SELECTEER * VAN qianguyihao_table WHERE `titel` ZOALS "千古___";
```

### NULL oordeel

-`is null` geacht leeg te zijn

-`is niet null` beoordeeld als niet-leeg

Merk op dat er een verschil is tussen `is null` en **lege string**`""`. Nadat je de basis van js hebt geleerd, moet je weten: een lege tekenreeks is niet null, het is alleen dat de waarde erin leeg is; een lege tekenreeks neemt ook geheugenruimte in beslag.

Bijvoorbeeld:

``` sql
selecteer * FROM qianguyihao_table WHERE naam niet NULL is;

```

## join join tabelquery

### Opdracht voor Union-tabelquery

-`tableA inner join tableB`: rijen die overeenkomen met tabel A en tabel B verschijnen in het resultaat.

-`tableA left join tableB`: De rijen die overeenkomen met tabel A en tabel B verschijnen in het resultaat. De unieke gegevens in tabel A komen overeen met de nulvulling in tabel B.

-`tableA right join tableB`: De rijen die overeenkomen met tabel A en tabel B verschijnen in het resultaat. De unieke gegevens in tabel B komen overeen met de nulvulling in tabel A.

Het is moeilijk te begrijpen om het op deze manier te bekijken, laten we een voorbeeld geven.

### Voorbeelden

Nu zijn er de volgende twee tabellen: auteurstabel, boekentafelboek.

**Tabel 1**, auteur tabel auteur:

| id | authorId | authorName |
| :-- | :------- | :--------- |
| 1 | 11 | Wang Xiaobo |
| 2 | 12 | Wu juni |
| 3 | 88 | Eeuwige |

**Tabel 2**, boekenlijst boek:

| id | bookId | bookName | authorId |
| :-- | :----- | :--------- | -------- |
| 1 | 201 | Gouden Eeuw | 11 |
| 2 | 202 | Zilvertijd | 11 |
| 3 | 203 | Bronstijd | 11 |
| 4 | 204 | Top of the Wave | 12 |
| 5 | 205 | Het mysterie van Silicon Valley | 12 |
| 6 | 206 | De schoonheid van wiskunde | 12 |
| 7 | 777 | Ontwerppsychologie | 99 |

Merk op dat elk boek in Tabel 2 een corresponderende authorId heeft, en deze authorId komt overeen met de authorId in Tabel 1. **Relateer de twee tabellen op authorId**.

Laten we de queryresultaten vergelijken door de bovenstaande twee tabellen te doorzoeken door tabellen samen te voegen.

**Situatie 0**: (binnenste verbinding)

``` sql
SELECTEER * VAN auteur INNERLIJKE JOIN boek;
```

zoekresultaat:


![](https://github.com/qianguyihao/Web/blob/master/img/20200418_2300.png)


De bovenstaande query is zinloos omdat er geen queryvoorwaarde is toegevoegd.

**Situatie 1**: (binnenste verbinding)

``` sql
SELECTEER * FROM auteur INNERLIJKE WORD LID VAN boek ON author.authorId = book.authorId;
```

zoekresultaat:

![](https://github.com/qianguyihao/Web/blob/master/img/20200418_2305.png)


De bovenstaande opdracht is gelijk aan de volgende opdracht:

``` sql
SELECTEER * FROM auteur, boek WHERE author.authorId = boek.authorId;
```

**Situatie 2**: (linker join)

``` sql
SELECTEER * FROM auteur LEFT JOIN boek ON author.authorId = book.authorId;
```

zoekresultaat:

![](https://github.com/qianguyihao/Web/blob/master/img/20200418_2310.png)

**Situatie 3**: (rechter aansluiting)

``` sql
SELECTEER * FROM auteur RECHTS WORD LID FROM boek ON author.authorId = book.authorId;
```

zoekresultaat:

![](https://github.com/qianguyihao/Web/blob/master/img/20200418_2315.png)

### Referentielink

-[Mysql-tabelquery](https://blog.csdn.net/qmhball/article/details/8000003)


## Zelf-geassocieerde zoekopdracht

Als het gaat om hiërarchische relaties, kunt u self-associated queries gebruiken.


## Subquery

Wanneer het resultaat van een query een voorwaarde is van een andere query, wordt de query een subquery genoemd.






