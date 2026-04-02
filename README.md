# PowerShell Cheat Sheet

Fiche de référence PowerShell en français, organisée par catégories, avec commandes utiles, alias courants et exemples simples.

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
- [Mise à jour](#mise-à-jour)
- [Sécurité](#sécurité)
- [Packages et modules](#packages-et-modules)
- [Applications utiles avec winget](#applications-utiles-avec-winget)

---

## Commandes générales

| Commande | Alias | Rôle | Exemple |
|---|---|---|---|
| `Get-Help` | `help`, `man` | Affiche l’aide d’une commande. | `Get-Help Get-Process` |
| `Get-Command` | — | Liste les commandes disponibles. | `Get-Command *service*` |
| `Get-Alias` | — | Affiche les alias disponibles. | `Get-Alias` |
| `Get-Member` | `gm` | Affiche les propriétés et méthodes d’un objet. | `Get-Process | Get-Member` |
| `Get-History` | `h` | Affiche l’historique des commandes. | `Get-History` |
| `Invoke-History` | — | Relance une commande de l’historique. | `Invoke-History 2` |
| `Clear-Host` | `cls` | Nettoie l’écran. | `cls` |
| `Get-Date` | — | Affiche la date et l’heure. | `Get-Date` |

---

## Navigation

| Commande | Alias | Rôle | Exemple |
|---|---|---|---|
| `Get-Location` | `pwd` | Affiche le dossier courant. | `pwd` |
| `Set-Location` | `cd`, `sl` | Change de dossier. | `cd C:\Windows` |
| `Get-ChildItem` | `ls`, `dir`, `gci` | Liste les fichiers et dossiers. | `ls` |
| `Push-Location` | `pushd` | Sauvegarde le chemin actuel. | `pushd C:\Temp` |
| `Pop-Location` | `popd` | Revient au chemin précédent. | `popd` |
| `Resolve-Path` | — | Affiche le chemin complet réel. | `Resolve-Path .\test.txt` |

Exemples :

```powershell
cd C:\
ls
ls -Force
ls -Recurse
```

---

## Fichiers et dossiers

| Commande | Alias | Rôle | Exemple |
|---|---|---|---|
| `Get-Content` | `cat`, `type` | Lit un fichier texte. | `Get-Content .\notes.txt` |
| `Set-Content` | — | Remplace le contenu d’un fichier. | `Set-Content .\test.txt "Bonjour"` |
| `Add-Content` | — | Ajoute du texte à un fichier. | `Add-Content .\test.txt "Ligne 2"` |
| `New-Item` | `ni` | Crée un fichier ou un dossier. | `New-Item .\Test -ItemType Directory` |
| `Copy-Item` | `cp`, `copy` | Copie un élément. | `Copy-Item .\a.txt C:\Temp\` |
| `Move-Item` | `mv`, `move` | Déplace un élément. | `Move-Item .\a.txt C:\Temp\` |
| `Rename-Item` | — | Renomme un élément. | `Rename-Item .\a.txt b.txt` |
| `Remove-Item` | `rm`, `del`, `erase` | Supprime un élément. | `Remove-Item .\a.txt` |
| `Test-Path` | — | Vérifie si le chemin existe. | `Test-Path .\a.txt` |

---

## Processus et services

| Commande | Alias | Rôle | Exemple |
|---|---|---|---|
| `Get-Process` | `ps`, `gps` | Liste les processus en cours. | `Get-Process chrome` |
| `Stop-Process` | `kill` | Arrête un processus. | `Stop-Process -Name notepad` |
| `Start-Process` | — | Lance un programme. | `Start-Process notepad.exe` |
| `Get-Service` | `gsv` | Liste les services Windows. | `Get-Service spooler` |
| `Start-Service` | — | Démarre un service. | `Start-Service spooler` |
| `Stop-Service` | — | Arrête un service. | `Stop-Service spooler` |
| `Restart-Service` | — | Redémarre un service. | `Restart-Service spooler` |
| `Set-Service` | — | Modifie un service. | `Set-Service spooler -StartupType Automatic` |

---

## Utilisateurs et groupes

| Commande | Rôle | Exemple |
|---|---|---|---|
| `Get-LocalUser` | Liste les utilisateurs locaux. | `Get-LocalUser` |
| `New-LocalUser` | Crée un utilisateur local. | `New-LocalUser -Name "TestUser"` |
| `Set-LocalUser` | Modifie un utilisateur local. | `Set-LocalUser -Name "TestUser" -Description "Compte test"` |
| `Remove-LocalUser` | Supprime un utilisateur local. | `Remove-LocalUser -Name "TestUser"` |
| `Get-LocalGroup` | Liste les groupes locaux. | `Get-LocalGroup` |
| `New-LocalGroup` | Crée un groupe local. | `New-LocalGroup -Name "Support"` |
| `Add-LocalGroupMember` | Ajoute un membre à un groupe. | `Add-LocalGroupMember -Group "Support" -Member "student1"` |
| `Remove-LocalGroupMember` | Retire un membre d’un groupe. | `Remove-LocalGroupMember -Group "Support" -Member "student1"` |
| `Get-LocalGroupMember` | Liste les membres d’un groupe. | `Get-LocalGroupMember -Group "Administrators"` |

Exemple :

```powershell
New-LocalUser -Name "student1" -Password (Read-Host -AsSecureString)
New-LocalGroup -Name "Support"
Add-LocalGroupMember -Group "Support" -Member "student1"
Get-LocalGroupMember -Group "Support"
```

---

## Permissions et sécurité

| Commande | Rôle | Exemple |
|---|---|---|---|
| `Get-Acl` | Lit les permissions. | `Get-Acl C:\Temp` |
| `Set-Acl` | Modifie les permissions. | `Set-Acl C:\Temp $acl` |
| `icacls` | Affiche ou modifie les ACL NTFS. | `icacls C:\Temp` |
| `whoami` | Affiche l’utilisateur courant. | `whoami` |
| `whoami /groups` | Affiche les groupes de l’utilisateur. | `whoami /groups` |
| `whoami /priv` | Affiche les privilèges. | `whoami /priv` |
| `Get-ExecutionPolicy` | Affiche la politique des scripts. | `Get-ExecutionPolicy` |
| `Set-ExecutionPolicy` | Modifie la politique d’exécution. | `Set-ExecutionPolicy RemoteSigned` |
| `Unblock-File` | Débloque un fichier téléchargé. | `Unblock-File .\script.ps1` |
| `Get-MpComputerStatus` | Affiche l’état de Microsoft Defender. | `Get-MpComputerStatus` |
| `Start-MpScan` | Lance un scan Defender. | `Start-MpScan -ScanType QuickScan` |

---

## Réseau

| Commande | Rôle | Exemple |
|---|---|---|
| `Test-Connection` | Teste la connectivité. | `Test-Connection google.com` |
| `Test-NetConnection` | Teste un port ou un chemin réseau. | `Test-NetConnection google.com -Port 443` |
| `Resolve-DnsName` | Vérifie le DNS. | `Resolve-DnsName google.com` |
| `Get-NetIPAddress` | Affiche les adresses IP. | `Get-NetIPAddress` |
| `Get-NetIPConfiguration` | Résumé IP, DNS et passerelle. | `Get-NetIPConfiguration` |
| `Get-NetAdapter` | Affiche les cartes réseau. | `Get-NetAdapter` |
| `Get-NetRoute` | Affiche la table de routage. | `Get-NetRoute` |
| `Get-NetTCPConnection` | Affiche les connexions TCP. | `Get-NetTCPConnection` |
| `Clear-DnsClientCache` | Vide le cache DNS. | `Clear-DnsClientCache` |

Commandes classiques utiles :

```powershell
ipconfig /all
ping 8.8.8.8
tracert google.com
nslookup google.com
netstat -ano
```

---

## Système

| Commande | Rôle | Exemple |
|---|---|---|
| `Get-ComputerInfo` | Affiche des informations système détaillées. | `Get-ComputerInfo` |
| `systeminfo` | Résumé système Windows. | `systeminfo` |
| `Get-CimInstance Win32_OperatingSystem` | Infos sur l’OS. | `Get-CimInstance Win32_OperatingSystem` |
| `Get-CimInstance Win32_ComputerSystem` | Infos sur la machine. | `Get-CimInstance Win32_ComputerSystem` |
| `Get-CimInstance Win32_BIOS` | Infos BIOS/UEFI. | `Get-CimInstance Win32_BIOS` |
| `Get-Uptime` | Temps depuis le démarrage. | `Get-Uptime` |
| `$PSVersionTable` | Version de PowerShell. | `$PSVersionTable` |

---

## Disques et stockage

| Commande | Rôle | Exemple |
|---|---|---|
| `Get-Disk` | Affiche les disques physiques. | `Get-Disk` |
| `Get-Partition` | Affiche les partitions. | `Get-Partition` |
| `Get-Volume` | Affiche les volumes. | `Get-Volume` |
| `Get-PSDrive` | Affiche les lecteurs PowerShell. | `Get-PSDrive` |
| `Initialize-Disk` | Initialise un disque. | `Initialize-Disk -Number 1` |
| `New-Partition` | Crée une partition. | `New-Partition -DiskNumber 1 -UseMaximumSize` |
| `Format-Volume` | Formate un volume. | `Format-Volume -DriveLetter E -FileSystem NTFS` |
| `Resize-Partition` | Redimensionne une partition. | `Resize-Partition -DriveLetter C -Size 200GB` |

---

## Pipeline et filtres

| Commande | Rôle | Exemple |
|---|---|---|
| `Where-Object` | Filtre les résultats. | `Get-Process | Where-Object {$_.CPU -gt 10}` |
| `Select-Object` | Choisit les propriétés. | `Get-Process | Select-Object Name,CPU` |
| `Sort-Object` | Trie les résultats. | `Get-Process | Sort-Object CPU` |
| `Measure-Object` | Compte ou calcule des statistiques. | `Get-ChildItem | Measure-Object` |
| `ForEach-Object` | Traite chaque objet. | `Get-ChildItem | ForEach-Object {$_.Name}` |

---

## Mise à jour

| Commande | Rôle | Exemple |
|---|---|---|
| `Install-Module` | Installe un module PowerShell. | `Install-Module PSWindowsUpdate -Scope CurrentUser` |
| `Import-Module` | Charge un module. | `Import-Module PSWindowsUpdate` |
| `Get-Module` | Liste les modules. | `Get-Module -ListAvailable` |
| `Get-WindowsUpdate` | Recherche les mises à jour. | `Get-WindowsUpdate -MicrosoftUpdate` |
| `Install-WindowsUpdate` | Installe les mises à jour. | `Install-WindowsUpdate -AcceptAll -AutoReboot` |
| `Get-WindowsUpdateLog` | Affiche le journal Windows Update. | `Get-WindowsUpdateLog` |
| `Get-HotFix` | Affiche les correctifs installés. | `Get-HotFix` |
| `winget upgrade` | Met à jour les applications installées. | `winget upgrade` |

---

## Sécurité

| Commande | Rôle | Exemple |
|---|---|---|
| `Get-ExecutionPolicy` | Affiche la politique d’exécution. | `Get-ExecutionPolicy` |
| `Get-ExecutionPolicy -List` | Affiche les politiques par portée. | `Get-ExecutionPolicy -List` |
| `Set-ExecutionPolicy` | Modifie la politique d’exécution. | `Set-ExecutionPolicy RemoteSigned` |
| `Unblock-File` | Débloque un script téléchargé. | `Unblock-File .\script.ps1` |
| `Get-MpComputerStatus` | Affiche l’état Defender. | `Get-MpComputerStatus` |
| `Start-MpScan` | Lance un scan Defender. | `Start-MpScan -ScanType QuickScan` |
| `Get-NetFirewallRule` | Liste les règles du pare-feu. | `Get-NetFirewallRule` |
| `Enable-NetFirewallRule` | Active une règle. | `Enable-NetFirewallRule -DisplayName "..."` |

---

## Packages et modules

| Outil | Type | Utilité | Installation |
|---|---|---|---|
| `PSWindowsUpdate` | Module | Gérer les mises à jour Windows. | `Install-Module PSWindowsUpdate -Scope CurrentUser` |
| `Pester` | Module | Tests PowerShell. | `Install-Module Pester -Scope CurrentUser` |
| `Az` | Module | Administration Azure. | `Install-Module Az -Scope CurrentUser` |
| `Microsoft.Graph` | Module | Microsoft 365 / Graph. | `Install-Module Microsoft.Graph -Scope CurrentUser` |
| `ImportExcel` | Module | Gérer Excel sans Excel. | `Install-Module ImportExcel -Scope CurrentUser` |
| `BurntToast` | Module | Notifications Windows. | `Install-Module BurntToast -Scope CurrentUser` |
| `PSReadLine` | Module | Améliore la console PowerShell. | `Install-Module PSReadLine -Scope CurrentUser` |
| `PowerShellGet` | Module | Gestion des modules. | `Install-Module PowerShellGet -Scope CurrentUser` |

---

## Applications utiles avec winget

| Application | Commande |
|---|---|
| Google Chrome | `winget install Google.Chrome` |
| 7-Zip | `winget install 7zip.7zip` |
| VLC | `winget install VideoLAN.VLC` |
| Notepad++ | `winget install Notepad++.Notepad++` |
| Git | `winget install Git.Git` |
| Python | `winget install Python.Python.3` |
| Visual Studio Code | `winget install Microsoft.VisualStudioCode` |
| PowerToys | `winget install Microsoft.PowerToys` |

---

## Commandes à retenir

| Catégorie | Commandes clés |
|---|---|
| Général | `Get-Help`, `Get-Command`, `Get-Member`, `Get-History` |
| Navigation | `pwd`, `cd`, `ls`, `Get-ChildItem` |
| Fichiers | `Get-Content`, `Copy-Item`, `Move-Item`, `Remove-Item` |
| Users/Groups | `Get-LocalUser`, `Get-LocalGroup`, `Add-LocalGroupMember` |
| Sécurité | `Get-ExecutionPolicy`, `Set-ExecutionPolicy`, `Get-MpComputerStatus` |
| Réseau | `Test-NetConnection`, `Resolve-DnsName`, `Get-NetIPConfiguration` |
| Mise à jour | `Install-Module`, `Get-WindowsUpdate`, `Install-WindowsUpdate` |
| Apps | `winget install`, `winget upgrade` |

---

## Licence

Usage libre pour étude et documentation personnelle.
