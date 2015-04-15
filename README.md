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
