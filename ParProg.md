# Par prog zh cheat sheet

###### Nincs garancia arra, hogy minden amit ide írtam fedi a valóságot, elképzelhető, hogy elírtam valamit (vagy szimplán b.romságot írtam), ez esetben kérlek kommentelj a kódba giten, hogy mire kellene kijavítan.

### **1** sokprocesszoros rendszerek létrehozásának okai, alkalmazási területek, ahol a nagy számítási teljesítménye, nagy memória méret fontos

        A 2000-es évek közepéig a processzorok fejlődése
        nagy részben az órajelciklus növelésének volt
        köszönhető. Egy processzor minél nagyobb frekvencián
        működött, annál gyorsabb volt. Azonban elértek egy
        felső határt, amit a melegedési problémákból és a
        tranzisztorok tulajdonságágából adódóan nem tudtak
        megoldani. Az Intel 2004-ben beharangozta a Pentium
        4 4.0 Ghz-es processzorát, de teszteléskor
        lényegében „elolvadt”. Erre találtak ki egy
        lehetséges megoldás, mégpedig több magot használnak
        egy processzoron belül, a frekvenciát pedig sokkal
        lejjebb viszik, 2-3 Ghz környékére, de sokszor 2 alá
        is leviszik, így jelentősen csökkentve a fogyasztást
        és a melegedési probléma se okoz gondot. Az egymagos
        processzorok korszaka véget ért, manapság már csak
        több magosak léteznek.
    
### **2** közös és elosztott memóriájú rendszerek felépítésének elvi különbségei

**Elosztott memóriás rendszerek:**
        
    Nincs közös memória, minden processzornak sajátja van és
    üzenetekkel kommunikálnak egymással egy közös hálózaton
    (pl. Ethernet). Munkaállomások összeköttetésére ezt
    használják.

    Előny:

        - Nagy teljesítményű munkaállomások kis/nulla plusz
            költséggel elérhetőek lehetnek
        - A legújabb generációs processzorokkal rendelkeznek 
           -> nagy teljesítmény
        - Alacsonyabb teljesítményű szuper-számítógépek
            teljesítményével vetekszik.

**Közös memóriájú rendszerek:**

    Egy többmagos processzorban alapvetően minden mag egy
    közös rendszermeóriát (RAM) használ, de a processzornak
    is lehet cache memóriája. Ekkor minden magnak van külön
    1. szintű cache, de a 2. szintű cache már közös. Cache
    memóriával a processzor gyorsítható, mivel közvetlenül a
    prcesszorokhoz van kötve, nincs szükség buszokra, így
    sokkal gyorsabban elérhető, mint a rendszermemória és
    lecsökken a buszon keresztüli adatátvitel. De hátránya,
    hogy drágább lesz a processzor és nő a lapka mérete is
    ezzel. Ezért van minden „megfizethető” processzoron csak
    1-2 MB cache.

    Előny:

        - A cache behozatala nagymértékben gyorsította a processzort
        - Csökkenti a cache megléte a rendszerbusz terhelését
        - Több processzort lehet egybekötni (100-200 akár)

    Hátrány

        - Drágább
        - Komplexebb
        - Memória koherencia problémák (megoldás: cache sync)
    

### **3** a memória modell hatása a programozási modellre

    Ha két mag egyszerre beolvas egy változót a
    rendszermemóriából a
    saját cache-ébe és az egyik felülírja az értékét, a másik
    erről nem tud és még a régi értékkel
    dolgozik, innentől a változó értéke a hibás lesz.
    
    Memória koherenciára figyelni kell.
    
    Közös (shared variables) változókat nem tárolunk cacheben.
    
    Semaphor

### **4** közös memóriájú párhuzamos számítógépek összeköttetés rendszerei, lehetséges megoldások, azok előnyei és hátrányai

* **Dinamikus összeköttetések:**

    * Crossbar

            A processzorok és memóriák közötti utat rács-szerűen
            behuzalozzuk és a kereszteződésekbe egy
            kapcsolót teszünk. P párhuzamosítás esetén P2
            kapcsoló szükséges.

    * Multistage network

            Csak vizszintesen huzalozzuk be és inteligens kapcsolókat használunk.
            Nem minden út elérhető egyidőben (hotspots)
    
    * Hierarchikus busz-rendszer

* **Statikus összeköttetés:**

        Pont-pont összeköttetés és egy processzor mindig
        ugyanazokkal
        van összekötve, a rendszer működésekor ez nem
        változik.
        Mindent mindennel össze lehetne kötni, ez nagyon
        gyors adatátvitelt eredményez, hiszen
        minden processzornak közvetlen szomszédja egy másik,
        de sok processzornál már sok
        csatlakozónak kell lennie, illetve bővítéskor le
        kell cserélni az összeset olyanra, aminek több
        csatlakozója van. Egy jobb megoldás, ha minden
        processzort legfeljebb 4 másikkal kötünk
        össze, így mindegyiknek elég 4 csatlakozó és könnyen
        bővíthető is.
        
        Az összeköttetés lehetőségei:

            - Teljesen összekötött (4 mag fölött nem éri meg)
            - Ring ("1D tömb")
            - Háló ("2D tömb")
            - Csillag
            - Bináris fa
            - hyper-kocka

### **5** szuperszámítógépek jelenlegi számítási teljesítmény tartománya, várható továbbfejlődési irányok

1. Cray-1 80-180 MFLOPS
2. Numerical Wind Tunnel 124 GFLOPS
3. Intel ASCI Red 1.8 TFLOPS
4. K computer 10.5 PFLOPS
5. Cray Titan 17 PFLOPS
6. Tianhe-2 34 PFLOPS
7. Summit 143.5 PFLOPS


### **6** Process fogalma

        A folyamat egy olyan szekvenciális programkód aminek
        van saját adata és állapota.
        
        Párhuzamos programozásban képesnek kell lennünk menedzselni a folyamatokat (processeket),
        szinkronizálni őket, ha szükséges.
        
        Az alap ötlet az lenne, hogy minden folyamatot
        szétosztunk különböző részekre amiket párhuzamosan
        futtathatunk.

### **7** adat- és algoritmikus párhuzamosítás elve, példákkal

* **Adatpárhuzamosítás:**

        Az adathalmaz, amin műveletet el kell végezni,
        felosztjuk a processzorok között.
        
        Példa:

            Mátrixszorzásnál részeire bontjuk
            a mátrixot és minden
            processzor csak egy kis részen végzi el a
            szórzást.

* **Algoritmuspárhuzamosítás:**

        A műveletet osztjuk fel.

        Példa:

            Komplex képletet felbonytjuk részekre

* **Pipeline:**

        Van egy munkadarab, amin minden processzor végez
        valamilyen műveletet. Ha az egyik processzor
        végzett, továbbadja a következőnek.

* **Farm:**

        A problémát kisebb egységekre felosztják, mindig van
        egy vezérlő, ami kiosztja a
        munkát a dolgozóknak, az eredményt üzenetként kapja
        vissza. Dinamikus, mert a munka igény szerint
        osztható ki.
        
### **8** a kritikus szakasz fogalma

        Egy kód kritikus szakaszán azt értjuk, amikor az 
        utasításokat kölcsönös kizárással kell végrehajtani
        miközben figyelni kell más kódrészek kritikus szakaszaira,
        hogy a megosztott változókhoz hozzá férhessünk

### **9** az atomi művelet fogalma 

        Egy párhuzamos process által végzett olyan műveletet értünk,
        amely nem szakítható meg más művelettel.
        Amíg ez dolgozik, addig más process nem juthat
        az adott adathoz.
        Az atomi művelet oszthatatlan legkisebb egység.

### **10** a kölcsönös kizárás fogalma, alkalmazásának célja, megvalósítási lehetőségei (busy waiting, szemafor, monitor)

* **Semaphore:**

        Definiálunk egy logikai változót, ami megmondja,
        hogy egy adott szál beléphet-e a kritikus
        szakaszba. Ha beléphet, a szál beállítja az értéket
        hamisra, kilépéskor visszaállítja igazra.

* **Busy waiting:**

        Egy process akkor van ebben az állapotban, ha egy változó állapotának a megváltoztatására vár.
        Várhat rendszer erőforrásra, blokkol process-listában van.
        Nem túl hatékony, CPU időt pazarol

* **Monitor**

        A monitor egy olyan struktúra, ami összegyűjti
        a kritikus szakaszokat egy modulba.
        Monitort használó processeknek így nincs már többé
        kritukus szakasza.
        
        Eljáráshívásokk lesznek a monitorban.
        
        Nem elérhető a monitoron kívülről.

        Megosztott adatoknak a monitorban kell(ene) lennie,
        így csak az eljáráshívások érhetik el.

        Implicit kölcsönös kizárást ad.
        Egyszerre csak egy eljáráshívás van végrehajtva.
        
        Azon processek amelyek nem fértek hozzá a monitorhoz,
        autómatikusan a várólistájára kerülnek


### **11** a feltételes szinkronizáció jelentése, megvalósítási lehetőségei


### **12** a OpenMP programozási modell alapelveinek bemutatása, direktívák, a fordítóprogram szerepe, párhuzamos régió, stb.


### **13** a Producer-Consumer probléma ismertetése elvi szinten, a helyes működéshez szükséges szinkronizációs megoldások

```
ProducerConsumer
{
    // Multiple Producer Consumer problem with single shared
    // buffer buff
    // Solution uses split binary semaphores
    int buff;
    semaphore empty = 1;
    semaphore full = 0; // binary semaphores
    process Producer
    {
        while (true) {
            // generate data x
            P(empty); // wait until buffer empty
            buff = x;
            V(full); // signal full
        }
    }
    process Consumer
    {
        while (true) {
            P(full); // wait until buffer full
            y = buff;
            V(empty); // signal empty
            // consume data y
        }

    }
}
```

### **14** a teljesítmény jellemzésének mérőszámai, párhuzamos futási idő, gyorsulás, hatékonyság. Képletek, ezek kapcsolata, illetve melyik mit mond el a rendszer működéséről, mire használhatók?



