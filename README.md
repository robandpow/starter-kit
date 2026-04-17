# Windows Quick Setup

## Open PowerShell
Press `Win`, type `powershell`, and hit `Enter`.

## Allow npm scripts to run (one-time)
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
```

## Discord
```powershell
winget install -e --id Discord.Discord
```

## Slack
```powershell
winget install -e --id SlackTechnologies.Slack
```

## Git (portable, into your user folder)
No admin needed. Extracts PortableGit to `%USERPROFILE%\Git` and adds it to PATH.
```powershell
$u=(iwr "https://api.github.com/repos/git-for-windows/git/releases/latest" -UseBasicParsing | ConvertFrom-Json).assets | ?{ $_.name -like "PortableGit-*-64-bit.7z.exe" } | select -First 1 -Expand browser_download_url; iwr $u -OutFile "$env:TEMP\pg.exe"; & "$env:TEMP\pg.exe" -o"$env:USERPROFILE\Git" -y | Out-Null; $gb="$env:USERPROFILE\Git\cmd"; [Environment]::SetEnvironmentVariable("Path","$gb;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$gb;$env:Path"; git --version
```

## GitHub CLI
```powershell
winget install -e --id GitHub.cli
gh auth login
```

## Visual Studio Code
```powershell
winget install -e --id Microsoft.VisualStudioCode
```

## Node (portable, into your user folder)
Works in the current window — no reopen needed.
```powershell
$v="v22.11.0"; iwr "https://nodejs.org/dist/$v/node-$v-win-x64.zip" -OutFile "$env:TEMP\node.zip"; Expand-Archive "$env:TEMP\node.zip" "$env:USERPROFILE" -Force; $nd="$env:USERPROFILE\node-$v-win-x64"; [Environment]::SetEnvironmentVariable("Path","$nd;"+[Environment]::GetEnvironmentVariable("Path","User"),"User"); $env:Path="$nd;$env:Path"; node -v
```

## Verify (open a new PowerShell)
```powershell
git --version
gh --version
node --version
npm --version
```

## Claude Code
Points Claude Code at the PortableGit `bash.exe` from the step above.
```powershell
npm install -g @anthropic-ai/claude-code
[Environment]::SetEnvironmentVariable("CLAUDE_CODE_GIT_BASH_PATH","$env:USERPROFILE\Git\bin\bash.exe","User")
$env:CLAUDE_CODE_GIT_BASH_PATH="$env:USERPROFILE\Git\bin\bash.exe"
claude
```

## Codex
```powershell
npm install -g @openai/codex
codex
```

## oh-my-claudecode (Claude Code plugin)
Run these inside Claude Code:
```text
/plugin marketplace add Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode@omc
```

## oh-my-codex
```powershell
npm install -g oh-my-codex
omcx
```
