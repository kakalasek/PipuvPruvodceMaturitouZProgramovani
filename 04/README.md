Anonymní metody (Lambda), speciální (magické) metody, statické metody, ukazatel na metodu (delegát)
===

Povídání
---

V této otázce bude více kódu než povídání. Ale nějaký přehled si udělat můžeme.             
Anonymní metody, AKA lambda. Nu, je to přesně to, co to říká, jakási nepojmenovaná metoda. V různých jazycích jsou implementované rozdílně. My si zde budeme ukazovat implementaci v Pythonu, Javě a C++.               
Často se využívají např. v metodách map či filter, kde specifikují metodu, na základě které se daná operace provádí. Ostaně to uvidíte v praxi v kódu.          

Python využívá klíčového slova *lambda*. V Pythoní lambdě může být opravdu jen jeden příkaz. 

```Python
# Vytvorime jednoduchou lambda fci, ktera umocni cislo na druhe cislo
# V Pythonu se lambda vytvari klicovym slovem 'lambda'
# V lambda muze byt prave jeden prikaz
# Lambdu muzeme takhle elegantne ulozit do promenne
pow_on = lambda x, y: x**y

print(pow_on(10, 3))

# Prakticke vyuziti muze byt napr. u fci map a filter
# Zde je metoda opravdu anonymni, protoze vstupuje pouze jako parametr, podobne jako cislo. Nema jmeno a po provedeni uz ji nikdy neuvidime
lst = [1, 2, 4, 7, 9, 11]

lst = map(lambda x: x**2, lst)  # Umocnime kazdy prvek listu na druhou

print(list(lst))

lst = [1, 2, 4, 7, 9, 11]

lst = filter(lambda y: y % 2, lst) # Odstranime vsechna suda cisla

print(list(lst))
```

V javě můžeme lambdu vytvořit pomocí tzv. FunctionalInterface. To je interface, který má pouze jednu metodu. Narozdíl od Pythonu ale samotná implementace metody může obsahovat i více řádků kódu. Lambda se pak tvoří pomocí definice proměnné typu našeho FunctionalInterface.

```Java
public class Main{

    @FunctionalInterface
    static interface UniMath{
        Integer operate(Integer x);
    }

    static void printResultOfMathematicalOperation(UniMath u, int t){
        System.out.println(u.operate(t));
    }

    public static void main(String[] args) {
        UniMath square = (x) -> x * x;

        printResultOfMathematicalOperation(square, 5);
    }
}
```

Speciální, někdy také magické, ale to je za mě naprosto otřesné označení, nic magického nedělají, metody se vyskytují např. v Pythonu. Najdeme je také pod názvem double-underscore metody, nebo dunder metody. Jmenují se tak proto, protože před jejich a za jejich jménem píšeme dvě podtržítka  V čem že jsou tak speciální? Nu, dají se třeba ve třídě přepsat a tak změnit chování třeba některých operátorů a tak podobně. Jak se to liší od přetěžování operátorů? No .. v podstatě nijak, jen to má fancy název. Proto si zde zahrnem i přetěžování operátorů v C++.           
Joo a třeba PHP má také magické metody, ale nikdo normální nemá rád PHP, takže budeme dělat, že neexistuje.           
Taková zajímavost, Java nemá ani speciání metody ani přetěžování operátorů a funguje i bez toho. Když chcete sčítat dva objekty stejného typu, zkrátka si pro to naprogramujete metodu, bada bum bada bem, ízi ne? Přetěžování operátorů může také přivést určité problémy, ale ty nás nemusí zajímat.               

```Python
# Toto je je pomocna trida Node, aby nas Stack fungoval plus minus tak, jak ma. Nemusite ji venovat velkou pozornost
class Node():

    def __init__(self, value, next):
        self._next = next
        self._value = value

    def getNext(self):
        return self._next

    def getValue(self):
        return self._value

    def setNext(self, next):
        self._next = next

    def setValue(self, value):
        self._value = value


# Udelame si tridu Stack. Na ni muzeme specialni metody hezky demonstrovat
class Stack():

    # Prvni z nich je __init__, ktery ze zavola pri vytvoreni objektu pro inicializaci. Je to ekvivalent konstruktoru 
    def __init__(self):
        self._head = None
        self._len = 0

    def push(self, value):
        if self._head == None:
            self._head = Node(value, None)
            self._len += 1
            return

        temp = Node(value, self._head)
        self._head = temp
        self._len += 1

    # Dalsi specialni metoda. Mela by vracet vypsatelnou verzi objektu. Treba print() by ji mel vyuzit defaultne
    def __repr__(self):
        temp = self._head
        s = ""
        while temp:
            s += str(temp.getValue()) + " "
            temp = temp.getNext()

        return s

    # Tuto metodu vyuzije metoda len(), kterou nyni muzeme zavolat i na nas stack a ten poslusne vrati svou velikost 
    def __len__(self):
        return self._len
    
# Magickych metod existuje nespocet, ruzne casti pythonu je mohou ruzne vyuzivat. Takovym nepsanym pravidlem je, ze by se nikdy nemely volat takto: __len__(), tedy beznym zpusobem

stack = Stack()
stack.push(10)
stack.push('hello')

print(stack)
print(len(stack))
```

Ačkoliv Java nic jako přetěžování operátorů nemá, každý objekt je odděděn od objektu, který má určitě standardizované metody, některé známé metody je volají. Hezkým příkladem je třeba toString(). Ten volá náš známy System.out.println().

```Java
public class Main{

    public static class Person{

        private String name;
        private int id;

        public Person(String name, int id){
            this.name = name;
            this.id = id;
        }

        public int getId() {
            return id;
        }

        @Override
        public String toString(){
            return "My name is " + name + " and this is my id: " + id;
        }

        @Override
        public boolean equals(Object o){
            if(o == this) return true;
            if(o == null) return false;
            if(!(o instanceof Person)) return false;
            Person person = (Person) o;
            if (id == person.getId()) return true;
            return false;
        }

        @Override
        public int hashCode(){
            return id;
        }
    }

    public static void main(String[] args) {
        Person p1 = new Person("Karel", 325132);
        Person p2 = new Person("Pepa", 325132);
        Person p3 = new Person("Karel", 521231);

        System.out.println(p1.equals(p2));
        System.out.println(p1.equals(p3));
    }
}
```

Statické metody. Otázka mluví vyloženě o metodách, takže vynecháme chování statických proměnných v mimo třídu třeba C++ nebo C.                 
Vytvoříme-li statickou metodu nebo proměnnou ve třídě, váže se ke třídě, nikoliv k nějaké instanci třídy. Polopaticky to znamená, že statická vlastnost třídy je společná pro všechny její instance. Když máme třídu kočka a vytvoříme v ní statickou proměnnou počet životů nastávíme ji na devět, všechny kočky budou mít při vytvoření 9 životů. Co se stane, když tuto proměnnou snížíme o jedna? Efektivně jsme jednou zabili všechny vytvořené kočky. Jak je to monžné? Statická vlastnost je společná pro všechny kočky, opakuji, váže se ke třídě samotné, nikoliv ke konkrétní instanci.               
Se statickou metodou je to podobné. Prozradím vám jednu věc. Nic jako metoda neexistuje, všechno je to pouze funkce, která má jako první parametr objekt, na kterém je volána. Ano, je mi to líto, OOP je jen iluze. Je to velmi hezky vidět v jazycích, jako třeba Python, kde musíte do instančních metod dávat jako první parametr vždy *self*. Proč myslíte? Aby jste v metodě mohli používat vlastnosti dané instance. No, statická metoda tento první parametr nemá. Není tedy závislá na konkrétní instanci, ale opět se váže ke třídě.              
Z evidentních důvodů tak nemůžeme ve statické metodě využívat instanční proměnné. Nemáme v ní přístup ke konkrétní instanci, protože nemá žádný parametr, který by jí tento objekt předal.              
V Javě a v C++ nám stačí před proměnnou nebo metodu dát klíčové slovo *static*. V Pythonu musíme využít dekorátor @staticmethod a nesmíme do metody jako vstup dávat *self*.

```Python
class Calculator:

    @staticmethod
    def add(a, b):
        return a + b

    @staticmethod
    def subtract(a, b):
        return a - b

    @staticmethod
    def multiplicate(a, b):
        return a * b

    @staticmethod
    def divide(a, b):
        return a/b

if __name__ == "__main__":
    print(Calculator.add(2, 3))
    print(Calculator.divide(15, 11))
```

A zde příklad v Javě:

```Java
public class Main{

    public static class Test{

        private static int numberOfInstances;

        public static int getNumberOfInstances(){
            return numberOfInstances;
        }

        public Test(){
            numberOfInstances++;
        }
    }

    public static void main(String[] args) {
        Test t1 = new Test();

        System.out.println(Test.getNumberOfInstances());

        Test t2 = new Test();
        
        System.out.println(Test.getNumberOfInstances());

        Test t3 = new Test();
        
        System.out.println(Test.getNumberOfInstances());
    }
}
```

Ukazatele na metodu. V zadání je vyloženě napsáno delegát. Delegát se tomu říká jenom v ostrém céčku a ostré céčku je hnus, takže o tom se tu bavit nebudeme. Když se podíváme na tu samou věc v našich 3 vybraných jazycích:           
V Python je funkce tzv. first class objekt. Co to znamená? Že se k nim můžeme chovat úplně stejně jako ke všem ostatním datovým typům. Můžeme je ukládat do proměnných, předávat jako parametry, ... Takže nic jako trapného ukazatele na metodu nepotřebujeme, naše proměnná může být metoda.          
Java ... huh, Java. Nu, Java má jakýsi Function interface, který dovede reprezentovat funkci tak, že to něj uložíte lambda metodu. Má i více typů podobných objektů. Nicméně v Javě zpravidla ukazatele na metodu nepotřebujete, takže žádný jiný šikovně zabudovaný fígl na to nemá, nebo alespoň já jsem ho nikdy nepotřeboval.               
No v C++ máme jednu věc, která nám efektivně odpoví na otázku, jak fungují ukazatele na metody zde. C++ má pointery. Proč bychom tedy nemohli mít pointer na funkci. Funkce se také nachází někde v paměti a stejně jako pole má v paměti nějaký začátek, kam může pointer ukazovat. No a práce s pointerem na metodu už je v podstatě analogická k práci s kterýmkoliv jiným pointerem, jen má zkrátka trochu specifický datový typ.

```Python
def multiple_wrapper(n):
    
    def inner_function():
        return n * "O"

    return inner_function

def double_trouble(function):
    
    def wrapper():
        return function() * 2
    
    return wrapper

@double_trouble     # Python Decorator
def say_hi():
    return "Hello there\n"


if __name__ == "__main__":
    # Funkce je first class, lze ji libovolne ulozit do promenne a zachazet s ni
    three_timer = multiple_wrapper(3)
    print(three_timer())

    print(say_hi())
```

Takhle může vypadat ukazatel na metodu v C++:

```C++
#include <iostream>

using namespace std;

int on_pow(int num, int exp){
    if(exp <= 0){
        return 1;
    }
    return num * on_pow(num, exp-1);
}

int main(){
    int (*fc_pointer)(int, int);       

    fc_pointer = on_pow;

    cout << fc_pointer(10, 2) << endl;

    return 0;
}
```

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