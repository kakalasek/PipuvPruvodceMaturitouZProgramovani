Anonymní metody (Lambda), speciální (magické) metody, statické metody, ukazatel na metodu (delegát)
===

Povídání
---

V této otázce bude více kódu než povídání. Ale nějaký přehled si udělat můžeme.             
Anonymní metody, AKA lambda. Nu, je to přesně to, co to říká, jakási nepojmenovaná metoda. V různých jazycích jsou implementované rozdílně. My si zde budeme ukazovat implementaci v Pythonu, Javě a C++.               
Často se využívají např. v metodách map či filter, kde specifikují metodu, na základě které se daná operace provádí. Ostaně to uvidíte v praxi v kódu.          

Speciální, někdy také magické, ale to je za mě naprosto otřesné označení, nic magického nedělají, metody se vyskytují např. v Pythonu. Najdeme je také pod názvem double-underscore metody, nebo dunder metody. Jmenují se tak proto, protože před jejich a za jejich jménem píšeme dvě podtržítka  V čem že jsou tak speciální? Nu, dají se třeba ve třídě přepsat a tak změnit chování třeba některých operátorů a tak podobně. Jak se to liší od přetěžování operátorů? No .. v podstatě nijak, jen to má fancy název. Proto si zde zahrnem i přetěžování operátorů v C++.           
Joo a třeba PHP má také magické metody, ale nikdo normální nemá rád PHP, takže budeme dělat, že neexistuje.           
Taková zajímavost, Java nemá ani speciání metody ani přetěžování operátorů a funguje i bez toho. Když chcete sčítat dva objekty stejného typu, zkrátka si pro to naprogramujete metodu, bada bum bada bem, ízi ne? Přetěžování operátorů může také přivést určité problémy, ale ty nás nemusí zajímat.               

Statické metody. Otázka mluví vyloženě o metodách, takže vynecháme chování statických proměnných v mimo třídu třeba C++ nebo C.                 
Vytvoříme-li statickou metodu nebo proměnnou ve třídě, váže se ke třídě, nikoliv k nějaké instanci třídy. Polopaticky to znamená, že statická vlastnost třídy je společná pro všechny její instance. Když máme třídu kočka a vytvoříme v ní statickou proměnnou počet životů nastávíme ji na devět, všechny kočky budou mít při vytvoření 9 životů. Co se stane, když tuto proměnnou snížíme o jedna? Efektivně jsme jednou zabili všechny vytvořené kočky. Jak je to monžné? Statická vlastnost je společná pro všechny kočky, opakuji, váže se ke třídě samotné, nikoliv ke konkrétní instanci.               
Se statickou metodou je to podobné. Prozradím vám jednu věc. Nic jako metoda neexistuje, všechno je to pouze funkce, která má jako první parametr objekt, na kterém je volána. Ano, je mi to líto, OOP je jen iluze. Je to velmi hezky vidět v jazycích, jako třeba Python, kde musíte do instančních metod dávat jako první parametr vždy *self*. Proč myslíte? Aby jste v metodě mohli používat vlastnosti dané instance. No, statická metoda tento první parametr nemá. Není tedy závislá na konkrétní instanci, ale opět se váže ke třídě.              
Z evidentních důvodů tak nemůžeme ve statické metodě využívat instanční proměnné. Nemáme v ní přístup ke konkrétní instanci, protože nemá žádný parametr, který by jí tento objekt předal.              
V Javě a v C++ nám stačí před proměnnou nebo metodu dát klíčové slovo *static*. V Pythonu musíme využít dekorátor @staticmethod a nesmíme do metody jako vstup dávat *self*.

Ukazatele na metodu. V zadání je vyloženě napsáno delegát. Delegát se tomu říká jenom v ostrém céčku a ostré céčku je hnus, takže o tom se tu bavit nebudeme. Když se podíváme na tu samou věc v našich 3 vybraných jazycích:           
V Python je funkce tzv. first class objekt. Co to znamená? Že se k nim můžeme chovat úplně stejně jako ke všem ostatním datovým typům. Můžeme je ukládat do proměnných, předávat jako parametry, ... Takže nic jako trapného ukazatele na metodu nepotřebujeme, naše proměnná může být metoda.          
Java ... huh, Java. Nu, Java má jakýsi Function interface, který dovede reprezentovat funkci tak, že to něj uložíte lambda metodu. Má i více typů podobných objektů. Nicméně v Javě zpravidla ukazatele na metodu nepotřebujete, takže žádný jiný šikovně zabudovaný fígl na to nemá, nebo alespoň já jsem ho nikdy nepotřeboval.               
No v C++ máme jednu věc, která nám efektivně odpoví na otázku, jak fungují ukazatele na metody zde. C++ má pointery. Proč bychom tedy nemohli mít pointer na funkci. Funkce se také nachází někde v paměti a stejně jako pole má v paměti nějaký začátek, kam může pointer ukazovat. No a práce s pointerem na metodu už je v podstatě analogická k práci s kterýmkoliv jiným pointerem, jen má zkrátka trochu specifický datový typ.

Ukázky kódu
---

**Python - Lambda**
**Python - Special methods**
**Python - Static methods**
**Python - Functions**

**Java - Lambda**
**Java - Special methods .. except not at all**
**Java - Static methods**
**Java - Functions .. kind of**

**C++ - Lambda**
**C++ - Special methods**
**C++ - Static methods**
**C++ - Functions .. well, actually pointers**

Materiály
---

b001 - Python Lambda Functions -            
Coding with John - Lambda Expressions in Java -         
The Cherno - Lambdas in C++ -           

Bro Code - Python Magic Methods are easy! -         
Portfolio Courses - Operator Overloading Introduction -         

Bro Code - Learn Python Static Methods in 5 minutes -           
Coding with John - Static vs Non-Static Variables and Methods in Java -            
The Cherno - Static in C++ -        
The Cherno - Static for Classes and Structs in C++ - 

The Cherno - Function Pointers in C++ -         