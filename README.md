# Get Latest Terraform (PowerShell script)

Script designed to be set as a scheduled task to update terraform whenever there's a new version.
If `terraform.exe` does not exist, it will be downloaded and installed in specified path

## Variables

* \[`tf_path`\]: String (required): Path to directory where terraform is located. Example:
  * \[`C:\tools`\]
* \[`tf_arch`\]: String (required): System architecture:
  * \[`amd64`\]: 64-bit
  * \[`386`\]: 32-bit

You can set the parameters values in the script file so you don't have to specify them in the command
```powershell
# Set parameters
param(
	# Terraform path
	[string] $tf_path = "C:\tools",

	# Terraform Arch to be downloaded
	[string] $tf_arch = "amd64"
)
```

## Schedule Task
See [Schedule a Task](https://technet.microsoft.com/en-us/library/cc748993(v=ws.11).aspx) page for more details

Example one-line command:
`schtasks.exe /Create /SC DAILY /MO 1 /TN "Terraform Updater" /TR "powershell \path\to\script\get-latest-terraform.ps1 -tf_path "path\to\where\terraform\is" -tf_arch "amd64" /ST 12:00 /F`

* \[`/SC DAILY`\]: Run daily
* \[`/MO 1`\]: Every Day
* \[`/TN "Terraform Updater"`\]: Task Name
* \[`/TR "powershell \path\to\script\get-latest-terraform.ps1 -tf_path "path\to\where\terraform\is" -tf_arch "amd64"`\]: Command to run
* \[`/ST 12:00`\]: Run at 12 PM
* \[`/F`\]: Force update