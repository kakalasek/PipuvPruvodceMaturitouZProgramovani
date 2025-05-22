Dědičnost, method overriding, function overloading
===

Povídání
---

Dědičnost je princip v OOP, který nám dovoluje vytvořit rodičovskou třídu, od které lze oddědit společné vlastnosti a metody. Klasickým příkladem může být např. vozidlo. Každé vozidlo bude mít spotřebu, motor, maximální rychlost, bude se moci rozjet, zabrdit, natankovat, ...             
Místo toho, abychom každou z těchto vlastností a metod programovali do každé třídy, můžeme si vytvořit nějakou společnou třídu vozidlo. Každá třída odděděná od této třídy bude mít stejné vlastnosti a metody a bude si moci přidat nějaké své navíc.              
Dokonce můžeme i přepsat metody z rodičovské třídy. Tomu se říká method overriding. Je to běžná procedura.                      
Takto může vypadat dědičnost v Pythonu. Python to má velmi jednoduché. Třída, od které dědíme, se napíše do závorek za jméno naší třídy. Python dovoluje mnohonásobnou dědičnost. Můžeme tedy dědit od více než jedné třídy.

```Python
class Human:
    
    def __init__(self, name, health, base_damage):
        self._name = name
        self._health = health
        self._base_damage = base_damage

    def get_name(self):
        return self._name
    
    def get_health(self):
        return self._health
    
    def take_hit(self, amount):
        if self._health - amount < 0:
            self._health = 0
        else:
            self._health = self._health - amount

    def heal(self, amount):
        self._health = self._health + amount

    def hit(self):
        return self._base_damage
    

class Warrior(Human):

    def __init__(self, name, health, base_damage, strength):
        super().__init__(name, health, base_damage)
        self._strength = strength

    def hit(self):
        return self._base_damage + self._strength

class Ranger(Human):

    def __init__(self, name, health, base_damage, agility):
        super().__init__(name, health, base_damage)
        self._agility = agility

    def take_hit(self, amount):
        if amount < self._agility:
            return

        if self._health - amount < 0:
            self._health = 0
        else:
            self._health = self._health - amount


if __name__ == "__main__":
    warrior = Warrior("Big Man", 100, 12, 2)
    ranger = Ranger("Middle Man", 80, 8, 16)

    print("Warrior health: " + str(warrior.get_health()))
    print("Ranger health: " + str(ranger.get_health()))

    warrior.take_hit(ranger.hit())
    ranger.take_hit(warrior.hit())

    print()

    print("Warrior health: " + str(warrior.get_health()))
    print("Ranger health: " + str(ranger.get_health()))
```

V Javě se využívá klíčové slovíčko *extends*. Java narozdíl od Pythonu nedovoluje vícenásobné dědění. Místo toho má koncept Interfacu.              
Interface je třída, která však obsahuje jen hlavičky metod bez jejich implementace. Pro využití interfacu můžeme využít klíčové slovíčko *implements*. Implementovat můžeme i více než jeden interface.                 
Třída:

```Java
class Main{

    public static class Human{

        protected String name;
        protected int health;
        protected int baseDamage;

        public Human(String name, int health, int baseDamage){
            this.name = name;
            this.health = health;
            this.baseDamage = baseDamage;
        }

        public String getName() {
            return name;
        }

        public int getHealth() {
            return health;
        }

        public void takeHit(int amount){
            if(health - amount < 0){
                health = 0;
            } else {
                health = health - amount;
            }
        }

        public void heal(int amount){
            health = health + amount;
        }

        public int hit(){
            return baseDamage;
        }

    }

    public static class Warrior extends Human{

        private int strength;

        public Warrior(String name, int heal, int baseDamage, int strength){
            super(name, heal, baseDamage);
            this.strength = strength;
        }
        
        @Override
        public int hit(){
                return baseDamage + strength;
            }

    }
    
    public static class Ranger extends Human{

        private int agility;

        public Ranger(String name, int heal, int baseDamage, int agility){
            super(name, heal, baseDamage);
            this.agility = agility;
        }

        @Override
        public void takeHit(int amount){
            if(amount < agility) return;

            if(health - amount < 0){
                health = 0;
            } else {
                health = health - amount;
            }
        }
    }

    public static void main(String[] args) {
        Warrior warrior = new Warrior("Big Man", 100, 12, 2);
        Ranger ranger = new Ranger("Middle Man", 80, 8, 16);

        System.out.println("Warrior health: " + warrior.getHealth());
        System.out.println("Ranger health: " + ranger.getHealth());

        warrior.takeHit(ranger.hit());
        ranger.takeHit(warrior.hit());

        System.out.println();

        System.out.println("Warrior health: " + warrior.getHealth());
        System.out.println("Ranger health: " + ranger.getHealth());
    }
}
```

Interface:

```Java
class Main{

    public static interface Shape{

        int calculateArea();
        
    }

    public static class Square implements Shape{

        int a;

        Square(int a){
            this.a = a;
        }

        @Override
        public int calculateArea() {
            return a * a;
        } 

    }
    
    public static class Rectangle implements Shape{

        int a;
        int b;

        Rectangle(int a, int b){
            this.a = a;
            this.b = b;
        }

        @Override
        public int calculateArea() {
            return a * b;
        } 

    }

    public static void main(String[] args) {
        Shape shapes[] = {new Square(5), new Rectangle(5, 6)};
        for (Shape shape : shapes){
            System.out.println(shape.calculateArea());
        }
    }
}
```

Exisuje také fenomén, kterému říkáme polymorfismus. Řekněme, že vytvoříme třídu zvířátko, které bude moci udělat zvuk. Nicméně jaký zvuk dělá zvíře? No, záleží na tom, co za zvířátko to je. Takže v této třídě necháme tuto metodu prázdnou. Vlastně dokonce nemusíme ani psát tělíčko této metody, stačí nám hlavička, která může vypadat nějak takto: **void makeSound();**.            
Když se vrátíme k našemu milovanému interfacu. Lze ho využít právě třeba pro efektivní implementaci polymorfismu.           
V programovacích jazycích, jež interface nemají, Python a C++ např., existuje alespoň koncept abstraktní třídy, která funguje v podstatě obdobně, ačkoliv mají své rozdíly. Abstraktní třídy třeba mohou vytvořit nějaké metody, která mají konkrtétní implementaci. Všechny metody v interfacu musí být bez tělíčka. Abstraktní třída vás také neochrání před některými problémy dědění, které si za chvíli představíme. Od abstraktní třídy také nemůžeme vytvořit konkrétní instanci.           
Dobře, zpět k polymorfismu. Máme tedy abstraktní třídu, ve které je pouze tělíčko metody pro udělání zvuku. Abstraktní třídu nemůžeme vytvořit samu o sobě, to by nedávalo smysl, metody v ní přece nejsou implementované. Když si teď ale vytvoříme několik tříd zvířátek, třeba gorila, pes, kočička, ... a každou z nich od abstraktní třídy oddědíme, můžeme každému zvířátku metodu předělat tak, aby udělalo svůj specifický zvuk.            
Protože jsou to všechno zvířátka, můžeme deklarovat obecné zvířátko a inicializovat ho jako konkrétní zvířátko. Když pak na tomto objektu zavoláme metodu, která dělá zvuk, uvidíme zvuk našeho zvířátka. Hezké že?             
Můžeme tedy uložit potomka do rodiče, ale pozor, nikoliv naopak!                
Demonstrujeme si tento koncept opět v Javě. Ale ne pomocí interfacu, ale pomocí abstraktní třídy.           

```Java
public class Main {
    public static void main(String[] args) {
        Animal animal = new Cock();
        animal.makeSound();
        animal.die();
    } 
}

abstract class Animal {
    public abstract void makeSound();
    public void die(){
        System.err.println("Dead, not a big surprise");
    }
}

public class Cock extends Animal{

    @Override
    public void makeSound() {
        System.err.println("Kikiriki");
    }

}
```

Poslední koncept, který jsme si nezmínili, je function overloading (popř. method overloading, je to to samé). Řekněme, že máme naivní funkci sčítání v nějakém staticky typovaném jazyce. Chceme aby uměla sčítat proměnné typu int i proměnné typu float. Ale nechceme vytvářet funkce dvě. Právě k tomu slouží method overloading.            
Můžeme vytvořit dvě fce se jménem *add*. Jedna bude ale přijímat dva parametry typu int a druhá dva parametry typu float. Kompiler to rozezná jako dvě rozdílné metody. Stejným způsobem můžeme metody rozlišit podle návratového typu, počtu argumentů, ...            
U maturity ale pozor, Python tuto funkci nemá! Chcete-li ji demonstrovat, budete muset využít jiný jazyk.               
Třeba opět v Javě:

```Java
public class Main {
    public static void main(String[] args) {
        AddMaster3000 AddMaster3000 = new AddMaster3000();
        System.err.println(AddMaster3000.add(10, 10));
        System.err.println(AddMaster3000.add(12.5f, 31.678f));
    } 
}

public class AddMaster3000 {
    public int add(int a, int b){
        return a + b;
    } 

    public float add(float a, float b){
        return a + b;
    }

    public long add(long a, long b){
        return a + b;
    }
}
```

Zmínil jsem, že existuje jistý problém s abstraktiní třídou, porovnáváme-li ji s interfacem. Bylo by nefér to tedy neobjasnit. Zmiňovali jsme si mnohonásobnou dědičnost.                      
Při tomto přístupu mohou nastat různorodé problémy. Co, když se metoda z obou tříd, ze kterých dědíme, jmenuje stejně? Jakou máme použít? Nebo co když obě odděděné třídy dědí od stejného rodiče? Tomu se říká problém diamantu.           

![Diamond Problem](diamond_problem.png)

Nu, budeme v tom mít zkrátka velký guláš. Nicméně kompiler se s tím zpravidla vypřádá jednoduše. Když dědíme od více tříd, vypisujeme je postupně. No, kompiler prostě vezme tu první a řekne, tohle je tvoje implementace.             
Proč je interface o tolik lepší? No, narozdíl od jazyků jako Python a C++, Java zakazuje dědění od více než jedné třídy, čímž efektivně eliminuje tento problém. Ale nemyslete si, že nás to nějak limituje. Můžeme implementovat neomezené množství interfaců. Pamatujete? Interface nemůže obsahovat tělíčko metody, tedy ani žádnou konkrétní implementaci. Kdyby se nám náhodou nedopatřením stalo, že zdědíme stejnou metodu jako nějakou, kterou implementujeme, zkrátka se vezme zděděná implementace. Interface bude spokojený, že jeho metoda je ve třídě implementována a nám to nezpůsobí žádné problémy. Java jede ..               
Že to má i ostré cé? Myslíte Javu od Microsoftu? Asi odmítnu