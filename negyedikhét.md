# Negyedik hét

Szimulációk írása, további optimalizálási segítség és egy rövid bevezetés az _str_ függvény használatába és remek tulajdonságaiba.

## Az _str_ függvény
* az egyik legfontosabb Rben használatos függvény, mely segítségével egy adott objektum struktúrújáról tudhatunk meg többet ( az elnevezés a structure kifejezésből jön )
* nagyon sokoldalú - a _summary_ függvény alternatívájaként használható
* meghívás esetén a megadott objektum első sorát is visszaadja, de az alapkérdés melyre használatával választ kaphatunk, hogy mit is tartalmaz az argumentumban szereplő objektum
* ha egy függvény argumentummal hívjuk meg, akkor visszaadja az adott függvény argumentumait, ezek sorrendjét és alapértéküket
* ha egy adathalmazzal hívjuk meg, akkor visszaadja, hogy milyen típusú az adathalmaz, hány megfigyelést tartalmaz és az első pár megfigyelés értékét
* a _summary_hoz képest sokkal kompaktabb kimenetet ad, ami egy nagyon hasznos tulajdonság

## Szimulációk
* különböző eloszlásokból tudunk értékeket megadni ( véletlen számokat, az eloszlásfüggvény értékét egy adott pontban, a sürüségfüggény érétkét egy adott pontban, továbbá az eloszlás kvantilisét egy adott pontban )
* ezek a következő prefixekkel érhetőek el: _p_ - eloszlásfüggvény adott pontban; _d_ - sűrűségfüggvény adott pontban; _q_ - kvantilis adott pontban; _r_ - véletlen számok adott pontban
* ezen prefixek után írjuk az eloszlást meghívó szót - például ez lehet: norm, pois, gamma, binom, ... stb.
* ezen függvényekben az értelemszerű argumentumok mellett ( adott pont, vagy mennyiség; az eloszlás paraméterei ) beállítható, hogy vegyük e az érték logaritmusát, illetve hogy az eloszlásfüggvény bal, vagy jobb farkát tekintsük ( kisebb egyenlő, vagy nagyobb kifejezést vizsgáljuk )
* mikor géppel véltelen számokat generálunk, akkor igazából mégse véletlen számokat kapunk, hanem pszeudo véletlen számokat, így esetlegesen ha szükségünk van arra, hogy egy már korábban legenerált számsorozatot újra legeneráljunk, akkor ezt meg tudjuk tenni - ennek megvalósítására alkalmazható az úgynevezett _set.seed_ függvény
* mivel magát a véletlenszám generálási algoritmust nem ismerem, így csak annyit tudok feljegyezni, hogy ha beállítjuk a generálás méagját egy adott egész értékre ( például _set.seed(1)_ ), majd meghívunk egy véletlenszám generálást és ezt az egész procedúrát újra végrehajtjuk, akkor ugyanazt a véletlenszám szekvenciát kapjuk - mintha a folyamatban visszaugrás után újrakezdtük a volna generálást
* ezen szimulációs lehetőségeket tujduk használni liáris modellek esetén is
* fontos megjegyzeni, hogy létezik egy úgynevezett _sample_ függvény is, mely segítségével adott vektor elemeiből tudunk egy véletlen mintát generálni; több argumnetuma van, melyek a feladatához mérten értelemszerűek
* ha nem adunk meg semmi argumentumot a _sample_ függvénynek, akkor zimplán a megadott vektor elemeinek permutációját kapjuk vissza
* a _sample_ függvény prob argumentumával könnyen tudunk saját eloszlást is generálni - megjegyezve, hogy a megadott prob vektor elemeinek összegének nem kell 1-nek lennie


## Profiler, azaz sebességnövelés
* gyakorlatban előfordulhat, hogy habár a program fut és kiszámolja amit kell, mégis a sebessége miatt nem használható - a következőkben az R-be beépített gyorsítási lehetőségeket és ötleteket nézzük át
* a profiler általánosan egy olyan dolog, amely segítségével meg tudjuk nézni, hogy egy adott program, adott függényei/részei mennyi ideig futnak
* előfordulhat, hogy egy függvény egyszeri futtatása tökéletesen megfelel igényeinknek, de egy adott program keretein belül ezerszer iterálva már cseppet sem optimális megoldás
* viszont az sem egészséges, hogy egy program megalkotása közben azoptimalitás van főszerepben - aranyszabály, hogy először meglegyen a futó/működő porgram és csak uténa koncentráljunk a futásidő optimalizálására
* fontos, hogy a gyorsításhoz szükségünk van annak ismeretére, hogy a program mely részein lassú - ehhez nem meglepően tesztadatra van szükségünk
* az első futásidőt mérő függvényünk a _system.time_ függvény, mely argumentumában a mérendő számolást kifejező R kifejezést írjuk
* ha a megadott kifejezésben hiba szerepel, akkor az időt csak a hibáig méri, továbbá ez a visszaadott érték másodpercben értendő
* ez a visszaadott érték egy úgynevezett proc-time osztályú objektum, melyben több számérték is szerepel; ezek közül az úgynevezett _user time_ adja meg a processzor által felhasznált időt a kifejezés elérésére; míg az _elapsed time_ pedig a tényleges, kifejezés meghívása után, az értékvisszaadásig eltelt idő
* ez a kettő érték viszonylag közeli, de persze bármilyen "felállás" előfordulhat; például az _elapsed time_ várhatóan nagyobb lesz, mint a _user time_, ha a processzor a megadott függvény kiérétkeléséhez további dolgokra vár ( ilyen mikor egy honlapról olvasuk ki dolgokat ); viszont a fordított eset is bekövetkezhet ha a programban van párhuzamosítás ( a többmagos processzort kihasználja - szinguláris értékek számolása mehet párhuzamosan, szóval az ilyen lesz )
* megjegyezendő, hogy alapjáraton az R nyelv nem használ több magot egyszerre, de van lehetőség ilyen könyvtárak ( _BLAS_ ) használatára az R-en belül, illetve létezik egy úgynevezett _parallel_ package, mely segítségével szintén a többmagosságot lehet kihasználni
* a _system.time_ függvényben érhetünk hosszabb kifejezéseket is, egyszerűen bepakoljuk egy kapcsos zárójelbe az egészet
* a gond evvel a fügvénnyel az, hogy csak eglsz programok futásidejét tudjuk megnézni - azt, hogy konkrétan mely részein lassú a programunk azt már nem
