# Prakitkum 12

Käesolevas praktikumis tutvusin skriptide loomise ja jooksutamisega Linuxi käsureal. Ülesanded on sooritatud Ubuntu Virtualbox virtuaalmasinas.


## 3. skript
```#!/bin/bash
echo "Sisesta oma nimi:"
read nimi
echo "Sisesta oma eriala:"
read eriala
echo "Sisesta oma martiklinumber"
read mn
echo "Tere, $nimi, erialalt $eriala!!"
echo "Teie martiklinumber on $mn."

```

## 4. skript
```#!/bin/bash

if [ "$#" -ne 2 ]; then
    echo "Kasutamine: $0 laiend_A laiend_B"
    exit 1
fi

laiend_A=$1
laiend_B=$2

failid=$(ls *.$laiend_A 2>/dev/null)
if [ -z "$failid" ]; then
    echo "Faili laiendiga .$laiend_A ei leitud."
    exit 1
fi

for fail in *.$laiend_A; do
    if [ -e "$fail" ]; then
        uus_fail="${fail%.$laiend_A}.$laiend_B"
        mv "$fail" "$uus_fail"
        echo "Nimetati ümber: $fail -> $uus_fail"
    fi
done

```

## 5. skript
```#!/bin/bash

if [ "$#" -ne 1 ]; then
  echo "Kasutamine: $0 protsessi_nimi"
  exit 1
fi

protsess_nimi=$1

IFS=$'\n'

for line in $(ps -A); do
    pid=$(echo " $line" | tr -s ' ' | cut -d' ' -f2)
    nimi=$(echo " $line" | tr -s ' ' | cut -d' ' -f5)

    if [ "$nimi" == "$protsess_nimi" ]; then
        echo "Protsessi nimi: $nimi, PID: $pid"
    fi
done

```

## 6. skript
```#!/bin/bash

astenda_tsükliga() {
  baas=$1
  eksponent=$2
  tulemus=1

  for ((i=0; i<$eksponent; i++)); do
    tulemus=$(( tulemus * baas ))
  done

  echo $tulemus
}

tulemus=$(astenda_tsükliga 9 5)
echo "9^5 for-tsükliga: $tulemus"

```

## skriptide väjundid
![pilt1](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20054317.png?raw=true)


## Tehisaru versioon 6. skriptist
![pilt2](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20053345.png?raw=true)
![pilt3](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20053410.png?raw=true)
![pilt4](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20053423.png?raw=true)
![pilt5](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20053448.png?raw=true)
![pilt6](https://github.com/JoosepTT/Operatsioonisysteemide_praktikumid/blob/main/Pildid/Screenshot%202024-12-10%20053458.png?raw=true)
