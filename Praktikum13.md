# Praktikum 13

Käesolevas praktikumis tutvusin Virtualbox Windows 11 virtuaalmasinas Windows PowerShelli kasutamise ja skriptimisega. Järgnevalt on dokumenteeritud skript, mis kirjutab testarvuti kohta info faili.

## Skript
(Koodi seletus kommentaaride ja skripti väljastatavate sisuparameetritena.)
```
#$nr:	küsimuse number
#$param: mis parameetriga tegemist (võimalikult lühidalt)
#$sisu:	väljastatav sisu

# Eemaldatakse eelneva faili sisu või luuakse uus fail
$fail = ".\tulemus.txt"
if (Test-Path $fail) { # Kontrollib, kas fail on olemas
    Clear-Content -Path $fail # Kustutab eelneva sisu
} else {
    New-Item -Path $fail -ItemType File | Out-Null # Loob uue faili
}

# Skripti tulemuste väljastamine
function valjasta{
	param ($nr, $param, $sisu)
	$fail = ".\tulemus.txt"
	$aeg = Get-Date -Format "HH:mm:ss.fff"
	if($sisu -eq $null){
		$rida = "$nr.	$aeg	${param}:	NULL"
		Write-Output $rida
		$rida | Out-File -FilePath $fail -Append
	}elseif($sisu.GetType().Name -eq "Object[]"){
		$rida = "$nr.	$aeg	${param}:"
		Write-Output $rida $sisu
		$rida | Out-File -FilePath $fail -Append
		$sisu | Out-File -FilePath $fail -Append
	}else{
		$rida = "$nr.	$aeg	${param}:	$sisu"
		Write-Output $rida
		$rida | Out-File -FilePath $fail -Append
	}
}

[int]$aegA = (Get-Date).Millisecond
Valjasta 0 "ALGUS" ("Aeg: "+(Get-Date -Format "dddd MM/dd/yyyy HH:mm K")+" Teostaja: Joosep")


# 1. Masina nimi, PowerShelli ja Windowsi versioon
Valjasta 1 "Masina nimi" (hostname)
Valjasta 2 "PowerShelli versioon" ($PSVersionTable.PSVersion.ToString())
Valjasta 3 "Windowsi versioon" (Get-CimInstance Win32_OperatingSystem | Select-Object -ExpandProperty Version)

# 2. Võrgu konfiguratsioon
$network = Get-CimInstance Win32_NetworkAdapterConfiguration | Where-Object { $_.IPEnabled }
$ip = $network.IPAddress | Select-Object -First 1
$subnet = $network.IPSubnet | Select-Object -First 1
$gateway = $network.DefaultIPGateway | Select-Object -First 1
Valjasta 4 "IP-aadress" $ip
Valjasta 5 "Vorgumask" $subnet
Valjasta 6 "Gateway" $gateway
Valjasta 7 "DHCP lubatud" $network.DHCPEnabled
Valjasta 8 "MAC-aadress" $network.MACAddress

# 3. Protsessor ja RAM
$system = Get-CimInstance Win32_ComputerSystem
$cpu = Get-CimInstance Win32_Processor | Select-Object -ExpandProperty Name
Valjasta 9 "Protsessor" $cpu
Valjasta 10 "RAM kogus (GB)" ([math]::Round($system.TotalPhysicalMemory / 1GB, 2))

# 4. Graafikakaart ja ekraani lahutus
$video = Get-CimInstance Win32_VideoController
Valjasta 11 "Graafikakaart" $video.Name
Valjasta 12 "Draiveri versioon" $video.DriverVersion
Valjasta 13 "Draiveri kuupaev" $video.DriverDate
Valjasta 14 "Ekraani lahutus" ($video.CurrentHorizontalResolution.ToString() + "x" + $video.CurrentVerticalResolution.ToString())

# 5. Kõvakettad
$drives = Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3"
foreach ($drive in $drives) {
    $total = [math]::Round($drive.Size / 1GB, 2)
    $free = [math]::Round($drive.FreeSpace / 1GB, 2)
    Valjasta 15 "Ketas $($drive.DeviceID) mahutavus" "$total GB"
    Valjasta 16 "Ketas $($drive.DeviceID) vaba ruum" "$free GB"
}

# 6. PCI-siinil olevate seadmete draiverid
try {
    $pciDevices = Get-WmiObject -Class Win32_PnpSignedDriver | Where-Object { $_.DeviceName -like "*PCI*" } | Select-Object DeviceName, Manufacturer, DriverVersion
    if ($pciDevices) {
        foreach ($device in $pciDevices) {
            Valjasta 17 "PCI-seade: $($device.DeviceName)" "Tootja: $($device.Manufacturer), Versioon: $($device.DriverVersion)"
        }
    } else {
        Valjasta 17 "PCI-seadmed ja draiverid" "Ei leitud uhtegi PCI-seadet"
    }
} catch {
    Valjasta 17 "PCI-seadmed ja draiverid" "Torge PCI-draiverite hankimisel: $_"
}

# 7. Arvuti kasutajad
$users = Get-CimInstance Win32_UserAccount | Where-Object { $_.LocalAccount }
foreach ($user in $users) {
    $status = if ($user.Disabled) { "Keelatud" } else { "Aktiivne" }
    Valjasta 18 "Kasutaja: $($user.Name)" "Kirjeldus: $($user.Description), Staatus: $status"
}

# 8. Käimasolevate protsesside arv
$processCount = (Get-Process).Count
Valjasta 19 "Kaimasolevate protsesside arv" $processCount

# 9. 10 viimast käivitatud protsessi
$lastProcesses = Get-Process | Where-Object { $_.StartTime -is [datetime] } |
    Sort-Object StartTime -Descending | Select-Object -First 10 -Property ProcessName, Id, StartTime
Valjasta 20 "Viimased 10 protsessi" $lastProcesses

# 10. Arvuti kuupaev ja kellaaeg
Valjasta 21 "Kuupaev ja kellaaeg" (Get-Date -Format "dddd MM/dd/yyyy HH:mm:ss")

# Skripti lõpetamine
[int]$aegL = (Get-Date).Millisecond
$ajakulu = ($aegL - $aegA)
Valjasta "*" "TEHTUD" "$ajakulu ms`n`n"

```

## Skripti tulemus (faili "tulemus.txt" sisu)
[tulemusfail](Pildid/tulemus.txt)

