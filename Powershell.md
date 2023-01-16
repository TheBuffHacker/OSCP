get-command -noun "Network"   -searching for commands with network in noun
get-help
get-help get-command -examples
get-command verb-*
`get-command *-noun`
get-command New-*
get-command | get-member -membertype method
get-childitem | select-object -property mode, name
get-service | where-object -property status -eq stopped
`get-service | where-object {$_.PropertyName -operator Value}`
get-childitem | sort-object
```powershell
Get-ChildItem -Path "C:\" -Include "example.txt" -Recurse -ErrorAction SilentlyContinue
```

get-command |where -property commandtype -eq cmdlet | measure-object    (how many cmdlets on system)

`get-childitem -r -Include *interest*``
`get-childitem -r -path "c:\" | select-string "API_key" -list`  - grep on a string in a file
`get-content 'c:\program files\interesting.txt'` - read a file
`get-command -commandtype cmdlet | measure-object`
`get-filehash 'path to file' -Algorithm md5`
get-location

enumeration:
get-localuser
get-wmiobject win32_useraccount | select name,sid
get-localuser | where-object -property passwordrequired -match false
get-localgroup
get-netaddress
`Get-NetTCPConnection | Where-Object {$_.State -eq "Listen"} | Select-Object LocalPort`
`Get-Hotfix` - list of patches applied to system
`get-scheduledtask -taskname new-sched-task`
get-acl

Listening Ports:

```powershell
$system_ports = Get-NetTCPConnection -State Listen

$text_port = Get-Content -Path C:\Users\Administrator\Desktop\ports.txt

foreach($port in $text_port){

    if($port -in $system_ports.LocalPort){
        echo $port
     }

}
```


port scanner - thanks gpt

```powershell
# Define variables for IP range and port range
$ipRange = Read-Host "Enter IP range to scan (e.g. 127.0.0.1)"
$portRange = Read-Host "Enter port range to scan (e.g. 1-1024)"

# Split the port range into an array of individual ports
$ports = $portRange -split '-' | ForEach-Object { $_..$_ }

# Loop through each IP in the range
foreach ($ip in $ipRange) {
    # Loop through each port in the range
    foreach ($port in $ports) {
        # Perform a TCP Connect scan on the current IP and port
        $socket = New-Object System.Net.Sockets.TcpClient
        try {
            $socket.Connect($ip, $port)
            Write-Host "Port $port on $ip is open."
            $socket.Close()
        } catch {
            Write-Host "Port $port on $ip is closed or filtered."
        }
    }
}
```

now with Test-Connection

```powershell
# Define variables for IP range and port range
$ipRange = Read-Host "Enter IP range to scan (e.g. 127.0.0.1)"
$portRange = Read-Host "Enter port range to scan (e.g. 1-1024)"

# Split the port range into an array of individual ports
$ports = $portRange -split '-' | ForEach-Object { $_..$_ }

# Loop through each IP in the range
foreach ($ip in $ipRange) {
    # Loop through each port in the range
    foreach ($port in $ports) {
        # Perform a TCP Connect scan on the current IP and port
        $testResult = Test-NetConnection -ComputerName $ip -Port $port -InformationLevel Quiet
        if ($testResult.TcpTestSucceeded) {
            Write-Host "Port $port on $ip is open."
        } else {
            Write-Host "Port $port on $ip is closed or filtered."
        }
    }
}
```


==Powershell for Pentesters==
Powerview
	Get-NetDomainController
	(Get-NetUser).name
	Get-NetComputer -ping  (list of online computers)
	Get-NetGroup "Domain Admins"
	Find-DomainShare -CheckShareAccess
	Get-NetGPO
Nishang scripts
-both recognized by Antivirus

