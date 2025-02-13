Asymptotické paměťové a časové složitosti
===

Povídání
---

Předem avizuji. Valnou většinu věcí, včetně příkladů a struktury povídání jsem obšlehl z Průvodce labyrintem algoritmů, deal with it.           
Máme nějaký algoritmus. Je dobrý? Ano? Vážně? A jak to víme? Začneme intuitivně. Jak bychom mohli změřit, zda je nějaký algoritmus efektivní? Jednoduše. Vezmeme si stopky, spustíme algoritmus a změříme si, jak dlouho běží. Ačkoliv to zní nainvně, v praxi se tento přístup opravdu využívá. Nicméně pro náš případ se nechodí. Proč? Rychlost běhu našeho algoritmu bude závislá na programovacím jazyce, na operačním systému, výkonu procesoru a nespočtu dalších faktorů.               
Jak tento problém vyřešíme? Nu, v první řadě zapomeneme na konkrétní implementace algoritmu v programovacím jazyce. Popíšeme ho pouze pseudokódem. Budeme počítač, kolik základních operací algoritmus při každém běhu provádí. Základní operací může být např. zkontrolování podmínky, součet, multiplikace, ... asi máme nějaký obrázek.             
Vezmeme si konkrétní příklad, budeme vypisovat hvězdičky.                
Teď bude nutné se podívat na ukázky kódu, budu na ně totiž referovat. V první otázce pomocí hvězdiček vypisujeme čtverec. Čtverec má velikost n, pro každý sloupec musíme udělat n řádků. Taková funkce tedy vypíše **n^2** hvězdiček.                 
Druhá fce vytváří z hvězdiček schody. Počet vypsaných hvězdiček můžeme odvodit od součtu prvků aritmetické posloupnosti, tedy **n(n + 1)/2**.           
Třetí fce vypisujeme hvězdičku, dokud je n větší než jedna. Při každém vypsání hvězdičky n zmenšíme o polovinu. Projdeme-li cyklus k-krát, sníží se hodnota n na **n/2^k**. Tedy klesá exponenciálně rychle v závislosti na počtu iterací cyklu. Pomocí vyřešení jednoduché rovnice n/2^l = 1, kde l je naše neznámá, dostaneme zhruba dvojkový logaritmus n.               
Čtvrtá a poslední fce to má trochu složitější. Kolik hvězdiček vypíše je závislé na tom, jaké číslo vložíme na začátku. Nelze tedy s přesností odhadnout, kolik hvězdiček skutečně vypíše pro nějaké náhodné číslo. Co budeme dělat? Vyřešíme to jednoduše a intuitivně. Vezmeme v potaz nejhorší možnost, tedy takovou, kdy lichost pokaždé uspěje. Když vynecháme počítání, je to zhruba **n** hvězdiček.                 
Nuže dobrá, analyzujeme si teď, kolik operací musí jednotlivé funkce v jejich průběhu udělat. Samozřejmě máme na mysli vždy nejhorší případ. V prvních třech algoritmech je počet základních operací plus minus 4. Ve čtvrtém o trochu více, tedy 8.   

| Číslo Funkce    | Počet Operací           |
| --------------- | ----------------------- |
| 1               | 4n^2                    |
| 2               | 4n(n + 1)/2 = 2n^2 + 2n |
| 3               | 4log<sub>2</sub>n       |
| 4               | 8n                      |

Nuže, to je počet operací. Ale stále jsme se nedostali k té naší časové složitosti. Teď si ukážeme, jak ji dostaneme.           
Představme si, že n je nějaké hrozně velké číslo, třeba v řádu bilionů. Když se podíváme na první funkci, vidíme, že kvadrát nám způsobí, že naše číslo se opravdu hodně zvětší. Násobení čtyřmi toto číslo jen málo zvětší v poměru ku kvadrátu. Můžeme tak tuto multiplikativní konstantu vypustit.               
Asymptotickou složitost algoritmu zapisujeme následovně: **O(n<sup>2</sup>)**.          
V případě druhého algoritmu uděláme to samé. Dvojka před kvadrátem je multiplikativní konstanta, pryč s ní. Stejné je to u dvojky před n, šup a je pryč. Co uděláme s n? Nu, dobře, opět, jak velké bude n v porovnání n na druhou? Bude o dost menší. Co děláme s čísly, která jsou o dost menší? Zanedbáváme je, takže pryč s ním. Ano, i tato funkce má asymptotickou časovou složitost **O(n<sup>2</sup>)**.

Ukázky kódu
---

**Python - Stars n squared**

**Python - Stars n squared half**

**Python - Stars log n**

**Python - Stars n**

**Python - Measuring time and space complexity**

Materiály
---
