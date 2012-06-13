Jegyzetek
#########

1. dia - Oktatástámogató rendszerek kiszolgáló infrastruktúrájának felügyeleti lehetőségei
==========================================================================================

- Üdvözlés
- Bemutatkozás

2. dia - Miről is lesz szó?
===========================

- Gyorsan végig pörögni a tételeken

3. dia - Mik azok a tanulásmenedzsment rendszerek?
==================================================

Milyen rendszereket nevezünk Learning Management Systemnek (LMS-nek)?
---------------------------------------------------------------------

::

    Tanulásmenedzsment rendszernek, angolul Learning Management Systemnek 
    (LMS-nek), vagy oktatástámogató rendszernek nevezzük azt a szoftver 
    alkalmazást, amely automatizálja az oktatás adminisztrációját, követését, az
    online kurzusok és az azokkal kapcsolatos események, anyagok kezelését.
    
Automatizálja
    - az oktatás adminisztrációját, követését
    - kurzusok, események, anyagok kezelését  

Mik egy LMS feladatai?
----------------------

::

    Egy robusztus LMS-nek képesnek kell lennie:
        - központosított és automatizált adminisztrációra,
        - önkiszolgáló és önálló irányítású szolgáltatások nyújtására,
        - oktatási anyagok gyors összeállítására és elérhetőségének biztosítására,
        - konszolidált képzési kezdeményezésekre skálázható, web alapú platformon,
        - a portabilitás és a szabványok támogatására,
        - személyre szabott tartalom előállítására és a tudás újrafelhasználásának lehetővé tételére.
          
LSM-ek feladatai:
    - központosított és automatizált adminisztráció,
    - lehetőséget biztosít az önálló tanulásra,
    - lehetőséget biztosít oktatási anyagok összeállítására, publikálására,
    - képzésre kialakított, skálázható, webalapú platform,
    - portábilis, szabványokat támogató,
    - személyre szabott és újrafelhasználható tudást biztosít.

Milyen megoldásokat találunk a piacon?
--------------------------------------

::

    A piacon különböző nyílt forrású, ingyenesen elérhető és zárt, kereskedelmi 
    változatokat vagy vegyes koncepciókat is találunk, amelyek esetében ugyan a 
    rendszer maga nyílt forrású, de a támogatásért vagy akár bérüzemeltetésért 
    már pénzbeli juttatást kérnek.
    
Megoldások:
    - Nyílt forrású, ingyenesen elérhető
    - Zárt, kereskedelmi
    - Vegyes koncepciók
        - a rendszer nyílt, de
        - támogatásért, bérüzemeltetésért fizetni kell

Alkalmazott technológiák:
    - Java, PHP, Ruby on Rails, .NET
    - MySQL, MSSQL, PostgreSQL, Oracle

Miért fontos az átjárhatóság?
-----------------------------

Elkezdünk használni egy LMS-t, de
    - a korábbi igények kiegészülnek,
    - nem elég stabil a megnövekedett felhasználószámhoz, stb.

Nem kell kidobnunk az egészet, a már feltöltött tartalmat jó eséllyel könnyedén átmigrálhatjuk az új rendszerbe.

Mi az a SCORM, és mire jó?
--------------------------

A SCORM (Sharable Content Object Reference Model) web-alapú e-learning rendszerekkel kapcsolatos szabványok és specifikációk gyűjteménye. A SCORM definiálja a kommunikációt a kliens oldal és a futtatási környezet (run-time environment) között.

Felhasználói oldalról nézve a tanárok oktatási csomagokat tölthetnek fel/le a kurzusok között akár különböző LMS megvalósítások esetén is, ha azok támogatják az adott SCORM verziót (portabilitás).

Tehát a SCORM segítségével oldható meg az átjárhatóság.

4. dia - LMS-ek IT infrastruktúrája
===================================

- Nagyon gyors helyzet vázolás

5. dia - LMS-ek IT infrastruktúrája - Megvalósítás
==================================================

Önállólaboratóriumi munkám során telepítettem a Moodle LMS-t, Apache webkiszolgáló és MySQL adatbázisszerver alkalmazásával.

Természetesen ez csak egy döntés volt, a web és adatbázis réteget tetszőleges másik alkalmazásra cserélhettem volna, pl. ngnix az Apache, PostgreSQL a MySQL helyett.

6. dia - Tanulásmenedzsment rendszerek erőforrás igényei
========================================================

Webszerverek erőforrás igényei
------------------------------

Egy webszerver általában egy többfolyamatos (multi-process) vagy többszálas (multi-threaded) modell szerint működik. Ezek a feldolgozó folyamatok vagy szálak igény esetén jönnek létre, vagy egy tárolóban előre létrehozott számban várják a beérkező TCP kapcsolatokat, hogy kiszolgálhassák azokat. A széleskörűen használt Apache webszerver a többfolyamatos, készletes modellt alkalmazza.

A HTTP 1.1-es verziójában megjelent a perzisztens kapcsolat, amely lehetővé teszi, hogy egy kapcsolatba több kérés is belekerüljön. Ezek a perzisztens kapcsolatok egy új típusú szűk keresztmetszetet hoztak be a szerverekbe. Amióta a kiszolgáló folyamat egy perzisztens kapcsolathoz köthető, a CPU kihasználtsága nagyon alacsony. Ezen alacsony kihasználtságon a végrehajtó folyamatok számának növelésével segíthetünk, ám ekkor a virtuális memória kezdhet el vergődni (thrashing). Ezt csak viszonylag sok elérhető memóriával orvosolhatjuk. Ebből következik, hogy a webszerverek inkább memória-, mint processzorigényesek.
    
Adatbázisok erőforrás igényei
-----------------------------

Az adatbázisok erőforrásigénye igen összetett, hiszen egyik részről a lekérdezéseket, tranzakciókat optimalizálni kell (CPU terhelés), az adatokat a háttértárról be kell olvasni, vagy oda ki kell írni (I/O terhelés), és az ezeket az igények csökkentő technikák memóriaigénye növekedhet.

Az adatbázisszerverek nagy része támogatja az ún. connection pooling megoldást, amely a webszerverek perzisztens kapcsolat-kezeléséhez hasonló, és ezzel együtt ebben az esetben is az erőforrásigény a memória felé tolódik el. Tehát összességében az adatbázisszerverek is inkább memória és lemez I/O igényesek.

- Alapvető statisztikai modellek
    - eloszlások

Szakdolgozatomban próbáltam összegyűjteni olyan erőforrás igény változásokat, amelyek az LMS-ekre jellemzőek. Ilyenek pl. a

- kurzus-/vizsgajelentkezési időszak,
- kurzussal kapcsolatos feladatok beadási határideje,
- kurzus online teszt, vagy vizsga kitöltés (határ)ideje,
- egyéb a kurzussal kapcsolatos offline számonkérés,
- online előadás közvetítés,
- audiovizuális tananyagokkal rendelkező kurzus számonkérésének ideje, 

Ezekre a rendszer működését jellemző megfelelő historikus adatokkal statisztikai modelleket tudnánk alkotni, és ezzel előre jelezhetnénk azok lefolyását.

7. dia - Információs technológiai infrastruktúrák
=================================================

- A klasszikus részről nem kell sokat beszélni

Írásomban összegyűjtöttem a 3 rétegű architektúra egyes rétegeire jellemző szolgáltatásbiztonsággal kapcsolatos technikákat. Mint például a
- terheléselosztás (load balancing),
- replikálás,
- feladatátadás hiba esetén (failover).

Ezeknek a részletezésére itt most nem térnék ki.

Úgy érzem az oktatástámogató rendszerek szemszögéből érdekesebb a virtualizáció és ezzel együtt a felhőalapú megoldások áttekintése.
- Virtualizáció csak említés szintjén
    - Mi a lényege?
- Felhőalapú megoldásokat csak átvezetés szintjén, mert következő dián részletezésre kerül

8. dia - Felhőalapú infrastruktúrák az LMS-ek szemszögéből
==========================================================

Tárhely mint szolgáltatás (data-Storage-as-a-Service, dSaaS)
------------------------------------------------------------

Ezt a szolgáltatást nem minden irodalom szokta említeni, ám én itt mégis külön kezelném, hiszen ez a felhő legalapvetőbb szolgáltatása. Lényege, hogy online tárhelyet biztosít a felhasználóknak. Ilyen szolgáltatást nyújt pl. a Dropbox.com (főleg személyes felhasználásra, biztonsági mentés, megosztás céljából) vagy az Amazon S3 (inkább nagy szolgáltatók használják).

A dSaaS oktatási rendszerek esetében sok nagyméretű adat esetén lehet előnyös, hiszen nem kell a saját szerverünkön tárolni ezeket, megspórolva ezzel saját adattároló rendszer kialakítását, üzemeltetését. 

A dSaaS segítségével a rendszerünk tárhelye jól skálázható, hiszen igény esetén transzparens módon tudjuk növelni, vagy költségcsökkentés céljából visszaadni az erőforrásokat. 

Infrastuktúra mint szolgálatás (Infrastructure-as-a-Service, IaaS)
------------------------------------------------------------------

Az IaaS az infrastruktúra (számítási erőforrások és tárhely) bérbeadása. Ez nem csak virtualizált számítógépeket jelent garantált számítási teljesítménnyel, de fenntartott sávszélességet a tárhely és az internetelérésnek is. Ez lényegében egy számítógép vagy adatközpont bérbevételének lehetőségét jelenti, specifikált szolgáltatásminőség (QoS) megkötésekkel, amelyekkel képesek vagyunk egy tetszőleges operációs rendszer és szoftver futtatására.

A legismertebb IaaS szolgáltatók az Amazon (Amazon EC2) és a Rackspace. A különböző IaaS-t nyújtó cégek szolgáltatásai nagyjából hasonlóak. 

Egy LMS üzemeltetésével foglalkozó szervezet esetén rengeteg előnyt jelenthet a rendszer felhőben való üzemeltetése. Az IaaS elasztikus tulajdonságának köszönhetően gyorsan tudjuk a változó erőforrásigényeket kielégíteni. Ezek a szolgáltatások idő- és teljesítményalapú számlázást használnak, így jó közelítéssel előre meghatározhatóak a költségek. A szolgáltatók nagy rendelkezésre állást biztosítanak, így nem fordulhat elő, hogy a rendszerünk nem érhető el. Természetesen ezen a szinten még szükségünk van IT munkatársakra, hiszen a rendszert fel kell építeni, és szoftveres szinten karban kell tartani, de már a hardveres szint hiánya is egyszerűsítheti a munkát.

Platform mint szolgáltatás (Platform-as-a-Service, PaaS)
--------------------------------------------------------

A PaaS hasonló az IaaS-hoz, de olyan operációs rendszereket és kötelező szolgáltatásokat foglal magába, amelyek egy sajátos alkalmazásra fókuszálnak. Például PaaS-ként tekinthetünk egy virtualizált szerver, tárhelyszolgáltatás, operációs rendszer és alkalmazás halmazt (ami tipikusan egy virtuális gép fájl formátumban, pl. a VMware .vmdk állománya), hozzáféréssel a szükséges szolgáltatásokhoz, mint amilyen például egy MySQL adatbázis vagy egyéb, specializált helyi erőforrás. Más szavakkal a PaaS egy IaaS, testre szabott szoftver stackkel egy adott alkalmazáshoz.

A piacon több PaaS szolgáltató találunk, mint például a Google AppEngine (Python, Java, Go), Heroku (Ruby, Node.js, Clojure, Java, Python, Scala), Epio (Python). Ezek webes alkalmazásoknak nyújtanak platformot.

A PaaS egy környezetet biztosít az alkalmazásunknak, amely lehet akár egy LMS is. Az IaaS-szel ellentétben itt már nem kell foglalkoznunk az OS üzemeltetésével járó feladatokkal, csak is magával az LMS alkalmazással, amelyet nekünk kell telepíteni, vagy adott esetben a platformra fejleszteni. Ugyanakkor az IaaS-nél megjelent előnyök itt is érvényesek, mind üzemeltetés, mind költség szempontjából.

A erőforrás skálázódás a PaaS esetében teljesen automatikusan működik, ebből kifolyólag a felhasználónak nem is áll módjában azt befolyásolni, ő csak a saját alkalmazása szintjén kap(hat) lehetőséget a skálázásra, például szükség esetén több folyamatpéldány indításával.

Szoftver mint szolgáltatás (Software-as-a-Service,SaaS)
-------------------------------------------------------

Az alkalmazás mint szolgáltatás az előfizető számára rendelkezésre bocsájtja annak a lehetőségét, hogy használja a szolgáltató egy felhő infrastruktúrán futtatott alkalmazását. Az alkalmazások különböző kliens eszközökön keresztül érhetőek el vékony kliens interfészen, mint amilyen egy webböngésző (pl. web alapú levelezés) vagy egy program interfész. A felhasználó nem kezeli vagy vezérli a szolgáltatás alapjául szolgáló infrastruktúrát, beleértve a hálózatot, szervereket, operációs rendszereket, tárhelyet, de még az egyéni szoftver képességeket sem, kivételt talán a limitált felhasználói szintű alkalmazás konfigurációs beállítások kezelése képez. Egy felhőalapú infrastruktúra hardverek és szoftverek gyűjteménye, amelyek engedélyezik a számítási felhő öt alapvető jellemzőjét.

A SaaS a legegyszerűbb szolgáltatás, lehetőséget biztosít alkalmazások bérlésére és használati idő alapú számlázásra. A SaaS a felhő legfelső szintje, ez az a felület, amellyel az internetfelhasználók nagy része már találkozott, még ha nem is tudatosan. Ilyen SaaS szolgáltatás a Google Gmail, Docs, Apps, a Microsoft Office 365, a Prezi.com és még sorolhatnám.

Az LMS-ek tekintetében a SaaS jelenti a fő bevételi piacot. Rengeteg cég található az interneten, amely fizetős LMS szolgáltatást nyújt. Ezeknek nagy előnye, hogy egyáltalán nem kell a rendszer üzemeltetésével foglalkozunk, és a tartalomra, oktatási anyagra koncentrálhatunk, hátránya, hogy kötött a mozgásterünk egy ilyen rendszerben, nincs vagy korlátozott a lehetőség saját környezet kialakítására.

Ezen a szinten már nem jelenik meg a skálázás lehetősége, hiszen ez már felhasználói szintnek számít. Ennek ellenére ezen a szinten elő lehetne segíteni az alsóbb szintek skálázódását, ha például egy LMS-ből a már említett információk és modellek alapján megvalósításra kerülnének bizonyos proaktív folyamatok. 

9. dia - IT infrastruktúrák proaktív menedzsmentje általános és oktatástámogató rendszerek esetén
=================================================================================================

- Nagyon nincs mit hozzáfűzni

10. dia - IT infrastruktúrák menedzsmentje reaktív esetben
==========================================================

Egy menedzsment rendszert reaktívnak mondunk, ha képes gyorsan és hatékonyan reagálni a külső és belső kérelmekre a belső flexibilitás maximalizálásával. Ezt a reaktivitást a rendszer rugalmasságán alapulva decentralizált döntésekkel és a reflexszerű viselkedés fejlesztésével előre definiált szabályok segítségével érik el. Tehát egy reaktív menedzsment a rendszerben már bekövetkezett változásokra reagál. A reaktív vezérlés inkább egy cselekvés valamilyen szituációra válaszolva, mint annak a szituációnak a létrehozása, vagy vezérlése.

11. dia - IT infrastruktúrák menedzsmentje proaktív esetben
===========================================================

Egy menedzsment rendszer proaktív, ha a reaktív része az előrelátás, illesztés és tanulás folyamataival van kiegészítve, amely folyamatok célja a rendszer támogatása, és annak koherenciájáról és hatékonyságáról való gondoskodás. Egy proaktív rendszer folyamatos monitorozással, előrelátással és tanulással próbál reagálni a rendszerben még be nem következett eseményekre. A proaktív vezérlés inkább egy szituáció irányítása, mint a szituáció által okozott történésekre adott válasz.

12. dia - Hogyan kerül a csizma proaktívan az asztalra?
=======================================================

- Nagyon nem kell sokat hozzáfűzni
- Érdemes lehet megjegyezni, hogy ezen a részen tovább vihető a szakdolgozat témája

13. dia - Összefoglalás
=======================

- Miről is volt szó?

14. dia - A bíráló kérdése
==========================

Mi is itt a probléma?
---------------------

- Adattárolás felhőben
    - Nem ismert az adatok helye
    - Nem rendelkezünk az infrastruktúra felett
    - Mi a biztosíték arra, hogy a cloud szolgáltató nem fér hozzá a kutatásainkkal kapcsolatos adatokhoz?

Lehetőségek a probléma megoldására
----------------------------------

A PET-ek környékén érdemes lehet szétnézni:

- Vannak különféle alkalmazások, és megvalósítások
- Adatbázis lekérdezések
    - Lekérdezések átalakítása a kliensben
    - Intevallumok lekérdezése a tényleges adat helyett
- PIR (Privacy Information Retrieval)
    - Lekérdezés egy adatbázisból úgy, hogy a szerver ne tudja mi volt a kérdés

DE! Ezek nem igazán az LMS-ekre jellemző use-case-ek.

Legjobb megoldás:

- Rejtjelezés, titkosítás

15 . dia - Kérdések?
====================

16. dia - Köszönöm a figyelmet!
===============================

