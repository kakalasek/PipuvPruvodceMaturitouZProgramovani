Testování, Unit testování a dokumentace zdrojového kódu
===

Povídání
---

Vytvoření programu zdaleka není konec cesty. V našem programu může existovat spousta chyb, kterých jsme si zprvu nevšimly, nebo nám nedošly. Je potřeba si ověřit, zda všechny části našeho kódu pracují správně a zda příslušné chyby ošetřují patřičně.               
Proto potřebujeme tedy náš kód zdokumentovat a provést testování.               
To můžeme udělat několika způsoby. Prvním z nich je tzv. Unit testing. Tím dovedeme otestovat určité části našeho programu. Třeba zda metoda opravdu vyhazuje výjimku ve správnou chvíli, či zda pracuje tak, jak očekáváme. Unit testy, jak již název vypovídá, se zaměřují vždy na velmi konkrétní část našeho programu.              
Takto může vypadat unit test v Pythonu:             

```Python

```

A takto může vypadat test v Javě s knihovnou JUnit:

```Java

```

Další možnosti jsou tzv. test casy. Tedy testování založené na scénářích, které sepíše vývojář. Ty by měl projít někdo, kdo kód nepsal. To může být z mnoha důvodu. Jednak proto, že může simulovat opravdového uživatele.                  
Dokonce existuje i pozice, tester, která se zabývá přesně podobným zpracováním scénářů. Každý scénář je tzv. test case. Každý test case by měl mít jasně sepsaná pravidla testy a očekávané výsledky. Pokud tester z jakéhokoliv důvodu nedovedl test provést nebo nedopadl podle očekávání, je třeba takovou chybu řádně zapsat a ideálně opravit.             
Test reporty, do kterých tester píše výsledky své práce, bývají nějaké standardizované soubory, mají jasně danou strukturu.

Dalším důležitým pojmem ve světě trénování je tzv. coverage. Test coverage se měří v procentech a je to množství kódu, které se do našich testů dostalu, a tedy bylo otestováno. Vyšší test coverage nemusí nutně znamenat bezpečnější a lepší. Někdy se test coverage nabírá jen na tom, že se volají fce, které by vůbec nemusely, protože na nich není co testovat.          

Náš kód by měl být patřičně zdokumentovaný. Ideálně s nějakým návrhem architektury, např. pomocí UML diagramu. Máme-li v našem kódu databázi, měli bychom poskytnout její diagram.              
Mluvíme-li o dokumentaci samotného kódu, určitě je žádoucí využívat tzv. programátorskou dokumentaci. Tu lze vytvořit třeba u metod a tříd. Popisuje funkci metody či třídy, v případě metody její vstupní a výstupní parametry a výjimky, které mohou při spuštění metody nastat (ty bychom samozřejmě měli patřičně ošetřovat).               
Komentáře v kódu jsou přípustné jen v případě, kdy za sebe kód opravdu nemůže mluvit a není jiná možnost než popis pomocí komentáře.            
Programátorskou dokumentaci v Pythonu lze udělat kupříkladu takto:

```Python

```

Java to má trochu elegantnější. Lze ji vytvořit třeba takto:

```Java

```

Materiály
---