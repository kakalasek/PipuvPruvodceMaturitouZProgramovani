Principy objektového programování, agregace a kompozice objektů
===

Povídání
---

![FP vs OOP](fp_vs_oop.jpg)

Uděláme si takové zajímavé cvičení. Uvaříme si objektově orientované programování. Existují dva základní způsoby programování, funkcionální a objektové.                
O funkcionálním programování se tu nebudeme moc bavit, nicméně to je založené na tom, že máme nějaké proměnné a funkce, pomocí kterých na nich můžeme něco provádět. Někdy nám naprosto postačí, ale na některé příklady se nehodí a právě takový příklad si ukážeme.    

Řekněme, že máme zvířátka a farmu. Máme různé druhy zvířátek a potřebujeme jich vytvořit několik. Začneme naprosto intuitivním řešením. Pro každé zvířatko počet proměnných, který bude reprezentovat jejich vlastnosti. Pak uděláme funkce, které jednotlivá zvířátka potřebují.       
Nu, podívejme se teď na náš kód.

```
pig.name = Piggy
pig.weight = 40
pig.height = 50
pig.is_well_fed = True

cow.name = Cowie
cow.weight = 100
cow.is_healthy = True
cow.is_pregnant = True

dog.name = Rex
dog.weight = 12
dog.is_happy = True

func feed(pig):
    pig.is_well_fed = True

func take_care(cow):
    cow.is_healthy = True

func pet(dog):
    dog.is_happy = True
```

Vypadá trochu zvláštně že? Je zde hodně proměnných a s každým dalším zvířátkem se jejich počet značně zvyšuje. Natož abychom je chtěli nějak uložit na farmu.           
V tuto chvíli nám přichází na pomoc právě OOP. OOP je postavené především na určité abstrakci. Vytvoření počtu proměnných v paměti se nevyhneme, nicméně díky OOP to můžeme udělat tak, že kód bude mnohem čitelnější a škálovatelnější.            
Budeme-li třeba chtít přidat psa, bude nám na to stačit pouze jeden řádek místo 5.          
OOP nám nabízí možnost vytvořit tzv. třídu. Proměnné, které ve třídě deklarujeme, se nazývají vlastnosti třídy a funkce metody. Vidíte, jak každá funkce výše má jako parametr zvířátko, se kterým pracuje? Podobně je tomu i u OOP. Spíše než podobně vlastně úplně stejně.            
Metody, nebereme-li v potaz ty statické, jsou v postatě jen funkce, které mají jako první parametr objekt, se kterým pracují.               
To je nám ale zpravidla skryto, proto ta abstrakce. Třídy tedy dovedou šikovně spojit společné proměnné a funkce do jednoho konstruktu.             
Ten může vypadat třeba takhle:

```

class Pig:

    name = Piggy
    weight = 40
    height = 50
    is_well_fed = True

    func feed():
        is_well_fed = True

class Cow:

    name = Cowie
    weight = 100
    is_healthy = True
    is_pregnant = True

    func take_care():
        is_healthy = True

class Dog:

    name = Rex
    weight = 12
    is_happy = True

    func pet():
        is_happy = True
```

To už vypadá trochu lépe ne? Nuže, máme tu ještě jeden menší problém. Všechny třídy mají společné atributy. OOP nabízí jeden koncept, který nám ušetří toto opakování, dědičnost. Tu jsme již řádně probrali v minulé otázce, odkazuji se tedy tam.     

Důležitým konceptem OOP je tzv. zapouzdření. To znamená, že vlastnosti a metody třídy lze deklarovat jako soukromé a mimo samotnou třídu na ně nelze sáhnout. Pro přístup k vlastnostem se pak dělají gettery a settery. V nich lze nastavit např. nějaké kontroly.         
Dále každý správný objekt potřebuje konstruktor. To je metoda, která se volá při jeho inicializaci. Nastaví základní hodnotu objektů, tedy je inicializuje.             
Koncept polymorfismu jsme již také probrali v otázce o dědičnosti.    

![Aggregation and Composition](aggregation_vs_composition.png)

Je zde zmíněná i agregace a kompozice objektů. To je spíše takový fancy název. V podstatě, nahoře na obrázku je to pěkně vysvětlené, pokud třída A je naprosto závislá na třídě B a nemůže bez ní existovat, jedná se o kompozici.              
V případě, že třída A může existovat sama o sobě, jde o agregaci.           
Využívá se toho např. kdybychom chtěli dát zvířátka do naší farmy. Měli bychom nějaký list zvířátek, do kterého bychom je ukládali. To by byla agregace, protože zvířátko může existovat samo o sobě.                   
Takže v podstatě uložíme objekt do objektu. K uloženému objektu pak přistupujeme jen a pouze přes objekt, ve kterém je uložen.


Určitě stojí za to zmínit jednu speciální metodu, kterou zpravidla každá třída mívá, konstruktor. Tato metoda je zodpovědná za inicializaci objektu. Tedy za inicializaci jejich proměnný, popř. načtení jejich hodnot ze souboru.          
Konstruktor může být i prázdný, nemá-li smysl pro třídu nic inicializovat

Ukázky kódu
---

**Python - OOP**
```Python
class Square():

    # Konstruktor
    def __init__(self, a):
        self._a = a

    def set_a(self, a):
        self._a = a

    def get_a(self):
        return self._a
    
    def get_area(self):
        return self._a**2
    

if __name__ == "__main__":
    s1 = Square(5)
    
    print(s1.get_a())
    print(s1.get_area())
```

**Java - OOP**

```Java
class Main{

    static class Square{
        private int a;

        public Square(int a){
            this.a = a;
        }

        public int getA(){
            return this.a;
        }

        public void setA(int a){
            this.a = a;
        }

        public int getArea(){
            return a*a;
        }
    }

    public static void main(String args[]){
        Square s1 = new Square(10);
        System.out.println(s1.getA());
        System.out.println(s1.getArea());
    }
}
```

**C++ - OOP**

```C++
#include <iostream>

using namespace std;

class Square{
    private:
        int a;

    public:
        Square(int a){
            this->a = a;
        }

        int getA(){
            return this->a;
        }

        void setA(){
            this->a = a;
        }

        int getArea(){
            return this->a*this->a;
        }
};

int main(){
    Square s1 = Square(5);

    cout << s1.getA() << endl;
    cout << s1.getArea() << endl;

    return 0;
}
```

Materiály
---

Programming with Mosh - Object-Oriented Programming, Simplified -                   
GeeksForGeeks - Association, Composition and Aggregation in Java -              
Packt - Java: Object-Oriented Programming Concepts: Associations, Aggregation & Composition -                   
CodeAesthetic - The Flaws of Inheritance -              
Ave Coders - Python OOP Composition Clearly Explained -                 
Bro Code - Learn Python Composition in 7 minutes -              
0612 TV w/ NERDfirst - Composition & Aggregation -                          
BasicOverflow - FP vs OOP | For Dummies -           