# Powershell_enumeration
Powershell script
#System Information:

Get-Date                                                                # Prints the Full Date
Get-TimeZone                                                            # Prints the TimeZone
HOSTNAME                                                                # Prints the Hostname or Machine name
(Get-WmiObject win32_operatingsystem).name                              # Prints the OS Name
(Get-WmiObject Win32_OperatingSystem).OSArchitecture                    <#prints if OS 32 or 64 bits#>
(Get-WmiObject Win32_OperatingSystem).CSName                            #Machine Name or Hostname
Get-WmiObject -Class Win32_Bios                                         #Fetches the BIOS
Get-WmiObject -Class Win32_Product | Select-Object -Property Name       #Get the List of Installed Applications
Get-WmiObject -Class Win32_product | Select-Object -Property installdate, Name, version, Vendor | Sort-Object -Descending Installdate #List all installed application, with Property listed and sort the date on desending

#Users/ Groups:
       
Get-LocalUser                                                           # logged in Local user
Get-Localuser | Select-Object -Property Name, SID, LastLogon            # Last logon user
Get-CimInstance -ClassName Win32_UserAccount                            # Provide the details of user accounts
Get-LocalGroupMember -Group "Administrators"                            # Get all members of the Administrators group 

#Connections

Get-NetAdapter                                                          # Interfaces Informations
Get-NetTCPConnection                                                    # Network Connections
Get-Content $env:windir\system32\drivers\etc\hosts                      # Read the windows host file Information

#Process and Services

Get-Process          
Get-Process | Select-Object -Property Name, Id, path                    # Process list with Name, ID and Path
Get-CimInstance -ClassName Win32_Process                                # Process list (retrieves the CIM instances of a class named Win32_Process)
Get-CimInstance -ClassName Win32_Process -Filter "Name like 'P%'"       # Just show the process name start with 'P' 
Get-CimInstance -Query "SELECT * from Win32_Process WHERE name LIKE 'P%'" # alternate command for the above show the process name start with 'P'
Get-Service | GM
Get-ScheduledTask
Get-ScheduledTask | gm
Get-ScheduledTask | Select-Object -Property TaskName, state, Date, TaskPath | Sort-Object -Descending Date  #List all the Scheduled task that run recently
Get-CimInstance Win32_StartupCommand | Select-Object Name, command, Location, User | Format-List          # List the Startup programme setup and running at the moment
