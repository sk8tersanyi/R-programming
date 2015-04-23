# Harmadik hét
Az úgynevezett _ciklus függvények_ ( _loop functions_ )  - mintha valami ciklust csinálnának meg kompakt formában, így akár konzolról is können szerkezthető - használata és tulajdonságai, továbbá alapvető debuggolás.

## _lapply_ függvény
* végigmegy az argumentumában szereplő lista objektumain és ezekre alkalmazza a további bemenetként megadott függvényt
* három argumentuma van: az első, melyben a listát adhatjuk meg; a második, ahol az alkalmazandó fggvényt adjuk meg; míg az utolsó egy ... argumentum, melyben az előbbi függvény paramétereit tudjuk beállítani
* ha a megadott első argumentum mégsem egy lista, akkor meghívás esetén az lapply azzá teszi, ha ez lehetséges, különben hibaüzenetet ad
* ha meghívjuk argumentumok nélkül, akkor látható, hogy maga a függvény nem valami nagyon bonyolult szerekezetű dolog, illetve, hogy a megvalósítás, a sebesség maximalizálása érdekében, C nyelven történik
* a meghívott függvény által kiszámolt értékeket a _lapply_ listába rendezve adja vissza - az iménti példában egyenletes eloszlásból generálunk számokat, méghozzá úgy, hogy a lista elemében egy darabot, másodikban kettőt, stb.
<blockquote>
  <p> y <- 1:5 </p>
  <p> lapply(y, runif) </p>
</blockquote>
* fontos mégegyszer kiemelni, hogy a _lapply_ függvény harmadik, ... argumentumában adhatjuk meg a kiértékelendő függvény további paramétereit 
* az _lapply_ és a hozzá hasonló ( továbbiakban kifejtendő ) ciklus függvények nagyszerű tulajdonsága, hogy segítségükkel tudunk úgynevezett _névtelen függvényeket_ meghívni; ezek alatt olyan függvényeket értünk, melyeknek nincs nevük
* ezt úgy kell elképzelni, hogy a kiértékelendő függvényt a a _lapply_ függvényen belül definiáljuk, ahogyan ez a következő példában is látszik - a listában szereplő mátrixok első oszlopát adja vissza
<blockquote>
  <p> x <- list(a = matrix(1:4, 2), b = matrix(6:1, 3)) </p>
  <p> lapply(x, function(elt) elt[1,]) </p>
</blockquote>
* habár ez egy elég bugyuta példa és így nem teljesen látható, de az ilyen ciklus függvények ereje pont a névtelen függvények használatában rejlik

## _sapply_ függvény
* az előbb taglalt _lapply_ függvény által visszaadott OUTPUT-ot egyszerűsíti, amennyiben ez persze lehetséges
* ha az _lapply_ függvény eredménye egy olyan lista, mely minden eleme egy hosszú, akkor ha az _sapply_ függvényt használjuk, egy vektort kapunk vissza
* amennyiben az _lapply_ függvény eredménye egy olyan lista, mely minden eleme azonos hosszú vektor, akkor ha az _sapply_ függvényt használjuk, egy mátrixot kapunk vissza
* persze ha nem tudja elvégezni ezeket az egyszerűsítéseket, akkor az _lapply_-hoz hasonlóan listát ad vissza

## _apply_ függvény
* az _apply_ függvény egy olyan ciklus függvény, mellyel egy tömb indexein tudunk függvényeket kiértékelni
* ez a tömb leggyakrabban egy mátrix és így ennek indexei nem mások, mint a mátrix sorai, illetve oszlopai - emellett van lehetőség általánosabb ( magasabb dimenziós ) tömbök indexein számolni
* a közhiedelemmel ellentétben használata nem azért ajánlott, mert gyorsabb, mint egy ciklus, hanem mert kevesebbet kell gépelni ( régen volt csak igaz!!! )
* négy argumentuma van: az első maga a tömb; a második egy egész értékű vektor mellyel meghatározzuk, hogy a tömb mely dimenzióin akarunk függvényt alklamazni; a harmadik a kiértékelendő függvény; míg a negyedik egy a korábbiakból értelemszerűen következő ... argumentum, melyben az előbbi függvény további paramétereit tudjuk beállítani
* legegyszerűbb - két dimenziós - esetben úgy kell elképzelni, hogy az _apply_ függvény második változójában adjuk meg, hogy melyik dimenzió az amit rögzítünk, azaz ha 1-et írunk, akkor a mátrix soarira fogjuk kiértékelni a megadott függvényt
* fontos megjegyezni, hogy ebben a speciális esetben, ha összeget, vagy átlagot akarunk számolni, nem érdemes az _apply_ függvényt használni, ugyanis vannak futási időben optimalizált beépített függvényeink erre a célra, melyek nevei értelemszerűek: _rowSums_, _rowMeans_, _colSums_, _colMeans_. ( ezek sebbességbeli éltérése nagy adathalmaz esetén látható !! ) - ugyanezen függvények magasabb dimenzióban is működnek !!!
* többdimenziós tömbökre való alkalmazásnál érdemes lenne átgondolni, hogy hogyan is "néz ki" az összegzés

## _mapply_ függvény
* a korábban taglalt _lapply_ és _sapply_ ciklus függvények többváltozós általánosítása, ahol a többváltozós alatt azt kell érteni, hogy a kiértékelendő függvény több argumentummal rendelkezik és ezen értékeket különböző listákban tároljuk
* lehetne FOR ciklussal is, de ha az _mapply_-t használjuk akkor párhuzamosan dolgozunk, ami elég jó
* négy argumentuma van: az elsőben adjuk meg a kiértékelendő függvényt; a második egy ... argumentum, melyben ez egyes megadandó argumentumoknak megfelelő mennyiségű listát adhatjuk meg; a harmadik ( MoreArgs ) argumentumban a kiértékelendő függvény egyéb paramétereinek listáját adhatjuk meg; míg negyedik ( SIMPLIFY ) argumentumban azt ,hogy az output milyen tipusú legyen ( ugyanaz történik, mint _sapply_-nál ) - még van egy ötödik, mely az OUTPUTlistájának neveire vonatkozó logikai változó
* ezekből kiderül, hogy megint arról van szó, hogy szeretnénk kevesebbet gépelni - például, az első helyett érdemes a másodikat használni:
<blockquote>
  <p> list(rep(1,4), rep(2,3), rep(3,2), rep(4,1)) </p>
  <p> mapply(rep, 1:4, 4:1) </p>
</blockquote>

## _tapply_ függvény
* ezzel a ciklus függvénnyel vektorok részvektorain - azaz elemeinek részosztályain - tudunk függvényeket kiértékelni
* öt argumentuma van: az első az a vektor melyen a számítást végezzük; a második, az elsővel megegyező hosszúságú faktor, mely az egyes csoportok elemeit reprezentálja; a harmadik a kiértékelendő függvény; a negyedik a szokásos ... argumentum; míg az  utolsó ( simplify ) az eredmény egyszerűsítését meghatározó logikai változó ( mint az _sapply_-nál ) 
* ha az egyszerűsítést nem állítjuk be, akkor az eredményt egy listában kapjuk vissza, ahol e lista nevei pont a megfelelő faktorok szintjei lesznek

## _split_ függvény
* ez a függvényk issé kilóg a sorból, ugyanis nem ciklus függvény, viszont nagyon hasznos lehet egy egy ilyennel együtt ( összetetten ) alkalmazva
* a _split_ függvény segítségével vektorokat és más objektumok elemeit tudjuk különböző csoportokba rendezni
* négy argumentummal rendelkezik: az első a hasítandó objektum; a második a hasítást reprezentáló faktor, vagy faktorok listája, a harmadik ( drop ) az üres szintek elhagyaását megadó indikátor; míg a negyedik egy ... argumentum
* a _split_ függvény által visszaadott objektum egy lista lesz
* persze a korábbiakban taglaltak miatt látható, hogy példaául vektorok esetén, ahelyett hogy ilyen függvény összetételeket gyártanánk használhatunk szimplán _tapply_ ciklus függvényt is
* a _split_ függvény igazi ereje abban nyílvánul meg, hogy segítségével képesek vagyunk sokkal összetettebb objektumokat is hasítani - például egy data frame esetén tudunk egy egy oszlop elemei szerint hasítani a _split_ függvénnyel
* megjegyezendő, hogy tudunk vektor szerint is hasítani, ugyanis a függvény megvalósítása ilyen
* a diákon nagyon jó példák vannak, amiket most nem írnék ide - mert ronda formátumban tolom - de mindenképp érdemes átbogarászni őket
* előfordulhat, hogy nem csak egy faktorunk van, hanem egyszerre több, például ez van akkor, ha van egy nemet és egy rasszt reprezentáló érték is; ilyen esetben használható az úgynevezett _interaction_ függvény, mely kombinálja az egyes szinteket - ennek OUTPUT-ja szintén egy faktor lesz, melyben ilyen indexelt elemek vannak
* ha ilyen összevont faktorokkal dolgozunk, akkor sokszor keletkeznek olyan szintek, melyek üresek, ezeket a korábban említett drop argumentum igazra állításával ki tudunk hagyni a végeredményből
* szintén megjegyezendő, hogy ahogyan már korábban említettük lehet faktorok listái szerint hasítani, így ilyen alfaktorok esetén nem feltételenül kell az _interaction_ függvényt használni

## Hiba realizálása
* ugyanúgy, mint a többi programozási nyelvben, R-ben is akkor beszélünk debuggolásról, mikor egy program futása során hibát kaptunk és szeretnénk megtudni, hogy mi is ez a hiba, illetve, hogy hol található a programon belül
* az első kérdés, hogy honnan tudjuk meg, hogy a kódunk hibát tartalmaz
* alapjáraton három különböző szintű jelzést kapunk arról, hogy a programunk hibát tartalmaz
* az első a _message_, mely csak egy szimpla üzenet és melytől függetlenül a programunk ugyanúgy lefut ( az üzenet a message függvény által generálódik )
* a második a _warning_, mely figyelmeztet arra, hogy valami nem feltétlenül úgy történt ahogyan mi szerettük volna ( ez nem biztos, hogy egy probléma ), így ettől függetlenül a program lefut - alapértelmezetten ezt a futtatás után kapjuk meg ( az üzenet a warning függvény által generálódik )
* az utolsó az _error_, mely akkora problémára hívja fel a figyelmet, amely miatt a programot nem lehet lefuttatni, így maga a program is megáll ( az üzenet stop függvény által generálódik )
* ezek mind egy általánosabb koncepció részeit képzik, ezt nevezzük _állapotoknak_; habár ezen a szinten nem jellemző, de lehetőség van további állapotok készítésére, melyek által a saját dolgunkat tudjuk megkönnyíteni
* érdemes megemlíteni az úgynevezett _invisible_ függvényt, melyet arra használunk, hogy amikor egy függvényt meghvíunk és az automatikusan visszaadná az utolsó sorában taláható értéket, mégse tegye meg - azaz kiszámítja azt az értéket amit kell, de nem írja ki meghívás esetén
* fontos, hogy mikor egy függvény meghívása esetén hibaüzenetet kapunk végiggondoljuk a következőket: mi volt  az INPUT; hogyan kell meghívni a függvényt; mi az amit elvársz eredményként; ténylegesen az elvárást elégíti ki a program; tudom e reprodukálni a problémát ( ez a legfontosabb, enélkül nem lehetne megmutatni, hogy így generáltam a hibát )

## Debug függvények
* a következőkben öt ilyen debuggoló függvényt veszünk át - ezeket nem muszáj használni, de néha nagyon jól használhatóak
* az úgynevezett _traceback_ függgvény a konzolon megjeleníti az adott függvény hívási listáját addig a pontig ameddig a hiba fel nem tűnik
* ezt a hiba után kell meghívni közvetlenül, ugyanis a _traceback_ az épp aktuális hibára vonatkozik
* a _debug_ függvény segítségével a debug módba léphetünk át, ahol mindössze arról van szó, hogy az adott függvényünket tudjuk soronként futtatni, így pontosan meg tudjuk határozni, hogy a hiba melyik sorban van
* először meghívjuk a debuggolásra szánt függvénnyel mint argumentummal, majd utána a hibás függvényt és a megjelenő _Browse_ sorba n-eket gépelve ugrálunk sorrol sorra
* van lehetőség a _debug_ függvény meghívása közben egy belső függvényre ugyanúgy meghívni a _debug_ függvényt
* a _browser_ függvény hasonlóan működik az előbbihez, avval a különbséggel, hogy itt egy megadott pontig futtatjuk a függvényt rendesen és majd csak onnan kezdjük el soronként nézni
* a _trace_ függvény segítségével egy adott függvénybe tudunk debug kódot írni anélkül, hogy magát a függvényt teleírnánk ( például akkor lehet használni, mikor nem a saját programunkat akarjuk debuggolni )
* a _recover_ függvény által a hibákat tudjuk alapértelmezettől eltérően kezelni - arra kell gondolni, hogy alapból hiba esetén a program futása félbeszakad és visszatérünk a konzol felületre, a _recover_ által beállítható, hogy a függvény kiértékelése megálljon a hibánál és ne kerüljünk a konzolra
* ez egy globális beállítási lehetőség ( így nem kerülhető el az _options_ függvény használata )
* beállítása után egy kezelőfelületre ugrunk, melyen direkt módon kiválasztható, hogy mely felhasznált függvény környezetét szeretnénk megnézni, ezzel gyorsítva a folyamatot
* persze ezen speciálisan debuggolásra tervezett függvények mellett lehetőség van a hagyomános módszerek használatára is - például mikor teleírjuk print/cat függvényekkel a programunkat
* fontos megjegyezni, hogy a debuggolás nem a szent grál, szóval ugyanúgy kell és érdemes gondolkozni programalkotás közben
