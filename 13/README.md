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
Prakticky může vypadat třeba takto:

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

Druhý známy creational pattern je factory metoda. Je to docela intuitivní. V Javě ji lze implementovat s využitím interfacu. Dole je kódový příklad, ať to nemusím vypisovat. Nicméně jde o to, že na základě nějakého kritéria chceme vytvořit jeden z několika objektů. Vytvoříme si tedy metodu, která vrátí jeden z těchto objektů na základě té naší podmínky.                 
Praktická implementace může vypadat takto:

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

**Structural patterns** jsou patterny, které řeší, jak jsou jednotlivé objekty poskládané vůči sobě tak, aby byly flexibilní a efektivní. Příkladem může být dekorátor nebo bridge. Jsou zde také vzory, které se snaží o úsporu místa při vytváření nových objektů (Flyweight pattern, bridge pattern). Zkuste se na tyto patterny podívat sami, třeba princip structural patternů pochopíta lépe.              
Příkladem může být také fasáda. Ta se využívá, máme-li nějakou velkou, složitou knihovnu a potřebujeme jen několik málo metod z ní nebo si chceme přístup k ní zjednodušit. Implementujeme tedy třeba nějakou funkci, naši fasádu, která provede jen to nezbytně nutné a odstíní nás od detailů knihovny.               
Prakticky se můžeme podívat třeba na dekorátor. Dekorátor nám dovoluje k objektu přidávat dynamicky funkcionality pomocí wrapper objektů, které dané funkcionality obsahují.                         
Takto by takový dekorátor mohl vypadat v Javě:

```Java

```

**Behavioral patters** jsou patterny, které už se zabývají nějakým konkrétním chováním objektů, algoritmy. Třeba strategy pattern se zabývá implementací správného postupu, strategie, k problému, kde lze vybírat z několika postupů.                  
V Javě může vypadat nějak takhle:

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

    private Weapon weapon;  // Misto toho, bychom delali vice trid podle zbrane, vyuzijeme kompozici a udelame ze zbrane vlastnost tridy.
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

Iterátor, nám dobře známý, se stará o implementaci jednoduchého procházení kolekcí. Command pattern nám pomáhá vytvořit kvalitní meníčka.               

Materiály
---

Refractoring Guru - https://refactoring.guru