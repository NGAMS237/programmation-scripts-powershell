# programmation-scripts-powershell

Fiche PowerShell
1) Commandes générales
Commande	Alias	Rôle	Exemple
Get-Help	help	Affiche l’aide d’une commande.	Get-Help Get-ChildItem
Get-Command	—	Liste les commandes disponibles.	Get-Command *service*
Get-Member	gm	Montre les propriétés et méthodes d’un objet.	Get-Process | Get-Member
Get-History	h	Affiche l’historique des commandes.	Get-History
Invoke-History	—	Relance une commande de l’historique.	Invoke-History 5
Clear-Host	cls	Nettoie l’écran.	cls
Get-Date	—	Affiche la date et l’heure.	Get-Date
Write-Host	—	Affiche un message à l’écran.	Write-Host "Bonjour"
Write-Output	echo	Envoie une valeur dans le pipeline.	Write-Output "Test"
Get-Alias	—	Affiche les alias disponibles.	Get-Alias
2) Navigation et dossiers
Commande	Alias	Rôle	Exemple
Get-Location	pwd	Affiche le dossier courant.	pwd
Set-Location	cd, sl	Change de dossier.	cd C:\Windows
Get-ChildItem	ls, dir, gci	Liste les fichiers et dossiers.	ls
Push-Location	pushd	Sauvegarde l’emplacement actuel et change de dossier.	pushd C:\Temp
Pop-Location	popd	Revient au dossier précédent.	popd
Resolve-Path	—	Affiche le chemin complet réel.	Resolve-Path .\test.txt
Split-Path	—	Sépare un chemin en morceaux.	Split-Path C:\Windows\System32
Exemples utiles :

powershell
cd C:\
ls
ls -Force
ls -Recurse
3) Fichiers et dossiers
Commande	Alias	Rôle	Exemple
Get-Content	cat, type	Lit le contenu d’un fichier.	Get-Content .\notes.txt
Set-Content	—	Remplace le contenu d’un fichier.	Set-Content .\test.txt "Bonjour"
Add-Content	—	Ajoute du texte à un fichier.	Add-Content .\test.txt "Ligne 2"
Copy-Item	cp, copy	Copie un fichier ou dossier.	Copy-Item .\a.txt C:\Temp\
Move-Item	mv, move	Déplace un fichier ou dossier.	Move-Item .\a.txt C:\Temp\
Rename-Item	—	Renomme un fichier ou dossier.	Rename-Item .\a.txt b.txt
Remove-Item	rm, del, erase	Supprime un fichier ou dossier.	Remove-Item .\a.txt
New-Item	ni	Crée un fichier, dossier ou autre élément.	New-Item .\test.txt -ItemType File
Test-Path	—	Vérifie si un chemin existe.	Test-Path .\test.txt
Exemples :

powershell
New-Item .\DossierTest -ItemType Directory
New-Item .\fichier.txt -ItemType File
Copy-Item .\fichier.txt .\backup\fichier.txt
Remove-Item .\ancien.txt
4) Processus et services
Commande	Alias	Rôle	Exemple
Get-Process	ps, gps	Liste les processus actifs.	Get-Process
Stop-Process	kill	Arrête un processus.	Stop-Process -Name notepad
Start-Process	—	Lance un programme.	Start-Process notepad.exe
Get-Service	gsv	Liste les services Windows.	Get-Service
Start-Service	—	Démarre un service.	Start-Service spooler
Stop-Service	—	Arrête un service.	Stop-Service spooler
Restart-Service	—	Redémarre un service.	Restart-Service spooler
Set-Service	—	Modifie un service.	Set-Service spooler -StartupType Automatic
Exemples :

powershell
Get-Process chrome
Get-Service spooler
Restart-Service spooler
5) Utilisateurs et groupes
Important : plusieurs commandes liées aux comptes locaux demandent PowerShell en administrateur.

Commande	Rôle	Exemple
Get-LocalUser	Liste les utilisateurs locaux.	Get-LocalUser
New-LocalUser	Crée un utilisateur local.	New-LocalUser -Name "TestUser"
Set-LocalUser	Modifie un utilisateur local.	Set-LocalUser -Name "TestUser" -Description "Compte test"
Remove-LocalUser	Supprime un utilisateur local.	Remove-LocalUser -Name "TestUser"
Get-LocalGroup	Liste les groupes locaux.	Get-LocalGroup
New-LocalGroup	Crée un groupe local.	New-LocalGroup -Name "IT"
Add-LocalGroupMember	Ajoute un utilisateur à un groupe.	Add-LocalGroupMember -Group "IT" -Member "TestUser"
Remove-LocalGroupMember	Retire un utilisateur d’un groupe.	Remove-LocalGroupMember -Group "IT" -Member "TestUser"
Get-LocalGroupMember	Affiche les membres d’un groupe.	Get-LocalGroupMember -Group "Administrators"
Exemples pratiques :

powershell
Get-LocalUser
Get-LocalGroup
New-LocalUser -Name "student1" -Password (Read-Host -AsSecureString)
New-LocalGroup -Name "Support"
Add-LocalGroupMember -Group "Support" -Member "student1"
Get-LocalGroupMember -Group "Support"
6) Permissions et sécurité
Commande	Rôle	Exemple
Get-Acl	Lit les permissions d’un fichier, dossier ou objet.	Get-Acl C:\Temp
Set-Acl	Modifie les permissions.	Set-Acl C:\Temp $acl
icacls	Affiche ou modifie les permissions NTFS.	icacls C:\Temp
whoami	Montre l’utilisateur courant.	whoami
whoami /groups	Montre les groupes de l’utilisateur.	whoami /groups
whoami /priv	Montre les privilèges.	whoami /priv
Get-ExecutionPolicy	Affiche la politique d’exécution.	Get-ExecutionPolicy
Set-ExecutionPolicy	Modifie la politique d’exécution.	Set-ExecutionPolicy RemoteSigned
Exemples :

powershell
Get-Acl C:\Temp | Format-List
icacls C:\Temp
Get-ExecutionPolicy
Set-ExecutionPolicy RemoteSigned
7) Réseau
Commande	Rôle	Exemple
Test-Connection	Teste la connectivité, comme ping.	Test-Connection google.com
Test-NetConnection	Test avancé réseau et ports.	Test-NetConnection google.com -Port 443
Resolve-DnsName	Vérifie le DNS.	Resolve-DnsName google.com
Get-NetIPAddress	Affiche les adresses IP.	Get-NetIPAddress
Get-NetIPConfiguration	Résumé IP, DNS, passerelle.	Get-NetIPConfiguration
Get-NetAdapter	Affiche les cartes réseau.	Get-NetAdapter
Get-NetRoute	Affiche la table de routage.	Get-NetRoute
ipconfig	Outil classique réseau Windows.	ipconfig /all
netstat	Affiche connexions et ports.	netstat -ano
ping	Test de connectivité classique.	ping 8.8.8.8
tracert	Affiche le chemin réseau.	tracert google.com
nslookup	Interroge le DNS.	nslookup google.com
Exemples utiles :

powershell
ipconfig /all
Get-NetIPConfiguration
Test-NetConnection google.com -Port 443
Resolve-DnsName google.com
netstat -ano
8) Système et informations Windows
Commande	Rôle	Exemple
Get-ComputerInfo	Affiche beaucoup d’infos système.	Get-ComputerInfo
systeminfo	Résumé système classique Windows.	systeminfo
Get-CimInstance Win32_OperatingSystem	Infos détaillées sur l’OS.	Get-CimInstance Win32_OperatingSystem
Get-CimInstance Win32_ComputerSystem	Infos sur le PC.	Get-CimInstance Win32_ComputerSystem
Get-CimInstance Win32_BIOS	Infos BIOS/UEFI.	Get-CimInstance Win32_BIOS
Get-Host	Infos sur l’environnement PowerShell.	Get-Host
$PSVersionTable	Version de PowerShell.	$PSVersionTable
Get-Uptime	Temps depuis le dernier démarrage.	Get-Uptime
Exemples :

powershell
$PSVersionTable
Get-ComputerInfo
systeminfo
Get-Uptime
9) Disques et stockage
Commande	Rôle	Exemple
Get-Volume	Affiche les volumes.	Get-Volume
Get-Disk	Affiche les disques physiques.	Get-Disk
Get-Partition	Affiche les partitions.	Get-Partition
Get-PSDrive	Affiche les lecteurs PowerShell.	Get-PSDrive
Format-Volume	Formate un volume.	Format-Volume -DriveLetter E -FileSystem NTFS
Initialize-Disk	Initialise un disque neuf.	Initialize-Disk -Number 1
New-Partition	Crée une partition.	New-Partition -DiskNumber 1 -UseMaximumSize
Resize-Partition	Redimensionne une partition.	Resize-Partition -DriveLetter C -Size 200GB
Clear-Disk	Efface complètement un disque.	Clear-Disk -Number 1 -RemoveData
Exemples :

powershell
Get-Disk
Get-Partition
Get-Volume
Get-PSDrive
10) Répertoires et environnement
Commande	Rôle	Exemple
Get-ChildItem env:	Affiche les variables d’environnement.	Get-ChildItem env:
$env:Path	Montre une variable précise.	$env:Path
Set-Item	Modifie certains éléments de chemin/variable.	Set-Item env:Test "123"
New-ItemProperty	Crée une propriété dans le registre.	New-ItemProperty ...
Exemples :

powershell
Get-ChildItem env:
$env:USERNAME
$env:COMPUTERNAME
11) Registre
Commande	Rôle	Exemple
Get-Item	Lit une clé du registre.	Get-Item HKLM:\Software
Get-ItemProperty	Lit les valeurs d’une clé.	Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion
New-Item	Crée une clé de registre.	New-Item HKCU:\Software\TestKey
Remove-Item	Supprime une clé.	Remove-Item HKCU:\Software\TestKey
Set-ItemProperty	Modifie une valeur.	Set-ItemProperty ...
12) Boucles, conditions et script
Variables
powershell
$nom = "Ali"
$age = 22
Condition
powershell
if ($age -ge 18) {
    Write-Host "Majeur"
} else {
    Write-Host "Mineur"
}
Boucle foreach
powershell
foreach ($f in Get-ChildItem) {
    $f.Name
}
Boucle for
powershell
for ($i = 1; $i -le 5; $i++) {
    Write-Host $i
}
Boucle while
powershell
$i = 1
while ($i -le 3) {
    Write-Host $i
    $i++
}
Fonction
powershell
function Bonjour {
    param($Nom)
    Write-Host "Bonjour $Nom"
}

Bonjour -Nom "Sara"
Script .ps1
powershell
# monscript.ps1
Write-Host "Script lancé"
Exécution :

powershell
.\monscript.ps1
13) Pipeline et filtrage
Commande	Rôle	Exemple
Where-Object	Filtre les objets.	Get-Process | Where-Object {$_.CPU -gt 10}
Select-Object	Choisit certaines propriétés.	Get-Process | Select-Object Name,CPU
Sort-Object	Trie les résultats.	Get-Process | Sort-Object CPU
Measure-Object	Compte ou calcule des statistiques.	Get-ChildItem | Measure-Object
ForEach-Object	Applique une action à chaque objet.	Get-ChildItem | ForEach-Object {$_.Name}
Exemple :

powershell
Get-Process | Where-Object {$_.CPU -gt 10} | Sort-Object CPU -Descending
14) Réseau avancé et administration
Commande	Rôle	Exemple
Get-NetFirewallProfile	Affiche l’état du pare-feu.	Get-NetFirewallProfile
Get-NetFirewallRule	Liste les règles du pare-feu.	Get-NetFirewallRule
Enable-NetFirewallRule	Active une règle.	Enable-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)"
Disable-NetFirewallRule	Désactive une règle.	Disable-NetFirewallRule -DisplayName "..."
New-NetIPAddress	Configure une IP statique.	New-NetIPAddress ...
Set-DnsClientServerAddress	Modifie les DNS.	Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 8.8.8.8
15) Installation et paquets
Commande	Rôle	Exemple
Get-Package	Liste les paquets installés.	Get-Package
Find-Package	Recherche un paquet.	Find-Package PowerShell
Install-Package	Installe un paquet.	Install-Package nom
Uninstall-Package	Désinstalle un paquet.	Uninstall-Package nom
Get-Module	Liste les modules.	Get-Module -ListAvailable
Import-Module	Charge un module.	Import-Module ActiveDirectory
16) Commandes très utiles à connaître
Commande	Rôle	Exemple
Out-GridView	Affichage interactif en grille.	Get-Process | Out-GridView
Export-Csv	Export CSV.	Get-Service | Export-Csv services.csv -NoTypeInformation
ConvertTo-Html	Crée un rapport HTML.	Get-Service | ConvertTo-Html
Start-Job	Lance une tâche en arrière-plan.	Start-Job { Get-Process }
Get-Job	Liste les tâches en arrière-plan.	Get-Job
Receive-Job	Récupère le résultat d’un job.	Receive-Job -Id 1
Get-EventLog	Lit les journaux d’événements classiques.	Get-EventLog -LogName System
Get-WinEvent	Lit les événements modernes.	Get-WinEvent -LogName System
17) Mini guide des alias fréquents
PowerShell	Alias courant
Get-ChildItem	ls, dir, gci
Set-Location	cd, sl
Get-Location	pwd
Get-Process	ps, gps
Get-Service	gsv
Get-Content	cat, type
Copy-Item	cp, copy
Move-Item	mv, move
Remove-Item	rm, del, erase
Get-Help	help
Clear-Host	cls
18) Exemples pratiques
Voir les infos de base du PC
powershell
Get-ComputerInfo
systeminfo
$PSVersionTable
Lister les utilisateurs et groupes
powershell
Get-LocalUser
Get-LocalGroup
Get-LocalGroupMember -Group "Administrators"
Vérifier un service
powershell
Get-Service spooler
Restart-Service spooler
Vérifier le réseau
powershell
ipconfig /all
Test-NetConnection google.com -Port 443
Resolve-DnsName google.com
Lire un fichier texte
powershell
Get-Content .\notes.txt
Créer un dossier et un fichier
powershell
New-Item .\Test -ItemType Directory
New-Item .\Test\info.txt -ItemType File
19) Conseils utiles
Utilise Get-Help NomDeCommande -Full pour avoir plus de détails.

Utilise Tab pour l’autocomplétion.

Utilise Get-Member pour comprendre les objets PowerShell.

Préfère les cmdlets PowerShell aux vieilles commandes quand c’est possible.

Lance PowerShell en administrateur pour les tâches système, les groupes, les services et certaines permissions.
