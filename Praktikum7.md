# Praktikum 7

Käesolevas praktikumis uurisin Virtualboxi Windows 11 ja Ubuntu virtuaalmasinaid kasutades, kuidas kasutada lokaalseid ja võrgukettaid nii Windowsi kui ka Linuxi keskkonnas.

### 1.
Andmekandjad vajavad lähtestamist, sest uutel andmekandjatel on failiruum määramata ja sinna on lihtsam uut andmestruktuuri luua. Samuti võib lähtestaine aidata lahendada andmekandjal tekkinud failisüsteemi rikkeid ja taastada selle algse töövõime.

### 2.
GPT kasutamisel on MBRiga võrreldes mitu eelist. Esiteks, MBR toetab ainult kuni 4 partitsiooni, kuid GPT toetab 128 partitsiooni, mis võimaldab kasutajatel luua palju rohkem eraldiseisvaid partitsioone. Teiseks, MBR suudab hallata kuni 2 TB suuruseid kettaid, kuna selle aadressiruumi piirangud ei luba suuremaid mahtusid, kuid GPT toetab kuni 9,4 ZB suuruseid kettaid. Kokmandaks, MBR salvestab partitsioonitabeli ainult kettale algusesse, mistõttu võib selle kahjustumine viia kõigi partitsioonide kadumiseni. GPT hoiab aga partitsioonitablei koopiat nii ketta alguses kui ka lõpus.

### 3.
Võrguketta haakimise tõestus: [https://kodu.ut.ee/~jooseptiger/opsys/hdd.png](https://kodu.ut.ee/~jooseptiger/opsys/hdd.png)

### 4.
![pilt1](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-10-28%20133510.png?raw=true)

### 5.
Mount-käsu parameeter -o ro muudab ühendatud faili failisüsteemi kasutajatele ainult loetavaks ja blokeerib ühtlasi kõik muudatused. Parameeter -t auto tuvastab aga automaatselt ühendatud seadme failisüsteemi tüübi.

### 6.
Antud ketta ühendamisel asendas Ubuntu auto-parameetri väärtusega vfat, mis viitab failisüsteemi tüübile FAT32.

### 7. 
![pilt2](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-11-04%20235805.png?raw=true)



