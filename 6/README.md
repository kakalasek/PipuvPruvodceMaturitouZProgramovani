# Asymptotické paměťové a časové složitosti

## Povídání

Předem avizuji. Valnou většinu věcí, včetně příkladů a struktury povídání jsem obšlehl z Průvodce labyrintem algoritmů, deal with it.  
Máme nějaký algoritmus. Je dobrý? Ano? Vážně? A jak to víme? Začneme intuitivně. Jak bychom mohli změřit, zda je nějaký algoritmus efektivní? Jednoduše. Vezmeme si stopky, spustíme algoritmus a změříme si, jak dlouho běží. Ačkoliv to zní nainvně, v praxi se tento přístup opravdu využívá. Nicméně pro náš případ se nechodí. Proč? Rychlost běhu našeho algoritmu bude závislá na programovacím jazyce, na operačním systému, výkonu procesoru a nespočtu dalších faktorů.  
Jak tento problém vyřešíme? Nu, v první řadě zapomeneme na konkrétní implementace algoritmu v programovacím jazyce. Popíšeme ho pouze pseudokódem. Budeme počítač, kolik základních operací algoritmus při každém běhu provádí. Základní operací může být např. zkontrolování podmínky, součet, multiplikace, ... asi máme nějaký obrázek.  
Vezmeme si konkrétní příklad, budeme vypisovat hvězdičky.  
Teď bude nutné se podívat na ukázky kódu, budu na ně totiž referovat. V první otázce pomocí hvězdiček vypisujeme čtverec. Čtverec má velikost n, pro každý sloupec musíme udělat n řádků. Taková funkce tedy vypíše **n^2** hvězdiček.  
Druhá fce vytváří z hvězdiček schody. Počet vypsaných hvězdiček můžeme odvodit od součtu prvků aritmetické posloupnosti, tedy **n(n + 1)/2**.  
Třetí fce vypisujeme hvězdičku, dokud je n větší než jedna. Při každém vypsání hvězdičky n zmenšíme o polovinu. Projdeme-li cyklus k-krát, sníží se hodnota n na **n/2^k**. Tedy klesá exponenciálně rychle v závislosti na počtu iterací cyklu. Pomocí vyřešení jednoduché rovnice n/2^l = 1, kde l je naše neznámá, dostaneme zhruba dvojkový logaritmus n.  
Čtvrtá a poslední fce to má trochu složitější. Kolik hvězdiček vypíše je závislé na tom, jaké číslo vložíme na začátku. Nelze tedy s přesností odhadnout, kolik hvězdiček skutečně vypíše pro nějaké náhodné číslo. Co budeme dělat? Vyřešíme to jednoduše a intuitivně. Vezmeme v potaz nejhorší možnost, tedy takovou, kdy lichost pokaždé uspěje. Když vynecháme počítání, je to zhruba **n** hvězdiček.  
Nuže dobrá, analyzujeme si teď, kolik operací musí jednotlivé funkce v jejich průběhu udělat. Samozřejmě máme na mysli vždy nejhorší případ. V prvních třech algoritmech je počet základních operací plus minus 4. Ve čtvrtém o trochu více, tedy 8.

| Číslo Funkce | Počet Operací                     |
| ------------ | --------------------------------- |
| 1            | 4n<sup>2</sup>                    |
| 2            | 4n(n + 1)/2 = 2n<sup>2</sup> + 2n |
| 3            | 4log<sub>2</sub>n                 |
| 4            | 8n                                |

Nuže, to je počet operací. Ale stále jsme se nedostali k té naší časové složitosti. Teď si ukážeme, jak ji dostaneme.  
Představme si, že n je nějaké hrozně velké číslo, třeba v řádu bilionů. Když se podíváme na první funkci, vidíme, že kvadrát nám způsobí, že naše číslo se opravdu hodně zvětší. Násobení čtyřmi toto číslo jen málo zvětší v poměru ku kvadrátu. Můžeme tak tuto multiplikativní konstantu vypustit.  
Asymptotickou složitost algoritmu zapisujeme následovně: **O(n<sup>2</sup>)**.  
V případě druhého algoritmu uděláme to samé. Dvojka před kvadrátem je multiplikativní konstanta, pryč s ní. Stejné je to u dvojky před n, šup a je pryč. Co uděláme s n? Nu, dobře, opět, jak velké bude n v porovnání n na druhou? Bude o dost menší. Co děláme s čísly, která jsou o dost menší? Zanedbáváme je, takže pryč s ním. Ano, i tato funkce má asymptotickou časovou složitost **O(n<sup>2</sup>)**.  
Ano, vždy budeme brát v potaz jen počet operací na tu nejvyšší mocninu. Ta bude vždy suverénně největší.  
U třetího algoritmu provedeme ty samé změny. Čtyřka jde pryč. Zůstává nám log<sub>2</sub>n. Ten provedeme jednu věc, která může matematiky trochu bolet. Log(n) máme asociovaný s desítkovým logaritmem, že? No, tak protože v programování zpravidla najdeme logaritmy o základu dvou, píšeme Log(n) a máme na mysli dvojkový logaritmus. Správně. Štve vás to? Vaří se vám z toho krev v žilách? Že ne .. mně jo, jsem asi divnej, nevadí. Každopádně to tak je, složitost této funkce je tedy **O(log*n*)**.  
U poslední funkce je to analogický proces. Složitost nám vyjde lineární, tedy **O(n)**.  
Nuže, výsledné asymptotické časové složitosti nám vyjdou následovně:

| Číslo Funkce | Asymptotická časová složitost |
| ------------ | ----------------------------- |
| 1            | n<sup>2</sup>                 |
| 2            | n<sup>2</sup>                 |
| 3            | log*n*                        |
| 4            | n                             |

Teď si tedy ujasníme, jak uvařit asymptotickou časovou složitost algoritmu. Dle průvodce labyrintem algoritmů postupujeme následovně:

1. Ujasníme si, jak se měří velikost vstupu
2. Najdeme přesný, nebo nejlepší horní odhad maximálního počtu elementárních operací algoritmu provedených na vstupu o velikosti n
3. Ve výsledné formuli necháme nejrychleji rostoucí člen a ostatní zanedbáme
4. Seškrtnáme multiplikativní konstanty. Ale opravdu jenom ty, pokud je něco třeba v exponentu, neškrtat!

Podíváme se ještě na nějaké běžné složitosti algorimu. Pro zajímavost, funkce o konstantním čase se zapisuje jako O(1).

| Funkce        | n = 10 | n = 100             | n = 1000             | n = 10 000            |
| ------------- | ------ | ------------------- | -------------------- | --------------------- |
| log*n*        | 1      | 2                   | 3                    | 4                     |
| n             | 10     | 100                 | 1000                 | 10 000                |
| *n*log*n*     | 10     | 200                 | 3000                 | 40 000                |
| n<sup>2</sup> | 100    | 10 000              | 10<sup>6</sup>       | 10<sup>6</sup>        |
| n<sup>3</sup> | 1000   | 10<sup>6</sup>      | 10<sup>9</sup>       | 10<sup>12</sup>       |
| 2<sup>n</sup> | 1024   | asi 10<sup>31</sup> | asi 10<sup>310</sup> | asi 10<sup>3100</sup> |

Tak a pro zajímavost si ukážeme i jak dlouho by takové algoritmy opravdu běželi na moderním počítači. Alespoň přibližně, uvažujeme-li zhruba 10<sup>9</sup>:

| Funkce        | n = 10   | n = 100             | n = 1000             | n = 10 000            |
| ------------- | -------- | ------------------- | -------------------- | --------------------- |
| log*n*        | 1 ns     | 2 ns                | 3 ns                 | 4 ns                  |
| n             | 10 ns    | 100 ns              | 1 $\mu$s             | 10 $\mu$s             |
| *n*log*n*     | 10 ns    | 200 ns              | 3 $\mu$s             | 40 $\mu$s             |
| n<sup>2</sup> | 100 ns   | 10 $\mu$s           | 1 ms                 | 0.1 s                 |
| n<sup>3</sup> | 1 $\mu$s | 1 ms                | 10 s                 | 16.7 min              |
| 2<sup>n</sup> | 1 $\mu$s | 10<sup>24</sup> let | 10<sup>303</sup> let | 10<sup>3093</sup> let |

Z tabulky je hezky vidět, že algoritmus s exponenciální složitostí je pro větší počet prvků naprosto nepoužitelný.          

Další je paměťová složitost algoritmu. Ta vypadá analogicky k té časové. Jen s tím rozdílem, že místo času měříme prostor, který algoritmus v paměti zabere. Dobrý příkladem je např. libovolný jednoduchý třídící algortimus, třeba Bubble sort, vs. třídění sléváním. Bubble sort pracuje stále na jednom poli. Toto pole zabírá v paměti stále konstantní velikost. Paměťová složitost bublinkového třídění je tedy O(1). Na druhou stranu při třídění sléváním musíme vytvářet jednotlivá podpole. Počet těchto polí roste lineárně s počtem prvků v poli, takže třídění sléváním má paměťovou složitost O(n).

## Ukázky kódu

**Python - Stars n squared**

```Python
def star_square(n: int) -> None:
    for i in range (0, n):
        for j in range (0, n):
            print("*", end=' ')
        print()

star_square(10)
```

**Python - Stars n squared half**

```Python
def star_stairs(n: int) -> None:
    for i in range (0, n):
        for j in range (0, i): 
            print("*", end=' ')
        print()

star_stairs(10)
```

**Python - Stars log n**

```Python
def star_lower_by_half(n: int) -> None:
    while n >= 1:
        print('*', end=" ")
        n = n/2


star_lower_by_half(16)
```

**Python - Stars n**

```Python
def stars_if_odd(n: int) -> None:
    while n > 0:
        if n % 2 == 1:
            for i in range(0, int(n)):
                print('*', end=" ")
        n = n/2


stars_if_odd(7)
```

**Python - Measuring time and space complexity**

## Materiály

Martin Mareš a Tomáš Valla - Průvodce labyrintem algoritmů - https://pruvodce.ucw.cz/static/pruvodce.pdf

- **Kapitola 2** Časová a prostorová složitost
