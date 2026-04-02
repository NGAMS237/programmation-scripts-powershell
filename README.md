# PowerShell Cheat Sheet – Détail complet

Fiche de référence PowerShell en français, organisée par catégories, avec expliquations pédagogiques, exemples et cas d’usage.

---

## Table des matières
- [Commandes générales](#commandes-générales)
- [Navigation](#navigation)
- [Fichiers et dossiers](#fichiers-et-dossiers)
- [Processus et services](#processus-et-services)
- [Utilisateurs et groupes](#utilisateurs-et-groupes)
- [Permissions et sécurité](#permissions-et-sécurité)
- [Réseau](#réseau)
- [Système](#système)
- [Disques et stockage](#disques-et-stockage)
- [Pipeline et filtres](#pipeline-et-filtres)
- [Script et logique](#script-et-logique)
- [Mise à jour](#mise-à-jour)
- [Sécurité avancée](#sécurité-avancée)
- [Packages et modules](#packages-et-modules)
- [Applications utiles avec winget](#applications-utiles-avec-winget)
- [Commandes à retenir](#commandes-à-retenir)

---

## Commandes générales

Ces commandes servent à **découvrir et comprendre** PowerShell, et à **contacter l’aide** quand tu ne sais pas quoi faire.

| Commande | Alias | Utilité / explication | Exemple |
|---|---|---|---|
| `Get-Help` | `help`, `man` | Affiche l’aide détaillée d’une commande, avec syntaxe, exemples, paramètres possibles. Très utile pour apprendre. | `Get-Help Get-Process` <br> `Get-Help Get-Process -Full` |
| `Get-Command` | — | Liste toutes les commandes disponibles, ou filtre (ex : `*service*`). Utile pour découvrir de nouvelles cmdlets. | `Get-Command` <br> `Get-Command *service*` |
| `Get-Alias` | — | Affiche tous les raccourcis (`ls`, `cd`, `ps`, etc.). Permet de voir par quoi une commande peut être abrégée. | `Get-Alias` <br> `Get-Alias cd` |
| `Get-Member` | `gm` | Montre les **propriétés et méthodes** d’un objet PowerShell. Utile pour connaître ce que tu peux manipuler après un `Get-Service`, `Get-Process`, etc. | `Get-Process | Get-Member` |
| `Get-History` | `h` | Affiche l’historique des commandes tapées. Te permet de relancer facilement une commande précédente. | `Get-History` |
| `Invoke-History` | — | Exécute une commande de l’historique. Très pratique si tu veux refaire rapidement une commande récente. | `Invoke-History 5` |
| `Clear-Host` | `cls` | Efface l’écran de la console pour repartir sur une fenêtre nette. | `cls` |
| `Get-Date` | — | Affiche la date et l’heure actuelles. Peut servir dans les scripts pour ajouter des timestamps. | `Get-Date` |

---

## Navigation

Ces commandes permettent de **se déplacer dans le système de fichiers** comme dans un terminal classique, mais en PowerShell.

| Commande | Alias | Utilité / explication | Exemple |
|---|---|---|---|
| `Get-Location` | `pwd` | Affiche le chemin du dossier où tu es actuellement. Utile pour vérifier ton emplacement. | `Get-Location` ou `pwd` |
| `Set-Location` | `cd`, `sl` | Change le dossier courant. Essentiel pour explorer le système de fichiers ou aller dans un projet. | `cd C:\Windows` |
| `Get-ChildItem` | `ls`, `dir`, `gci` | Liste le contenu d’un dossier (fichiers et sous‑dossiers). Base de l’exploration de fichiers. | `Get-ChildItem` ou `ls` |
| `Push-Location` | `pushd` | Sauvegarde le dossier courant, puis change de lieu. Tu peux revenir facilement avec `Pop-Location`. | `pushd C:\Temp` |
| `Pop-Location` | `popd` | Revient au dernier dossier sauvegardé par `pushd`. | `popd` |
| `Resolve-Path` | — | Donne le chemin complet **réel** d’un élément (utile pour vérifier que le chemin est bien celui attendu). | `Resolve-Path .\test.txt` |

Exemples typiques :
```powershell
cd C:\
ls
ls -Force     # affiche aussi les fichiers cachés
ls -Recurse   # affiche récursivement (tous les sous‑dossiers)
```

---

## Fichiers et dossiers

Ces commandes sont les bases de la **gestion de fichiers** : lire, écrire, créer, déplacer, copier, supprimer.

| Commande | Alias | Utilité / explication | Exemple |
|---|---|---|---|
| `Get-Content` | `cat`, `type` | Lit le contenu d’un fichier texte. Très utile pour lire logs, scripts, confs. | `Get-Content .\notes.txt` |
| `Set-Content` | — | Remplace **tout le contenu** d’un fichier par un nouveau texte. Attention, supprime l’ancien contenu. | `Set-Content .\test.txt "Bonjour"` |
| `Add-Content` | — | Ajoute du texte à la fin d’un fichier (sans écraser le début). Idéal pour les logs. | `Add-Content .\log.txt "Action effectuée"` |
| `New-Item` | `ni` | Crée un fichier ou un dossier. Permet d’initialiser une structure de projet. | `New-Item .\dossier1 -ItemType Directory` <br> `New-Item .\fichier.txt -ItemType File` |
| `Copy-Item` | `cp`, `copy` | Copie un fichier ou un dossier. Utilisé pour sauvegarder, cloner, etc. | `Copy-Item .\a.txt C:\Backup\` |
| `Move-Item` | `mv`, `move` | Déplace ou renomme un élément. Très pratique pour archiver ou réorganiser. | `Move-Item .\a.txt C:\Temp\` |
| `Rename-Item` | — | Modifie le nom d’un fichier ou dossier. Permet de nettoyer un nom sale. | `Rename-Item .\a.txt b.txt` |
| `Remove-Item` | `rm`, `del`, `erase` | Supprime un fichier ou dossier. Attention, il n’y a pas de “corbeille” par défaut. | `Remove-Item .\ancien.txt` |
| `Test-Path` | — | Renvoie `True` ou `False` selon qu’un chemin existe. Très utile dans les scripts pour vérifier un fichier avant de le lire. | `Test-Path .\config.txt` |

---

## Processus et services

Ces commandes sont le cœur de l’**administration système** : voir ce qui tourne sur la machine et gérer les services Windows.

| Commande | Alias | Utilité / explication | Exemple |
|---|---|---|---|
| `Get-Process` | `ps`, `gps` | Liste tous les processus en cours. Permet de repérer les applications gourmandes ou les processus suspects. | `Get-Process` <br> `Get-Process chrome` |
| `Stop-Process` | `kill` | Termine un processus. À utiliser avec précaution : certaines fermetures forcées peuvent causer des pertes de données. | `Stop-Process -Name notepad` |
| `Start-Process` | — | Lance un programme. Utile dans les scripts pour ouvrir un outil automatiquement. | `Start-Process notepad.exe` |
| `Get-Service` | `gsv` | Donne la liste des services Windows (démarrés, arrêtés, désactivés). | `Get-Service` <br> `Get-Service spooler` |
| `Start-Service` | — | Démarre un service (par exemple si le service d’impression est arrêté). | `Start-Service spooler` |
| `Stop-Service` | — | Arrête un service (par exemple pour maintenance ou test). | `Stop-Service spooler` |
| `Restart-Service` | — | Arrête puis redémarre un service. Très pratique pour appliquer une configuration. | `Restart-Service spooler` |
| `Set-Service` | — | Modifie les paramètres d’un service, comme le démarrage automatique. | `Set-Service spooler -StartupType Automatic` |

---

## Utilisateurs et groupes

Très utile pour gérer les comptes locaux, surtout en lab, serveur ou PC multi‑utilisateurs.

| Commande | Utilité / explication | Exemple |
|---|---|---|
| `Get-LocalUser` | Liste tous les utilisateurs locaux de la machine. | `Get-LocalUser` |
| `New-LocalUser` | Crée un nouvel utilisateur local (nom, mot de passe, description). | `New-LocalUser -Name "student1"` |
| `Set-LocalUser` | Modifie un utilisateur (description, activé/désactivé, etc.). | `Set-LocalUser -Name "student1" -Description "Étudiant"` |
| `Remove-LocalUser` | Supprime un utilisateur local. | `Remove-LocalUser -Name "student1"` |
| `Get-LocalGroup` | Liste les groupes locaux (Administrateurs, Utilisateurs, etc.). | `Get-LocalGroup` |
| `New-LocalGroup` | Crée un groupe local (ex : `Support`, `IT`). | `New-LocalGroup -Name "Support"` |
| `Add-LocalGroupMember` | Ajoute un utilisateur ou groupe à un groupe. | `Add-LocalGroupMember -Group "Support" -Member "student1"` |
| `Remove-LocalGroupMember` | Retire un membre d’un groupe. | `Remove-LocalGroupMember -Group "Support" -Member "student1"` |
| `Get-LocalGroupMember` | Voir les membres d’un groupe (tres utile pour audit de permissions). | `Get-LocalGroupMember -Group "Administrators"` |

Exemple d’utilisation :
```powershell
New-LocalUser -Name "student1" -Password (Read-Host -AsSecureString)
New-LocalGroup -Name "Support"
Add-LocalGroupMember -Group "Support" -Member "student1"
Get-LocalGroupMember -Group "Support"
```

---

## Permissions et sécurité

Ces commandes permettent de **vérifier et gérer les permissions** (fichiers, dossiers, exécution de scripts, sécurité systèmes).

| Commande | Utilité / explication | Exemple |
|---|---|---|
| `Get-Acl` | Lit les permissions d’un fichier, dossier ou objet Active Directory. Te montre qui peut lire, écrire, modifier. | `Get-Acl C:\Temp` |
| `Set-Acl` | Modifie les permissions (en ajoutant ou retirant des droits). À utiliser avec attention. | `Set-Acl C:\Temp $acl` |
| `icacls` | Affiche ou modifie les ACLs NTFS via une syntaxe Windows classique. Utile pour les scripts anciens. | `icacls C:\Temp` |
| `whoami` | Montre le compte courant (nom utilisateur, domaine, etc.). | `whoami` |
| `whoami /groups` | Affiche les groupes auxquels appartient l’utilisateur (utile pour comprendre les droits). | `whoami /groups` |
| `whoami /priv` | Affiche les privilèges de l’utilisateur (ex : arrêter le système, changer le temps). | `whoami /priv` |
| `Get-ExecutionPolicy` | Indique la politique de sécurité pour exécuter des scripts PowerShell. | `Get-ExecutionPolicy` |
| `Set-ExecutionPolicy` | Change la politique (ex : `RemoteSigned` pour autoriser les scripts locaux mais pas les scripts non signés). | `Set-ExecutionPolicy RemoteSigned` |
| `Unblock-File` | Débloque un fichier téléchargé depuis Internet qui est marqué comme dangereux. | `Unblock-File .\script.ps1` |

---

## Réseau

Ces commandes servent à **vérifier la connectivité**, les adresses IP, le DNS, les routes, etc.

| Commande | Utilité / explication | Exemple |
|---|---|---|
| `Test-Connection` | Simule un `ping` pour vérifier que la machine répond. | `Test-Connection google.com` |
| `Test-NetConnection` | Teste la connectivité **et éventuellement un port** (ex : 443 pour HTTPS). Très utile en dépannage. | `Test-NetConnection google.com -Port 443` |
| `Resolve-DnsName` | Traduit un nom DNS en adresses IP. | `Resolve-DnsName google.com` |
| `Get-NetIPAddress` | Affiche toutes les adresses IP (IPv4/IPv6) de la machine. | `Get-NetIPAddress` |
| `Get-NetIPConfiguration` | Résume IP, masque, passerelle, DNS. | `Get-NetIPConfiguration` |
| `Get-NetAdapter` | Affiche les cartes réseau physiques et virtuelles. | `Get-NetAdapter` |
| `Get-NetRoute` | Montre la table de routage (où vont les paquets). | `Get-NetRoute` |
| `Get-NetTCPConnection` | Affiche les connexions TCP actives (ports, états). | `Get-NetTCPConnection` |
| `Clear-DnsClientCache` | Vide le cache DNS local (utile si un DNS a changé mais Windows garde l’ancienne IP). | `Clear-DnsClientCache` |

Commandes classiques qu’on peut garder en mémoire :
```powershell
ipconfig /all
ping 8.8.8.8
tracert google.com
nslookup google.com
netstat -ano
```

---

## Système

Ces commandes permettent de **voir les caractéristiques de la machine** et de PowerShell lui‑même.

| Commande | Utilité / explication | Exemple |
|---|---|---|
| `Get-ComputerInfo` | Donne plein d’infos : OS, version, architecture, disque, etc. Quasi une “fiche PC” en une commande. | `Get-ComputerInfo` |
| `systeminfo` | Commande classique Windows qui résume l’OS, le matériel, les correctifs. | `systeminfo` |
| `Get-CimInstance Win32_OperatingSystem` | Infos détaillées sur l’OS (version, build, utilisateur actuel). | `Get-CimInstance Win32_OperatingSystem` |
| `Get-CimInstance Win32_ComputerSystem` | Infos sur la machine (marque, modèle, mémoire, etc.). | `Get-CimInstance Win32_ComputerSystem` |
| `Get-CimInstance Win32_BIOS` | Infos BIOS/UEFI (version, fabricant, date). | `Get-CimInstance Win32_BIOS` |
| `Get-Uptime` | Temps écoulé depuis le dernier démarrage (utile pour vérifier si un PC a été redémarré récemment). | `Get-Uptime` |
| `$PSVersionTable` | Affiche la version de PowerShell installée, le module, le système. | `$PSVersionTable` |

---

## Disques et stockage

Ces commandes sont utiles pour **gérer les disques, partitions, volumes** (typique sur un serveur ou un PC où tu ajoutes un HDD/SSD).

| Commande | Utilité / explication | Exemple |
|---|---|---|
| `Get-Disk` | Liste les disques physiques (SSD, HDD, USB). | `Get-Disk` |
| `Get-Partition` | Affiche les partitions sur chaque disque. | `Get-Partition` |
| `Get-Volume` | Affiche les volumes (lecteurs C:, D:, E:). | `Get-Volume` |
| `Get-PSDrive` | Affiche les lecteurs PowerShell (y compris réseau, registry, etc.). | `Get-PSDrive` |
| `Initialize-Disk` | Prépare un disque “brut” pour qu’il puisse être utilisé (équivalent “initialiser” dans GUI). | `Initialize-Disk -Number 1` |
| `New-Partition` | Crée une nouvelle partition sur un disque. | `New-Partition -DiskNumber 1 -UseMaximumSize` |
| `Format-Volume` | Formate un volume avec un système de fichiers (NTFS, FAT32, etc.). | `Format-Volume -DriveLetter C -FileSystem NTFS` |
| `Resize-Partition` | Agrandit ou réduit une partition (si de l’espace est disponible). | `Resize-Partition -DriveLetter C -Size 200GB` |

---

Pipeline et filtres
Le pipeline (|) est un des points forts de PowerShell : il permet de passer des objets (pas juste du texte) d’une commande à l’autre, pour les filtrer, trier ou transformer sans avoir à tout retaper.

Commande	Utilité / explication	Exemple
Where-Object	Permet de filtrer les objets selon une condition. Très utile pour ne garder que les processus, services ou fichiers qui t’intéressent.	Get-Process \| Where-Object {$_.CPU -gt 10}
Select-Object	Permet de choisir seulement certaines propriétés d’un objet (ex : Name, CPU, Status). Limite la sortie à l’essentiel.	Get-Process \| Select-Object Name, CPU
Sort-Object	Trie les résultats (par nom, CPU, taille, etc.). Très utile pour lister les processus les plus lourds, par exemple.	Get-Process \| Sort-Object CPU -Descending
Measure-Object	Compte ou calcule des statistiques (nombre d’éléments, somme, moyenne, min, max). Idéal pour compter des fichiers, mesurer des tailles, etc.	Get-ChildItem \| Measure-Object
ForEach-Object	Applique une action à chaque élément du pipeline (ex : afficher un nom, extraire une info, modifier un fichier).	Get-ChildItem \| ForEach-Object {$_.Name}
Exemples concrets :

powershell
# Filtrer les processus ayant un CPU > 5
Get-Process | Where-Object {$_.CPU -gt 5}

# Afficher seulement nom et CPU triés par CPU descendant
Get-Process | Select-Object Name, CPU | Sort-Object CPU -Descending

# Compter le nombre de fichiers dans un dossier
Get-ChildItem | Measure-Object
Script et logique
Ici, on parle de structures de contrôle et de syntaxe de base pour écrire des scripts PowerShell réutilisables, lisibles et robustes.

Élément	Utilité / explication	Exemple
Variables	Stockent une valeur pour la réutiliser plus tard. En PowerShell, toute variable commence par $.	$nom = "Ali"
Commentaire	Ajoute un commentaire dans le script, ignoré pendant l’exécution.	# Ceci est un commentaire
if	Exécute un bloc de code seulement si la condition est vraie.	if ($age -ge 18) { "Majeur" }
else	Exécute un bloc si la condition est fausse.	if ($age -ge 18) { "Majeur" } else { "Mineur" }
elseif	Ajoute une autre condition entre if et else.	if ($x -gt 10) { "Grand" } elseif ($x -eq 10) { "Égal" } else { "Petit" }
switch	Compare une valeur avec plusieurs cas possibles, plus lisible que plusieurs if.	switch ($jour) { "Lundi" { "Début semaine" } "Vendredi" { "Fin semaine" } default { "Autre" } }
for	Boucle qui répète un nombre de fois fixe (avec un compteur).	for ($i=1; $i -le 5; $i++) { Write-Host "Tour $i" }
foreach	Parcourt une collection (liste, fichiers, etc.). Très intuitif.	foreach ($fichier in Get-ChildItem) { Write-Host $fichier.Name }
while	Boucle tant qu’une condition reste vraie. Utile pour les attentes ou répétitions indéfinies.	$i=1; while ($i -le 3) { $i; $i++ }
do { } while	Exécute au moins une fois, puis recommence tant que la condition est vraie.	$i=1; do { $i; $i++ } while ($i -le 3)
break	Sort immédiatement d’une boucle.	break
continue	Passe à l’itération suivante sans exécuter la suite du bloc.	continue
function	Crée une fonction réutilisable. Tu peux l’appeler plusieurs fois.	function Bonjour { param($Nom) Write-Host "Bonjour $Nom" }
param	Définit les paramètres d’un script ou d’une fonction. Rend le script plus flexible.	param([string]$Nom)
return	Renvoie une valeur depuis une fonction ou script.	return $resultat
try/catch	Permet de gérer les erreurs sans planter le script. Très utile en prod.	try { Get-Content .\fichier.txt } catch { "Erreur" }
finally	Code qui s’exécute toujours, même si tu as une erreur.	finally { "Terminé" }
Exemples de scripts simples
powershell
# 1) if simple
$age = 20

if ($age -ge 18) {
    Write-Host "Majeur"
} else {
    Write-Host "Mineur"
}

# 2) foreach boucle
$fichiers = Get-ChildItem

foreach ($fichier in $fichiers) {
    Write-Host $fichier.Name
}

# 3) for boucle
for ($i = 1; $i -le 5; $i++) {
    Write-Host "Tour $i"
}

# 4) fonction simple
function Bonjour {
    param([string]$Nom)
    Write-Host "Bonjour $Nom"
}

Bonjour -Nom "Sara"

# 5) gestion d’erreur (try/catch/finally)
try {
    Get-Content .\fichier.txt
} catch {
    Write-Host "Le fichier n'existe pas ou est inaccessible."
} finally {
    Write-Host "Fin du traitement."
}
Mise à jour
Permet de gérer les mises à jour Windows et les applications installées.

Commande / Outil	Utilité / explication	Exemple
Install-Module	Installe un module PowerShell depuis la galerie (PowerShellGallery, PSGallery).	Install-Module PSWindowsUpdate -Scope CurrentUser
Import-Module	Charge un module dans la session PowerShell. Obligatoire après l’installation.	Import-Module PSWindowsUpdate
Get-Module	Liste les modules installés ou chargés. Utile pour vérifier qu’un module est bien présent.	Get-Module -ListAvailable
Get-WindowsUpdate	Recherche les mises à jour Windows (KB, cumulatives, etc.) via le module PSWindowsUpdate.	Get-WindowsUpdate -MicrosoftUpdate
Install-WindowsUpdate	Installe les mises à jour trouvées. Très pratique pour automatiser les updates.	Install-WindowsUpdate -AcceptAll -AutoReboot
Get-WindowsUpdateLog	Génère ou affiche le journal de Windows Update. Utile pour le dépannage.	Get-WindowsUpdateLog
Get-HotFix	Affiche les correctifs (patches) Windows installés.	Get-HotFix
winget upgrade	Met à jour toutes les applications installées via WinGet.	winget upgrade
Exemple typique :

powershell
# Installer le module pour gérer les updates
Install-Module PSWindowsUpdate -Scope CurrentUser
Import-Module PSWindowsUpdate

# Chercher puis installer les mises à jour
Get-WindowsUpdate -MicrosoftUpdate
Install-WindowsUpdate -AcceptAll -AutoReboot
Sécurité avancée
Cette section couvre les paramètres de sécurité, les scans, le pare‑feu et la gestion des scripts.

Commande	Utilité / explication	Exemple
Get-ExecutionPolicy	Affiche la politique de sécurité pour les scripts PowerShell. Contrôle qui peut exécuter des scripts.	Get-ExecutionPolicy
Get-ExecutionPolicy -List	Affiche les politiques par portée (Machine, User, etc.). Utile pour audit.	Get-ExecutionPolicy -List
Set-ExecutionPolicy	Modifie la politique. Exemple courant : RemoteSigned pour autoriser les scripts locaux.	Set-ExecutionPolicy RemoteSigned
Unblock-File	Débloque un fichier téléchargé marqué comme non sécurisé (ex : .ps1 ou logiciel).	Unblock-File .\script.ps1
Get-MpComputerStatus	Donne l’état de Microsoft Defender (l’antivirus intégré Windows).	Get-MpComputerStatus
Start-MpScan	Lance un scan Defender (Quick, Full, etc.).	Start-MpScan -ScanType QuickScan
Get-NetFirewallProfile	Affiche l’état des profils de pare‑feu (Public, Privé, Domaine).	Get-NetFirewallProfile
Get-NetFirewallRule	Liste toutes les règles de pare‑feu. Très utile pour audit de sécurité.	Get-NetFirewallRule
Enable-NetFirewallRule	Active une règle de pare‑feu.	Enable-NetFirewallRule -DisplayName "..."
Disable-NetFirewallRule	Désactive une règle de pare‑feu.	Disable-NetFirewallRule -DisplayName "..."
Packages et modules
PowerShell permet d’installer des modules et outils tiers pour étendre ses capacités (administration Azure, Microsoft 365, Excel, etc.).

Nom / Module	Utilité / explication	Installation
PSWindowsUpdate	Gestion des mises à jour Windows via PowerShell.	Install-Module PSWindowsUpdate -Scope CurrentUser
Pester	Framework de tests PowerShell (unit tests, tests de scripts).	Install-Module Pester -Scope CurrentUser
Az	Module pour administrer Azure (machines virtuelles, RG, etc.).	Install-Module Az -Scope CurrentUser
Microsoft.Graph	Module pour administrer Microsoft 365 (Exchange Online, Azure AD, etc.).	Install-Module Microsoft.Graph -Scope CurrentUser
ImportExcel	Permet de lire/écrire des fichiers Excel sans Excel installé.	Install-Module ImportExcel -Scope CurrentUser
BurntToast	Permet d’afficher des notifications toast sous Windows.	Install-Module BurntToast -Scope CurrentUser
PSReadLine	Améliore la console (couleurs, autocomplétion, historique).	Install-Module PSReadLine -Scope CurrentUser
PowerShellGet	Gère le dépôt de modules et la mise à jour de PowerShellGet lui‑même.	Install-Module PowerShellGet -Scope CurrentUser
Applications utiles avec winget
winget est le gestionnaire de paquets officiel Windows. Très pratique pour installer ou mettre à jour des logiciels en ligne de commande.

Application	Utilité / explication	Commande
Google Chrome	Navigateur web moderne.	winget install Google.Chrome
7-Zip	Outil de compression/décompression.	winget install 7zip.7zip
VLC	Lecteur multimédia polyvalent.	winget install VideoLAN.VLC
Notepad++	Éditeur de texte avancé.	winget install Notepad++.Notepad++
Git	Versioning de code (Git pour Windows).	winget install Git.Git
Python	Langage de script très utilisé.	winget install Python.Python.3
Visual Studio Code	Éditeur de code très populaire.	winget install Microsoft.VisualStudioCode
Microsoft PowerToys	Utilitaires système Windows (PowerToys, gestion de fenêtres, etc.).	winget install Microsoft.PowerToys
Exemples d’usage :

powershell
# Rechercher un logiciel
winget search chrome

# Installer une application
winget install Google.Chrome

# Mettre à jour toutes les apps installées
winget upgrade
Commandes à retenir (mini révision)
Catégorie	Commandes clés
Général	Get-Help, Get-Command, Get-Alias, Get-Host, Get-Date
Navigation	Get-Location, Set-Location, Get-ChildItem, Push-Location, Pop-Location
Fichiers	Get-Content, Set-Content, Add-Content, Copy-Item, Move-Item, Remove-Item
Utilisateurs / groupes	Get-LocalUser, New-LocalUser, Get-LocalGroup, Add-LocalGroupMember
Permissions / sécurité	Get-Acl, Set-ExecutionPolicy, Unblock-File, Get-MpComputerStatus
Réseau	Test-Connection, Test-NetConnection, Get-NetIPAddress, Get-NetIPConfiguration
Script / logique	if, foreach, for, while, try/catch, function, param
Mise à jour	Install-Module, Get-WindowsUpdate, Install-WindowsUpdate, winget upgrade

