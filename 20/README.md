Testování, Unit testování a dokumentace zdrojového kódu
===

Povídání
---

Vytvoření programu zdaleka není konec cesty. V našem programu může existovat spousta chyb, kterých jsme si zprvu nevšimly, nebo nám nedošly. Je potřeba si ověřit, zda všechny části našeho kódu pracují správně a zda příslušné chyby ošetřují patřičně.               
Proto potřebujeme tedy náš kód zdokumentovat a provést testování.               
To můžeme udělat několika způsoby. Prvním z nich je tzv. Unit testing. Tím dovedeme otestovat určité části našeho programu. Třeba zda metoda opravdu vyhazuje výjimku ve správnou chvíli, či zda pracuje tak, jak očekáváme. Unit testy, jak již název vypovídá, se zaměřují vždy na velmi konkrétní část našeho programu.              
V Pythonu využijeme knihovny *unittest*. Oddědíme-li třídu od třídy TestCase, dovede nám poskytnout prostor pro testování. Zpravidla vytváříme pro každou specifickou skupinu testů takovouto třídu. Měla by se jmenovat nějak smysluplně vzhledem k tomu, co testujeme. Každý unit test by měl testovat právě jednu věc. K tomu lze využít AssertEqual, AsseertNotEqual, .. to jsou metody ve třídě TestCase, které nám oddědění od ní poskytne. Každý jeden test se pak píše jako jedna nová fce. Testy spouštíme pomocí metody *main()* opět ve třída TestCase. Takto to může vypadat:             

```Python
import unittest

class Calc():

    def __init__(self, a: int, b: int):
        self.a: int = a
        self.b: int = b

    def sum(self):
        return self.a + self.b
    
    def diff(self):
        return self.a - self.b
    

class CalcTest(unittest.TestCase):

    def testSum(self):
        calc = Calc(4, 6)
        self.assertEqual(calc.sum(), 10, 'The sum has failed')

    def testDiff(self):
        calc = Calc(4, 6)
        self.assertEqual(calc.diff(), -2, 'The diff has failed')

if __name__ == "__main__":
    unittest.main()
```

A takto může vypadat test v Javě s knihovnou JUnit:

```Java
package testing;

public class Main {
    public static void main(String[] args) {
        
    } 
}

package testing;

public class Square {
    private int a;
    
    Square(int a){
        this.a = a;
    }

    public int getA() {
        return a;
    }

    public int area(){
        return a * a;
    }
}

package testing;

import static org.junit.Assert.assertEquals;

import org.junit.Test;

public class SquareTest {

    @Test
    public void areaTest(){
        Square s = new Square(5);
        assertEquals(25, s.area());
    }
}
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