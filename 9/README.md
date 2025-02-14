Integrita dat, bezpečnost, logování, kontrola vstupů, zpracování chyb
===

Povídání
---

Dobře, rovnou povím, že tahle otázka je docela zvláštně zadaná a vlastně nemám tak úplně páru, co po vás budou přesně chtít. Nicméně zkusíme tu společně něco uvařit.       

V rámci integrity dat a bezpečnosti. Ukládáme-li třeba nějaká data, naprosto logicky by měla být v nějakém společném formátu, ať s nimi můžeme rozumně manipulovat. Integrita např. v databázích je zajištěna pomocí transakcí. Tedy nemělo by se stát, že změna nějakých dat závisí na změně jiných, a pokazí-li se nám něco v průběhu, data zůstanou napůl změněna. Tedy data by vždy měla být uložena pouze v konzistentním stavu. Já vím, spousta buzz words.                   
V rámci bezpečnosti, existuje pár pravidel, kterých bychom se měli držet. Když třeba načítáme data z konfiguračního souboru a máme v něm kvůli testování nějaké hodnoty, které by mohly být citlivé, rozhodně tento soubor neukládáme na Github. Můžeme to vyřešit např. tak, že uděláme nějaký template konfiguračního souboru, který koncový uživatel pouze přejmenuje a vyplní do něj své hodnoty.           
Samozřejmostí by také mělo být hashovat hesla, pokud je ukládáme kamkoliv do databáze nebo do souboru.                  
Další důležitou věcí je pamatovat, že uživatel je debil a bude se jako debil taky chovat. Kdekoliv může napsat něco, co nemá, udělá to. Jaké to může mít následky? Nu, v nejlepším případě program vyhodí nějaký zvláštní nečekaný error a pokračuje směle dál. V horším případě nám program spadne. V tom úplně nejhorším případě nám mohou třeba uniknout nějaká data.            
Jak, ptáte se? Nu, třeba nějakým injectionem. Takový SQL Injection, Command Injection, Cross-Site Scripting, ... Je toho spousta. Jen zběžně se podíváme, co který z nich znamená a jak vypadá.             
SQL injection je nečekaně vsunutí SQL příkazu někam, kde rozhodně nemá co dělat. Může to vypadat třeba nějak takto: **105 OR 1 == 1; DROP TABLE users; --**. Bum. Pokud jste si dobře neohlídali vstup, máte po tabulce.            
Command injection není tak častý. V podstatě do vstupu, který by třeba byl zadán následně do konzole, vložíte nějaký příkaz, který tam evidentně nemá být.                  
Cross-Site Scripting je vložený script tagu někam do inputu stránky. Pokud stránka špatně parsuje uživatelský vstup, javascript umístěný do tohoto tagu se normálně provede. Dovede do nadělat docela neplechu.             
V rámci bezpečnosti a kontroly vstupů je ještě dobrý si v dynamicky typovaných jazycích hlídat, zda uživatel vážně zadal správný datový typ a tak podobně. Ohlídat si mezní hodnoty, nesmyslné hodnoty. Zkrátka se snažit vše zařídit tak, aby uživatel opravdu nemohl nic podělat.             

Pokud ale uživatel stejně něco podělá, chceme dvě věci. Chceme vědět, kdo to podělal a kdy a určitě se nám bude hodit vědět, co tedy chceme dělat v případě, že se něco podělá.             
Podíváme se nejdříve na to první. Toho se dá efektivně docílit správným logováním. Co to znamená? Nuže, máme nějaký soubor, do kterého můžeme zapisovat různé věci. Např. že aplikace se spustila v tento čas tímto způsobem. Nebo že aplikace spadla a proč. Můžeme tam ale zapisovat i různé akce uživatelů tak, že bude jednoduše dohledatelné, proč nějaký problém vznikl.              
Správný log musí obsahovat čas, abychom ho dovedli někam zařadit. Logování je zpravidla ještě rozřazené do závažnosti hlášení. Typicky od nějakých DEBUG hlášení po FATAL. Méně důležitá hlášení v rámci úspory místa někdy ani defaultně nelogují.             
Je také dobré logy po nějaké době promazávat, protože loguje-li aplikace často a hodně, mohou logy docela nabýt na velikosti.   

A nakonec, jak se vypořádáme s případným problémem? Měla by být samozřejmost, že na všechny očekávatelné problémy umí náš program patřičně zareagovat. Samozřejmě pokud nastane velmi nečekaný problém, nebo se zkrátka jedná o problém, který nelze vyřešit jinak, než shozením programu, nemůžeme nic dělat.                  
V programovacích jazycích existuje konstrukt try-catch a tzv. výjimky. Výjimky jsou speciální objekty, která může program ve svém průběhu vyhodit, stane-li se něco špatného, nebo zkrátka při nějakých přesně daných podmínkách. My je můžeme chytit a patřičně na ně reagovat.                
V bloku try je kód, který může vyhodit výjimku. Jednotlivé bloky catch pak výjimku zachytí. Výjimky mohou mít v programovacím jazyce nějakou hierarchii. Nějaká výjimka třeba může dědit on jiné výjimky. Chytáme-li pak ve sledu catchů nejdříve obecnější výjimku, catch, který chytá tu konkrétnější, nikdy nemůže proběhnout.           
Zpravidla platí, že můžeme mít libovolný počet catch bloků, nicméně právě jeden z nich se provede.                  
Existuje i blok finally, který se provede pokaždé nezávisle na tom, zda kód proběhne bez chyby, nebo s ní. V tomto bloku se zpravidla dělají nějaké úklidové práce, třeba uzavírání streamů.                
Nuže, dobrým zvykem tedy je, chytat nejdříve konkrétnější výjimky. Na konci bychom vždy měli chytat tu nejobecnější a vymyslet pro ní nějaké obecné řešení.             
Mělo by být samozřejmostí každou zajímavější vyhozenou výjimku také logovat.


Ukázky kódu
---

**Python - Logging**
**Python - Input checking**
**Python - Error handling**

**Java - Logging**
**Java - Input checking**
**Java - Error handling**

**C++ - Input checking**
**C++ - Error Handling**

Materiály
---
