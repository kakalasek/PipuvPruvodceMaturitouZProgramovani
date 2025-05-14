Zpracování a parsování textových dat, regulární výrazy, kódování a stringy
===

Povídání
---

Než se posuneme k reprezentaci stringů v kódu, podíváme se na kódování a co to vlastně ten string je.           
String je textový řetězec, což o něm vlastně říká hodně. Je to prostě nějaký počet znaků za sebou. Ne však jen písmen, ale taky různých mezer a speciálních znaků (null terminator, carriage return, ...). Kdysi stáli nějací lidé před problémem. Jak zakódovat do čísel písmena? Nejdříve přišli s něčím, čemu se říká ASCII. Tato tabulky reprezentuje mapování číselných hodnot ke znakům. Ve své původní podobě má pouze 7 bitů, takže jen 128 znaků. Nachází se tam znaky malé a velké abecedy, interpunkce, speciální znaky. Později bylo vytvořena ASCII Extended, která obsahuje 256 různých znaků. Ještě dnes se s ním hojně setkáte.          

```C
#include <stdio.h>

int main(){

    char c = 77;

    printf("This character is under the number 77 in ASCII encoding: %c", c); 

    return 0;
}
```

String tedy není nic jiného, než sekvence bytů, které překládáme jako řetězec znaků. ASCII ale samozřejmě už dlouho nestačí. Kódování, se kterým se setkáte asi nejčastěji, je Unicode. Unicode je opět pouze velmi velká tabulka čísel a písmen jim přiřazených. Znaky Unicodu můžeme reprezentovat pomocí UTF-8, UTF-16 nebo UTF-32. Vyhnu se zbytečným detailům. Rozdíl je v tom, jakým způsobem jednotlivé kódování zakóduje číslo do bitů. Např. UTF-8 se snaží efektivně šetřit místo, takže ačkoliv Unicode znak teoreticky může nabývat 32 bitů, při využití UTF-8 mohou některé znaky být kratší.          
Prvních 128 znaků Unicodu je stejných jako v ASCII, co že je velká výhoda v rámci zpětné kompatibility a zvyku.             
Existují i jiná kódování, ale pro ilustraci nám stačí Unicode a ASCII.              
Ukážeme si teď, jak vypadá string v Céčku a pak v Javě, abychom si udělali nějakou představu.               
V jazyce C se string vytváří prostě jako pole charů, které je ukončené null terminátorem (\0). To dost hezky ukazuje, co string vlastně je, prostě pole znaků uložené v paměti. Protože je to pole, dostaneme dokonce jen pointer kamsi na haldu na začátek našeho pole.            

```C
#include <stdio.h>

int main(){

    char my_string[50] = "Hello there";

    printf("%s", my_string);

    return 0;
}
```

V jazyce C++ už je to trochu abstraktnější. Existuje tu datový typ *string*. Ten už je trochu chytřejší a umí více věcí. Měl by být také uložen na haldě, nicméně to může být závislé na využití a implementaci.            

```C++
#include <iostream>
#include <string>

using namespace std;

int main(){

    string s = "Hello there!!!!!";

    cout << s << endl;    

    return 0;
}
```

A v poslední řadě Java. V Javě je string třída. Když vytváříme nějaký string, je nám vrácen ukazatel na haldu (ačkoliv to je za abstrakcí), vytváříme nový objekt. Stringy v Javě mají hned několik vlastnostní. Za prvé, jsou immutable. To znamená, že jakmile je vytvoříme, už je nemůžeme přepsat. Při přepsání ukazatele se vytvoří nový objekt a přepíše se ukazatel, starý objekt zaniká. Také jsou uloženy ve svém vlastním místečku v paměti. Dva rozdílné ukazatele mohou koukat na jeden string (v rámci úspornosti). Proto jsou mimo jiné Stringy v Javě neměnné. Celý tento mechanismus je totiž skrytý pod oponou abstrakce. A bylo by nežádoucí, kdyby bez našeho vědomí nějaký jeden náš string přepsal nějaký jiný.

```Java
public class Main{
    public static void main(String[] args) {
        String str1 = "Ho there, traveller";
        String str2 = "Hello there";
        
        System.out.println(str1); 
        System.out.println(str2); 
    }
}
```

Často musíme zpracovávat textová data od uživatele. Zpravidla chceme data v nějakém tvaru. Nechceme tam třeba písmena, nebo naopak nechceme čísla. Cokoliv chceme omezit, pomůže nám regex. Regulární výrazy jsou speciálním jazykem pro vybírání částí textů. Dovedou ale text nejen vybírat, ale pomocí nich jsme také schopni zhodnotit, zda string obsahuje to, co chceme. Ukážeme si pár příkladů.             
Začneme jednoduchým regexem, který ověří, zda v textu nachází alespoň jedno číslo.

```Regex
.*\d.*
```

Dále můžeme ověřovat třeba email (zjednodušeně samozřejmě).

```Regex
^[a-zA-Z\d]+@[a-zA-Z]+\.[a-z]{1,3}$
```

Zkusím jen zběžně vysvětlit, co co znamená. **^** udává začátek řádky, **$** udává, že na daném místě to musí končit. **[a-z]** znamená, všechny znaky od a po z. Nápodobně je to i s ostatními znaky v hranatých závorkách. **\*** znamená, že znak před ní, se má nacházet nula až nekonečně krát. **+** je stejné, jen je to jednou až nekonečně krát. **{1, 3}** říká, že se znak před ní má nacházet 1 až 3 krát. Tečka kóduje jakýkoliv znak.                 
Zkusíme si teď v Javě jednoduchou aplikaci, která zkontroluje, zda je string zadaný uživatelem platný email (dle mé aplikace samozřejmě).           

```Java
import java.util.Scanner;

public class Main{
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String userEmail;
        userEmail = sc.nextLine();

        if(userEmail.matches("^[a-zA-Z\\d]+@[a-zA-Z]+\\.[a-z]{1,3}$")){
            System.out.println("Your email is valid");
        } else {
            System.out.println("Your email is invalid");
        }
    }
}
```

Typická je metoda matches, která najde, zda string souhlasí s regexem.              
Se stringy lze dělat i spousty jiných kravinek. Můžeme v nich hledat, různě je splitovat, měnit v nich znaky, ...           
String processing je jedna velká věda, my si můžeme ukázat jen pár příkladů. Třeba v Pythonu.           

```Python
s = "Ahoj, ja jsem Vojta a jsem uplne retardovanej, ale uplne"

# Najde, zda se substring nachazi ve stringu
if s.find("Vojta") != -1:
    print("Je tam Vojta")

# Vrati novy string s nahrazenym substringem
s = s.replace('retardovanej', 'nejlepsi')
print(s)

# Najde, zda se substring nachazi ve stringu, jen elegantneji
if "Ahoj" in s:
    print("Je tam pozdrav")
```

Materiály
---
Deliciousbrains - How unicode works - https://deliciousbrains.com/how-unicode-works/