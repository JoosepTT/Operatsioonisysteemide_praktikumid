# Praktikum 9 

Käesolevas praktikumis tutvusin Windows 11 ja Ubuntu operatsioonisüsteemi ressursihaldusega. Õppisin tundma erinevaid tööriistu nii Linuxi kui Windowsi süsteemis. Windowsis kasutasin ülesannete lahendamisel graafilist liidest, Linuxi puhul aga ainult Unixi käsurida.

| nr  | Küsimus  | Linux  | Windows  | Linuxis kasutatud käsklus  | Windowsis kasutatud käsklus  |
|---|---|---|---|---|---|
| 1.  | Mitu protsessi kokku arvutis käivitub?  | 220  | 144  | ```ps -aux \| wc -l``` | Task Manager -> jõudlus  |
| 2.  | Milline on kõige esimesena käivitatud protsess?  | /sbin/init splash  | System Idle Process  | ```ps axo``` <br> ```pid,cmdcomm,etime```   | Process Explorer -> Start  |
| 3.  | Milliste kasutajate protsesse arvutis käib?  | root, joosep, systemd-t, systemd-r, system-o, avahi, messagebu, syslog, rtkit ja colord   | Joosep, SYSTEM  | htop  | Process Explorer -> View -> Select Columns -> User Name  |
| 4.  | Kui kaua on arvuti järjest töötanud (up time)? (Alternatiivselt võib vastata ka, millal (kuupäev ja kellaaeg) arvuti viimati käima pandi.)  | ```04:13:48```  | ```00:24:09```  | uptime  | Task Manager -> jõudlus -> CPU -> Tööaeg  |
| 5.  | Milline protsess käivitati kõige hiljem (viimasena)?  | ```[kworker/1:2]```  | smartscreen.exe  | ps -eo pid,etime,cmd  | Process Explorer (starttime tulp)  |
| 6.  | Milline on kõige rohkem protsessoriaega võttev protsess ja kui mitu protsenti protsessoriajast ta tarbib?  | gnome-shell  | System Idle Process  | top (TIME+ tulp)  | Process Explorer -> View -> Select Columns -> Process Performance -> CPU Time  |
| 7.  | Milline on kõige rohkem virtuaalmälu (aadressiruumi, commit, Virtual Size) võttev protsess?  | gnome-shell  | PhoneExperienceHost.exe  | ps -eo pid,comm,vsz --sort=-vsz  | Process Explorer -> View -> Select Columns -> Process Memory -> Virtual Size  |
| 8.  | Milline on kõige rohkem füüsilist mälu (working set) võttev protsess?  | gnome-shell  | Firefox  | ps -eo pid,comm,rsz --sort=-rsz  | Task Manager -> Processes (memory veerg)  |
| 9.  | Kui palju füüsilisest mälust (Physical Memory) on vaba ja kui palju hõivatud?  | 1,1GB hõivatud ja 1,8GB kasutamata | 2,4GB hõivatud ja 1,5GB vaba  | free -h  | Task Manager -> Jõudlus  |
| 10.  | Kui palju on põhikettal (C:, /) vaba ruumi mahult (GB) ja protsentuaalselt?  | 11GB (56%)  | 25,9GB (TreeSize Free ei näita käsureaväliselt protsenti, kuna selleks on vaja tasulist versiooni)  | df -h /  | File Explorer -> See Arvuti -> Kohalik Ketas (:C)  |
| 11.  | Milline on kõige suurem arvutis olev fail ja kõige rohkem andmemahtu hõivav kaust (arvesse võta ka alamkaustade mahtu, ja jätta juurkaust / või C: välja)?  | /home/joosep  | Windows  | ```sudo du -sh /home/* --exclude=/root``` | sort -rh | head -n 10  | TreeSize -> (:C) (>Suurus)  |

#### 12. 
Käsu ```sha1sum /dev/zero | sha1sum /dev/zero ``` puhul kulub protsessoril enim aega alamtegevusele _.
[pilt1]()!

Käsu ```sha1sum /dev/urandom | sha1sum /dev/urandom``` puhul läheb aga enim aega alamteegvusele _.
[pilt2]()!

#### 13. 
Milline protsess kõige rohkem salvestusseadmele kirjutab?
Millisesse faili eelmise küsimuse protsess kõige rohkem kirjutab?
Milline protsess kõige rohkem salvestusseadmelt loeb?
Millisest failist eelmise küsimuse protsess kõige rohkem loeb?

#### 14.
Suurima mahuga oli protsessi _ tekitatud võrguliiklus. 

#### 15.
Milliseid konkreetseid programme või käsureakäske kasutada arvuti agluse põhjustajate tuvastamiseks?  | Esmalt tasub vaadata Task manager'ist protsesside vahekaarti ning jälgida protsessori ja mälu kasutust, et tuvastada kõige ressursimahukamad protsessid. Teiseks saab uurida Resource Monitorist protsesside kettakasutust ja võrguaktiivsust, et näha, kas süsteemi aeglustavad ketta või võrgu probleemid. Kolmandaks on mõtekas kasutada arvuti jõudluse jälgimise tööriista Performance Monitor, et mõõta täpsmalt protsessori ja ketaste koormust. Süsteemivigu nagu kettarikkeid või teenuste töö ebaõnnestumisi saab otsida tööriistaga Event Viewer. Lõpuks tuleb piisava vaba ruumi tagamiseks kontrollida üle kettaruum ja vajadusel puhastada süsteemist ajutised failid: seda saab teha tööriistaga Disk Cleanup.
