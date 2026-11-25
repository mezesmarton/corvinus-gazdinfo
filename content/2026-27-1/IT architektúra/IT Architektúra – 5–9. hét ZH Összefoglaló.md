---
title: IT Architektúra – 5–9. hét ZH Összefoglaló
course: IT Architektúra
tags:
  - it-architektura
  - zh-felkeszules
  - halozatok
  - linux
  - git
  - docker
  - cicd
  - azure
---

> [!abstract] Rövid összefoglaló
> Ez a jegyzet az IT Architektúra tantárgy 5–9. heti tananyagát és a minta ZH legfontosabb buktatóit foglalja össze. Áttekinti a hálózati protokollokat és a Windows/Linux jogosultságokat, a Linux rendszerműködést és parancssori diagnosztikát, az elosztott Git verziókezelést, a Docker konténerizációt, valamint a CI/CD és az Azure felhős üzemeltetés (OIDC, ACR, Container Apps) kulcsfogalmait.

---

## 1. Hálózati protokollok és Windows jogosultságok

A hálózati szolgáltatások alapja, hogy minden tipikus feladatnak megvan a maga szabványos protokollja.

| Szolgáltatás / Feladat | Protokoll | Rövid szerepe |
| :--- | :--- | :--- |
| **Titkosított webes elérés** | `HTTPS` | HTTP forgalom TLS/SSL titkosítással (alapértelmezett port: `443`) |
| **Windows hálózati fájlmegosztás** | `SMB` | Fájlok és nyomtatók megosztása helyi hálózaton |
| **Automatikus IP-konfiguráció** | `DHCP` | IP-cím, alhálózati maszk, átjáró és DNS-szervercím dinamikus kiosztása |
| **Névfeloldás** | `DNS` | Tartománynevek (pl. `szerver.local`) IP-címre fordítása |

> [!warning] DHCP vs. DNS – Gyakori ZH-csapda!
> A **DHCP** kioszthatja a kliensnek a **DNS-szerver IP-címét** is, de a két szolgáltatás egymástól függetlenül működik:
> - A működő DHCP **nem bizonyítja**, hogy a DNS névfeloldás is helyes.
> - A DHCP **nem hoz létre automatikusan** minden szükséges DNS-rekordot. Ha egy kliens kap IP-t, de egy belső szerver nevét nem tudja feloldani, a hiba a DNS-oldalon (rekord hiánya, rossz DNS-cím) keresendő.

### SMB-megosztás és NTFS-jogosultságok együttműködése

> [!danger] Tényleges jogosultság hálózati elérésnél
> Ha egy felhasználó **hálózaton keresztül** ér el egy Windows-megosztást, a rendszer mindkét réteget ellenőrzi, és a **szigorúbb (korlátozóbb) jogosultság** érvényesül:
> $$J_{tenyleges} = J_{SMB} \cap J_{NTFS}$$
> - **Példa:** Ha az SMB-megosztás joga *Olvasás*, az NTFS-jogosultság pedig *Módosítás*, akkor a tényleges jogosultság hálózaton keresztül: **Csak olvasás**.
> - **Helyi elérésnél** (közvetlenül a gépen) az SMB-réteg nem játszik szerepet, kizárólag az NTFS érvényesül.

> [!done] 💡 Érthető magyarázat
> Képzeld el a két jogosultságot két egymás utáni biztonsági kapuként! Hiába ad az iroda ajtaja (NTFS) engedélyt arra, hogy átrendezd a szobát (Módosítás), ha már a portán (SMB) csak látogatói belépőt kaptál (Olvasás) – így végül csak nézelődhetsz.

---

## 2. Linux architektúra, jogosultságok és diagnosztika

> [!definition] Linux vs. Debian vs. Bash
> - **Linux:** Az operációs rendszer magja (**kernel**), amely a hardver és a felhasználói programok között közvetít (folyamat-, memória-, fájlrendszer-, hálózat- és eszközkezelés).
> - **Debian:** Egy teljes **Linux-disztribúció**, amely a Linux kernel köré csomagolja a rendszereszközöket (`systemd`, `Bash`, `apt` csomagkezelő) és az alkalmazásokat.
> - **Bash:** A Linux alapértelmezett parancsértelmezője (**shell**) és szkriptnyelve. Az `SSH` csak a titkosított hálózati csatorna, a terminál csak az ablak – a parancsokat a távoli gépen futó `Bash` értelmezi.

### Rendszerdiagnosztikai parancsok

| Feladat                                 | Parancs                | Mit ellenőriz?                                          |
| :-------------------------------------- | :--------------------- | :------------------------------------------------------ |
| **TCP-port elérhetőségének tesztelése** | `nc -zv <host> <port>` | Ellenőrzi, hogy adott TCP-port nyitott és elérhető-e    |
| **DNS névfeloldás ellenőrzése**         | `nslookup <domain>`    | Lekérdezi a névhez tartozó IP-címet a DNS-szervertől    |
| **SSH szolgáltatás állapota**           | `systemctl status ssh` | Megmutatja, fut-e az `sshd` démon és van-e hiba         |
| **Szabad memória áttekintése**          | `free -h`              | Kiírja a RAM és swap kihasználtságát olvasható formában |
|                                         |                        |                                                         |

### Szövegfeldolgozás, csővezeték és szkriptfuttatás

A Bash-ben a csővezeték (`|`) **nyers szöveget** ad tovább egyik parancstól a másikig (szemben a PowerShell-lel, amely objektumokat továbbít).

> [!example] Tipikus ZH-parancs elemzése
> ```bash
> grep -i error app.log | wc -l
> ```
> - `grep -i error app.log`: kiszűri az `app.log` fájlból azokat a **sorokat**, amelyek kis- és nagybetűtől függetlenül (`-i`) tartalmazzák az `error` szót.
> - `wc -l`: megszámolja a kapott **sorok számát**.
> - **Figyelem:** Nem az `error` szó összes előfordulását számolja meg (ha egy sorban kétszer szerepel, az akkor is csak 1 sor!), és nem az egész fájl sorszámát adja vissza.

> [!danger] Szkriptfuttatás és a "Permission denied" hiba
> Ha egy helyes `report.sh` fájl a `./report.sh` paranccsal `Permission denied` hibát dob:
> 1. **Ok:** Hiányzik a **végrehajtási jogosultság (`x`)** a fájlról. (Megoldás: `chmod +x report.sh`.)
> 2. **Alternatív futtatás:** A `bash report.sh` parancs `x` jog nélkül is lefut, ha van **olvasási (`r`)** jogosultságod a fájlra.
> 3. **Csapda:** A `bash -n report.sh` **nem futtatja** a szkriptet, csak szintaktikai ellenőrzést végez!

### Azure Debian VM – SSH hibaelhárítás

> [!warning] Ha az NSG engedi a TCP 22-t, de mégsem megy az SSH!
> Az Azure Network Security Group (NSG) 22-es portjának megnyitása **önmagában nem garantálja** az SSH működését. Ilyenkor ellenőrizni kell:
> 1. Fut-e maga az `sshd` szolgáltatás a VM-en (`systemctl status ssh`).
> 2. Nem blokkolja-e a VM **saját operációs rendszerének tűzfala** (pl. `ufw` / `iptables`) a kapcsolatot.
> 
> **Fontos:** A `systemctl enable ssh` csak a rendszerindításkori automatikus indulást állítja be, **nem indítja el azonnal** a leállított szolgáltatást (ahhoz `systemctl start ssh` kell).

---

## 3. Verziókezelés Git segítségével

> [!definition] Elosztott verziókezelő rendszer (DVCS – Git)
> A Git egy **elosztott** verziókezelő rendszer: minden fejlesztő saját gépén teljes értékű **helyi repository** található a teljes verziótörténettel. Ennek köszönhetően **hálózati kapcsolat nélkül (offline) is lehet helyi commitokat készíteni** – szemben a centralizált rendszerekkel (pl. SVN).

### A Git munkafolyamat és a Staging Area

| Parancs | Fő hatása |
| :--- | :--- |
| `git add <fajl>` | A módosítások **staging area**-ba (indexbe) helyezése |
| `git commit -m "..."` | A **staging area** pillanatnyi tartalmának rögzítése a helyi repository-ban |
| `git remote add origin <url>` | A távoli repository címének (`origin` néven) beállítása |
| `git push` | A már elkészített helyi commitok feltöltése a távoli repository-ba |
| `git fetch` | Távoli hivatkozások és változások letöltése a munkafájlok **automatikus összevonása nélkül** |
| `git pull` | Távoli változások letöltése és integrálása (`git fetch` + `git merge` / `rebase`) |

> [!danger] A Staging Area buktatója (Minta ZH!)
> Ha módosítasz egy fájlt, kiadod a `git add report.sh` parancsot, majd **ismét módosítod** a fájlt, és ezután újabb `git add` nélkül kiadod a `git commit` parancsot:
> - A commit **kizárólag a korábban stagingbe tett változatot** fogja rögzíteni!
> - A második módosítás a munkakönyvtárban marad (nem kerül bele a commitba).
> - Szintén fontos: a `git push` **soha nem commitol automatikusan** helyi módosításokat.

---

## 4. Konténerizáció és Docker

> [!definition] Konténer vs. Virtuális gép (VM)
> - **Virtuális gép (VM):** Hardveres virtualizáció (hypervisor segítségével), minden VM **saját vendég operációs rendszert és saját kernelt** futtat. Erősebb izoláció, nagyobb erőforrásigény.
> - **Konténer:** Operációs rendszer szintű virtualizáció. A Linux-konténerek **a gazdagép (host) kerneljét használják közösen**, így sokkal könnyebbek és gyorsabban indulnak, de izolációs határuk nem azonos a VM-ével.

### A Docker 4 alappillére

| Összetevő | Szerepe |
| :--- | :--- |
| **Dockerfile** | Szöveges recept, amely lépésről lépésre leírja az image összeállítását (`FROM`, `WORKDIR`, `COPY`, `RUN`, `CMD`) |
| **Image** | Statikus, csak olvasható rétegekből álló sablon, amelyből a konténereket indítjuk |
| **Registry** | Központi tároló image-ek tárolására és terjesztésére (pl. Docker Hub, GHCR, Azure Container Registry) |
| **Volume** | A **konténer életciklusától független** tartós adattárolás (adatbázisokhoz elengedhetetlen) |

> [!cite] A Docker alapelve
> „Registry-ből image-et szerzünk (`docker pull`), image-ből pedig konténert indítunk (`docker run`).”

> [!done] 💡 Érthető magyarázat
> A **Dockerfile** a sütemény receptje, az **Image** a fagyasztott, készre sütött sablon (osztály), a **Konténer** pedig a tányérra tett, élőben futó példány (objektum). Ha törlöd a konténert, a belsejében írt adatok elvesznek – kivéve, ha külső tárhelyet csatoltál hozzá.

### Porttovábbítás és Adatmegőrzés (Perzisztencia)

> [!example] Porttovábbítás értelmezése
> ```bash
> docker run -d -p 8080:80 nginx:stable
> ```
> A `-p` kapcsoló formátuma mindig: `-p hostPort:containerPort`.
> - A fenti parancs a **VM (host) 8080-as portjára** érkező forgalmat továbbítja a **konténer 80-as portjára**.
> - **ZH-figyelmeztetés:** Ez önmagában nem garantálja az internetes elérést, mert az **Azure NSG** külön korlátozhatja a 8080-as portot!
> - A `Dockerfile`-ban szereplő `EXPOSE 80` csak dokumentációs jellegű, nem nyitja meg a portot a hoston.

> [!tip] Hogyan őrizzük meg egy adatbázis-konténer adatait törlés és újralétrehozás után?
> Két helyes megoldás létezik:
> 1. **Docker volume** megfelelő csatolása (Docker által menedzselt tárhely).
> 2. **Bind mount** használata megfelelő hostkönyvtárral (a gazdagép egy konkrét mappájának becsatolása).

---

## 5. CI/CD, GitHub Actions és Azure felhő

> [!definition] CI / Continuous Delivery / Continuous Deployment
> - **CI (Continuous Integration):** Minden `push` / `commit` után automatikus építés (*build*) és tesztelés.
> - **Continuous Delivery (Folyamatos szállítás):** A CI-re épülve automatikusan elkészül a kiadható csomag/image, de az élesítéshez **emberi (manuális) jóváhagyás** szükséges.
> - **Continuous Deployment (Folyamatos üzembe helyezés):** Ha minden teszt sikeres, a rendszer **emberi beavatkozás nélkül, automatikusan élesíti** az alkalmazást.

### Felhős DevOps összetevők (Minta ZH!)

| Összetevő | Szerepe a folyamatban |
| :--- | :--- |
| **GitHub Actions** | Automatizált CI/CD munkafolyamatok (*workflow*-k) futtatása eseményekre (*trigger*) |
| **OIDC-hitelesítés** | Rövid életű, összevont identitásalapú (*federated*) Azure-hozzáférés a workflow-hoz (nincs szükség hosszú életű, tárolt jelszóra/titokra) |
| **Azure Container Registry (ACR)** | Privát felhős tároló konténerimage-ek tárolására |
| **Azure Container Apps (ACA)** | Menedzselt felhős szolgáltatás konténerizált alkalmazások futtatására (beépített *ingress* HTTPS eléréssel) |

> [!danger] Jogosultsági buktató: OIDC vs. ACR Pull
> Ha egy GitHub Actions workflow **OIDC-vel sikeresen hitelesít Azure-ba**, de az **Azure Container App mégsem tudja lehúzni a privát ACR image-et**:
> - A két jogosultság **különálló**!
> - Az OIDC a *GitHub Actions → Azure* telepítési (deployment) jogosultságát biztosítja.
> - Az *Azure Container App → ACR* közötti image-letöltéshez (`pull`) külön jogosultság (pl. Managed Identity + `AcrPull` szerepkör vagy registry-hitelesítés) ellenőrzése szükséges!
