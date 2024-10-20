# Praktikum 5

### 5-1
a) Kataloogis /tmp/kaust oleva faili minufail.txt lugemiseks on vaja, et failiõigused oleksid read ja kataloogiõigus execute.
a) Minufail.txt kustutamiseks kataloogist /tmp/kaust on vaja kaustatasemel write ja execute õigusi, kuid faili tasemel pole õigusi vaja, sest kustutamine toimub kausta tasandil.

### 5-2
chmod a=x skriptifail ei ole piisav õigus shelli skriptfaili käivitamiseks, sest lisaks käivitamisõigusele vajab shell skripti sisule ligipääsuks ja selle käivitamiseks lugemisõigust.

### 5-3
Igal Unixi süsteemi kasutajal on oma kaust, et luua failide haldamise ja juurdepääsu kontrollimise süsteem, mis oleks võimalikult efektiivne ja turvaline.

### 5-4
