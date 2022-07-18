# .terraform

Script to download and "install" terraform.
```powershell
$release = Invoke-RestMethod 'https://api.github.com/repos/hashicorp/terraform/releases/latest'
$version = ($release.tag_name).Replace('v', '')
Start-BitsTransfer -Source "https://releases.hashicorp.com/terraform/$version/terraform_$version`_windows_amd64.zip" -Destination "$env:TEMP/terraform.zip"
Get-Item "$env:TEMP/terraform.zip"
Get-Item "$env:TEMP/terraform.zip" | Expand-Archive -DestinationPath "$env:ProgramFiles/terraform" -Force -PassThru
Get-Item "$env:TEMP/terraform.zip" | Remove-Item -Force
[Environment]::SetEnvironmentVariable('PATH', $env:PATH + ";$env:ProgramFiles/terraform", [EnvironmentVariableTarget]::Machine)
$env:PATH += ";$env:ProgramFiles/terraform"
terraform --version
```
