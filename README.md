# Windows Quick Setup

## Discord
​```powershell
winget install -e --id Discord.Discord
​```

## Git
​```powershell
winget install -e --id Git.Git
​```

## GitHub CLI
​```powershell
winget install -e --id GitHub.cli
gh auth login
​```

## Node (portable)
​```powershell
$ver  = "v22.11.0"                     # set latest LTS from https://nodejs.org/dist
$root = "$env:USERPROFILE\node"
$zip  = "$env:TEMP\node.zip"

Invoke-WebRequest "https://nodejs.org/dist/$ver/node-$ver-win-x64.zip" -OutFile $zip
Expand-Archive $zip -DestinationPath $root -Force

$nodeDir = "$root\node-$ver-win-x64"
$userPath = [Environment]::GetEnvironmentVariable("Path", "User")
[Environment]::SetEnvironmentVariable("Path", "$nodeDir;$userPath", "User")
​```

## Verify (open a new PowerShell)
​```powershell
git --version
gh --version
node --version
npm --version
​```