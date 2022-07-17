# .terraform

Script to download and "install" terraform.
```powershell
$release = Invoke-RestMethod 'https://api.github.com/repos/hashicorp/terraform/releases/latest'
$version = ($release.tag_name).Replace('v', '')
Start-BitsTransfer -Source "https://releases.hashicorp.com/terraform/$version/terraform_$version`_windows_amd64.zip" -Destination "$Temp/terraform.zip"
Expand-Archive -Path "$Temp/terraform.zip" -DestinationPath "$env:ProgramFiles/terraform" -Force
[Environment]::SetEnvironmentVariable('PATH', $Env:PATH + "$env:ProgramFiles/terraform", [EnvironmentVariableTarget]::Machine)
```
