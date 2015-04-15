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
* viszont van lehetőség rögtön indexek nélkül az elemeken végigmenni, ekkor a porgramkód így nézhet ki:
<blockquote>
  <p> x <- c("a", "b", "c", "d") </p>
  <p> for(letter in x) { print(letter) } </p>
</blockquote>


* ha egy függvényen belül csak egy utasítás van, akkor a kapcsos zárójelek elhagyhatóak

