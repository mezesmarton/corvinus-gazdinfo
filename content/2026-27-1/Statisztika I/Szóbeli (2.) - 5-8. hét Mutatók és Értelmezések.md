---
title: Szóbeli (2.) - 5-8. hét Mutatók és Értelmezések
course: Statisztika I.
tags:
  - statisztika
  - szóbeli
  - koncentráció
  - asszociáció
  - korreláció
  - regresszió
---

> [!abstract] Rövid összefoglaló
> Ez a jegyzet a Statisztika I. tárgy 5-8. hetének (Koncentráció, Asszociáció, Rész-/összetett viszonyszámok, Vegyes kapcsolat, Korreláció és Regresszió) legfontosabb mutatóit, azok képleteit és gyakorlati értelmezését foglalja össze. Kifejezetten a szóbeli vizsgára fókuszál, kiemelve a statisztikai összefüggéseket és a leggyakoribb buktatókat, hogy magabiztosan tudd alkalmazni a józan paraszti ész logikáját.

---

## 5. Hét: Koncentráció (Egyenlőtlenség mérése)

A koncentráció azt vizsgálja, hogy egy adott értékösszeg (pl. vagyon, bevétel, földterület) mennyire egyenlőtlenül oszlik el a sokaság egységei (pl. lakosság, cégek) között.

> [!definition] A Koncentráció fajtái
> *   **Abszolút koncentráció:** Az értékösszeg jelentős része azért összpontosul kevés kézben, mert **eleve kevés a szereplő** a piacon (pl. telekommunikációs szektor, autógyártás).
> *   **Relatív koncentráció:** Sok szereplő van, de az eloszlás **nagyon egyenlőtlen** (pl. a globális vagyoneloszlás, ahol az emberek 1%-áé a vagyon közel fele).

### A Koncentráció Vizuális Eszköze: A Lorenz-görbe

> [!danger] Aranyszabály a Lorenz-görbéhez!
> A Lorenz-görbe megrajzolásához vagy értelmezéséhez az adatokat **szigorúan növekvő sorrendbe** kell rendezni az ismérvérték szerint (a legkisebbtől a legnagyobbig)!

A görbe az X-tengelyen a kumulált relatív gyakoriságot ($g'_i$), az Y-tengelyen a kumulált relatív értékösszeget ($Z'_i$) ábrázolja. 

> [!done] 💡 Érthető magyarázat az Átlagpontra
> A Lorenz-görbén az **Átlagpont** mutatja meg, hol tartunk azoknál a szereplőknél, akiknek pont átlagos értékük (pl. vagyonuk) van. Mindenki, aki a görbén ez előtt a pont előtt van, az átlag alatti. *Értelmezés:* "A sokaság $g'_{átlag}$ százaléka átlag alatti értékkel rendelkezik, és ők együttesen a teljes értékösszeg $Z'_{átlag}$ százalékát birtokolják."

### A Koncentráció Mutatószámai

| Mutató neve                     | Képlet                                                      | Értelmezés és Szélsőértékek                                                                                                                                                                                                  |
| :------------------------------ | :---------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Herfindahl-index ($HI$)**     | $$HI = \sum_{i=1}^N Z_i^2$$                                 | Az abszolút koncentrációt (piaci uralmat) méri. A részesedéseket ($Z_i$) négyzetre emeljük, hogy a nagyokat jobban "büntessük".<br>**Min:** $1/N$ (Tökéletes egyenlőség).<br>**Max:** $1$ (Monopólium, teljes koncentráció). |
| **Robin Hood-index ($H$)**      | $$H = g'_{átlag} - Z'_{átlag}$$                             | Megmutatja, hogy a teljes értékösszeg **hány százalékát kellene átcsoportosítani** az átlag felettiektől az átlag alattiaknak, hogy a koncentráció (egyenlőtlenség) megszűnjön.                                              |
| **Gini-együttható ($L$ / $G$)** | A Lorenz-görbe alatti "has" (koncentrációs terület) aránya. | 0 - 0,25: alacsony koncentráció<br>0,25 – 0,35: mérsékelt koncentráció<br>0,35 – 0,4: közepes koncentráció<br>0,4 – 0,5: magas koncentráció<br>0,5 – 1: extrém koncentráció                                                  |

---

## 6. Hét: Asszociációs kapcsolat és Viszonyszámok

### 1. Asszociáció (Minőségi ismérvek kapcsolata)

Két kategória-jellegű (nominális) szöveges adat kapcsolatát vizsgáljuk (pl. *Állampolgárság* és *Foglalkoztatási státusz*). Eszköze a **kontingenciatábla**.

> [!definition] Függetlenség és Elméleti gyakoriság ($f_{ij}^*$)
> Két ismérv akkor független, ha az egyik ismerete nem ad többletinformációt a másikról. A függetlenség feltételezése melletti elméleti gyakoriság azt mutatja meg, mennyi lenne az érték az adott cellában a puszta matematikai véletlen alapján.
> $$f_{ij}^* = \frac{f_{i.} \cdot f_{.j}}{N} \quad \text{(Sorösszeg} \cdot \text{Oszlopösszeg / Összesen)}$$

> [!warning] A $\chi^2$ (Khi-négyzet) probléma
> A $\chi^2 = \sum \frac{(f_{ij} - f_{ij}^*)^2}{f_{ij}^*}$ azt méri, hogy a valóság mennyire tér el a függetlenségtől (az elméleti értéktől). **Baj vele:** Önmagában értelmezhetetlen a nagysága, mert függ az esetszámtól ($N$) és a táblázat méretétől.

Ennek orvoslására használjuk a **Cramer-együtthatót ($C$)**:

$$C = \sqrt{\frac{\chi^2}{N \cdot \min(r-1, c-1)}}$$

> [!tip] A Cramer-skála (Szóbeli kötelező!)
> A $C$ mutató 0 és 1 között mozog. Százalékosan **NEM** értelmezhető!
> *   $C = 0$: Függetlenség.
> *   $C < 0,3$: Mérhető, de **gyenge** kapcsolat.
> *   $0,3 \le C < 0,7$: **Közepesen szoros** kapcsolat.
> *   $C \ge 0,7$: **Szoros** kapcsolat.
> *   $C = 1$: **Függvényszerű** kapcsolat (minden sorban/oszlopban max 1 nem nulla érték van).

### 2. Összetett viszonyszámok: Melyik átlagot használjam?

> [!danger] A leggyakoribb vizsgahiba!
> Ha egy feladatban részátlagokból (pl. megyei átlagfizetésekből) kell országos átlagot (összetett viszonyszámot, $\overline{V}$) számolni, sosem vonhatsz sima átlagot! Súlyozni kell, de nem mindegy, mivel!

Írd fel a viszonyszám képletét (pl. $V = \frac{\text{Összbér}}{\text{Létszám}}$). A megadott súlyok alapján dönts:

| Megadott Súly | Használandó Átlag | Magyarázat |
| :--- | :--- | :--- |
| A **NEVEZŐ** adata (pl. Létszám, $B_j$) | **Súlyozott Számtani Átlag** | $$\overline{V} = \frac{\sum B_j V_j}{\sum B_j}$$ |
| A **SZÁMLÁLÓ** adata (pl. Összbér, $A_j$) | **Súlyozott Harmonikus Átlag** | $$\overline{V} = \frac{\sum A_j}{\sum \frac{A_j}{V_j}}$$ |

---

## 7. Hét: Vegyes kapcsolat és Varianciafelbontás

Egy minőségi (szöveges, pl. *Beosztás*) és egy mennyiségi (számos, pl. *Fizetés*) ismérv kapcsolatát vizsgáljuk.

> [!done] 💡 Érthető magyarázat a Szórásfelbontásra
> Miért tér el a te fizetésed a cégátlagtól? Két okból:
> 1. Mert a te csoportod (pl. fizikaiak) átlaga eleve eltér a cégátlagtól. **(Külső ok $\rightarrow$ Külső szórás, $K$)**
> 2. Mert a te csoportodon belül is van ingadozás, te is eltérsz a többi fizikaitól. **(Belső ok $\rightarrow$ Belső szórás, $B$)**

> [!danger] A Variancia-szabály (Vigyázat, beugratós!)
> A teljes variancia egyenlő a belső és a külső variancia összegével:
> $$\sigma^2 = \sigma_B^2 + \sigma_K^2$$
> **FIGYELEM:** Ez az egyenlőség szigorúan csak a varianciákra (négyzetekre) igaz! A sima szórásokra ($\sigma = \sigma_B + \sigma_K$) **SOHA NEM IGAZ!**

### A kapcsolat szorosságát mérő mutatók

A vegyes kapcsolat mérése a **PRE-elven** (Proportional Reduction of Errors - Relatív hibacsökkenés) alapul. Azt mutatja meg, hogy ha megismerem az X (csoport) ismérvet, mennyivel csökken a hibám az Y becslésénél.

*   **Variancia-hányados ($H^2$):** $H^2 = \frac{\sigma_K^2}{\sigma^2}$
    *   *Értelmezés:* A $H^2$ **százalékosan mutatja meg**, hogy az Y (pl. fizetés) szóródását hány százalékban magyarázza az X (pl. beosztás).
*   **Szóráshányados ($H$):** $H = \sqrt{H^2}$
    *   *Értelmezés:* Nem százalékos mutató! A kapcsolat szorosságát méri 0 és 1 közötti skálán (Ugyanaz a 0,3 és 0,7-es skála, mint a Cramer $C$-nél!).

---

## 8. Hét: Korreláció és Regresszió

Két mennyiségi (számszerű) ismérv (pl. *Tanulási idő* és *ZH pontszám*) kapcsolatát vizsgáljuk egy XY diagramon (pontfelhő).

> [!definition] Alapfogalmak
> *   **Korreláció:** A kapcsolat (együttmozgás) irányát és szorosságát méri.
> *   **Regresszió:** Modellt (függvényt) készít a kapcsolatra, amivel a jövőbeli Y értékek megbecsülhetők (jósolhatók) az X értékek ismeretében.

### 1. Korrelációs mutatók

| Mutató neve | Képlet/Jele | Értelmezés és skála |
| :--- | :--- | :--- |
| **Kovariancia** | $C(X,Y)$ | Csak az **irányt** mutatja meg. Ha $>0$ egyirányú, ha $<0$ ellentétes irányú a kapcsolat. A nagysága nem értelmezhető (függ a mértékegységtől). |
| **Pearson-féle korrelációs együttható** | $$r = \frac{C(X,Y)}{\sigma_X \sigma_Y}$$ | **-1 és 1 között mozog.** Az előjele az irányt, az abszolútértéke a szorosságot mutatja. (Skála: 0,3-ig gyenge, 0,7-ig közepes, 0,7 felett szoros). |
| **Spearman-féle rangkorreláció** | $\rho$ (Ró) | Akkor használjuk, ha nincsenek konkrét számok, csak **sorrendi (rang) helyezések** (pl. tenisz világranglista helyezés vs. életkori sorrend). Értelmezése azonos az $r$-rel. |

### 2. A Lineáris Regresszió ($\hat{Y} = \beta_0 + \beta_1 X$)

> [!tip] Vizsgakérdés: A paraméterek értelmezése!
> A szóbelin gyakran megkérik, hogy mondd el, mit jelent a $\beta_0$ és a $\beta_1$ a valóságban.
> *   **$\beta_1$ (Meredekség):** Ha az X (magyarázó változó) értékét **1 egységgel növeljük**, az Y (eredményváltozó) értéke **átlagosan $\beta_1$-gyel változik meg** (nő vagy csökken).
> *   **$\beta_0$ (Tengelymetszet):** Megmutatja az Y becsült átlagos értékét olyankor, amikor az **X értéke 0**. (Néha csak illeszkedést segítő paraméter, ha az $X=0$-nak a valóságban nincs logikus értelme).

### 3. Az Illeszkedés Jósága

Hiába húztunk egy szép trendvonalat, tudnunk kell, hogy a pontok mennyire tapadnak hozzá.

*   **Determinációs együttható ($R^2$):** A Pearson $r$ négyzete ($R^2 = r^2$). Szintén PRE-elvű mutató.
*   *Értelmezése:* Százalékosan mutatja meg, hogy az X változó ismerete **hány százalékkal csökkenti a bizonytalanságot** az Y változó becslésekor. (Vagy úgy is mondhatjuk: X változó az Y varianciájának hány százalékát magyarázza meg).

> [!cite] Anscombe-kvartett (Elméleti kérdés)
> *Kérdés:* "Miért kell mindig felrajzolni a pontdiagramot, miért nem elég csak a mutatókat ($r, R^2, \beta_1$) kiszámolni?"
> *Válasz:* Mert az Anscombe-kvartett bizonyítja, hogy létezhetnek teljesen más alakzatot formáló (pl. U-alakú, vagy egyetlen extrém outlier-t tartalmazó) adathalmazok, amelyeknek az átlaga, szórása és korrelációs együtthatója hajszálpontosan megegyezik. Grafikus ábrázolás nélkül a puszta számok félrevezetőek lehetnek!