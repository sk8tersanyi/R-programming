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
*
