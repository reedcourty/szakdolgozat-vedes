Jegyzetek
#########

1. dia - Oktatástámogató rendszerek kiszolgáló infrastruktúrájának felügyeleti lehetőségei
==========================================================================================

- Üdvözlés

2. dia - Miről is lesz szó?
===========================

- Gyorsan végig pörögni a tételeken

3. dia - Mik azok a tanulásmenedzsment rendszerek?
==================================================

Milyen rendszereket nevezünk Learning Management Systemnek (LMS-nek)?
---------------------------------------------------------------------

Tanulásmenedzsment rendszernek, angolul Learning Management Systemnek (LMS-nek), vagy oktatástámogató rendszernek nevezzük azt a szoftver alkalmazást, amely automatizálja az oktatás adminisztrációját, követését, az online kurzusok és az azokkal kapcsolatos események, anyagok kezelését.

Mik egy LMS feladatai?
----------------------

Egy robusztus LMS-nek képesnek kell lennie:
    - központosított és automatizált adminisztrációra,
    - önkiszolgáló és önálló irányítású szolgáltatások nyújtására,
    - oktatási anyagok gyors összeállítására és elérhetőségének biztosítására,
    - konszolidált képzési kezdeményezésekre skálázható, web alapú platformon,
    - a portabilitás és a szabványok támogatására,
    - személyre szabott tartalom előállítására és a tudás újrafelhasználásának lehetővé tételére.

Milyen megoldásokat találunk a piacon?
--------------------------------------

A piacon különböző nyílt forrású, ingyenesen elérhető és zárt, kereskedelmi változatokat vagy vegyes koncepciókat is találunk, amelyek esetében ugyan a rendszer maga nyílt forrású, de a támogatásért vagy akár bérüzemeltetésért már pénzbeli juttatást kérnek.

Alkalmazott technológiák:
    - Java, PHP, Ruby on Rails, .NET
    - MySQL, MSSQL, PostgreSQL, Oracle

Miért fontos az átjárhatóság?
-----------------------------

Elkezdünk használni egy LMS-t, de a korábbi igények kiegészülnek, nem elég stabil a megnövekedett felhasználószámhoz, stb. Ilyenkor nem kell kidobnunk az egészet, hiszen a már feltöltött tartalmat jó eséllyel könnyedén átmigrálhatjuk az új rendszerbe.

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

- Webszerverek erőforrás igényei
    - Főleg memória a kérések kiszolgálás modellje miatt

Egy webszerver általában egy többfolyamatos (multi-process) vagy többszálas (multi-threaded) modell szerint működik. Ezek a feldolgozó folyamatok vagy szálak igény esetén jönnek létre, vagy egy tárolóban előre létrehozott számban várják a beérkező TCP kapcsolatokat, hogy kiszolgálhassák azokat. A széleskörűen használt Apache webszerver a többfolyamatos, készletes modellt alkalmazza.

A HTTP 1.1-es verziójában megjelent a perzisztens kapcsolat, amely lehetővé teszi, hogy egy kapcsolatba több kérés is belekerüljön. Ezek a perzisztens kapcsolatok egy új típusú szűk keresztmetszetet hoztak be a szerverekbe. Amióta a kiszolgáló folyamat egy perzisztens kapcsolathoz köthető, a CPU kihasználtsága nagyon alacsony. Ezen alacsony kihasználtságon a végrehajtó folyamatok számának növelésével segíthetünk, ám ekkor a virtuális memória kezdhet el vergődni (thrashing). Ezt csak viszonylag sok elérhető memóriával orvosolhatjuk. Ebből következik, hogy a webszerverek inkább memória-, mint processzorigényesek.
    
- Adatbázisok hasonlóak a webszerverekhez

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
- Virtualizáció csak említés szintjén
    - Mi a lényege?
- Felhőalapú megoldásokat csak átvezetés szintjén, mert következő dián részletezésre kerül

8. dia - Felhőalapú infrastruktúrák az LMS-ek szemszögéből
==========================================================

- Minden réteget jellemezni, LMS szemszögéből is

9. dia - IT infrastruktúrák proaktív menedzsmentje általános és oktatástámogató rendszerek esetén
=================================================================================================

- Nagyon nincs mit hozzáfűzni

10. dia - IT infrastruktúrák menedzsmentje reaktív esetben
==========================================================

- Reaktív rendszereket jellemezni

11. dia - IT infrastruktúrák menedzsmentje proaktív esetben
===========================================================

- Proaktív rendszerek jellemezni

12. dia - Hogyan kerül a csizma proaktívan az asztalra?
=======================================================

- Nagyon nem kell sokat hozzáfűzni
- Érdemes lehet megjegyezni, hogy ezen a részen tovább vihető a szakdolgozat témája

13. dia - Összefoglalás
=======================

- Miről is volt szó?

14. dia - A bíráló kérdése
==========================

- Mi is itt a probléma?
    - Adattárolás felhőben
        - Nem ismert az adatok helye
        - Nem rendelkezünk az infrastruktúra felett
    - Mi a biztosíték arra, hogy a cloud szolgáltató nem fér hozzá a kutatásainkkal kapcsolatos adatokhoz?
- Vannak különféle PET alkalmazások, és megvalósítások
    - Rejtjelezés
    - Adatbázis lekérdezések
        - Lekérdezések átalakítása a kliensben
        - Intevallumok lekérdezése a tényleges adat helyett
    - PIR (Privacy Information Retrieval)
        - Lekérdezés egy adatbázisból úgy, hogy a szerver ne tudja mi volt a kérdés 

15 . dia - Kérdések?
====================

16. dia - Köszönöm a figyelmet!
===============================

