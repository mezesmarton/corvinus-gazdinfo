---
title: Mennyiségi sorok és Statisztikai mutatók
course: Statisztika I
tags: [statisztika, mennyisegi_sorok, mutatok, kozepertekek, szoras, aszimmetria, dobozabra]
---

> [!abstract] TL;DR
> A leíró statisztika célja a sokaság nagy mennyiségű adatának tömör, számszerű jellemzése. A jegyzet bemutatja az adatok táblázatos rendszerezését (**gyakorisági** és **értékösszegsorok**), a sokaság centrumának meghatározását (**helyzeti** és **számított középértékek**), a belső ingadozás mérését (**szóródási mutatók**), valamint a gyakorisági görbe formájának számszerűsítését (**alakmutatók**).

### 1. A Sokaság Rendszerezése: Gyakorisági sorok

A mennyiségi ismérvek (számszerűsíthető adatok) feldolgozásának első lépése a rangsorba állítás, majd az adatok csoportosítása.

> [!definition] Gyakorisági sor
> Olyan eloszlás, amely bemutatja a sokaság egyedeinek megoszlását az ismérv lehetséges értékei vagy kategóriái (osztályközei) szerint.

Kevés ismérvváltozat esetén az értékeket közvetlenül soroljuk fel:
* **Abszolút gyakoriság** ($f_i$): Az adott ismérvváltozatot felvevő egyedek tényleges száma (összegük $N$).
* **Relatív gyakoriság** ($g_i$): A csoport aránya a teljes sokasághoz képest ($g_i = f_i / N$).
* **Kumulált gyakoriságok** ($f'_i$, $g'_i$): Folyamatosan összeadott (felhalmozott) gyakoriságok, amelyek megmutatják, hogy az adott értékig bezárólag hány elem található a sokaságban.

#### Osztályközös gyakorisági sor
Folytonos ismérvek vagy túl sok eltérő érték esetén az adatokat **osztályközökbe** (egymást át nem fedő sávokba) soroljuk.
* **Osztályközép** ($Y_i$): Az osztályköz alsó és felső határának átlaga, ez reprezentálja a sávot.
* **Sturges-szabály**: Az osztályközök ideális számának ($k$) meghatározására szolgál: a legkisebb olyan $k$ egész szám, amelyre igaz, hogy $2^k \ge N$.
* Eltérő osztályközhosszúságok esetén a grafikus ábrázolásnál és az elemzésnél a **gyakorisági sűrűséget** ($f_i / h_i$) kell használni.

---

### 2. Értékösszegsorok

Míg a gyakorisági sor az egyedek számát mutatja, az értékösszegsor azt jelzi, hogy ezek az egyedek együttesen mekkora volument képviselnek.

> [!definition] Értékösszeg ($S_i$)
> Az adott osztályközbe tartozó egyedi ismérvértékek összege. Gyakorisági sorból **becsült értékösszeg** számítható az osztályközép és a gyakoriság szorzataként: $	ilde{S}_i = f_i \cdot Y_i$.

Ennek is létezik **relatív** ($Z_i$) és **kumulált** ($S'_i$, $Z'_i$) formája. A kumulált relatív gyakoriság és a kumulált relatív értékösszeg összevetésével vizsgálható a sokaság **koncentrációja**.

---

### 3. Helyzetmutatók I.: Kvantilisek

> [!definition] Kvantilis
> A nagyság szerint rendezett (monoton növekvő) sokaságot egyenlő gyakoriságú részekre osztó határérték. 

* **Medián** ($Me$): 2 részre oszt (50% – 50%).
* **Kvartilisek** ($Q_1, Q_2, Q_3$): 4 részre osztanak (negyedelő pontok).
* **Kvintilisek** ($K_1 \dots K_4$): 5 részre osztanak (ötödölő pontok).
* **Decilisek** ($D_1 \dots D_9$): 10 részre osztanak.
* **Percentilisek** ($P_1 \dots P_{99}$): 100 részre osztanak.

> [!note] 💡 Érthető magyarázat
> Ha a fizetésed a felső decilis határán ($D_9$) van, az azt jelenti, hogy az emberek 90%-a kevesebbet keres nálad, és te a legjobban kereső 10%-ba tartozol.

**Számítás egyedi adatok rangsorából:**
A keresett kvantilis sorszáma: $S_{i/k} = rac{i}{k} \cdot (N+1)$. Ha nem egész szám, a két szomszédos érték között lineárisan interpolálunk.

---

### 4. Helyzetmutatók II.: Középértékek

A középértékek egyetlen számmal jellemzik az eloszlás "tipikus" helyzetét. 

#### Helyzeti középértékek (Robusztusak, nem érzékenyek a kiugró adatokra)
* **Módusz** ($Mo$): A leggyakrabban előforduló érték, vagy a gyakorisági görbe maximumhelye. Minimalizálja a helyettesítéskor elkövetett hibák számát.
* **Medián** ($Me$): A rangsor középső eleme. Minimalizálja az **abszolút eltérések** összegét ($\sum |Y_i - A| = \min \implies A = Me$).

#### Számított középértékek (Minden adatot felhasználnak, érzékenyek a kiugró adatokra)
* **Számtani átlag** ($ar{Y}$): Az adatok összege osztva a darabszámmal. Minimalizálja a **négyzetes eltérések** összegét ($\sum (Y_i - A)^2 = \min \implies A = ar{Y}$).
* **Mértani átlag** ($ar{Y}_g$): Az értékek szorzatának $N$-edik gyöke (pl. növekedési ütemekhez).
* **Harmonikus átlag** ($ar{Y}_h$): A reciprok értékek átlagának reciproka (pl. részviszonyszámok, sebesség).
* **Négyzetes átlag** ($ar{Y}_q$): Az értékek négyzetei átlagának gyöke (pl. szórás számításához).

---

### 5. Szóródási Mutatók

A szóródás a megfigyelt értékek különbözőségét, az átlagtól vagy egymástól való ingadozását méri.

* **(Teljes) terjedelem** ($R$): A legnagyobb és a legkisebb érték különbsége ($Y_{max} - Y_{min}$).
* **Interkvartilis terjedelem** ($IQR$): A felső és alsó kvartilis távolsága ($Q_3 - Q_1$). A sokaság középső 50%-ának terjedelme (kiszűri az outliereket).
* **Szórás** ($\sigma$): Az átlagtól vett eltérések négyzetes átlaga.
  $$\sigma = \sqrt{rac{\sum (Y_i - ar{Y})^2}{N}}$$
* **Variancia**: A szórás négyzete ($\sigma^2$).
* **Relatív szórás** ($V$): A szórás és az átlag hányadosa ($V = \sigma / ar{Y}$). Dimenzió nélküli (általában százalékos) szám, ami eltérő mértékegységű adatsorok összehasonlítására alkalmas.

> [!note] 💡 Érthető magyarázat a lineáris transzformációhoz
> Ha minden dolgozó kap egységesen 50 000 Ft fizetésemelést, az átlag megnő 50 000 Ft-tal, de a **szórás változatlan marad**, mert a dolgozók közötti vagyoni távolság nem nőtt. Ha viszont mindenki 10%-os emelést kap, akkor a különbségek is tágulnak, így a szórás is megnő 10%-kal! ($\sigma_{uj} = |b| \cdot \sigma$)

---

### 6. Alakmutatók (Aszimmetria és Csúcsosság)

Az alakmutatók a görbét egy azonos szórású és átlagú **normális eloszláshoz** viszonyítják.

#### Aszimmetria (Ferdeség)
A három fő helyzetmutató sorrendje egyértelműen meghatározza az eloszlás alakját:
1. **Szimmetrikus**: $ar{Y} = Me = Mo$.
2. **Balra elnyúló (negatív/jobbra ferde)**: $ar{Y} < Me < Mo$. A hosszú farok a kisebb értékek felé nyúlik.
3. **Jobbra elnyúló (pozitív/balra ferde)**: $Mo < Me < ar{Y}$. A hosszú farok a nagyobb értékek felé nyúlik (pl. jövedelmek eloszlása).

*Pearson-mutató*: $P = rac{3(ar{Y} - Me)}{\sigma}$

#### Csúcsosság (Kurtosis)
A görbe relatív emelkedését, hegyességét méri a normális eloszláshoz képest.
* Ha pozitív ($lpha_4 > 0$): A normálisnál **csúcsosabb**.
* Ha negatív ($lpha_4 < 0$): A normálisnál **lapultabb**.
* Ha nulla ($lpha_4 = 0$): Normális csúcsosságú.

---

### 7. Mennyiségi Sorok Ábrázolása

* **Hisztogram**: Folytonos adatok oszlopdiagramja hézagok nélkül. *Kritikus szabály:* Az oszlopok **területe** arányos a gyakorisággal! Ha az osztályközök hossza eltérő, a magasság a gyakorisági sűrűség ($f_i / h_i$) kell legyen.
* **Dobozábra (Boxplot)**:
  * *5-pontos*: Minimum, $Q_1$, Medián, $Q_3$, Maximum értékeket köti össze. A doboz hossza maga az $IQR$.
  * *7-pontos (Tukey-féle)*: Kiszámítja az alsó ($Q_1 - 1{,}5 \cdot IQR$) és felső kerítést ($Q_3 + 1{,}5 \cdot IQR$). A kerítésen kívül eső adatok extrém **kilógó (outlier)** értékek, ezeket külön pontként ábrázolja, és a doboz "bajszát" csak a kerítésen belüli szélsőértékekig húzza ki.

---

### Aktív Felidézés és Önellenőrző Kérdések

> [!faq]- Mi történik egy adatsor átlagával és szórásával, ha minden értéket megszorzunk 2-vel, majd kivonunk belőlük 5-öt?
> A lineáris transzformáció szabályai alapján ($L_i = -5 + 2 \cdot Y_i$): Az új átlag az eredeti átlag kétszerese mínusz 5 lesz. A szórást viszont a konstans eltolás (-5) nem befolyásolja, csak a szorzótényező abszolút értéke, így az új szórás pontosan az eredeti szórás kétszerese lesz ($\sigma_{uj} = 2 \cdot \sigma$).

> [!faq]- Egy cégnél az átlagfizetés 350 ezer Ft, a medián 310 ezer Ft, a módusz 280 ezer Ft. Milyen az eloszlás alakja?
> Mivel $Mo < Me < ar{Y}$ ($280 < 310 < 350$), az eloszlás **jobbra elnyúló** (pozitív aszimmetriájú). A cég dolgozóinak többsége kevesebbet keres, de néhány magas fizetésű vezető erősen felhúzza az átlagot.

> [!faq]- Miért mondjuk, hogy a medián és a módusz robusztus mutatók a számtani átlaghoz képest?
> Azért, mert a medián és a módusz értékét nem torzítják el a sokaság szélein megjelenő extrém (kiugróan nagy vagy kicsi) adatok. A számtani átlag kiszámításába viszont minden érték belekerül, így az outlierek drasztikusan elhúzhatják a centrumtól.

> [!faq]- Mikor elengedhetetlen a relatív szórás ($V$) használata a sima szórás ($\sigma$) helyett?
> Amikor eltérő mértékegységű (pl. testsúly kg-ban és fizetés forintban), vagy azonos mértékegységű, de nagyságrendileg jelentősen különböző (pl. magyar és dán árszintek) sokaságok ingadozását, belső változatosságát szeretnénk közvetlenül összehasonlítani.

> [!faq]- Hogyan számolod ki a 7-pontos dobozábránál a belső kerítéseket, és mire valók?
> Elsőként kiszámítjuk az interkvartilis terjedelmet ($IQR = Q_3 - Q_1$). Az alsó kerítés a $Q_1 - 1{,}5 \cdot IQR$, a felső kerítés a $Q_3 + 1{,}5 \cdot IQR$. Ezek a határok arra szolgálnak, hogy az ezen kívül eső értékeket statisztikailag **kiugró (outlier)** adatnak minősítsük, és a diagramon különálló pontként ábrázoljuk.
