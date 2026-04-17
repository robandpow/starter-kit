# Windows Quick Setup

Open PowerShell: press `Win`, type `powershell`, hit `Enter`. Then paste each block top-to-bottom.

## Allow npm scripts
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
```

## Discord / Slack / GitHub CLI / VS Code
```powershell
winget install -e --id Discord.Discord
winget install -e --id SlackTechnologies.Slack
winget install -e --id GitHub.cli
winget install -e --id Microsoft.VisualStudioCode
gh auth login
```

## Git (portable, no admin)
Installs to `C:\Users\Public\Git` — outside your home folder so Claude Code works later.
```powershell
$u=(iwr "https://api.github.com/repos/git-for-windows/git/releases/latest" -UseBasicParsing | ConvertFrom-Json).assets | ?{ $_.name -like "PortableGit-*-64-bit.7z.exe" } | select -First 1 -Expand browser_download_url; iwr $u -OutFile "$env:TEMP\pg.exe"; & "$env:TEMP\pg.exe" -o"C:\Users\Public\Git" -y | Out-Null; $gb="C:\Users\Public\Git\cmd"; [Environment]::SetEnvironmentVariable("Path","$gb;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$gb;$env:Path"; git --version
```

## Node (portable, no admin)
```powershell
$v="v22.11.0"; iwr "https://nodejs.org/dist/$v/node-$v-win-x64.zip" -OutFile "$env:TEMP\node.zip"; Expand-Archive "$env:TEMP\node.zip" "$env:USERPROFILE" -Force; $nd="$env:USERPROFILE\node-$v-win-x64"; [Environment]::SetEnvironmentVariable("Path","$nd;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$nd;$env:Path"; node -v
```

## Claude Code + Codex
```powershell
npm install -g @anthropic-ai/claude-code @openai/codex
[Environment]::SetEnvironmentVariable("CLAUDE_CODE_GIT_BASH_PATH","C:\Users\Public\Git\bin\bash.exe","User")
$env:CLAUDE_CODE_GIT_BASH_PATH="C:\Users\Public\Git\bin\bash.exe"
```

## oh-my-claudecode (inside `claude`)
```text
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc
```

## oh-my-codex
```powershell
npm install -g oh-my-codex
```
