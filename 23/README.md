Vlastnosti datových struktur - Seřazenost a opakování prvků, Indexace, hashování a klíče prvků
===

Povídání
---

Začneme se seřazeností. Seřazeností bez dalších úprav zpravidla neoplývá žádná z klasických datových struktur. Pole přirozeně seřazené není. Lze ale vytvořit mechanismus, který každý další prvek zařadí do těch předchozích, tudíž takové pole seřazené být může. To samé platí pro linked list, množinu i strom. Datová struktura, která má zabudovanou jistou formu seřazenosti, je halda. Ze shora dolů je vždy seřazena od největších čísel po nejmenší, nebo vice versa.                     
Např. Java má datovou strukturu TreeSet. To je množina, která je však přirozeně seřazená.                   
Takhle lze v Javě vytvořit pole, které se samo automaticky řadí:

```Java
public class Main {
    public static void main(String[] args) {
        SortedList s = new SortedList<Integer>();
        s.add(12);
        s.add(8);
        s.add(9);
        s.add(13);
        s.add(9);
        s.add(12);
        System.out.println(s);
    } 
}

import java.util.ArrayList;

public class SortedList<T extends Comparable> {
    
    private ArrayList<T> lst;

    public SortedList(){
        lst = new ArrayList<T>();
    }

    public void add(T newItem){
        if(lst.isEmpty()){
            lst.add(newItem);
            return;
        }

        for(int i = 0; i < lst.size(); i++){
            System.out.println("doing");
            if(lst.get(i).compareTo(newItem) <= 0){
                lst.add(i, newItem);
                return;
            }
        }
        lst.add(newItem);
    }

    @Override
    public String toString() {
        return lst.toString();
    }
}
```

Dostaneme se tedy k opakování prvků. V podstatě jediná datová struktura, která nedovoluje opakování prvků, je set neboli množina. Fakt, že nemůže mít opakující se prvky, vyplývá již z toho, že to je množina. Za neopakující se datovou strukturu lze považovat i klíče ve slovníku (Dictionary, v Javě HashMap). Ty mají nějaký klíč a hodnotu. Klíče musí být unikátní, nedovolují tudíž jejich opakování.              
Zde je využití HashSetu a HashMapy v Javě:

```Java
import java.util.HashMap;
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        HashSet<Integer> hashSet = new HashSet<Integer>();
        hashSet.add(12);
        hashSet.add(13);
        hashSet.add(12);
        System.out.println(hashSet);

        System.out.println("------------------------");

        HashMap hashMap = new HashMap<String, Integer>();
        hashMap.put("odin", 1);
        hashMap.put("dva", 2);
        hashMap.put("tri",3);
        System.out.println(hashMap.keySet());
        System.out.println(hashMap.values());
    } 
}
```

Indexace znamená, že se k prvkům pole lze dostat pomocí nějakého identifikátoru, indexu. Takovým indexem je zpravidla číslo. Jako jistou formu indexace lze považovat i klíč prvku. Indexované je tedy rozhodně pole a všechny jeho možné formy (linked listy zpravidla bývají také indexované, ačkoliv nemusí). Také dictionary používá klíče. Nicméně zde to již nemusí být pouhá čísla.                  
Neindexovaný je Set. To je prostá množina, prvky jsou v ní uspořádány tak docela nahodile. Neindexovaná je také halda. Z ní můžeme vzít vždy prvek úplně zeshora. Podobným způsobem mohou být neindexované struktury zásobníku a fronty.            

Implementace množiny velmi často závisí na něčem, čemu se říká hashování. Podrobněji jsem ho vysvětloval v otázce o integritě dat, logování a bezpečnosti. Nicméně tak ve zkratce .. hash je řetězec, který vznikne při prohnání algoritmu z nějakého stringu. Důležité je, aby stejný string dal vždy stejný hash. Může se stát, že dva různé stringy dají stejný hash, nicméně při moderních hashovacích funkcích je to nepravděpodobné. Druhou podmínkou pro hash je, že už z něj nikdy nedostaneme zpátky původní string.                 
Jak toho tedy množina využívá? Z vloženého prvku vytvoří hash a je-li stejný jako nějakého již vloženého prvku, do množiny ho prostě nevloží. V realitě je to malinko složitější, ale zpravidla záleží na implementaci.              
Praktický příklad v Javě. Java implementuje dvě metody, HashCode a Equals. Equals porovnává, zda jsou dva objekty stejné, či nikoliv. HashCode dovede převést objekt na hash. Je pravidlem, že přepisujeme-li Equals, musíme nutně přepsat i HashCode, aby měly objekty, které jsou si rovny, stejný hash. Takhle by mohl vypadat objekt, který tyto metody má i s využitím v HashSetu:

```Java

```

Materiály
---