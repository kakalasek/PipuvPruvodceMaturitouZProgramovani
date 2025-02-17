Komunikace v síti - tvorba síťových aplikací, Berkeley socket a jeho rozhraní
===

Podíváme se teď na síťové aplikaci a jejich tvorbu. V moderních programovacích jazycích domestikoval tzv. Berkeley socket interface.     

![ISO/OSI](iso_osi_model.png)

Uděláme si takový malý vhled do počítačových sítí, abychom pochopili, proč potřebujeme takový level abstrakce. Máme síťový model, který má hned několik vrstev. Říkáme mu ISO/OSI model, popř. TCP/IP, kde jsou některé vrstvy spojené.              
Spodní vrstvy se starají fyzickou implementaci, tedy přenos bitů po síti. Jako programátora by nás němeělo zajímat, zda se bude signál přenášet bezdrátově či po kabelu. Podobně by nás nemuselo zajímat, kudy naše data poletí, zda se dostanou k cíli, poř. jejich retransitace a tak podobně. To vše zajišťují spodní vrstvy a protokoly. Píšeme-li síťovou aplikaci, konkrétní implementace a funkce spodních vrstev vědět nepotřebujeme.           

![Berkeley Socket](berkeley_socket.png)

Je nám prezentováno jen jednoduché rozhraní, pomocí kterého můžeme interagovat se sítí. Berkeley socket je jakž takž standardizovaný. Stěžejním konceptem Berkeley socketu je .. no, socket. Ze síťování známe socket jako spojení IP adresy a portu. Zde je socket jakýsi objekt, přes který můžeme se sítí komunikovat. Nicméně platí, že musí mít ip adresu a port.                  
Máme také tzv. serverový soket a klientský soket. K tomu serverovému se může ten klientský připojit.                
Když vytváříme serverový soket, musíme nejdříve provést operaci bind, která soket napojí na určitý port a IP adresu.        
Pak lze zavolat listen, který označí soket jako pasivní. Tedy, že bude poslouchat pro příchozí spojení.                 
Následně lze využít metody accept, která je blokující, takže kód se zde zastaví, dokud se se soketem nespojí nějaký klientský soket.            
Lze pak využít metod pro recieve a send pro příjem a zaslání dat přes síť. Data se přes síť posílají zásadně v bytech. Záleží na konkrétní implementaci v konkrétním jazyce, zda musíte data nějakým způsobem parsovat, nebo si to knihovna pro Berkeley soket vyřeší sama.             
Je důležité soket také zavřít. To můžeme udělat na základě nějakého uživatelského příkazu, nebo pomocí nějakého timeoutu při dlouhé neaktivitě klienta.                 
Timeout je důležitá věc v síti. Většina zařízení na síti má pro komunikaci implementovaný nějaký timeout. Nemůžeme si být jisti, jak tyto timeouty přesně vypadají, proto je dobrým zvykem vytvořit vlastní timeouty v našem kódu, nejlépe nastavitelné.                
Serverové vlákno zpravidla vytváří pro každé spojení vlastní vlákno. Konkrétně vytvoří klientské vlákno, které si povídá s připojeným uživatelem. Takto lze obsluhovat více spojení najednou.               
Samozřejmě se na konci také musí zavřít samotné serverové vlákno.

Klientské vlákno se chová mírně odlišně. Po vytvoření musíme využít metodu connect, která dovede klientské vlákno dovede spojit s nějakým serverovým vláknem na základě zadané IP adresy a portu.           
Komunikace pak opět probíhá stejně, metodami send a recieve. Opět připomínám, že připojení musíme na konci opět uzavřít.            

![Client-Server](client_server.png)

Síťové aplikace mohou mít několik základních podob. Jednou z nich je architektura klient-server. Na této architektuře pracuje třeba databázový server, webový server atp. Jednoduše, je jeden server, který přijímá a odbavuje libovolné množství klientských připojení.                

![Peer-to-peer](peer_to_peer.png)

Druhou základní možností je architektura P2P (Peer-to-peer). Zde není žádný centrální server, ale každé zařízení dovede fungovat jako server i jako klient. Zpravidla může každé zařízení komunikovat s každým pomocí nějakého společného protokolu. Na této architektuře funguje třeba Torrent. Je několik nodů, kdy žádný nemá celou část požadovaného souboru, ale každý má nějakou a komunikují spolu za účelem nalezení a složení celého souboru.

Jako možnost architekturu lze ještě brát třeba dedikovanou komunikaci mezi dvěma zařízeními. Příkladem využití takové architektury je např. Bluetooth.

Povídání
---

Ukázky kódu
---

**Python - Berkley socket server**

**Java - Berkley socket server**

**C++ - Berkley socket server**

Materiály
---

Wikipedia - Berkeley sockets - https://cs.wikipedia.org/wiki/Berkeley_sockets       
GeeksForGeeks - Client-Server model - https://www.geeksforgeeks.org/client-server-model/            
GeeksForGeeks - Peer-to-peer - https://www.geeksforgeeks.org/what-is-p2p-peer-to-peer-process/

