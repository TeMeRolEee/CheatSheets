# Par prog zh cheat sheet

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

    
