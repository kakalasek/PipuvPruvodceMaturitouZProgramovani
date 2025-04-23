Metodiky a životní cyklus vývoje softwaru
===

Povídání
---

Začneme klasikou, vodopádovým modelem. Ten by měl zároveň účinně představit otázku.

![Waterfall](waterfall.jpg)

Vodopádový model je jakýsi prehistorický model postupu při vývoji nějakého projektu. Začíname kompletními požadavky zákazníka, vytvoříme design, vyvineme aplikaci, otestujeme ji, nasadíme ji a sledujeme její běh. Důležité také je, že každý jeden krok může začít být vykonáván až po tom předchozím. Nesměli bychom tak třeba začít s testováním, dokud jsme celou aplikaci nedokončili.                 
Kde je problém? Dostaneme-li se do další části vývoje, správně bychom již neměli nikdy putovat zpátky. Takže podle toho pravého vodopádového modelu, když nám aplikace neprojde testy, celou ji zahodíme a začínáme opět požadavky zákazníka nebo designem aplikace. Můžete si asi představit, že v praxi je tento přístup tak docela nevyužitelný.         
V realitě tedy třeba na menších projektech lze implementovat jistou formu vodopádového modelu, kde se ale lze vrátit o jeden stupeň zpět.               
Trochu praktičtějším modelem vývoje projektu je model iterativní.         

![Iterative](iterative.jpg)

Tento model už je trochu chytřejší. Vývoj softwaru rozdělíme do několika fází, iterací. Na konci každé dostaneme fungující verzi softwaru. Následně se vracíme k požadavkům a pokračujeme v jejich implementaci pro další verzi softwaru.               
Má velikou výhodu v tom, že mezi jednotlivými iteracemi probíhá komunikace se zákazníkem. Takže se lépe přizpůsobuje změnám v požadavcích. Také je mnohem tolerantnější k týmu, který se s nástroji vývoje teprve řádně učí.            
Nicméně mimo jiné trpí trochu opačným problémem, než jeho předchůdce vodopádový model. Lze ho smysluplně uplatnit jen při větších projektech, protože ne každý projekt jde rozdělit tak, aby na konci každé iterace vznikla funkční verze projektu.     
Když už jsme si zmínili ty verze, může si ukázat, jak se typicky verzuje projekt.           

![Versioning](version.jpg)

Naprosto klasické je verzování číselné. Zpravidla máme dvě nebo tři čísla. První je tzv. Major, hlavní číslo. Označuje nějaký velký patch, zpravidla měnící zásadní aspekty aplikace. Důležitá zde je rizikovost změn. Pokud je velké riziko, že změna aplikaci nějak rozhází, je pro takovou verzi změněno hlavní číslo. Druhé, Minor, označuje změnu, která představuje menší riziko, nicméně aplikaci nějakým způsobem mění, něco přidává. Poslední číslo je pouze pro nějaké patche.


Materiály
---

Tutorialspoint - SDLC - https://www.tutorialspoint.com/sdlc             
Wikipedia - Software versioning - https://en.wikipedia.org/wiki/Software_versioning     
Wikipedia - Software release lifecycle - https://en.wikipedia.org/wiki/Software_release_life_cycle      
