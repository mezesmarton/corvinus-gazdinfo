---
title: Exceles Gyakorlati ZH Felkészítő Jegyzet
course: Statisztika I.
tags:
  - statisztika
  - ZH
  - excel
  - adatelemzés
  - gyakorlat
---

> [!abstract] Rövid összefoglaló
> Ez a jegyzet a Statisztika I. tárgy első 6 hetének anyagát öleli fel, kifejezetten a gyakorlati, Excel-alapú zárthelyi dolgozatra koncentrálva. A ZH konzultáció videóleirata és a tanár instrukciói alapján készült, részletesen bemutatva az 5 várható feladattípust (viszonyszámok, dobozábra, mennyiségi sorok, asszociáció, koncentráció), az Exceles megoldási trükköket, és a leggyakoribb buktatókat.

## 🎓 A Tanár tippjei: Így zajlik a ZH!

> [!tip] A ZH felépítése és időkerete
> *   **Időtartam:** 90 perc áll rendelkezésre.
> *   **Feladatok:** 5 feladat lesz. Arra lehet számítani, hogy minden témakörből lesz valami (az első 6 hét anyagából).
> *   **Nehézség:** Ne várjátok, hogy a ZH pont ugyanolyan nehézségű lesz, mint a gyakorló feladatsor. Lesz, ami könnyebb, lesz, ami hosszabb/munkásabb (pl. a 3. feladat).
> *   **Pontozás:** Összesen 30 pontos lesz a ZH. Nem feltétlenül lesz minden feladat egyformán 6 pontos. Egy rövidebb feladat kevesebb, egy munkásabb (mint a 3-as) akár 8 pontot is érhet. Oda lesz írva minden feladathoz a pontszám.
> *   **Értelmezés vs. Számolás:** Sokszor az értelmezés több pontot ér, mint maga a számolás (pl. Lorenz-görbe leolvasása vs. értelmezése).
> *   **Képletgyűjtemény:** Hozhattok magatokkal! Érdemes kinyomtatni az ide vonatkozó 1-2 oldalt.

> [!danger] Két nagyon fontos szabály!
> 1.  **MINDIG hivatkozz (linkelj) a cellákra!** Sose írj be "kézzel" kiszámolt vagy leolvasott számot. Ha rossz értéket írsz be kézzel, a tanár nem tudja visszakövetni, honnan vetted, és nem tud részpontot adni! Ha hivatkozol, látja a logikát, és jár a részpont.
> 2.  **Segédszámítások helye:** Lehetőleg **ne jobbra** haladjatok a végtelenbe a segédszámításokkal! A tanár osztott képernyőn javít, és nem szereti görgetni a táblázatot oldalra. A segédszámításokat mindig lefelé (függőlegesen) vagy az erre kijelölt oszlopokban végezzétek.

> [!warning] Mit tegyek, ha elakadtam? (Részpontok megmentése)
> Ha egy feladatban elakadsz (pl. nem tudod kiszámolni az $IQR$-t a $K$ mutatóhoz, vagy nem jön ki a $\chi^2$), de tudod a következő lépést, **írj be egy hasraütésszerű értéket**, és azzal számolj tovább! Erre meg fogod kapni a részpontokat! (Pl. ha az $F$ mutatóhoz nem tudod a $Q_1$-et, beírsz oda mondjuk 40-et, és a képletet erre hivatkozva jól írod be, a tanár elfogadja a logikát).

---

## 1. Feladat: Viszonyszámok és Dinamika

Ez a témakör a táblázatos adatok elemzéséről, arányok és változások számításáról szól.

> [!definition] Viszonyszámok fajtái
> *   **Megoszlási viszonyszám:** Egy részarányt mutat az egészhez képest (pl. Óvoda kiadása / Összes oktatási kiadás).
> *   **Dinamikus viszonyszám:** Időbeli változást mutat.
>     *   **Bázisviszonyszám:** Minden évet egy kiválasztott, fix évhez (bázis) viszonyítunk.
>     *   **Láncviszonyszám:** Minden évet a közvetlenül megelőző évhez viszonyítunk.
> *   **Intenzitási viszonyszám:** Két különböző mértékegységű adat hányadosa (pl. egy főre jutó GDP).

### Exceles megvalósítás és trükkök

> [!example] A gyakorló feladat logikája
> A táblázatban oktatási kiadások (millió Ft) szerepeltek 2014-2020 között.
> *   **Megoszlás:** A cella értéke osztva az adott oszlop (év) **Összesen** sorával. Excelben: A nevező sorát fixálni kell dollárjellel (pl. `C5/C$10`).
> *   **Bázisviszonyszám:** A cella értéke osztva a bázisév (pl. 2014) azonos sorában lévő értékével. Excelben: Az osztó oszlopát kell fixálni (pl. `D5/$C5`).
> *   **Láncviszonyszám:** A cella értéke osztva az előző év értékével (pl. `D5/C5`). Nincs szükség dollározásra.

> [!done] 💡 Érthető magyarázat a dollárjelhez (`$`)
> A dollárjel az Excelben a "lehorgonyzás". 
> *   Ha az `$A1`-et húzod jobbra, mindig az A oszlopból fog adatot venni (jó bázisviszonyszámhoz).
> *   Ha az `A$1`-et húzod lefelé, mindig az 1. sorból vesz adatot (jó megoszláshoz, ha az 'Összesen' a legalsó sorban van).
> *   Ha nem akarsz a dollározással szenvedni, csinálhatod **tömbképlettel** is: Kijelölöd az egész helyet, ahova az eredményt várod, beírod a képletet (pl. egy egész oszlop osztva egy cellával), és `Ctrl+Shift+Enter` (vagy sima Enter az újabb Excelekben). Ez sokkal gyorsabb, és nincs dollár-hiba!

### Értelmezés - Mire figyelj!

> [!danger] Százalék vs. Százalékpont!
> Két százalékos érték (pl. két megoszlási viszonyszám) különbsége MINDIG **százalékpont**. 
> *Kérdés:* Hány százalékponttal változott az alapfokú oktatás aránya 2017-ről 2020-ra?
> *Válasz:* Egyszerűen kivonod a kettőt egymásból (pl. $49,46\% - 50,37\% = -0,91$). A válasz: **0,9 százalékponttal csökkent**. Soha ne mondd, hogy ennyi százalékkal csökkent!

*   **Bázisviszonyszám értelmezése:** Ne úgy fogalmazz, hogy "nőtt 2014-hez képest", hanem úgy, hogy "felette volt" vagy "magasabb volt, mint 2014-ben". (Hiszen lehet, hogy az előző évhez képest csökkent, csak a 2014-es bázisnál még mindig magasabb).

---

## 2. Feladat: Dobozábra (Boxplot) és Aszimmetria

A dobozábra (Boxplot) 7 kulcsfontosságú értékből épül fel.

> [!definition] A Dobozábra (Boxplot) 7 pontja
> 1.  **Minimum:** A legkisebb adat, ami *még nem* kiugró.
> 2.  **Alsó kerítés:** $Q_1 - 1,5 \cdot IQR$
> 3.  **Alsó kvartilis ($Q_1$):** Az adatok 25%-a kisebb nála.
> 4.  **Medián ($Me$ / $Q_2$):** A középső adat (50%).
> 5.  **Felső kvartilis ($Q_3$):** Az adatok 75%-a kisebb nála.
> 6.  **Felső kerítés:** $Q_3 + 1,5 \cdot IQR$
> 7.  **Maximum:** A legnagyobb adat, ami *még nem* kiugró.
> *(Az $IQR$ az interkvartilis terjedelem: $Q_3 - Q_1$)*

### Exceles kiszámítás
*   **Minimum/Maximum:** `=MIN(adatok)`, `=MAX(adatok)`
*   **Kvartilisek ($Q_1, Q_3$):** Kétféleképpen is lehet:
    *   `=KVARTILIS.KIZÁR(adatok; 1)` (vagy 3)
    *   `=PERCENTILIS.KIZÁR(adatok; 0.25)` (vagy 0.75)
*   **Kerítések:** Kiszámolod az $IQR$-t ($Q_3 - Q_1$), majd képlettel: $= Q_1 - 1,5 \cdot IQR$ és $= Q_3 + 1,5 \cdot IQR$.
*   **Diagram készítés:** Kijelölöd az eredeti adatsort -> Beszúrás -> Dobozábra (Box and Whisker).

> [!warning] Vigyázat: A kerítés és az ábra
> A vizsgán gyakori hiba: Ha ránézel egy dobozábrára, és meg kell mondani az alsó kerítést, sokan a legalsó bajusz végét mondják. **Helytelen!** A bajusz a minimum/maximum értékig ér. Az alsó/felső kerítés láthatatlan az ábrán (hacsak nincs rajta kiugró pont). Az értékük képlettel számítandó!

### Aszimmetria mutatók

A tanár hangsúlyozta, hogy a három mutató mást-mást fejez ki, mert máshogy reagálnak a szélsőségekre.

| Mutató neve | Mit használ? | Mire érzékeny? | Leolvasható dobozábráról? |
| :--- | :--- | :--- | :--- |
| **$F_{0,25}$** | Csak $Q_1$, $Me$, $Q_3$ | **Egyáltalán nem** (Robusztus). Csak a középső 50%-ot nézi. | **Igen** |
| **$P$ (Pearson)** | Átlag, Medián (Módusz) | **Közepesen** (Fél-robusztus). A kiugrók húzzák az átlagot. | Nem (pontosan), de az átlag helyzetéből becsülhető. |
| **$\alpha_3$** | Minden adat 3. hatványa | **Nagyon erősen** (Köbösen). A szélsőségek dominálnak. | Nem |

> [!example] Példa az értelmezésre
> Ha a dobozábrán a medián pontosan középen van a dobozban ($F_{0,25} \approx 0$), akkor a középső 50% **szimmetrikus**.
> De ha van pár nagyon nagy kiugró érték (fent pöttyök), az az átlagot felhúzza. Így az Átlag > Medián lesz, tehát a $P$ mutató **pozitív** lesz (enyhe jobbra elnyúlás). Az $\alpha_3$ pedig a 3. hatvány miatt **határozottan nagy pozitív** értéket fog adni.

---

## 3. Feladat: Osztályközös Mennyiségi Sor

Ez a leghosszabb, leginkább "számolós" feladat. Gyakorisági sorból (ahol -tól -ig osztályközök vannak) kell statisztikákat becsülni.

### Diagram: Hisztogram
*   Kijelölöd az adatokat -> Oszlopdiagram.
*   Az oszlopdiagramon a térközt (Gap Width) **0%-ra** (vagy nagyon kicsire) kell állítani, hogy az oszlopok összeérjenek!

### Helyzetmutatók becslése (A 3 legfontosabb)

Mielőtt számolsz, **ellenőrizd az osztályközök hosszát ($h$)!** Ha egyenlőek, mehet a sima számolás.

1.  **Módusz ($Mo$):** A leggyakoribb érték. Keresd meg a legnagyobb gyakoriságú sort ($f_{max}$).
    *   Excelben képlettel: $= Alsó\_határ + h \cdot \frac{f_{max} - f_{elozo}}{(f_{max} - f_{elozo}) + (f_{max} - f_{kovetkezo})}$
2.  **Medián ($Me$):** Hol érjük el az 50%-ot?
    *   **Trükk:** A tanár szerint a legegyszerűbb, ha csinálsz egy **Kumulált Relatív Gyakoriság ($g'_i$)** oszlopot (százalékokban). Keresd meg azt a sort, ahol átlépjük az 50%-ot.
    *   Képlet (interpoláció): $= Alsó\_határ + h \cdot \frac{50\% - g'_{elozo}}{g_{sajat}}$
3.  **Átlag ($\bar{Y}$):**
    *   Csinálj egy **Osztályközép ($Y_i$)** oszlopot: `=(Alsó+Felső)/2`.
    *   Számold ki az átlagot a `SZORZATÖSSZEG` függvénnyel: `=SZORZATÖSSZEG(Gyakoriság_oszlop; Osztályközép_oszlop) / SZUM(Gyakoriság_oszlop)`. (Sokkal gyorsabb, mint oszlopokat szorozgatni!)

> [!done] 💡 Érthető magyarázat a Kvantilisek (Pl. $D_1, D_9, Q_1$) becsléséhez
> A kvantiliseket pontosan ugyanazzal a "hegymászós" logikával (interpolációval) számoljuk, mint a mediánt, csak más "magasságot" keresünk!
> *   $Q_1$ (Alsó kvartilis): Hol érjük el a **25%**-ot? Képlet: $= Also\_hatar + h \cdot \frac{25\% - g'_{elozo}}{g_{sajat}}$
> *   $D_9$ (9. decilis): Hol érjük el a **90%**-ot? Képlet: $= Alsó\_határ + h \cdot \frac{90\% - g'_{elozo}}{g_{sajat}}$
> *   **Tipp:** Excelben az első (pl. $D_1$ azaz 10%) képletét dollározd fel úgy, hogy a sorokat ne fixáld, csak az oszlopokat, és **húzd lefelé**! Utána a cellában manuálisan be tudod húzni a színes kereteket a megfelelő sorba (pl. ahol a 75% van), és csak a $10\%$-ot kell átírnod $75\%$-ra a képletben!

### Alakmutatók: Lapultság
*   **$\alpha_4$ (Negyedik momentum alapján):** Ha negatív, akkor az eloszlás **lapultabb**, mint a normális eloszlás. (A képlete nagyon hosszú, a vizsgán oda kell figyelni a zárójelekre!).
*   **$K$ mutató:** $K = \frac{IQR}{2 \cdot IDR} = \frac{Q_3 - Q_1}{2(D_9 - D_1)}$. 
    *   Ha $K > 0,263$, akkor **lapult**.
    *   Ha $K < 0,263$, akkor **csúcsos**.
    *   *(Figyeld a logikát: Az $\alpha_4$-nél a kisebb (negatív) jelent lapultabbat, a $K$-nál a nagyobb érték jelent lapultabbat!)*

---

## 4. Feladat: Asszociáció (Kontingenciatábla)

Két minőségi (nominális) ismérv kapcsolatát vizsgáljuk. (Pl. Állampolgárság és Tartózkodási hely).

> [!definition] Asszociációs mutatók
> *   **Elméleti gyakoriság ($f_{ij}^*$):** Függetlenség feltételezése esetén hány darabnak kéne lennie az adott cellában. $f_{ij}^* = \frac{f_{i.} \cdot f_{.j}}{N}$ (Sorösszeg $\cdot$ Oszlopösszeg / Összesen).
> *   **$\chi^2$ (Khi-négyzet):** A tényleges és az elméleti gyakoriságok négyzetes eltérése.
> *   **Cramér-együttható ($C$):** $C = \sqrt{\frac{\chi^2}{N \cdot \min(r-1, c-1)}}$. A kapcsolat szorosságát méri 0 és 1 között.

### Excel megvalósítás
1.  **Összesen sor/oszlop:** Ha nincs kitöltve a táblázatban, első dolgod a `SZUM` függvénnyel kiszámolni a sorok és oszlopok összesenjét, és a legalsó sarokba az $N$-et (fősokaság).
2.  **Függetlenség ($f_{ij}^*$) számítása:**
    *   Létrehozol egy ugyanolyan üres táblázatot.
    *   A bal felső cellába beírod: `= $Sorösszeg \cdot Oszlopösszeg\$ / $N\$`.
    *   **Trükk a dollározáshoz:** A Sorösszeg oszlopát fixáld (pl. `$K5`), az Oszlopösszeg sorát fixáld (pl. `C$10`), az $N$-et pedig teljesen fixáld (pl. `$K$10`). Ezt utána jobbra és lefelé is húzhatod, egy mozdulattal kész a teljes $f^*$ táblázat!
3.  **$\chi^2$ kiszámítása:**
    *   `=SZUM( (Tényleges_tábla - Elméleti_tábla)^2 / Elméleti_tábla )` 
    *   *(Tömbképlettel, vagy ha az új Excelt használod, simán kiadja).*
    *   Ha nagyon nem jön ki a $\chi^2$, valószínűleg a zárójelezés a rossz! Ha nincs időd megkeresni a hibát, **írj be egy számot**, és a Cramér mutatót számold ki arra hivatkozva a részpontért!
4.  **Cramér ($C$) kiszámítása:**
    *   Gyök alatt: $\chi^2$ osztva ($N$ szorozva a (sorok száma - 1) és (oszlopok száma - 1) közül a kisebbikkel).
    *   Pl. 5 sor és 8 oszlop esetén a kisebbik az $(5-1)=4$.
    *   Képlet: `=GYÖK( Chi2 / (N * 4) )`

### Értelmezés
*   Mikor független? Ha $C = 0$.
*   Mikor függvényszerű? Ha minden sorban és oszlopban maximum egy nem nulla elem van (azaz $C = 1$). A feladatban: ha függvényszerű lenne a kapcsolat, a cellában 0 állna, vagy a teljes oszlopösszeg/sorösszeg.
*   **Cramér ($C$) értékelése:**
    *   $C < 0,3$: Mérhető, de **gyenge** kapcsolat.
    *   $0,3 \le C < 0,7$: **Közepesen szoros** kapcsolat.
    *   $C \ge 0,7$: **Szoros** kapcsolat.

---

## 5. Feladat: Koncentráció

Azt vizsgálja, hogy egy értékösszeg (pl. lakosság, vagyon) mennyire egyenlőtlenül oszlik el az egységek (pl. országok, cégek) között.

> [!definition] A Koncentráció mérése
> *   **$Z_i$:** Relatív értékösszeg (Az adott elem értéke / Összes érték).
> *   **Herfindahl-index ($HI$):** $HI = \sum Z_i^2$. 
>     *   Koncentráció hiánya (Alsó határ): $1/N$ (Ahol $N$ az elemek száma, pl. 45 ország).
>     *   Teljes koncentráció (Felső határ): $1$.
> *   **Lorenz-görbe:** Kumulált relatív gyakoriságokat ($g'_i$) és kumulált relatív értékösszegeket ($Z'_i$) ábrázol. 

### Excel megvalósítás és trükkök
*   **Herfindahl-index:** Számold ki a $Z_i$ értékeket (`Adat / Összesen`), majd a négyzetük összegét (`=SZORZATÖSSZEG(Z_i_oszlop; Z_i_oszlop)`).
*   **Rendezés!** A koncentráció számításához, különösen a Lorenz-görbéhez az adatokat **SZIGORÚAN NÖVEKVŐ** sorrendbe kell rendezni! (A gyakorló feladatban már így volt, de erre vizsgán figyelni kell! Ha nem rendezed, a Lorenz-görbéd úgy fog kinézni, mint egy EKG-görbe, ahelyett, hogy szépen az alsó háromszögben ívelne).
*   **Kumulált értékek a Lorenz-görbéhez:**
    *   $g_i = 1/N$ (minden sornak egyforma a súlya). A kumulált $g'_i$ az előző + $1/N$.
    *   A kumulált $Z'_i$ az előző $Z'_i$ + aktuális $Z_i$.
    *   *(Figyelem: A Lorenz görbe mindig a $(0;0)$ pontból indul, ehhez be kell szúrni egy 0% - 0% sort az adatok elé!)*
*   **Diagram készítés:**
    *   Jelöld ki a $g'_i$ és $Z'_i$ oszlopokat (fejléc nélkül, a 0-tól indulva).
    *   Beszúrás -> Pont (Scatter) diagram -> Sima vonalakkal összekötve.
    *   Ha az Excel megcseréli az X és Y tengelyt, akkor a diagramon Jobb klikk -> Adatok kijelölése -> Szerkesztés, és cseréld meg az X és Y tartományokat.
    *   **Tipp:** A diagram tengelyeinek maximumát állítsd be fixen 1-re (vagy 100%-ra), hogy normális négyzet alakú legyen!

> [!example] A Lorenz-görbe pontjának értelmezése
> A feladatban Magyarország a $g'_i = 64,4\%$ és $Z'_i = 14,7\%$ ponton volt.
> *Helyes értelmezés:* "A népesség szerint sorba rendezett országok **64,4%-a kisebb vagy azonos lakosságszámú**, mint Magyarország. Ezek az országok együttesen Európa (vizsgált 45 országának) **összlakosságából 14,7%-kal** részesednek."

---

## 📝 Vizsgaszerű Tesztkérdések

Ezekkel ellenőrizheted a tudásod a ZH előtt! (A nyilakra kattintva lenyílik a válasz).

> [!faq]- Ha az A országban $HI = 0,15$, a B országban $HI = 0,32$, melyik országban nagyobb a koncentráció?
> A **B országban**. A Herfindahl-index ($HI$) értéke $1/N$ és $1$ között mozog. Minél nagyobb az érték (minél közelebb van az 1-hez), annál nagyobb, szorosabb a koncentráció az adott sokaságban.

> [!faq]- Két százalékos érték (pl. $45\%$ és $40\%$) különbségét hogyan kell helyesen megfogalmazni statisztikai elemzésben?
> A helyes válasz: **5 százalékpont**. (Nem "5 százalék"!).

> [!faq]- Egy dobozábrán (Boxplot) az alsó bajusz vége a 15-ös értéknél van, míg az alsó kerítés kiszámolt értéke 10. Mi az alsó kerítés a diagram alapján?
> Az alsó kerítés **10**. A kerítés láthatatlan vonal, az értékét a $Q_1 - 1,5 \cdot IQR$ képlet határozza meg, függetlenül attól, hogy meddig ér a bajusz.

> [!faq]- Számítás során nem tudod kihozni a $\chi^2$ (Khi-négyzet) értékét a képlet hiba miatt. Mi a teendő a ZH-n?
> Írj be egy tetszőleges számot (pl. 250) a $\chi^2$ helyére, és azzal a számmal számold ki a Cramér-együtthatót ($C$). Így a Cramér képlet felírásáért és kiszámításáért, valamint az ahhoz fűzött értelmezésért megkapod a maximális részpontokat!

> [!faq]- Ha az $\alpha_4$ mutató értéke -0,64 és a $K$ mutató értéke 0,275, mit mondhatunk az eloszlás alakjáról?
> Mindkét mutató azt jelzi, hogy az eloszlás a normális eloszláshoz képest **lapultabb**. (Az $\alpha_4$ negatív, a $K$ pedig nagyobb, mint a normális eloszlás 0,263-as referenciaértéke).
