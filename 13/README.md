Návrhové vzory - creational design patterns, structural design patterns, behavioral patterns
===

Povídání
---

Návrhové vzory. Jsem si dost jistý, že vás budou strašit ve spaní ještě dlouho po maturitě. Nicméně my si zde ukážeme, že nejsou tak hrozné.            
Vynecháme architektonické návrhové vzory, na ty je samostatná otázka. Návrhové vzory můžeme tak nějak rozdělit do tří skupin. Rovnou se přiznám, že budu hodně vycházet především ze stránky Refracoring Guru, mají to tam velmi pěkně popsané a zpracované.        
Ještě předtím, než si několik paternů projdeme, by se hodilo zmínit, že jejich implementace velmi závisí na vybraném jazyce. Některé patterny dokonce není v některých jazycích vůbec třeba implementovat, protože už je nabízí sám od sebe. A také nějaké ponětí o tom, co to vlastně ty návrhové vzory jsou. Jsou to nějaká řešení určitých programovacích problémů, které se vyskytovaly tak často, že se hodilo zapsat nějaký ucelený způsob jejich řešení. Návrhové vzory se také zpravidla spoléhají na OOP.          
**Creational patterns**. Tak ze nazývá první ze tříd. Zabývají se vytvářením objektů. Dobrými příklady, které všichni známe, jsou singleton a factory metoda. Podíváme se na tyto dva trochu zblízka, abychom pochopili, co to jsou ty creational patterny.         
Singleton je návrhový vzor, který se využívá, chceme-li nějaký objekt inicializovat v našem projektu jen jedno. Resp. chceme-li v celém našem projektu jen jednu jeho instanci. Kdy se nám to může hodit? Nu, párkrát už jsem ho využil, nicméně z fleku si vzpomenu jen na připojení k databázi. To nám zpravidla stačí jen jedno a inicializace několika by mohla působit nechtěné problémy. Singleton zaručí, že v jednu chvíli bude existovat jen jedna instance.           
Jak toho dosáhne? V Javě se vytvoří ve třídě statická metoda a statická vlastnost *instance*, kterou defaultně nastavíme na null. Konstruktor uděláme privátní a dovolíme objekt vytvořit pouze pomocí té statické metody. V případě, že ještě nebyla vytvořena instance třídy, metoda vytvoří a vrátí její instanci. Zároveň ale do vlastnosti *instance* uloží tuto instanci. Takže při příštím pokusu o vytvoření objektu zkrátka vrátí tu samou instanci.               
Druhý známy creational pattern je factory metoda. Je to docela intuitivní. V Javě ji lze implementovat s využitím interfacu. Dole je kódový příklad, ať to nemusím vypisovat. Nicméně jde o to, že na základě nějakého kritéria chceme vytvořit jeden z několika objektů. Vytvoříme si tedy metodu, která vrátí jeden z těchto objektů na základě té naší podmínky.                 
**Structural patterns** a **Behavioral patters**. Teď se vám přiznám. Konkrétní rozdíl mezi těmito dvěma druhy jsem možná nepochopil tak úplně. Nicméně se posnažím ho tu nějak zformulovat. Mezi structural návrhové vzory patří nepř. dekorator nebo bridge. Tyto vzory se starají o uspořádání objektů tak, aby se daly co nejlépe využít samy o sobě a změny v jiných objektech na ně měly co nejmenší vliv. Také se snaží o úsporu místa v rámci vytváření nových objektů (Flyweight pattern, bridge pattern). Zkuste se na tyto patterny podívat sami, třeba to pochopíte lépe.           
Behavioral patterns jsou patterny, které už se zabývají nějakým konkrétním chováním objektů, algoritmy. Třeba strategy pattern se zabývá implementací správného postupu, strategie, k problému, kde lze vybírat z několika postupů. Iterátor, nám dobře známý, se stará o implementaci jednoduchého procházení kolekcí. Command pattern nám pomáhá vytvořit kvalitní meníčka.               
Upřímně, nejlépe pochopíte význam těchto vzorů, když si je zkusíte naprogramovat. Nebo alespoň juknete na mé kódové příklady některých známějších patternů.

Ukázky kódu
---

Vzhledem k charakteru návrhových vzorů je nejjednodušší je programovat v nějakém solidním OOP jazyce. Všechny příklady zde tudíž budou v Javě.

### Creational Design Patterns

**Singleton**

```Java
public class MySingleton {

    private static MySingleton instance = null;
    private int myNumber;

    public static MySingleton createMe(int myNumber){
        if(instance != null){
            return instance;
        }
        instance = new MySingleton(myNumber);
        return instance;
    }

    private MySingleton(int myNumber){
        this.myNumber = myNumber;
    }

    public int getMyNumber() {
        return myNumber;
    }
}
```

**Factory Method**

```Java
public class Main{

    public static FastFood giveMeFood(int howHungry){
        if(howHungry > 10){
            return new BigMac();
        }
        return new Cheeseburger();
    }

    public static void main(String[] args) {
        FastFood food = giveMeFood(11);
        food.consume();
    }
}

public interface FastFood {
    void consume();
}

public class Cheeseburger implements FastFood{
    @Override
    public void consume() {
        System.out.println("Mňam, mňam, mňam, je to fresh, mám to rád");
    }
}

public class BigMac implements FastFood{
    @Override
    public void consume() {
        System.out.println("BIGMAC!");
    }
}
```

### Structural Design Patterns

**Bridge**

```Java
public class Main{

    public static void main(String[] args) {
        Hero hero = new Hero(new Sword());
        System.out.println(hero.attack());
        hero.changeWeapon(new Axe());
        System.out.println(hero.block());
    }
}

public class Hero {

    private Weapon weapon;  // Tohle je ten most. Misto toho, bychom delali vice trid podle zbrane, vyuzijeme kompozici a udelame ze zbrane vlastnost tridy.
                            // Zmeny v hrdinovy jsou tedy naprosto nezavisle na zmenach ve zbranich a vice versa. Zbrane navic muzeme menit za pochodu

    public Hero(Weapon weapon){
        this.weapon = weapon;
    }

    public int attack(){
        return weapon.attack();
    }

    public int block(){
        return weapon.block();
    }

    public void changeWeapon(Weapon newWeapon){
        this.weapon = newWeapon;
    }
}

public interface Weapon {
    int attack();
    int block();
}

public class Sword implements Weapon{
    @Override
    public int attack() {
        System.out.println("The sword is attacking");
        return 12;
    }

    @Override
    public int block() {
        System.out.println("The sword is blocking");
        return 2;
    }
}

public class Axe implements Weapon{
    @Override
    public int attack() {
        System.out.println("The axe is attacking");
        return 5;
    }

    @Override
    public int block() {
        System.out.println("The axe is blocking");
        return 10;
    }
}
```

**Flyweight**

```Java

```

**Decorator**

```Java

```

**Proxy**

```Java

```

### Behavioral Design Patterns

**Command**

```Java

```

**Strategy**

```Java

```

**State**

```Java

```

Materiály
---

Refractoring Guru - https://refactoring.guru