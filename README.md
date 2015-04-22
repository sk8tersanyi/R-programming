# R programozás

## Első hét
Az első hét anyagát nem írom le, mivel már tudom azokat, de majd ha lesz időm lehet, hogy a lényegesebbeket beleillesztem

## Második hét
Alapvető függvények használata, illetve különleges tulajdonságai.

### IF-ELSE függvény
* az _else_-t nem szükségszerűen kell használni, de ha használjuk, akkor az _if_-et lezáró kapcsos zárójel után kell írni
* értelemszerűen van _if else_ használati lehetőség is, ha több opció lehetséges
* az ami különleges az eddigi tapasztalatomhoz képest, hogy lehet egy ilyen _if-else_ kifejezéssel rögtön értéket adni
<blockquote>
  <p> y <- if(x > 3) { 10 } else { 0 }</p>
</blockquote>

### FOR ciklus
* indexeken tudunk ugrálni - ahogyan azt már megszokhattuk
* viszont van lehetőség rögtön indexek nélkül az elemeken végigmenni - pont ezért nem használok *i* indexet, hogy ezt rendesen szemléltessem:
<blockquote>
  <p> x <- c("a", "b", "c", "d") </p>
  <p> for(letter in x) { print(letter) } </p>
</blockquote>
* a *seq_len()* függvénnyel lehet rögtön olyan hosszú ciklust hívni amekkora kell

### WHILE ciklus
* megszokottnak megfelel
* a feltételek mindig balról jobbra értékelődnek ki !!!!!!!!!!!!!!!!!!

### REPEAT, BREAK, NEXT függvények
* a _repeat_ függvény végtelen ciklus generálására használható ( például konvergencia feltevések megsejtésére )
* egyedül a _break_ segítségével tudunk kilépni a ciklusból
* nem érdemes használni, mivel ha nincs például konvergencia, akkor nem fog figyelmeztetni, hogy nem áll meg soha - inkább egy nagy iterációszámú _for_ ciklust használjunk
* a _next_ függvénnyel iterációkat tudunk átlépni - ahogyan azt megszokhattunk
* a _return_ függvénnyel függvényekből tudunk kilépni - ahogyan azt megszokhattuk


Ha egy függvényen belül csak egy utasítás van, akkor a kapcsos zárójelek elhagyhatóak. Fontos megjegyezni, hogy ezeket az alapfüggvényeket főleg akkor használjuk, mikor függvénykeet írunk. Ha parancssorból akarunk bármit is csinálni, akkor érdemes használni a majd későbbiekben taglalt _apply_ függvényt.

### Függvények írása

* nem szükséges a _return_ -t használni a visszaadandó értéknél, ugyanis az utolsó sorban található kifejezés lesz a visszatérési érték automatikusan
* egy függvény adott paraméterének tudunk alapértéket adni, azaz, ha a felhasználó nem adja meg a szükséges értéket, akkor a megadott alapérték mellett történik a függvény futtatása - ezt a következőképp lehet megtenni ( a példafüggvény visszaadja egy vector n-nél nagyobb elemeit, ahol n alapértéke 10 lesz ):
<blockquote>
  <p> above <- function(v, n = 10) { v[v > n] } </p>
</blockquote>
* az eddigiekhez hasonlóan, a függvények szintén, mint objektumok vannak eltárolva
* továbbá ugyanúgy, mint az összes többi programozási nyelvben a függvények itt is _"first-class-object"_-ként vannak eltárolva, ami annyit tesz, hogy képesek vagyunk egy függvény argumentumába függvényt meghívni
* beszélhetünk úgynevezett _formal_ argumentumokról is, melyek nem mások, mint azon argumentumok, melyeket a függvényben be tudunk állítani - tetszőleges függvény formális argumentumainak listáját a _formals_ függvénnyel tudjuk megtekinteni ( ha van _default_ értékes argumentum is, akkor annak kiírja a alapértelmezett értékét is
* emellett az _args_ függvénnyel is megtehető ugyanez - ha minden igaz itt a sorrend óet is megtartja a kiírás során
* függvény változóinak megadás kétféleképp ( hely, illetve név szerint ) lehetséges
* előfordulhat, hogy egyes változókra nevükkel, másokra pedig helyzetük alapján hivatkozunk a függvényen belül, ekkor a helyzet szerintiek sorrendje úgy alakul, hogy melyekre a nevükkel hivatkoztunk kiesik a listából és a megmaradtak közül a soron következő lesz hely szerint hivatkozható
* ha egy függvény argumentumában nincs feltüntetve alapértelmezett érték, akkor hívás esetén azt mindenképp meg kell adni - nélküle _error_-t kapunk vissza
* akkor érdemes név szerint hívni változót, ha a függvény legtöbb változóját mint alapértelmezett érték használjuk és amit felülírnánk az pedig nem az első helyen van - például az ábrázoló függvényeknél, ugyanis itt rengeteg beállítási lehetőségünk van
* megtörténhet az is, hogy nem emlékszünk az egyes változó nevére, ekkor sem kell elkeseredni, ugyanis van lehetőség részleges név szerinti egyezéssel definiálni egy változót a függvényben
* összegezve, egy függvényen belül az argumentumokat úgy nézi át a program, hogy először megnézni név szerint hol van teljes egyezés - ezeket ekkor értelemszerűen felülírja, ezután megnézi a részleges név szerinti egyezést, majd a pozíció szerintit
* ugyanúgy. mint a legtöbb programnyelve esetén, itt is lehetőségünk van _lusta kiértékelés_-re, ami annyit jelent, hogy ha egy függvényben, egy adott változót nem használunk fel ( a függvény definíciója során ), akkor meghívás esetén nem szükségszerű értéket adni neki
* persze ha kihagyunk egy olyan változót melyet a definíció során felhasználtunk, akkor a függvény meghívása során addig értékelődik ki amíg az őt tartalmazó sorig el nem jutottunk, aztán egy hibaüzenettel megáll a futás
* érdekes függvény argumentum az úgynevezett _..._ argumentum, melyet elsősorban arra használunk, hogy feltüntessünk olyan változókat, melyek még ott vannak, de nem szükségszerű definiálni őket - például ha egy már megírt függvény alapértelmezett értékeinek változtatásával szeretnénk egy új függvény írni ( felhasználva a már elkészültet ) akkor a következőt írhatjuk:
<blockquote>
  <p> myplot <- function(x, y, type = "l", ...) { plot(x, y, type = type, ... } </p>
</blockquote>
* továbbá akkor is ezt használjuk, mikor a függvényünknek előre nem meghatározható számú bemenő változója van - ilyen lehet a stringek összefűzésére használt _paste_ függvény
* sőt amikor csak megnézzük, hogy egy egy függvénym ilyen metódusokat használ, akkor is van szerepe - ez majd később lesz!
* nagyon fontos megjegyezni, hogy minden _..._ argumentum után szereplő változó nevére csak és kizálóag teljes név alapján lehet hivatkozni!!!!!

### Túlterhelés
* a kérdés a következő, ha van két azonos nevű függvényünk, akkor honnan tudja a program, hogy aktuálisan melyik függvényt hívjuk meg - nem meglapően az az ötelt, hogy miden szimbólumhoz egy-egy értéket értéket rendelünk, így itt is az történik, hogy a megfelelő helyen keressük a megfelelő értéket
* gyakorlatban ez a keresési lista - hogy a program milyen sorrendben nézi végig az eléhető helyeket - a _search_ függvény segítségével tekinthető meg
* a lista első eleme mindig a _global environment_ míg az utolsó pedig az alapfüggvényeket tartalmazó _base_ package
* amennyiben egy felhasználó új csomagot hív meg, akkor az a keresési listában a második helyet foglalja majd el, a többi ( a global environment-et kivéve ) pedig eggyel lejjebb csúszik
* fontos megjegyezni, hogy a függvény  és nemfüggvény objektumok elkülönülő környezetben találhatóak, így meg lehet tenni hogy egy szimpla változónak olyan nevet adunk ami már egy függvényt reprezentál

### Változók hatásköre
* a probléma a követketkező, minden függvényben szerepelhetnek úgynevezett _szabad változók_, azaz olyan változók, melyek a függvény argumentumába nincsenek feltüntetve, egy ilyen esetén hogyan találja meg a program a nei szánt megfelelő értéket - az alábbi példában z a szabad változó
<blockquote>
  <p> f <- function(x, y) { x^2 + y / z } </p>
</blockquote>
* akkor beszélhetünk _lexikus, vagy statikus hatáskör_-ről egy szabad változó esteén, ha annak értékét azon függvény környezetében keressük, ahol az a változó definiálva volt
* a _környezet_ alatt (szimbólum, érték) párok gyűjteményét értjük, továbbá minden ilyen _környezet_-enk létezik egy _szülő környezet_-e, mely úgymond tartalmazza azt
* előfordulhat, hogy egy környezetnek több gyereke van, de minden környezetnek csak egy szülője lehet
* egyedül csak az _üres környezet_-nek nem létezik szülő környezete
* az egyes _package_-ek _namespace_-ei is környezetet alkotnak
* _closure_ = _function_ + _environment_ - ez fontos struktúra, amit érdemes megjegyezni
* térjünk vissza arra, hogyan is keresi egy ilyen szabad váltzó értékét a program - először megnézi a függvényt tartalmazó környezetben, ezután ennek a szülő környezetében, és így tovább, amíg el nem érjük a legfelső szinten található környezetet, ami általában a _global environment_, vagy az adott package namespace-e
* ha ezen legfelső szinten lévő környezetekben sem találjuk a megfelelő értéket akkor a mér korábban említett _search_ listában a sorrendben következő elemre ugrunk; ezt az egészet addig iterájuk, míg el nem érjük az üres környezetet - ha itt sem találjuk meg a megfelelő értéket, akkor a programunk hibaaüzenetet fog adni
* felmerülhet a kérdés, hogy mégis mi az értelme ennek az egésznek - előfordulhat hogy egy függvény visszatérési értéke szintén egy függvény, és így az a környezet ahol a függvény definiálva van nem a globális környezet lesz
<blockquote>
  <p> make.power <- function(n) {  </p>
  <p>       pow <- function(x) {x^n} </p>
  <p>       pow }   </p>
</blockquote>
* ezen példában szereplő hatvány függvénnyel úgy tudunk egy négyzetre emelést végrehajtó függvényt készíteni, hogy:
<blockquote>
  <p> square <- make.pow(2) </p>
</blockquote>
* egy adott függvény környezetének lekérdezése az _environment_ függvény segítségével történik
* további programozási nyelvek esetén beszélhetünk _dinamikus hatáskör_-ről is - ez alatt azt kell érteni, hogy egy függvényben szereplő szabad változó értékét NEM abban a környezetben keressük, ahol a függvény definálva volt, hanem ahol meghívtuk ( ezen környezetet _meghívó környezetnek_ szokás nevezni, R esetén _parent frame_-nek )
<blockquote>
  <p> y <- 10 </p>
  <p> f <- function(x) {y <- 2; y^2 + g(x)} </p>
  <p> g <- function(x) {x*y} </p>
</blockquote>
* _lexikus hatáskör_ esetén y értéke 10 lesz, míg _dinamikus hatáskör_ esetén pedig 2
* előfordulhat, hogy egy függvényt a globális környezetben definiálunk, majd később innen is hívjuk meg, ekkor olyan mintha dinamikus hatáskörrel lenne dolgunk
* ennek az egésznek az értelme abban rejlik, hogy a nagy adathalmaz miatt nagyon sok memóriát kéne felhasználni akár egyszerű műveletek elvégzésére, így ennek segítségével tudunk spórolni, továbbá mivel minden függvényt pointerekkel hivatkozunk, így további komplexitásokat tudunk elkerülni

### Optimalitás
* az eddig elmondottak szerepe akkor lesz igazán nyilvánvaló, ha valamilyen statisztikai probléma megoldása esetén az optimalitási dolgok is bekürlnek a buliba
* pár R-ben található optimalizáló rutin: _optim_, _nlm_, _optimize_; ezek paraméternek egy függvényt kapnak meg, mely argumentuma egy vektor és adott intervallumban próbálják megkeresni a szükséges paraméterre vonatkozó minimumot, illetve maximumot
* statisztikában előfordulhat, hogy a az optimalizálandó célfüggvény maximuma/minimuma nem csak a paramétertől, hanem példauál magától az adathalmaztól is függ - így felmerül a probléma, hogy hogyan lehetne ez jól átláthatóan megvalósítani
* az első fontos gondolat, hogy eltároljuk azon paramétereket melyek fixek az optimalizálás során - ezt tesszük az úgynevezett _konstruktor_ segítségével, melyet itt úgy használunk, hogy a fixált paramétereket megadjuk, így a tényleges meghívás esetén a tárgyfüggvényben már ezeket ne mkell újra megadni
* R-ben minden optimalizáló függvény minimumot számít, így maximum számításához mínusz eggyel kell szorozni!!!!!
* azaz a korbbi hatáskör tulajdonságok miatt lehetőségünk van olyan olyan függvényeket generálni konstruktorokkal, melyek a fixált értékeket már alapból tartalmazzák, így például optimalizálás eseén nem kell mindent megint újra bevinni ( nem lesznek hosszú argumentum listák )
* Robert Gentleman & Ross Ihaka - Lexical Scope and Statistical Computing (2000): https://www.stat.auckland.ac.nz/~ihaka/downloads/lexical.pdf

### Kódolási sztenderd
* a könnyebb áttekinthetőség értelmében érdemes pár kinézetre vonatkozó, alapvető programozási szabályt - ezek szubjektív dolgok - betartani
* az első, hogy a kódot mindig valamilyen text fájlba csináljuk, például RStudio esetén erre a célra tökéletesen megfelel az a felület ahova a szkript fájlunkat írjuk
* a második, hogy próbáljunk meg nagyobb bekezdéstávolságokat használni - érdemes négynél több karakterre gondolni - ez RStudio esetén az Options opció alatt érhető el
* a harmadik, hogy korlátozzuk a sorok hosszát, azaz kizárjuk annak a lehetőségét, hogy átláthatatlanul hosszú kódokat írjunk - ennek alapértelmezett érték 80 oszlop RStudio-ban
* a negyedik, hogy korlátozzunk az egyes függvények sorainak számát
* ha nagy bekezdésekkel dolgozunk, akkor átértékeljük az egymásba ágyazott ciklusok használatát, ami alapjáraton egy jó dolog
* a függvényeink neve ténylegesen a működésüket reprezentálja!
* a program különböző részet taglaljuk jól, így nem csak az átlthatóságot növeljük, hanem debuggolásben is segíthet

### Dátum és Idő
* R-ben külön osztály van a dátumok reprezentálására, ez nem más mint a _Date_ 
* míg az idő reprezentálására két osztályt használhatunk, ezek: _POSIXct_ és _POSIXlt_
* dátumok és idők eltárolásá az 1970 január 1. időponttól történik, mint egynumerikus érték, mely dátum esetén az eltelt napok számát reprezentálja, idő esetén pedig az eltelt másodpercek számát
* az _as.Date_ függvény segítségével tudunk YMD formátumban megadott dátum sztringeket dátummá konvertálni
* a _POSIXct_ formátumot használjuk idő tárolására abban az esetben, ha data frame-re van szükségünk - ekkor az időt reprezentáló egész szám nagyon nagy érték
* míg ezzel szemben a _POSIXlt_ formátum az idő listában tárolja, ahol ezen lista olyan további hasznos információkat is tartalmaz, mint, hogy az adott dátum napja a hét melyik napjár esett, vagy hányadik napja volt az adott évnek
* sok úgynevezett _generikus függvény_ ( azt nevezzük generikusnak melynek több típusa is lehet ) is van dátumokra és időre, ilyen például a _weekday_, mely megadja hogy az adott nap a hét melyik napjára esett, vagy a _month_, mely visszaadja az adott számmal reprezentált hónap nevét, ... stb
* tudunk típuskonverziót használni idő esetén is, ez nem meglepően az _as.POSIXlt_ és _as.POSIXct_ függvényekkel történik
* ahhoz hogy le tudjuk kérdezni az a _POSIXlt_-ben tárolt plusz információkat, a megadott időre alkalmazzuk az _unclass_ függvényt, ezután a $ jel segítségével tudunk hivetkozni az időt leíró adatokra, mint ahogyan azt egy listától el lehet várni
* ha szeretnénk kölünböző sztring formátumban megadott dátumokat azonos ( _POSIXct, vagy _POSIXlt_ ) formátumúra hozni, akkor erre a célra használhatjuk az _strptime_ függvényt - a formális argumentumok jelentése a help segtségével megnézhető
* különböző osztályokból származtatott dátumok és idők között nem lehet műveleteket végezni, így minden művelet előtt érdemes típuskonverzót végrehajtani
* azért érdemes ezeket a beépített függvényeket használni, mivel nagyon jól kezelik azokat a bajos dolgokat, mint a szökőéve, téli-nyári időszámítás és időzóna fogalma
* érdemes megnézni, hogy dátum objektumok ábrázolását milyen jól kezeli az R

## Harmadik hét
Az úgynevezett _ciklus függvények_ ( _loop functions_ )  - mintha valami ciklust csinálnának meg kompakt formában, így akár konzolról is können szerkezthető - használata és tulajdonságai, továbbá alapvető debuggolás.

### _lapply_ függvény
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

### _sapply_ függvény
* az előbb taglalt _lapply_ függvény által visszaadott OUTPUT-ot egyszerűsíti, amennyiben ez persze lehetséges
* ha az _lapply_ függvény eredménye egy olyan lista, mely minden eleme egy hosszú, akkor ha az _sapply_ függvényt használjuk, egy vektort kapunk vissza
* amennyiben az _lapply_ függvény eredménye egy olyan lista, mely minden eleme azonos hosszú vektor, akkor ha az _sapply_ függvényt használjuk, egy mátrixot kapunk vissza
* persze ha nem tudja elvégezni ezeket az egyszerűsítéseket, akkor az _lapply_-hoz hasonlóan listát ad vissza

### _apply_ függvény
* az _apply_ függvény egy olyan ciklus függvény, mellyel egy tömb indexein tudunk függvényeket kiértékelni
* ez a tömb leggyakrabban egy mátrix és így ennek indexei nem mások, mint a mátrix sorai, illetve oszlopai - emellett van lehetőség általánosabb ( magasabb dimenziós ) tömbök indexein számolni
* a közhiedelemmel ellentétben használata nem azért ajánlott, mert gyorsabb, mint egy ciklus, hanem mert kevesebbet kell gépelni ( régen volt csak igaz!!! )
* négy argumentuma van: az első maga a tömb; a második egy egész értékű vektor mellyel meghatározzuk, hogy a tömb mely dimenzióin akarunk függvényt alklamazni; a harmadik a kiértékelendő függvény; míg a negyedik egy a korábbiakból értelemszerűen következő ... argumentum, melyben az előbbi függvény további paramétereit tudjuk beállítani
* legegyszerűbb - két dimenziós - esetben úgy kell elképzelni, hogy az _apply_ függvény második változójában adjuk meg, hogy melyik dimenzió az amit rögzítünk, azaz ha 1-et írunk, akkor a mátrix soarira fogjuk kiértékelni a megadott függvényt
* fontos megjegyezni, hogy ebben a speciális esetben, ha összeget, vagy átlagot akarunk számolni, nem érdemes az _apply_ függvényt használni, ugyanis vannak futási időben optimalizált beépített függvényeink erre a célra, melyek nevei értelemszerűek: _rowSums_, _rowMeans_, _colSums_, _colMeans_. ( ezek sebbességbeli éltérése nagy adathalmaz esetén látható !! ) - ugyanezen függvények magasabb dimenzióban is működnek !!!
* többdimenziós tömbökre való alkalmazásnál érdemes lenne átgondolni, hogy hogyan is "néz ki" az összegzés

### _mapply_ függvény
* a korábban taglalt _lapply_ és _sapply_ ciklus függvények többváltozós általánosítása, ahol a többváltozós alatt azt kell érteni, hogy a kiértékelendő függvény több argumentummal rendelkezik és ezen értékeket különböző listákban tároljuk
* lehetne FOR ciklussal is, de ha az _mapply_-t használjuk akkor párhuzamosan dolgozunk, ami elég jó
* négy argumentuma van: az elsőben adjuk meg a kiértékelendő függvényt; a második egy ... argumentum, melyben ez egyes megadandó argumentumoknak megfelelő mennyiségű listát adhatjuk meg; a harmadik ( MoreArgs ) argumentumban a kiértékelendő függvény egyéb paramétereinek listáját adhatjuk meg; míg negyedik ( SIMPLIFY ) argumentumban azt ,hogy az output milyen tipusú legyen ( ugyanaz történik, mint _sapply_-nál ) - még van egy ötödik, mely az OUTPUTlistájának neveire vonatkozó logikai változó
* ezekből kiderül, hogy megint arról van szó, hogy szeretnénk kevesebbet gépelni - például, az első helyett érdemes a másodikat használni:
<blockquote>
  <p> list(rep(1,4), rep(2,3), rep(3,2), rep(4,1)) </p>
  <p> mapply(rep, 1:4, 4:1) </p>
</blockquote>

### _tapply_ függvény
* ezzel a ciklus függvénnyel vektorok részvektorain - azaz elemeinek részosztályain - tudunk függvényeket kiértékelni
* öt argumentuma van: az első az a vektor melyen a számítást végezzük; a második, az elsővel megegyező hosszúságú faktor, mely az egyes csoportok elemeit reprezentálja; a harmadik a kiértékelendő függvény; a negyedik a szokásos ... argumentum; míg az  utolsó ( simplify ) az eredmény egyszerűsítését meghatározó logikai változó ( mint az _sapply_-nál ) 
* ha az egyszerűsítést nem állítjuk be, akkor az eredményt egy listában kapjuk vissza, ahol e lista nevei pont a megfelelő faktorok szintjei lesznek

### _split_ függvény
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

### Hiba realizálása
* ugyanúgy, mint a többi programozási nyelvben, R-ben is akkor beszélünk debuggolásról, mikor egy program futása során hibát kaptunk és szeretnénk megtudni, hogy mi is ez a hiba, illetve, hogy hol található a programon belül
* az első kérdés, hogy honnan tudjuk meg, hogy a kódunk hibát tartalmaz
* alapjáraton három különböző szintű jelzést kapunk arról, hogy a programunk hibát tartalmaz
* az első a _message_, mely csak egy szimpla üzenet és melytől függetlenül a programunk ugyanúgy lefut ( az üzenet a message függvény által generálódik )
* a második a _warning_, mely figyelmeztet arra, hogy valami nem feltétlenül úgy történt ahogyan mi szerettük volna ( ez nem biztos, hogy egy probléma ), így ettől függetlenül a program lefut - alapértelmezetten ezt a futtatás után kapjuk meg ( az üzenet a warning függvény által generálódik )
* az utolsó az _error_, mely akkora problémára hívja fel a figyelmet, amely miatt a programot nem lehet lefuttatni, így maga a program is megáll ( az üzenet stop függvény által generálódik )
* ezek mind egy általánosabb koncepció részeit képzik, ezt nevezzük _állapotoknak_; habár ezen a szinten nem jellemző, de lehetőség van további állapotok készítésére, melyek által a saját dolgunkat tudjuk megkönnyíteni
* érdemes megemlíteni az úgynevezett _invisible_ függvényt, melyet arra használunk, hogy amikor egy függvényt meghvíunk és az automatikusan visszaadná az utolsó sorában taláható értéket, mégse tegye meg - azaz kiszámítja azt az értéket amit kell, de nem írja ki meghívás esetén
* fontos, hogy mikor egy függvény meghívása esetén hibaüzenetet kapunk végiggondoljuk a következőket: mi volt  az INPUT; hogyan kell meghívni a függvényt; mi az amit elvársz eredményként; ténylegesen az elvárást elégíti ki a program; tudom e reprodukálni a problémát ( ez a legfontosabb, enélkül nem lehetne megmutatni, hogy így generáltam a hibát )

### Debug függvények
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
