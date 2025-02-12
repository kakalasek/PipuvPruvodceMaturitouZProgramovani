Algoritmizace - Rekurze, Brute Force, Heuristiky, Nedeterministické algoritmy
===

Povídání
---

Jdeme se podívat na další zajímavou otázku o algoritmizaci. Tentokrát si ale dáme pohov od grafů a jejich prohledávání a čekají nás trochu obecnější algoritmy, nebo spíše metody jejich tvoření.       
Začneme hned u rekurze, se kterou jsme se již setkali v minulé otázce, konkrétně třeba u DFS a třídění sléváním. Když to povím naprosto bez omáčky okolo, rekurze stojí na tom, že nějaká metoda či fce volá sama sebe. Jo, to je opravdu všechno, čekali jste něco komplexnějšího?             
Nicméně právě tento tríček nám dovoluje vytvářet velmi zajímavé algoritmy. Já jsem v ukázkách uvedl jen velmi jednoduchý algoritmus na rekurzivní umocňování, ale pro demonstraci nám postačí.          
Každá rekurze potřebuje nějakou podmínku, pod kterou se zastaví a místo dalšího volání sama sebe, fce vrátí konkrétní hodnotu.              
Z první otázky víme, že existuje zásobník volání metod (Call Stack). Každé další rekurzivní volání je přidání na call stack a shora vykonáváno. Takže když poslední metoda vrátí jedničku, zpracuje ji metoda, která ji volala, a její výsledek pak zpracuje metoda, která ji zavolala a tak dále a tak dále, než se dostaneme k metodě, která nebyla zavolána rekurzivně, ale byla zavolána někde v hlavním kódu a ta vrátí konečný výsledek.              
Rekurzivní algoritmy často mívají specifické vlastnosti nebo nám dovedou zjednodušit či zrychlit řešení problému. Jednou evidentní nevýhodou je velká spotřeba paměti. Každé další volání je přidáno na vrchol zásobníku. Pokud se opravdu hodně zanoříme, může nám také jednoduše přetéct (Stack Overflow).            

![Lock](lock.avif)

Podíváme se na jednoduchý problém. Potřebujeme zjistit heslo od zámku sousedovi garáže. Neptejte se mě proč, prostě to potřebuji vědět. Je několik možností, jak se s takovým problémem vypořádat.          
Jedním z nich, který asi napadne nás všechny, je, že člověk zkrátka vyzkouší všechny kombinace, jedna přeci musí fungovat. Tomuto přístupu se říká Brute Force, hrubá síla, mělo by to být docela intuitivní pojmenování.           
No, ačkoliv tento přístup naprosto bez pochyby funguje, soused má na zámku šestimístný kód. Než to vyzkouším všechno, přijedou benga a mám po prdeli.           
V tomto konkrétním případě by bylo potřeba vyzkoušet 10^6 kombinací zámku. Máme šest pozic, na každé může být jedno z deseti čísel, čísla se mohou opakovat, to je variace s opakováním, takže n^k různých kombinací.           
Všechny možné kombinace nazýváme stavovým prostorem problému. Jo, když si na internetu najdete definici stavového prostoru, vyjede vám něco neskutečně složitého a zvláštního a budete tomu prd rozumět. Já jsem v praxi vždy nazýval množinu kombinací, ze kterých vybíráme řešení problému, stavovým prostorem.               
V případě sousedova zámku je má stavový prostor velikost 10^6 prvků. Nu, velmi často se setkáváme s tím, že stavový prostor je monožina permutací nějakého pole. Důležitým poznatkem je, že stavový prostor dovede být opravdu hodně velký.         
Nuže, hrubá síla tedy funguje, nicméně využití hrubé síly na stavový prostor větší než pár tisíc prvků, možná i méně, je nesmírně pomalé a pro ještě větší prostory dokonce v podstatě nemožné. Algoritmus, který implementuje hrubou síly má automaticky tu nejhorší možnou časovou složitost pro daný problém, protože musí projít opravdu všechny možnosti a nich vybrat tu nejlepší.            
Útěchou nám může být snad jen to, že takový přístup opravdu pokaždé najde to nejlepší řešení.



Ukázky kódu
---

**Python - Rekurzivní umocňování**

```Python
# Vytvorime funkci power(x, n), ktera vola sama sebe, aby dosahla umocneni cisla
def power(x: int, n: int) -> int:
    if n == 0:  # Kazda rekurze potrebuje podminku, pri ktere uz nespousti sama sebe, ale vrati konkretni hodnotu
        return 1    # Cokoliv na nultou je jedna, takze muzeme smele vratit jednicku
    
    return x * power(x, n-1)    # Fce vraci cislo x vynasobene o jedna nizsi mocninou cisla x

# Vypiseme vysledky
print(power(3, 4))
```

**Python - Brute Force**

**Java - Rekurzivní umocňování**
**Java - Brute Force**

**C++ - Rekurzivní umocňování**
**C++ - Brute Force**


Materiály
---

Bro Code - Learn Recursion in 8 minutes -             

Nikhill Lohia - Brute Force algorhitms with real life examples -

Complexity Explorer - Indroduction to Computation Theory: Heiristics -            
Anish Krishnan - A* Search and Heuristic Intution in 2 minutes -            
Computerphile - Non-Determinitic Automata -                 
TutorialsPoint - Non Determinitic Algorithms -              
Hackerdashery - P vs. NP and the Computational Complexity Zoo -             