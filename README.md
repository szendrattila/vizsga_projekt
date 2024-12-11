# vizsga_projekt
vizsga
Csapatunk egy képzeletbeli hotelt talált ki mely négy fő részre bontható. A hotelben található egy szerver szoba, hotel szobák az étkező valamint a recepció.
Szerver szoba:
A szerver szobában található a hotel összes hálózati eszköze. A szerverszobák olyan zárt terek, amelyek központi helyet biztosítanak a hálózati szerver erőforrásainak. Az ilyen szobák kulcsfontosságú szerepet játszanak az informatikai infrastruktúrában, különös figyelmet kell fordítani az eszközök hűtésére, az áramellátásra, a hálózati kapcsolatokra valamint a biztonságra. A mi hotelünk hálózata layer 3-as biztonsággal van ellátva. Ez lehetővé teszi azt ha a szálloda egyik routere meghibásodik akkor a másik két router segítségével akadálytalanul tovább tud működni a hálózat. A szerver szoba tartalmaz három routert, két switchet valamint egy windows szervert és egy linux szervert. 
Hotel szobák:
A hotel szobák kaptak egy külön WRT300N névre hallgató vezetéknélküli routert melyhez egyéb informatikai eszközöket társítottunk számítógépek, laptopok, tabletek. Mindezeket hozzákötöttük a hotel szerverszobájához.


Étkező:
Az étkező nem igényel magához nagyobb informatikai struktúrát. Viszont a rendeléseket valahogy fel kell venni, így elhelyeztünk egy számítógépet az étkezőben is melyet csatlakoztattunk a hotel szerveréhez. Ez az egy számítógép hozzá van kötve egy 2960-24TT névre hallgató switchhez azon belül pedig a Vlan 10-hez van hozzárendelve a számítógép. A VLAN (Virtual Local Area Network) egy virtuális, logikailag elkülönített hálózati szegmens, amelyet egy fizikai hálózaton belül hoznak létre. A VLAN-ok között az adatforgalom alapértelmezetten nem látható. Az adatok szétválasztása csökkenti a biztonsági kockázatokat. Egyszerűvé teszi a hálózat átszervezését. Például egy VLAN-hoz tartozó eszközt fizikailag áthelyezhetünk, és a logikai tagságát megtarthatja.
Recepció:
A szálloda recepciójánál érkeznek be a szálloda foglalásai így oda is elhelyeztünk két számítógépet melyek szintén hozzá vannak rendelve a szálloda szerveréhez. A szerveren DHCP szolgáltatás érhető el. A DHCP (Dynamic Host Configuration Protocol) egy hálózati protokoll, mely automatikusan kiosztja az IP-címeket és egyéb hálózati beállításokat például alhálózati maszkot, gateway-t és DNS szervereket a hálózathoz csatlakozó eszközöknek. Például: számítógépeknek, okostelefonoknak, nyomtatóknak. Ebben az esetben a recepcióban lévő 2 gép fog kapni ip-címet automatikusan a DHCP szervertől.
Routerek ip-cím kiosztása:
A routerek között 192.168.x.x  hálozatot használtunk amit a /30 netmask-al láttunk el. A /30 netmask 255.255.255.252 decimális formában. Van 1db Hálozati címe, hálozatonként 2 ip-címet lehet kiosztani és egy Közvetlenül hozzáférhető (broadcast) cím, ez nekünk tökéletesen illik a topográfiához 2 router között van kiosztva 2 ip cím egy hálozatban. A routerek között OSPF-t használtunk.Az OSPF (Open Shortest Path First) egy dinamikus útvonalválasztási protokoll, amelyet az IP hálózatokban használnak. Ez egy link-state (kapcsolati állapot alapú) protokoll, amely az IGP-k (Interior Gateway Protocols) közé tartozik, vagyis olyan protokoll, amelyet egy adott hálózaton belüli útvonalválasztásra használnak.Példa:
    • Mire jó az OSPF?
1.	Hálózati forgalom optimalizálása:
o	Az OSPF a hálózati topológiát teljes mértékben megismeri, és az SPF-algoritmust (Dijkstra algoritmus) használja, hogy megtalálja az optimális útvonalat az egyes célállomásokhoz.
2.	Gyors konvergencia:
o	Ha egy hálózati link leáll vagy megváltozik, az OSPF gyorsan frissíti az útvonalakat, minimalizálva az adatforgalom kiesését.
3.	Skálázhatóság:
o	Nagy és összetett hálózatokban is jól működik, mivel támogatja a hierarchikus felépítést (Area-k használatával).
4.	VLSM és CIDR támogatás:
o	Támogatja a változó hosszúságú alhálózati maszkokat (VLSM) és az osztályfüggetlen útválasztást (CIDR), ami rugalmasabbá teszi a címkezelést.
5.	Redundancia és megbízhatóság:
o	Az OSPF több útvonalat is ismerhet egy célállomás felé, és automatikusan választ egy alternatívát, ha az elsődleges útvonal meghibásodik.
Hogyan működik az OSPF?
1.	Link-state adatbázis (LSDB) kialakítása:
o	Az OSPF routerek a közvetlen szomszédaikkal cserélnek információt a hálózati kapcsolatokról (linkekről). Ez az információ bekerül egy LSDB-be, amely minden routernél azonos egy adott OSPF Area-ban.
2.	Dijkstra algoritmus:
o	Az OSPF minden routeren futtatja a Dijkstra algoritmust, hogy a legkisebb költségű útvonalakat számolja ki.
3.	Area-k:
o	Az OSPF hálózatokat Area-kra bontja, hogy egyszerűsítse az útválasztást. Az Area 0 (Backbone Area) köti össze a többi Area-t.
4.	LSA-k (Link-State Advertisement):
o	A routerek LSA-k segítségével osztják meg a hálózati információkat, például az elérhető útvonalakat és a költségeket.
Mikor használjunk OSPF-et?
•	Ha a hálózat nagyobb és bonyolultabb, mint amit egy egyszerűbb protokoll, például a RIP kezelni tud.
•	Amikor szükséges a gyors konvergencia és a pontos útvonalválasztás.
•	Ha több alhálózat van, és fontos a skálázhatóság.


Parancsok amiket a switch beállításához használtunk:
1. username admin password 1234
1.	Célja: Felhasználónév és jelszó létrehozása az eszköz eléréséhez.
2.	Magyarázat:
a.	Egy admin nevű felhasználót hoz létre a 1234 jelszóval.
b.	Ezt a hitelesítést használhatják például SSH vagy Telnet hozzáféréshez.
2. ip domain-name wmszki.hu
1.	Célja: A hálózati eszköz domain nevének beállítása.
2.	Magyarázat: A domain név szükséges az SSH konfigurációhoz, mert a kulcsgenerálás során a rendszer ezt a nevet használja az eszköz azonosítására.
3. enable secret cisco
1.	Célja: Egy titkosított jelszó beállítása az enable (privilegizált) módhoz.
2.	Magyarázat:
o	A "cisco" lesz a privilegizált mód eléréséhez szükséges jelszó.
4. line vty 0 15
1.	Célja: A virtuális terminálvonalak (VTY) konfigurációs módjának megnyitása.
2.	Magyarázat:
a.	A 0 15 az eszközön elérhető összes VTY vonalat jelöli (általában 16 vonal).
b.	Ezeket a vonalakat távoli elérésre használják (pl. SSH vagy Telnet).
5. login local
1.	Célja: Beállítja, hogy a VTY vonalakhoz történő hozzáféréshez a helyileg létrehozott felhasználói hitelesítés legyen szükséges.
2.	Magyarázat: A felhasználónév és jelszó az előzőleg a username paranccsal létrehozott adatokból lesz ellenőrizve.
6. transport input ssh
1.	Célja: Meghatározza, hogy a VTY vonalakhoz csak SSH protokollon keresztül lehessen hozzáférni.
2.	Magyarázat: Tiltja a Telnet elérést, így biztonságosabbá teszi a távoli hozzáférést.
7. password 1234
1.	Célja: Egy jelszó beállítása a vonalakhoz (például konzolhoz vagy VTY-hoz).
2.	Magyarázat: Ez a jelszó lesz az alap hitelesítési adat, ha nincs login local használatban.
8. crypto key generate rsa
1.	Célja: RSA kulcs generálása az SSH-hoz.
2.	Magyarázat:
a.	Az SSH működéséhez szükséges titkosítási kulcsokat hozza létre.
b.	A parancs kiadása után meg kell adnod a kulcs hosszát (például 1024 vagy 2048 bit), amely meghatározza a biztonság erősségét.

Költségvetés
Routerek
1.	Cisco ISR 1100-4G (4G LTE támogatással, kis- és középvállalkozásoknak)
o	Ár: kb. 296 000 – 370 000 HUF/db
o	4 db összesen: 1 184 000 – 1 480 000 HUF
2.	Cisco ISR 4321 (moduláris router, nagyobb hálózatokhoz)
o	Ár: kb. 555 000 – 740 000 HUF/db
o	4 db összesen: 2 220 000 – 2 960 000 HUF
Switchek
1.	Cisco Catalyst 2960-L (Layer 2, 24 port, alap funkcionalitás)
o	Ár: kb. 111 000 – 185 000 HUF/db
o	4 db összesen: 444 000 – 740 000 HUF
2.	Cisco Catalyst 9200L (Layer 3, 24 port, haladó funkcionalitás)
o	Ár: kb. 555 000 – 740 000 HUF/db
o	4 db összesen: 2 220 000 – 2 960 000 HUF
Kiegészítők és további költségek
•	Hálózati kábelek: 18 500 – 37 000 HUF
•	Rack szekrény: 111 000 – 185 000 HUF
•	Tápellátás és redundancia (UPS-ek): 111 000 – 370 000 HUF
•	Licenszek: 185 000 – 740 000 HUF
•	Szállítási költség: változó, becsülhető 50 000 – 150 000 HUF




Szerverek
1.	Windows Server (HP ProLiant DL360 Gen10)
o	Ár: 1 100 000 – 1 500 000 HUF
o	Windows Server licenc (Datacenter vagy Standard): 370 000 – 1 000 000 HUF
o	Összesen: 1 470 000 – 2 500 000 HUF
2.	Linux Server (Dell PowerEdge R540)
o	Ár: 1 000 000 – 1 400 000 HUF
o	Linux operációs rendszer: ingyenes (Ubuntu, CentOS) vagy Red Hat licenc: 185 000 – 370 000 HUF
o	Összesen: 1 000 000 – 1 770 000 HUF
3.	ASA Server (Cisco ASA 5506-X)
o	Ár: 300 000 – 600 000 HUF
o	Licenc (Firepower vagy VPN): 185 000 – 370 000 HUF
o	Összesen: 485 000 – 970 000 HUF
Összesített költség (forintban)
1.	Belépő szintű konfigurációval (Cisco ISR 1100-4G + Catalyst 2960-L + alap szerverek):
4 713 500 – 6 789 000 HUF
2.	Haladó konfigurációval (Cisco ISR 4321 + Catalyst 9200L + fejlett szerverek):
9 540 500 – 13 872 000 HUF


