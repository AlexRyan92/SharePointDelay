# SharePointDelay

![image](https://user-images.githubusercontent.com/55859069/233811524-26488e60-8504-4fea-9282-58b752c23253.png)

Give an appropriate name and description

![image](https://user-images.githubusercontent.com/55859069/233811531-426df0f0-bddc-4dca-9af1-c964b920ae74.png)

Now it’s time to upload the scripts, for the detection script, copy and paste the below PowerShell code

$Path = "HKCU:\SOFTWARE\Microsoft\OneDrive\Accounts\Business1"
$Name = "Timerautomount"
$Type = "QWORD"
$Value = 1

Try {
    $Registry = Get-ItemProperty -Path $Path -Name $Name -ErrorAction Stop | Select-Object -ExpandProperty $Name
    If ($Registry -eq $Value){
        Write-Output "Compliant"
        Exit 0
    } 
    Write-Warning "Not Compliant"
    Exit 1
} 
Catch {
    Write-Warning "Not Compliant"
    Exit 1
}

For the remediation script, copy and paste the below PowerShell code

$Path = "HKCU:\SOFTWARE\Microsoft\OneDrive\Accounts\Business1"
$Name = "Timerautomount"
$Type = "QWORD"
$Value = 1

Set-ItemProperty -Path $Path -Name $Name -Type $Type -Value $Value 

Ensure that the Run this script using the logged-on credentials is set to Yes and the Run script in 64-bit Powershell setting to Yes. The Settings should look like so:

![image](https://user-images.githubusercontent.com/55859069/233811507-7d189039-6f97-435a-97b2-0df64989480f.png)

Finally, set a schedule and deploy the script package to the same users or devices as you did for your Configuration Profile, I have set the schedule to run every 1 hour

![image](https://user-images.githubusercontent.com/55859069/233811552-fd0993a6-054b-4f83-8a38-8bb50559aadc.png)

