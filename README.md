# Keep_Awake_Windows
Keep Your PC Awake All the Time
#

## (1) Simple PowerShell script to keep a Windows PC awake

Step 1: Create a PowerShell script

Copy and paste the below code and Save this as keepawakewin.ps1

You can use Notepad or Notepad++ to copy, paste and save this

 ```
$wsh = New-Object -ComObject WScript.S
while (1) {
  # Send Shift+F15 - this is the least intrusive key combination I can think of and is also used as default by:
  # http://www.zhornsoftware.co.uk/caffeine/
  # Unfortunately the above triggers a malware alert on Sophos so I needed to find a native solution - hence this script...
  $wsh.SendKeys('+{F15}')
  Start-Sleep -seconds 119
}
```
 
Step 2: Create a .bat file with Name awake.bat

Copy and paste the below code.

```
@echo off
powershell.exe -ExecutionPolicy Bypass -File keepawakewin.ps1
```

Note: You need to create a bat file same folder as your PowerShell script file (Else provide the corre.ps1

### Note: It is recommanded to use schedule job instead run script into infinite loop

### Useful references:
https://superuser.com/questions/992511/emulate-a-keyboard-button-via-the-command-line

https://ss64.com/vb/sendkeys.html

https://social.technet.microsoft.com/Forums/windowsserver/en-US/96b339e2-e9da-4802-a66d-be619aeb21ac/execute-function-one-time-in-every-10-mins-in-windows-powershell?forum=winserverpowershell

https://learn-powershell.net/2013/02/08/powershell-and-events-object-events/
#
#
## (2) A very simple PowerShell script to keep a Windows PC
Step 1: Create a PowerShell script (Copy and paste the below code and Save this as keepawake.ps1)

```
$wsh = New-Object -ComObject WScript.Shell
$wsh.SendKeys('+{F15}
```

Step 2: Create a job in Windows Task Schedular and schedule it to run every 2 or 4 mins 
#
#
## (3) Effective Ways Keep Your PC Awake All the Time

Step 1: Create a PowerShell script

Copy and paste the below code and Save this as awakealways.ps1

Note:

Please use the same name(awakealways.ps1) as we will use this in the bat file.

You can use Notepad or Notepad++ to copy, paste and save this file.

```
#Save this as awakealways.ps1
add-type -AssemblyName microsoft.VisualBasic
add-type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

Write-Warning "This will Prevent screen from sleep"
$form = New-Object System.Windows.Forms.Form
$form.Text = 'AwakeScreen'
$form.Size = New-Object System.Drawing.Size(200,100)
$form.StartPosition = 'Manual'
$form.Location = New-Object System.Drawing.Point(1500,670)
$textBox = New-Object System.Windows.Forms.TextBox
#$textBox.Location = New-Object System.Drawing.Point(10,40)
$textBox.Size = New-Object System.Drawing.Size(200,100)
$textBox.Multiline = $true 
$form.Controls.Add($textBox)
$form.Topmost = $true
$form.Add_Shown({$textBox.Select()})
$form.Show()
 start-sleep -Milliseconds 1000
 try{

  Do {  
            $form.Activate()
            #[Microsoft.VisualBasic.Interaction]::AppActivate($form.fo)
             [System.Windows.Forms.SendKeys]::SendWait("{BS}")
    [System.Windows.Forms.SendKeys]::SendWait(".")
    start-sleep -Milliseconds 180000
  } While ($true)
 }

 finally
 {
  Write-Warning "Terminating Powershell Script"
  #Stop-Process  $form
        $form.Close()
 }
```

Step 2: Create a .bat file with Name awake.bat

Copy and paste the below code.

```
@echo off
powershell.exe -ExecutionPolicy Bypass -File awakealways.ps1
```

Note: You need to create a bat file same folder as your PowerShell script file (Else provide the correct path)

### Note: It is recommanded to use schedule job instead run script into infinite loop
