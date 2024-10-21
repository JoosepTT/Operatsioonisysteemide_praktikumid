# Praktikum 5

Käesolevas praktikumis tuvusin Ubuntu Linuxi virtuaalmasinas Unixi failiõiguste seaduspärasuste ja olemusega. Sooritasin juhendi põhjal erinevate süsteemikasutajatega mitmeid erinevaid failiõiguste muutmise harjutusi, millest osade vastused on esitatud järnevalt.

### 5-1
a) Kataloogis /tmp/kaust oleva faili minufail.txt lugemiseks on vaja, et failiõigused oleksid read ja kataloogiõigus execute.
a) Minufail.txt kustutamiseks kataloogist /tmp/kaust on vaja kaustatasemel write ja execute õigusi, kuid faili tasemel pole õigusi vaja, sest kustutamine toimub kausta tasandil.

### 5-2
chmod a=x skriptifail ei ole piisav õigus shelli skriptfaili käivitamiseks, sest lisaks käivitamisõigusele vajab shell skripti sisule ligipääsuks ja selle käivitamiseks lugemisõigust.

### 5-3
Igal Unixi süsteemi kasutajal on oma kaust, et luua failide haldamise ja juurdepääsu kontrollimise süsteem, mis oleks võimalikult efektiivne ja turvaline.

### 5-4
Tavakasuatajal on faili uusfail.txt sisu lugemiseks vaja read õigust.
![pilt1](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-10-21%20180141.png?raw=true)

### 5-5
![pilt2](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-10-21%20183923.png?raw=true)
Setuid (Set User ID) õigust on Unix süsteemides vaja selleks, et fail käivituks omaniku  õigustes, mitte selle kasutaja õigustes, kes faili käivitab. 

### 5-6
Setuid õiguste kasutamine võib vähendada süsteemi turvalisust, kui seda ei kasutata ettevaatlikult. Näiteks kui setuid õigused on antud valedele või halvasti kirjutatud programmidele, võivad need võimaldada pahatahtlikul kasutajal omandada kõrgendatud õigusi ja nt käivitada pahavara. Samuti võib see anda kasutajatele ligipääsu tundlikele failidele ning setuid programmide haldamine ja jälgimine muutub keerulisemaks.

### 5-7
Sticky bit õigustega kasutast saavad faile kustutada ainult kasutajad peeter, kes on sealsed failid loonud, ja opetaja, kes on loonud kausta "yhiskaust" ehk tal on selle omanikuõigused. Teised kasutajad saavad kustutada ainult enda loodud faile, kuid mitte peetri omi.

### 5-8
```opetaja@tilgar24:~/klass$ getfacl hinded.txt
# file: hinded.txt
# owner: opetaja
# group: opetaja
user::rw-
group::---
group:direktor:rw-
mask::rw-
other::---
```

### 5-9
Chattr +i -parameetritega faili sisu ei saa keegi muuta, isegi mitte omanik ega root. +i atribuudiga faili saab kustutada eemaldades sellelt atribuudi käsuga chattr -i testfail-2 ja seejärel kustutades käsuga rm testfail-2.
