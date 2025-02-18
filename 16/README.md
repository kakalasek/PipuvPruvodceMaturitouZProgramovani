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

Druhým jednoduchým formátem je JSON (Javascript Object Notation). Tento formát dovede velmi jednoduše uložit objekt. Dá se dobře parsovat do dictionary. Podporuje řadu datových typů, od objektů přes pole ke klasickým stringům a numberickým datovým typům.               
Já osobně ho mám nejraději, je dobře čitelný a dobře se s ním pracuje. Často se využívá u webových aplikací, prací s HTTP.

![XML](xml.jpg)

Dalším dříve hojně používaným formátem je XML (Extensible Markup Language). Vychází z podobné notace jako HTML. Má své výhody, jako třeba XML schéma. Nicméně osobně jsem s ním nijak extensivně nepracoval, tak maximálně v nějakém konfiguračním souboru, třeba Maven ho využívá.                      
Nevýhodou je, že kvůli nutnosti otevíracího a uzavíracího tagu u každého záznamu mohou být větší XML soubory skutečně větší.

![YAML](yaml.jpg)

Posledním, tentokrát velmi elegantním, formátem souboru, je YAML (YAML Aint Markup Language). Narozdíl od všech předchozích formátu aktivně využívá whitespaci, tedy neviditelné znaky, mezera, newline, ...                
Využívá ho např. Ansible nebo Docker-compose. V rámci serializace jsem s ním nikdy nepracoval, opět pouze jako konfigurační soubor nějaké externí aplikace.

Do souboru se zpravidla zapisuje pomocí tzv. streamů. Streamem, který určitě znáte např. v Javě, je System.out a System.in. Jeden dovede načítat data z konzole, druhý je dovede vypsat. Takový stream ale můžeme vytvořit v podstatě libovolný. Můžeme do něj psát data, která se budou posílat na síť, nebo psát a číst data do a ze souboru.             
Soubory lze číst a zapisovat charakter po charakteru, byte po bytu, řádek po řádku. Zkrátka, jak se nám to hodí. Programovací jazyk nám k tomu dá patřičné nástroje.

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