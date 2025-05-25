Výjimky a aserce, debugování a zpracování chyb
===

Povídání
---

Podíváme se teď společně na velmi důležitý koncept v programování, zpracování výjimek. Co to vůbec ta výjimka je? Je to nějaký stav v kódu, který může nastat a my se s ním ideálně chceme adekvátně vypořádat. Konkrétně, třeba dělení nulou. Nemůžeme si být jisti, že třeba uživatele nenapadne zadat do jmenovatele nulu. V takovém případě by nám program třeba mohl spadnout. To ale rozhodně nechceme, tvoříme-li kupříkladu kalkulačku.                  
Na pomoc nám přichází právě nástroje pro práci s výjimkami. Takovou výjimku pro dělení nulou můžeme odchytit a místo spadnutí programu uživateli napsat, že dělit nulou nelze.              
Tzv. Try-Catch nám obvykle slouží právě pro tento účel. Do bloku Try dáme kód, který potencionálně může nějakou výjimku vyhodit, a v bloku Catch potencionálně vyhozenou výjimku ošetříme. Catch bloků pro jeden Try může být více, nicméně pouze jeden z nich může být spuštěn v případě vyhození výjimky.             
Výjimek existuje různé množství a jejich rozdělení je závislé také na programovacím jazyce. Zpravidla jsou implementované jako třídy. Lze si vytvářet i vlastní výjimky.                
Výjimku můžeme vyhodit i my v nějaké z vlastních metod.             
Důležitým blokem, který také existuje, je blok Finally. Tento blok se provede vždy, nezávisle na tom, zda byla v kódu vyhozena výjimka, či nikoliv.             
Debugování .. nu, chceme-li se podívat, co náš kód dělá, dělá-li něco, co se nám nezdá, nebo dělá něco úplně špatně, můžeme využít debugování. Běžně to vypadá třeba tak, že si do nějaké části kódu vložíme breakpoint. To je místo, ve kterém se provádění kódu zastaví a my můžeme ovládat jeho průběh. Spouštět ho postupně po řádcích, vstupovat do jednotlivých metod, sledovat hodnoty proměnných.           
Debugovat lze také pomocí asercí. Ty zkrátka zkontrolují nějakou podmínku a je-li náhodou nepravdivá, zastaví program.

Ukázky kódu
---

**Python - Error Handling**

```Python
def basicErrorHandling():
    try:
        10/0
    except ZeroDivisionError as e:
        print("Cannot devide by zero")
    except Exception as e:
        print(f"What the hell happened?: {e}")

def ErrorHandlingWithElse():
    try:
        10/1
    except ZeroDivisionError as e:
        print("Cannot devide by zero")
    except Exception as e:
        print(f"What the hell happened?: {e}")
    else:
        print("Everything went alright")

def ErrorHandlingWithFinally():
    try:
        10/0
    except ZeroDivisionError as e:
        print("Cannot devide by zero")
    except Exception as e:
        print(f"What the hell happened?: {e}")
    finally:
        print("I am Inevitable")
```

**Python - Custom Exception**

```Python
class MyException(BaseException):
    pass
```

**Java - Error Handling**

```Java 
class Main{

    public static void main(String args[]){
        try{
            int a = 10/0;
        } catch(ArithmeticException e){
            System.out.println("Cannot devide by zero");
        } finally {
            System.out.println("I am inevitable");
        }
    }
}
```

**Java - Custom Exception**

```Java
public class CustomException  extends RuntimeException{
    public CustomException(String message){
        super(message);
    }
}

```