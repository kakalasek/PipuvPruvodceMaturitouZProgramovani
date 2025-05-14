Vlákna, Paralelní programování, Asynchronní metody, Concurrent design patterns
===

Povídání
---

Chceme-li zrychlit běh naší aplikace, často musíme přistoupit k něčemu, čemu se říká paralelní programování. Když běží něco paralelní, běží to tzv. současně. V paralelním programování tedy běží současně nějaké procesy nebo vlákna. Paralelní programování nám ale zpravidla přináší také nespočet složitých problémů. Na ty se brzy podíváme, nejdříve se ale podíváme, jak toto paralelní programování využít, resp. jak napsat program, který využívá více procesů či vláken.             
Začneme více procesy, to je možná trochu intuitivnější. Dobře se to demonstruje na procesu v Linuxu. Každý proces má svou strukturu. Plánovač rozhoduje, kdy poběží. Žije si zkrátka svým životem. Má svůj stack i heap. V Linuxu byl historicky vytvořen tak, že byl nejdříve vytvořen klon původního procesu (na chlup stejný proces) pomocí metody fork(). Následně mu byl nahrán jiný kód jedním z příkazů exec().                  
U maturity ale Linux k dispozici nejspíš nebude, takže tuto demonstraci záměrně zanedbám. Ukážeme si, jak lze proces vytvořit např. v Pythonu. Pomůže nám k tomu knihovna multiprocessing. Spuštění nového procesu znamená spuštění nové instance Python interpreteru. Zkrátka jako kdybychom spustili další kompletně nový skript. Důležité je si uvědomit, že nový proces má **svou haldu**.

```Python
from multiprocessing import Process
import os

def very_hard_computational_task(greetings):
    print(f"{greetings}, I am working very hard\nThis is my pid {os.getpid()}")

if __name__ == '__main__':
    new_process = Process(target=very_hard_computational_task, args=["Hello"])

    new_process.start()

    new_process.join()

    print(f"Hi there, I do nothing.\nThis is my pid: {os.getpid()}")
```

Na vidlích je velmi důležité *if \__name__ == '\__main__':*. Bez něj totiž nedovolí nový process spustit. Každý proces je unikátně identifikován svým pidem. Vidíme, že pidy jsou jiné, takže i procesy, které tuto metodu volaly, jsou rozdílné. Metoda *join()* je blokující metodou, která donutí volající proces čekat na skončení volaného procesu.

Materiály
---