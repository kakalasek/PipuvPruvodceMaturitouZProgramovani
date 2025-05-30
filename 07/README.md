Datové typy, Generika, Výčtové datové typy, Struktury, Anotace, Operátory
===

Povídání
---

![Data Types](data_types.jpg)

Datové typy. Podstatu datového typu si ukážeme na jednoduchém příkladu. Když vám tu napíši toto: **01100001**, dovede odhadnout, co to znamená? Dobře, ještě trochu upřesním. Tohle bude binární hodnota v jedné paměťové buňce. Co to je za hodnotu? Je to číslo? Nebo část většího čísla? Ukazatel? Znak?. To nevíme, může to být cokoliv si zamaneme. Dokud tomu nedáme jasný datový typ.            
Datové typy nám tedy říkají, jak se máme k daným datům chovat, jak je máme interpretovat. Označíme-li tedy naše číslo jako INT, bude jeho hodnota 97. Oznáčíme-li ho jako CHAR, bude jeho hodnota písmeno 'a'. Pokud kódujeme podle ASCII, kódováním se v této otázce nebudeme hlouběji zabývat.            
Datových typů existuje spousta a každý programovací jazyk s nimi může zacházet mírně odlišně. Ku příkladu jazyk C má sice datový typ *char*, nicméně ten, místo aby nutně určoval, že hodnota je znak, udává jen číslo ve velikosti jednoho bytu. Zda ho budeme interpretovat jako číslo nebo ne, nechává na nás. Jiné jazyky ale nemusí být ve své interpretaci tak volné.             
Na obrázku nahoře máte docela hezký výpis různých datových typů, asi netřeba je všechny rozebírat. Podíváme se jen na nějaké zajímavé.              
Zde je nějaký výčet numerických datových typů v jazyce C:

```C
#include <stdio.h>
#include <stdbool.h>

void main(){
    // Numericke datove typy
    // ---------------------
    char c = 96;    // 1 byte
    short s = 128;  // 2 bytes
    int i = 1024;   // 4 bytes
    long l = 10120L;// 8 bytes

    // Nic nam nebrani do techto datovych typu ulozit charakter. Charakter je take reprezentovan cislem.
    // Jedine, co oddeluje charakter od cisla, je, jak se rozhodneme ho interpretovat v danou chvili
    // Nazorne ukazi
    char character = 'a';
    printf("The character: '%c'. \nThe number: %d\n", character, character);

    // Kazde cislo muze a nemusi mi znak. Znak byva zpravidla prvni bit cisla, ktery urcuje, zda je cislo kladne, nebo zaporne.
    // Defaultne se kazdy numericky datatyp se znackou. Pokud ale nechceme ukladat zaporna cislo a hodi se nam vetsi rozpeti do tech kladnych, muzeme vyuzit neoznackovane datove typy
    unsigned char uc = 255;
    unsigned short us = 564;
    unsigned int ui = 2064;
    unsigned long ul = 30641L;

    // Existuji take datove typy na reprezentaci realnych cisel
    float f = 10.7f;
    double d = 20.166;

    // Ackoliv to nemusi vypadat jako numbericky typ, zaradim ho sem, protoze ve spouste programovacich jazyku lze vyuzit i cislo ke stejnemu ucelu.
    // V jazyce C musite dokonce importovat systemovou knihovnu, abyste ho mohli vyuzivat
    // V podstate boolean reprezentouje true nebo false, nicmene kazdopadne zabira alespon 1 byte, mensi jednotka v pameti zkratka neexistuje
    // To zabira i char. Bezne jazyk chape jakoukoliv hodnotu ruznou od nuly nebo null jako true
    bool b = true;

    return 0;
}
```

Asi nejzajímavějším a přitom jedním z nejběžnějších datových typů je STRING, textový řetězec. Každý programovací jazyk si s ním hraje jinak. V jazyce C není STRING nic víc než pole charů ukončené null terminátorem. Když se podíváme ještě více do hloubky, proměnná, kterou dostaneme po vytvoření STRINGU nebo jiného libovolného pole, není nic jiného, než pointer na první prvek pole. Víme, jak velký je jeden prvek pole a jak je pole dlouhé, takže se v něm můžeme libovolně pohybovat pomocí přičítání a odčítání čísel k ukazateli.       
V moderních programovacích jazycích je String nějaký objekt, např. v Javě. To je užitečné, protože nás to odstiňuje od zbytečných detailů implementace, hraní si s byty, ...                
Takto vypadají Stringy v jazyce C:                    

```C
#include <stdio.h>
#include <string.h>

int main(){
    // Pole a stringy
    // --------------

    // Spravne, string je jenom pole charu. Alespon v cecku a je nejjednodusi si ho tak predstavit. Na konci se nachazi null terminator, ktery signalizuje konec stringu
    char my_string[30] = "Hello there";

    printf("This is our little string: %s\n", my_string);

    // Muzeme vytvorit pole libovolnych datovych typu
    // Pole neni nic jineho, nez ukazatel na prvni prvek pole
    // Neverite? Ukazi
    int little_array[5] = {1, 2, 3 ,4 ,5};

    // Vysvetlim. Hvezdicka pred promenou takto se vyuziva k tzv. dereferencovani pointeru. Proste vezme hodnotu, na kterou pointer ukazuje
    // A hle, zde je to nase jednicka
    printf("First element of the array: %d\n", *little_array);

    // Co se stane, kdyz k nasemu pointeru prictu jednicku a pak ho dereferencuji?
    // Dostanu dvojku
    printf("Second element of the array: %d\n", *(little_array + 1));

    return 0;
}


```

V Pythonu máme datové typy trochu rozmanitější, zde je pár z nich:

```Python
""" Data types """

n1 = 10 # Integer
n2 = 10.12 # Double
b1 = True # Boolean
s1 = 'Hello' # String
nn = None   # Null

t1 = (12, 3, 5) # Tuple
a1 = [12, 5, 'No'] # Array
set1 = {45, 'Hoho', 552} # Set
dict1 = {"Hello": 562, 11: "no"} # Dictionary

def plus(x: int, y: int):
    return x + y

func = plus # function

print(func(2, 3))
```

Nu, ale co když nevíme, jaký datový typ chceme využít? Na pomoc nám přichází generika. V jazyku C bohužel nic takového nemáme, ale např. Java nám je nabízí. Řekněme, že si opět vytváříme vlastní zásobník a chtěli bychom do něj ukládat více různých datových typů. Nu, ve třídě tedy budeme pracovat s nějakým generikem, typicky označováným T. Když pak object deklarujeme, místo generika vložíme datový typ, který chceme ukládat. Jednoduché, že?              
Takto mohou vypadat generika třeba v Javě:

```Java
class Main{

    // Trida, ktera vyuziva generika. Zapisuji se do spicatych zavorek. Typicky se oznacuji T. Muze jich byt i vice
    static class GenericMaster<T>{

        private T myGeneric;    // Promenna generickoho datoveho typu

        public GenericMaster(T myGeneric){
            this.myGeneric = myGeneric;
        }

        // Jednoducha metoda, ktera vypise datovy typ vlastnosti myGeneric
        public Object getDatatype(){
            return myGeneric.getClass();
        }
    }

    public static void main(String[] args) {
        /* Vytvorime instanci tridy. Pri deklaraci musime specifikovat datovy typ, ktery bude interne vyuzivat vsude, kde jsme zapsali genericky
         * datovy typ T. Zde je to Integer. V Jave nelze vyuzit primitivni datove typy na miste generika, Integer je trida, ktera se chova analogicky k datovemu typu int.
         */
        GenericMaster<Integer> g = new GenericMaster<>(3000);
        System.out.println(g.getDatatype());

        /* Zde jsme vytvorili instanci stejne tridy, nicmene tentokrat jsme do ni ulozili String */
        GenericMaster<String> g2 = new GenericMaster<>("Hello");
        System.out.println(g2.getDatatype());
    }
}
```

A takto např. v jazyce C++:

```C++
#include <iostream>

using namespace std;

template <typename T>
class GenericClass{
    private:
        T genericVariable;

    public:
        GenericClass(T genericVariable){
            this->genericVariable = genericVariable;
        }

        string getMeDataType(){
            return typeid(this->genericVariable).name();
        }
};

int main(){
    GenericClass<int> g(20);
    cout << g.getMeDataType() << endl;

    GenericClass<string> s("Hello");
    cout << s.getMeDataType() << endl; 

    GenericClass<float> *t = new GenericClass(20.12f);
    cout << t->getMeDataType() << endl;

    delete t;

    return 0;
}
```

Existuje také něco, čemu zde pan ředitel fancy názvem říká výčtové datové typy. My lidi tomu budeme říkat enum. Enum se využívá, máme-li několik pevně daných neměnných hodnot, ze kterých chceme vybírat. Třeba dny v týdnu, měsíce, ... Každá hodnota je v realitě jenom číslo. To nás ale nemusí zajímat, my jen potřebujeme mezi těmito hodnotami rozlišovat.               

```C
#include <stdio.h>

void main(){
    // Vyctove datove typy
    // -------------------

    enum WeekDay {
        MON,
        TUE,
        WEN,
        THU,
        FRI,
        SAT,
        SUN
    };

    enum WeekDay w1 = FRI;

    printf("Value of a weekday. Yes, its just a number: %d\n", w1);

    return 0;
}
```

V Pythonu lze enum vytvořit pomocí třídy odděděné od třídy Enum:

```Python
from enum import Enum

class Color(Enum):  # Enum
    RED = 0
    GREEN = 1
    BLUE = 2
```

Struktury. Upřímně, nechápu, proč přesně je tady tento specifický .. datový typ? zařazen. Lze ho smysluplně využít v podstatě jen v programovacích jazycík jako C nebo C++.                         
Struktura není nic jiného, než že namrdáme několik datových typů do paměti za sebou a pak k nim můžeme přistupovat pomocí tečky a jména datového typu v dané struktuře. Ano, opravdu, to je všechno. Struktura se dovede chovat jako třída. Protože, fanfáry, funkce je také datový typ. Můžeme tedy vytvořit strukturu, která bude mít nějaké proměnné, vlastnosti, a nějaké funkce, metody.        
Tady je příklad jednoduché struktury v jazyce C:

```C
#include <stdio.h>

void main(){
    // Struktury
    // ---------

    // Takovy predchudce trid, struktura.
    // V podstate, vezmeme nekolik datovych typu a nacpeme je do pameti za sebou a pak se k nim chovame, jako by byly v necem specialni
    struct Student {
        long id;
        char name[20];
        char surname[20];
        int number;
    };

    struct Student s1;
    s1.id = 20000L;
    strcpy(s1.name, "Peter");
    strcpy(s1.surname, "Parker");
    s1.number = 120;

    printf("This is our student: id = %d ; name = %s ; surname = %s ; number = %d\n", s1.id, s1.name, s1.surname, s1.number);

    return 0;
}
```

Anotace. Dobře, no, jediný programovací jazyk, ve kterém jsem kdy s anotacemi pracoval, je Java. Jestli to umí i nějaký jiný, nevím, možná ostré cé, ale v tom mi tu neděláme. Nicméně, anotace můžeme chápat jako jakýsi koment, který funguje jako metadata pro program. Anotace zpravidla vypadají nějak takto: **@Text(Paramtery)** a typicky se píši nad metodu, vlastnost nebo třídu. Ne každá anotace musí mít parametry.            
Z příkladů anotací třeba @SupressWarning(*nazev upozorneni*). To dovede potlačit nějaké upozornění, které vám dává IDE. Nebo náš dobře známý @Override. Tato anotace je spíše dekorativní, nic specifického nedělá. Pomocí reflekce pak můžeme anotace využívat, chceme-li. Dají se vytvořit i uživatelské anotace.             
Anotace typicky hojně využívají frameworky, třeba Spring.           
Zde je příklad:

```Java
class Main {

    public static class Shape{
        public String calculateArea(){
            return "I have no idea, what my area is";
        }
    }
   
    /* Anotace zpravidla funguji jako takova metadata, pri samotnem zkompilovani pak jiz nehraji roli
     * Napr. anotace FunctionalInteface nam bude rvat, kdyz se pokusime pridat to rozhrani dalsi metodu. Functional interface musi mit totiz prave jednu
     */
    @FunctionalInterface
    public static interface ExtremelyFunctional {
        void doSomethingVeryFunctional(); 
    }

    public static class Square extends Shape implements ExtremelyFunctional{
        
        /* Nase stara znama Override anotace. V postate nic nedela, jen informuje programatora o tom, ze metoda je prepsana z rodicovske tridy */
        @Override
        public String calculateArea(){
            return "My side on the power of two";
        }

        /* Podobne jako u Override, Deprecated nas muze informovat o metode, ktera jiz byla nahrazena nejakou lepsi */
        @Deprecated
        public void doSomethingVeryFunctional(){
            /* Z tech uzitecnejsich anotaci je tu treba SupressWarnings, ktera nam dovede umlcet nejake varovani od naseho vyvojoveho prostredi */
            @SuppressWarnings("unused")
            int unused = 10;
        }

    }

    public static void main(String args[]){
    }    
}
```

Operátory. Nu, mám jich hodně. Od těch aritmetických až po různé speciální operátory. Některé se dají přepsat, některé nedají. Nebo se nedá přepsat vůbec nic, pracujeme-li v Javě. Můžeme je rozdělit na unární, binární a ternární podle počtu výrazů, se kterými pracují.            
Unární operátor je např. **!**, negace.             
Binární je v podstatě každý aritmetický operátor od sčítání po modulo.          
Ternární operátor znám jen jeden, lze ho velmi hezky využít, ale ne každý programovací jazyk ho implementuje. Vypadá asi takhle: **Vyraz ? proved pokud vyraz plati : proved pokud vyraz neplati**.             
Neměli bychom zapomínat, že např. závorky, pomocí kterých přistupujeme k prvkům v poli, jsou také operátor. V některých jazycích i ty lze přepsat.                  
Tady je takový výčet operátorů dostupných v jazyce C:

```C
#include <stdio.h>

void main(){
    // Operatory
    // ---------

    // Aritmeticke 
    int aa = 1 + 1; // Soucet
    int bb = 1 - 1; // Rozdil
    int cc = 1 * 1; // Socin
    int dd = 1 / 1; // Podil .. pozor na vysledek. Zde bude vzdy celociselny, protoze ho ukladame do promenne typu int
    int ee = 1 % 1; // Modulo AKA zbytek po deleni
    aa++; ++aa;   // Pricist 1 k promenne. POZOR, zalezi na tom, zda to napisete pred, nebo za promennou
    bb--; --bb;   // Odesict 1 od promenne. POZOR, -//-

    // Prirazovaci
    // Nebudu je listovat vsechny, ukazu prvni tri, ostatni si domyslite, funguje to v podstate s kazdym aritmetickym a bitovym operatorem
    int ff = 10;
    ff += 2;
    ff /= 3;
    ff %= 4;

    // Porovnavaci
    bool one = (1 == 1);
    bool two = (1 != 1);
    bool three = (1 > 1);
    bool four = (1 < 1);
    bool five = (1 >= 1);
    bool six = (1 <= 1);

    // Bitove
    char bit = 2;
    bit = 2 & 1;   // AND
    bit = 2 | 6;   // OR
    bit = 0x2 ^ 10;  // XOR
    bit = bit << 2;// Left shift
    bit = bit >> 4;// Right shift

    // Logicke
    bool log = 1 && 1;  // AND
    log = 1 || 1;   // OR
    log = !log; // Negace

    // Ternarni operator
    // Velmi uzitecny operator. Na zaklade vysledku operace pred otaznikem prideli intu bud hodnotu 12, je-li uspesna, nebo 13 v opacnem pripade
    int hello = (1 == 1) ? 12 : 13;

    return 0;
}
```

Zde je výčet některých operátorů v Pythonu:

```Python
""" Operators """

# Arithmetic

1 + 1
1 - 1
2 * 2
3 / 3
3 // 3
4**2
4 % 3

# Comparison

1 == 1
2 != 1
2 > 1
2 < 1
2 >= 1
2 <= 1

# Assignment

x = 0
x += 2
x -= 5
x *= 10
x /= 2
x //= 7
x **= 3
x % 9

# Logical

x == x
x and x
x or x
not x

# bitwise

1 & 1   # AND
1 | 1   # OR
~1  # NOT
1 ^ 1   # XOR
1>>1    # BIT SHIFT RIGHT
2<<2    # BIT SHIFT LEFT
```

Materiál
---

Coding with John - Annotations in java tutorial -   https://inv.nadeko.net/watch?v=DkZr7_c9ry8              
Coding with John - Java Strings are Immutable - https://inv.nadeko.net/watch?v=Bj9Mx_Lx3q4          
