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
    
Mik egy LMS feladatai?
----------------------

::
        
    LSM-ek feladatai:
        - központosított és automatizált adminisztráció,
        - lehetőséget biztosít az önálló tanulásra,
        - lehetőséget biztosít oktatási anyagok összeállítására, publikálására,
        - továbbképzésre kialakított, skálázható, webalapú platform,
        - portábilis, szabványokat támogató,
        - személyre szabott és újrafelhasználható tudást biztosít.

Milyen megoldásokat találunk a piacon?
--------------------------------------

::

    A piacon különböző nyílt forrású, ingyenesen elérhető és zárt, kereskedelmi 
    változatokat vagy vegyes koncepciókat is találunk, amelyek esetében ugyan a 
    rendszer maga nyílt forrású, de a támogatásért vagy akár bérüzemeltetésért 
    már pénzbeli juttatást kérnek.

Miért fontos az átjárhatóság?
-----------------------------

::

    A kiválasztott rendszer használata során kiderülhet, hogy nem felel meg 
    100%-osan, mivel esetleg új igények merülnek fel, vagy nem elég stabil a 
    megnövekedett felhasználószám mellett.

    Szerencsére a legtöbb rendszer között biztosított az átjárhatóság, így nem 
    kell kidobnunk a már elkészült rendszertől független tartalmat.

Mi az a SCORM, és mire jó?
--------------------------

::
    
    Az átjárhatóság biztosítására alkották meg a SCORM-ot, vagyis a Sharable 
    Content Object Reference Model-t, amely web-alapú LMS-ekkel kapcsolatos
    szabványok és specifikációk gyűjteménye.
    
    Felhasználói oldalról nézve ez annyit tesz, hogy tetszőleges SCORM-ot 
    támogató rendszerből átmigrálhatjuk az oktatással kapcsolatos anyagokat.
    
4. dia - LMS-ek IT infrastruktúrája
===================================
  
::

    A webes megoldásból következik a 3 rétegű architektúra alkalmazása.

5. dia - LMS-ek IT infrastruktúrája - Megvalósítás
==================================================
        
::

    Korábbi munkám során az egyik PHP alapú LMS-t, Moodle-t telepítettem és
    üzemeltem be. A webkiszolgáló réteg feladatait Apache, az adatbázis rétegét
    pedig MySQL adatbázis szerver látta el.
    
    Természetesen ez csak egy személyes döntés volt, az egyes rétegek feladatait
    más szolgáltatások is elláthatták volna, pl. ngnix az Apache, PostgreSQL a
    MySQL helyett.

6. dia - Tanulásmenedzsment rendszerek erőforrás igényei
========================================================

Modellek
--------

::

    Szakdolgozatomban próbáltam összegyűjteni olyan erőforrás igény 
    változásokat, amelyek az LMS-ekre jellemzőek.
    Ilyen lehet pl. a
        - kurzus-/vizsgajelentkezési időszak,
        - kurzussal kapcsolatos feladatok beadási határideje,
        - kurzus online teszt, vagy vizsga kitöltés (határ)ideje,
        - egyéb a kurzussal kapcsolatos offline számonkérés,
        - online előadás közvetítés,
        - audiovizuális tananyagokkal rendelkező kurzus számonkérésének ideje.

    Ezek eltérő módon befolyásolhatják az egyes erőforrások kihasználtságát.
    
    Lehetőség lenne modellek alkotására statisztikai módszerekkel a rendszer 
    működését jellemző historikus adatokból és a felhasználói viselkedések
    elemzéséből, és ezzel előre jelezhetnénk az erőforrás igények változásainak
    lefolyását.

7. dia - Információs technológiai infrastruktúrák
=================================================

- A klasszikus részről nem kell sokat beszélni

::

    Írásomban érintettem a 3 rétegű architektúra egyes rétegeire jellemző 
    szolgáltatásbiztonsággal kapcsolatos technikákat, mint pl. a 
    terheléselosztást, replikálást, de ezeknek a részletezésére most nem
    térnék ki.

    Úgy érzem az oktatástámogató rendszerek szemszögéből érdekesebb a
    virtualizáció és ezzel együtt a felhőalapú megoldások áttekintése.

- Felhőalapú megoldásokat csak átvezetés szintjén, mert következő dián 
  részletezésre kerül

8. dia - Felhőalapú infrastruktúrák az LMS-ek szemszögéből
==========================================================

::

    Az ábrán a felhőalapú infrastruktúra szolgáltatás szintje láthatók. Az egyes
    szintek jellemzését most kihagynám, inkább az LMS-ekkel való kapcsolatukat
    emelném ki.

Tárhely mint szolgáltatás (data-Storage-as-a-Service, dSaaS)
------------------------------------------------------------
       
::

    A tárhely mint szolgáltatás az LMS-ek esetében nagyméretű adatok esetén
    lehet előnyös, hiszen nem kell a saját szerverünkön tárolni ezeket, 
    megspórolva ezzel saját adattároló rendszer kialakítását, üzemeltetését.

Infrastuktúra mint szolgálatás (Infrastructure-as-a-Service, IaaS)
------------------------------------------------------------------
   
::

    Az infrastruktúra mint szolgáltatás használatával rengeteg előnyre tehet
    szert egy LMS üzemeltetője, mint pl. az elasztikus tulajdonság, idő- és
    teljesítményalapú számlázás és a nagy rendelkezésre állás.

Platform mint szolgáltatás (Platform-as-a-Service, PaaS)
--------------------------------------------------------
    
::

    A platform mint szolgáltatás előnye, hogy nekünk már nem kell foglalkozni
    az infrastruktúrával, operációs rendszerrel, egyedül az oktatástámogató
    rendszerünk fejlesztésére, telepítésére kell csak fókuszálnunk.
    
    Mindemelett itt is megtalálhatóak az alsóbb szintekből származó előnyök.

Szoftver mint szolgáltatás (Software-as-a-Service,SaaS)
-------------------------------------------------------
  
::

    Az LMS-ek tekintetében a szoftver mint szolgáltatás jelenti a fő bevételi 
    piacot. Rengeteg cég található az interneten, amely fizetős LMS 
    szolgáltatást nyújt. Ezeknek nagy előnye, hogy egyáltalán nem kell a 
    rendszer üzemeltetésével foglalkozunk, és a tartalomra, oktatási anyagra 
    koncentrálhatunk, hátránya, hogy kötött a mozgásterünk egy ilyen 
    rendszerben, nincs vagy korlátozott a lehetőség saját környezet 
    kialakítására.

9. dia - IT infrastruktúrák proaktív menedzsmentje általános és oktatástámogató rendszerek esetén
=================================================================================================

- Nagyon nincs mit hozzáfűzni

::

    Rendszermenedzsment szempontjából az IT infrastuktúrákat két típusba 
    sorolhatjuk:
        - raktívba és
        - proaktívba

10. dia - IT infrastruktúrák menedzsmentje reaktív esetben
==========================================================
   
::

    Egy menedzsment rendszert reaktívnak mondunk, ha képes gyorsan és hatékonyan
    reagálni a külső és belső kérelmekre, már bekövetkezett változásokra.

11. dia - IT infrastruktúrák menedzsmentje proaktív esetben
===========================================================

::

    Egy menedzsment rendszer proaktív, ha a reaktív részen felül folyamatos 
    monitorozással, előrelátással és tanulással próbál reagálni a rendszerben 
    még be nem következett eseményekre.

12. dia - Hogyan kerül a csizma proaktívan az asztalra?
=======================================================

- Érdemes lehet megjegyezni, hogy ezen a részen tovább vihető a szakdolgozat témája

::

    Próbáljuk meg összerakni az eddig elhangzott dolgokat. Említettem, hogy a
    változó erőforrás igényekre megpróbálhatunk modelleket alkotni, amely
    modellek alapján proaktívan kezelhetjük a rendszer változásait.
    
    A felhő alapú szolgáltatások nagy részénél az IaaS szintjén rendelkezésünkre
    bocsájtanak egy API, amely segítségével saját magunk tudjuk rugalmasan
    kezelni a rendelkezésre álló erőforrásokat.
    
    Ha ezt a két dolgot összerakjuk egy LMS rendszer alkalmazási rétegében,
    akkor egy automatikusan működő, proaktív, nagy rendelkezésre álló, költség-
    hatákony rendszer kapunk.
    
    Vegyük példának mondjuk az Amazon EC2 API-ját, a Moodle rendszert. A Moodle
    nyílt forráskódú, tehát lehetőséget biztosít arra, hogy saját magunk
    bővítsük ki. A megfelelő helyen implementálhatjuk azt, hogy egy teszt
    kitöltési időszak, vagy kurzus felvételi időszak kezdete előtt automatikusan
    meghívódjon az API megfelelő metódusa, és az előzetes tapasztalatok alapján
    megnöveljük a rendszert kiszolgáló erőforrások számát.

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

