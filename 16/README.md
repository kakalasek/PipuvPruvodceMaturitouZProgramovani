Soubory a serializace - Ukládání a načítání dat, formáty souborů
===

Povídání
---

Nuže, podíváme se nejdříve na jednolivé formáty souborů. Nebo alespoň na ty typické. Pak si v kódu ukážeme, jak lze do nějakého z nich zapsat a jak z některých číst.           

![CSV](csv.PNG)

První formát, který si ukážeme, je zároveň ten nejjednodušší a nejintuitivnější, CSV (Comma Separated Values). Jsou to zkrátka a dobře hodnoty oddělené čárkou. Nemusí to nutně být čárka, zpravidla to bývá třeba ještě středník. Teoreticky to může být jakýkoliv znak, který se nenachází nikde v našich datech.             
Běžně se první řádek ponechává na pojmenování sloupců.              
Práce s CSV souborem je velmi jednoduchá. Rozdělené řádky se dobře parsují na list. CSV soubory lze také jednoduše naimportovat do Excelu nebo do databáze.

![JSON](json.png)

Druhým jednoduchým formátem je JSON (Javascript Object Notation). Tento formát dovede velmi jednoduše uložit objekt. Je velmi jednoduché ho parsovat do dictionary. Podporuje řadu datových typů, od objektů přes pole ke klasickým stringům.               
Já osobně ho mám nejraději, je dobře čitelný a dobře se s ním pracuje.

![XML](xml.jpg)

Další dříve hojně používaným formátem je XML. Vychází z podobné notace jako HTML. Má své výhody, jako třeba XML schéma. Nicméně osobně jsem s ním nijak nepracoval.

![YAML](yaml)

Poslední

Ukázky kódu
---

**Python - Read/Write Csv**
**Python - Read/Write Json**

**Java - Read/Write Csv**
**Java - Read/Write Json**

**C++ - Read/Write Csv**
**C++ - Read/Write Json**

Materiály
---

Coding with John - Java File Input/Output - It's Way Easier Than You Think - 