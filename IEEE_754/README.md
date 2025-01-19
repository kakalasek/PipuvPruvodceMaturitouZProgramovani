IEEE 754
===

Povídání
---

Zkuste v nějakém programovacím jazyku přičíst 0.1 k 0.2. Pokud očekáváte jako výsledek 0.3, je mi líto vám sdělit, že takto to bohužel ve světě dnešních počítačů nefunguje. Počítač reprezentuje desetinná čísla tak docela jinak, dokonce je pro aritmetiku s desetinnými čísly vyhrazen speciální chip, tzv. FPU (Floating Point Unit).                  
Dobrá, jak to tedy ten počítač dělá? Nu, využívá k reprezentaci desetinných čísel standardu IEEE 754. Kdo chce, může si přečíst přesnou definici, nicméně já se ho tu pokusím alespoň trochu shrnout tak, aby jste si pak u maturity náhodou neudělali ostudu. 

![Floating_point](Floating_point_standard.jpg)

Obrázek výše je potichu ukradený z GeeksForGeeks a ukazuje, jakým způsobem počítač reprezentuje reálná čísla. Tento kokrétní případ ukazuje reálné číslo uložené ve 32 bitech, 64 bitů (tedy double, jako double precision) mění pouze velikost exponentu a mantisy. Počítač tedy reprezentuje reálná čísla tzv. věděckou notací (třeba 3*10^8). Rozdělí tedy reálné číslo na exponent a mantisu. Např. číslo 325.32 by mohlo být uloženo následovně. 3.2532 by se nacházelo v mantise a 129 by se nacházelo v exponentu.               
Proč prohoba 129? Hraje zde roli tzv. bias. Nebudu zacházet do detailů, nicméne v případě 32 bitového reálného čísla je to 127. Toto číslo znamená na nultou. Tento bias máme proto, abychom mohli reprezentovat i záporné mocniny desíti. Pokud by se tedy v exponentu nacházelo číslo menší, znamenalo by to posouvat desetinnou čárku na druhou stranu. 
**Sign** je pole, které říká, zda je číslo kladné (0), nebo záporné (1).            
**Exponent** je .. well exponent, který zahrnuje nám již známý bias.
**Mantissa** je pole, kde je uloženo samotné číslo ve tvaru, který jsme si ukázali.             
A teď se konečně dostaneme k tomu, proč 0.1 + 0.2 není 0.3. Je to jednoduché. Pokud vytváříme desetinné číslo v desítkové soustavě, využíváme desetiny, setiny, tisíciny, ... Ve dvojkové soustavě je to ale tak docela jiné. Využíváme poloviny, čtvrtiny, osminy, šestnáctiny, ... No a pokud se pomocí nich snažíme vytvořit třeba právě číslo 0.1, zjistíme, že je periodické.          
Jak se počítače s tímto problémem vypořádávají? Číslo zkrátka zaokrouhlí.        
Co si z toho můžeme odnést? Nu, že reprezentace reálných čísel je v počítačích tak trochu oříšek a nic nejde úplně přesně.

Materiály
---

Computer Science Lessons - IEEE 754 Standard for Floating Point Binary Arithmetic - https://inv.nadeko.net/watch?v=RuKkePyo9zk              
Computerphile - Floating Point Numbers - https://invidious.privacyredirect.com/watch?v=PZRI1IfStY0              
Náhodná prezentace o  IEEE 754 - https://people.iith.ac.in/rogers/pds_theory/lect15_truncated.pdf        
IEEE 754 definice standardu - https://pcv.oss-cn-shanghai.aliyuncs.com/wp-content/upload/2022/12/ieee-std-754-2019.pdf