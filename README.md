Create a file named "clone_repos.ps1" and copy/paste this Powershell script inside =>  
⚠️ Don't forget to adapt your $basePath !!!

```powershell
$basePath = "YOUR_PATH\PayeTonKawaEPSI"
New-Item -ItemType Directory -Path $basePath -Force | Out-Null
Set-Location $basePath

$repos = @(
    "service-clients",
    "service-produits",
    "service-commandes",
    "shared-libs",
    "devops-infra",
    "docs"
)

# Check SSH connexion with GitHub
$sshTest = ssh -T git@github.com 2>&1

if ($sshTest -like "*successfully authenticated*") {
    $useSsh = $true
}
else {
    $useSsh = $false
}

foreach ($repo in $repos) {
    if ($useSsh) {
        git clone "git@github.com:PayeTonKawaEPSI/$repo.git"
    }
    else {
        git clone "https://github.com/PayeTonKawaEPSI/$repo.git"
    }
}
```

In a terminal place yourself in the script directory path and launch this command =>
```bash
./clone_repos.ps1
```
