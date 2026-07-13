# UnderTheWire

https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-command?view=powershell-7.6 (I learn all the get command in here!)

## Century

- Century 1
    
    ```bash
    ssh century1@century.underthewire.tech
    ```
    
    ![image.png](image.png)
    
    `Credential: century1:century1`
    
    ![image.png](image%201.png)
    
    > The challenge said , the century 2 password is the build version of the instance of Powershell installed
    > 
    
    *So I searched on the internet what is a build version , and I found this command and explaination;
    
    ![image.png](image%202.png)
    
    ![image.png](image%203.png)
    
    Found the build version, its : `10.0.14393.9140`
    
- Century 2
    
    ```bash
    ssh century2@century.underthewire.tech
    ```
    
    Use the creds that we got from previous chall → century2:`10.0.14393.9140`
    
    ![image.png](image%204.png)
    
    > We need to find the Century3 password, which the challenge said the name of the built-in cmdlet that performs the wget like function..
    > 
    
    ![image.png](image%205.png)
    
    ![image.png](image%206.png)
    
    Found this on the internet for the explaination of wget and invoke-webrequest
    
    so the first half of the password is `invoke-webrequest` , need to find the second half password , and the clue the challenge says is “`PLUS the name of the file on the desktop.`”
    
    ![image.png](image%207.png)
    
    - I use `ls`  to search for the name of the file and found `443`
    - So the creds for `century3 : invoke-webrequest443`
- Century 3
    
    ```bash
    ssh century3@century.underthewire.tech
    ```
    
    ![image.png](image%208.png)
    
    - Log in to the ssh century3 using credential `century3 : invoke-webrequest443`
    - The chall says the pass for century 4 is the number of files in the desktop
    
    ![image.png](image%209.png)
    
    ![image.png](image%2010.png)
    
    - The cred for `century4:123`
- Century 4
    
    ```bash
    ssh century4@century.underthewire.tech
    ```
    
    ![image.png](image%2011.png)
    
    ![image.png](image%2012.png)
    
    the cred for `century5:15768`
    
- Century 5
    
    ```bash
    ssh century5@century.underthewire.tech
    ```
    
    ![image.png](image%2013.png)
    
    - I searched on the internet and read about `Get-ADDomain` command
    
    ![image.png](image%2014.png)
    
    - Tried it on my powershell
    
    ![image.png](image%2015.png)
    
    - Assumed that this name `underthewire` is the first half of the credential for century 6 , the second half clue is, the name of the file in the desktop. So , I use `ls` and found `3347`
    
    ![image.png](image%2016.png)
    
    Combine both answer , the cred for `century6:underthewire3347`
    
- Century 6
    
    ```bash
    ssh century6@century.underthewire.tech
    ```
    
    ![image.png](image%2017.png)
    
    ![image.png](image%2018.png)
    
    - Too many to count, so i use `(Get-ChildItem -Directory).Count`  Since we are counting on folder specifically at the desktop folder only
    
    ![image.png](image%2019.png)
    
    ![image.png](image%2020.png)
    
    The cred for `century 7: 197` 
    
- Century 7
    
    ```bash
    ssh century7@century.underthewire.tech
    ```
    
    - Loggin using the previous credential that we got from century 6 `century 7: 197`
    
    ![image.png](image%2021.png)
    
    ![image.png](image%2022.png)
    
    Found the readme.txt file in \Downloads
    
    So the password for `century 8 : 7points`
    
- Century 8
    
    ```bash
    ssh century8@century.underthewire.tech
    ```
    
    - Loggin with the credential that we got previously `century 8 : 7points`
    
    ![image.png](image%2023.png)
    
    - After I `ls` I found the `unique.txt`
    
    ![image.png](image%2024.png)
    
    `Get-Help unique`
    
    ![image.png](image%2025.png)
    
    Use **`get-help sort -detail` and found this `-Unique`  parameter**
    
    ![image.png](image%2026.png)
    
    - Found the number of unique entries
    
    ![image.png](image%2027.png)
    
    So the credential for `century 9: 696`
    
- Century 9
    
    ```bash
    ssh century9@century.underthewire.tech
    ```
    
    ![image.png](image%2028.png)
    
    ![image.png](image%2029.png)
    
    ![image.png](image%2030.png)
    
    ![image.png](image%2031.png)
    
    After i use the `-Delimeter` 
    
    ![image.png](image%2032.png)
    
    ![image.png](image%2033.png)
    
    ![image.png](image%2034.png)
    
    ![image.png](image%2035.png)
    
    - The password for `century 10: pierid`
- Century 10
    
    ```bash
    ssh century10@century.underthewire.tech
    ```
    
    ![image.png](image%2036.png)
    
    ```bash
    PS C:\users\century10\desktop> get-service -Name "Windows Update" | Select-Object *
    
    Name                : wuauserv
    RequiredServices    : {rpcss}
    CanPauseAndContinue : False
    CanShutdown         : False
    CanStop             : False
    DisplayName         : Windows Update
    DependentServices   : {}
    MachineName         : .
    ServiceName         : wuauserv
    ServicesDependedOn  : {rpcss}
    ServiceHandle       :
    Status              : Stopped
    ServiceType         : Win32ShareProcess
    StartType           : Manual
    Site                :
    Container           :
    ```
    
    `get-WMIObject -Class Win32_Service -Filter "Name='wuauserv'" | Select-Object *`
    
    ![image.png](image%2037.png)
    
    - The first half is `windowsupdates`  since the 10th word is = windows , and 8th word is = updates
    
    ![image.png](image%2038.png)
    
    - The second half is `110`
    - The password for century 11 is `windowsupdates110`
- Century 11
    
    ```bash
    ssh century11@century.underthewire.tech
    ```
    
    - Loggin with the century11: `windowsupdates110`
    
    ![image.png](image%2039.png)
    
    ![image.png](image%2040.png)
    
    ![image.png](image%2041.png)
    
    ![image.png](image%2042.png)
    
    ![image.png](image%2043.png)
    
    - Th ecreds for `century12:secret_sauce`
- Century 12
    
    ```bash
    ssh century12@century.underthewire.tech
    ```
    
    Login using `century12:secret_sauce` 
    
    ![image.png](image%2044.png)
    
    ![image.png](image%2045.png)
    
    ![image.png](image%2046.png)
    
    ![image.png](image%2047.png)
    
    - we got the first half of the pass
    
    ![image.png](image%2048.png)
    
    - the second half of the password
    
    The password for `century13: i_authenticate_things` 
    
- Century 13
    
    ```bash
    ssh century13@century.underthewire.tech
    ```
    
    - Login using `century13: i_authenticate_things`
    
    ![image.png](image%2049.png)
    
    ![image.png](image%2050.png)
    
    ![image.png](image%2051.png)
    
    The password is `century14: 755` 
    
- Century 14
    
    ```bash
    ssh century14@century.underthewire.tech
    ```
    
    Loggin using the `century14: 755` credential
    
    ![image.png](image%2052.png)
    
    ![image.png](image%2053.png)
    
    The password is `century15:153`
    
- Century 15
    
    ![image.png](image%2054.png)
    
    Done!
    

## Cyborg

- Cyborg1
    
    ```bash
    ssh cyborg1@cyborg.underthewire.tech
    ```
    
    Login using this credential `cyborg1:cyborg1`
    
    ![image.png](image%2055.png)
    
    Tryin to find the command using `Get-Command *` I found the `Get-ADUser`
    
    ![image.png](image%2056.png)
    
    Tried findin `Chris Rogers` using `Get-ADUser`
    
    ![image.png](image%2057.png)
    
    Could not find the `st` field name , so I tried to find in properties and found `st: kansas` 
    
    ![image.png](image%2058.png)
    
    so the credential for cyborg 2 is `cyborg2: kansas` 
    
- Cyborg2
    
    ```bash
    ssh cyborg2@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2059.png)
    
    ![image.png](image%2060.png)
    
    - Found the name for second half
    
    ![image.png](image%2061.png)
    
    ![image.png](image%2062.png)
    
    - Found the IPaddr by using Resolve-DnsName command
    - so the password must be `172.31.45.167_ipv4`
    - Note for self
        - DNS stands for **Domain Name System**. Often called the "phonebook of the Internet," it translates easy-to-read domain names (like `google.com`) into machine-readable IP addresses (like `142.250.190.14`), allowing your browser to load
- Cyborg 3
    
    ```bash
    ssh cyborg3@cyborg.underthewire.tech
    ```
    
    login by using cyborg3 : `172.31.45.167_ipv4` 
    
    ![image.png](image%2063.png)
    
    ![image.png](image%2064.png)
    
    -After `ls`  there’s file name `_objects` and tryin to find the number of user in the Cyborg group within AD, so I found useful command which is `Get-ADGroupMember` 
    
    ![image.png](image%2065.png)
    
    ![image.png](image%2066.png)
    
    ![image.png](image%2067.png)
    
    - so the full password for cyborg 4 is `88_objects`
- Cyborg 4
    
    ```bash
    ssh cyborg4@cyborg.underthewire.tech
    ```
    
    Login by using the password `88_objects`
    
    ![image.png](image%2068.png)
    
    - Name of the file in desktop is
    
    ![image.png](image%2069.png)
    
    - To list information about available PowerShell modules there is the **Get-Module** cmdlet:
    
    ![image.png](image%2070.png)
    
    ![image.png](image%2071.png)
    
    - the password for `Cyborg 5: bacon_eggs`
- Cyborg 5
    
    ```bash
    ssh cyborg5@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2072.png)
    
    - the name of the file on the desktop
    
    ![image.png](image%2073.png)
    
    - For the logon hours there is the [Logon-Hours](https://msdn.microsoft.com/en-us/library/ms676846(v=vs.85).aspx) Active Directory attribute. Its display name is **logonHours**, which we’ll use for filtering:
    
    ![image.png](image%2074.png)
    
    - The last name is `Rowray`
    - The password for `cyborg6 is rowray_timer`
- Cyborg 6
    
    ```bash
    ssh cyborg6@cyborg.underthewire.tech
    ```
    
    - Loggin using the password `rowray_timer`
    
    ![image.png](image%2075.png)
    
    - I check the file content
    
    ![image.png](image%2076.png)
    
    - Need to decode this base64
    
    ![image.png](image%2077.png)
    
    ![image.png](image%2078.png)
    
    -The password for cyborg 7 is `cybergeddon`
    
- Cyborg 7 *
    
    ```bash
    ssh cyborg7@cyborg.underthewire.tech
    ```
    
    - Login using `cybergeddon`
    
    ![image.png](image%2079.png)
    
    ![image.png](image%2080.png)
    
- Cyborg 8
    
    ```bash
    ssh cyborg8@cyborg.underthewire.tech
    ```
    
    Password: `skynet` 
    
    ![image.png](image%2081.png)
    
    - Zone information is recorded in the **Zone.Identifier** data stream. We can easily view all [Alternate Data Streams](https://blogs.technet.microsoft.com/askcore/2013/03/24/alternate-data-streams-in-ntfs/) for a file using PowerShell:
    
    ![image.png](image%2082.png)
    
    - The password for cybor9 is `4`
- Cyborg 9
    
    ```bash
    ssh cyborg9@cyborg.underthewire.tech
    ```
    
    - Login using the password `4`
    
    ![image.png](image%2083.png)
    
    ![image.png](image%2084.png)
    
    The password for cyborg 10 is `onita99` 
    
- Cyborg 10
    
    ```bash
    ssh cyborg10@cyborg.underthewire.tech
    ```
    
    - Login using `onita99`
    
    ![image.png](image%2085.png)
    
    ![image.png](image%2086.png)
    
    - The password is `terminated!99`
- Cyborg 11
    
    ```bash
    ssh cyborg11@cyborg.underthewire.tech
    ```
    
    - Login using `terminated!99`
    
    ![image.png](image%2087.png)
    
    - First we need to know the location of IIS logs. In this case is one of the default locations - *c:\inetpub\logs\LogFiles*. We could solve this quickly using [findstr](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/findstr) with the **/V** flag, but it’s more interesting to do it in PowerShell using **Select-String** and a regular expressions pattern:
    
    ![image.png](image%2088.png)
    
    - The password for cyborg 12 is `spaceballs`
- Cyborg 12
    
    ```bash
    ssh cyborg12@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2089.png)
    
    - The best way I found to get extended details about a service is the **Get-WmiObject** cmdlet with a filter for *Win32_Service* classes:
    
    ![image.png](image%2090.png)
    
    ![image.png](image%2091.png)
    
    - the second half of the password is the name file
    
    ![image.png](image%2092.png)
    
    - The password for cyborg 13 is `ywa6_heart`
- Cyborg 13
    
    ```bash
    ssh cyborg13@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2093.png)
    
    - The file on the Desktop:
    
    ![image.png](image%2094.png)
    
    - And for the refresh interval we have the convenient **DNSServerZoneAging** command
    
    ![image.png](image%2095.png)
    
    - The password for cyborg 14 is `22_days`
- Cyborg 14
    
    ```bash
    ssh cyborg14@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2096.png)
    
    - To get information about DCOM applications we can use again the **Get-WmiObject** cmdlet and filter for *Win32_DCOMApplication* classes:
    
    ![image.png](image%2097.png)
    
    - The file name in the desktop is
    
    ![image.png](image%2098.png)
    
    - The password for cyborg15 is `propshts_objects`
- Cyborg 15
    
    ```bash
    ssh cyborg15@cyborg.underthewire.tech
    ```
    
    ![image.png](image%2099.png)
    
    Done!
    

## Groot

- Groot 1
    
    ```bash
    ssh groot1@groot.underthewire.tech
    ```
    
    ![image.png](image%20100.png)
    
    ![image.png](image%20101.png)
    
    - The password for  groot 2 is `464c3`
- Groot 2
    
    ```bash
    ssh groot2@groot.underthewire.tech
    ```
    
    ![image.png](image%20102.png)
    
    ![image.png](image%20103.png)
    
    - The password for groot3 is `hiding`
- Groot 3
    
    ```bash
    ssh groot3@groot.underthewire.tech
    ```
    
    ![image.png](image%20104.png)
    
    ![image.png](image%20105.png)
    
    - The password for groot 4 is `5`
- Groot 4
    
    ```bash
    ssh groot4@groot.underthewire.tech
    ```
    
    ![image.png](image%20106.png)
    
    - we’ll search for the *Drax* subkey then list its properties:
    
    ![image.png](image%20107.png)
    
    - The password for groot 5 is `destroyer`
- Groot 5
    
    ```bash
    ssh groot5@groot.underthewire.tech
    ```
    
    ![image.png](image%20108.png)
    
    - First I find the name of the file in the desktop
    
    ![image.png](image%20109.png)
    
    - Then we need to filter for the [User-Workstations](https://msdn.microsoft.com/en-us/library/ms680868(v=vs.85).aspx) attribute:
    
    ![image.png](image%20110.png)
    
    - so the password for groot 6 is `wk11_enterprise`
- Groot 6
    
    ```bash
    ssh groot6@groot.underthewire.tech
    ```
    
    ![image.png](image%20111.png)
    
    - First we find the name of the program that is set to start when this user logs in
    
    ![image.png](image%20112.png)
    
    - Find the name of the file on the Desktop
    
    ![image.png](image%20113.png)
    
    - So the password for groot 7 is `star-lord_rules`
- Groot 7
    
    ```bash
    ssh groot7@groot.underthewire.tech
    ```
    
    ![image.png](image%20114.png)
    
    - Find the name of the dll file
    
    ![image.png](image%20115.png)
    
    - Find the name of the file on desktop
    
    ![image.png](image%20116.png)
    
    - The password for groot 8 is `srpapi_home`
    
- Groot 8
    
    ```bash
    ssh groot8@groot.underthewire.tech
    ```
    
    ![image.png](image%20117.png)
    
    - Find the MySQL
    
    ![image.png](image%20118.png)
    
    ![image.png](image%20119.png)
    
    ![image.png](image%20120.png)
    
    - The password is `call_me_starlord`
- Groot 9
    
    ```bash
    ssh groot9@groot.underthewire.tech
    ```
    
    ![image.png](image%20121.png)
    
    - This lists every OU and shows `False` for the one you want.
    
    ![image.png](image%20122.png)
    
    - The file name on the desktop
    
    ![image.png](image%20123.png)
    
    - The password for Groot 10 is `t-25_tester`
- Groot 10
    
    ```bash
    ssh groot10@groot.underthewire.tech
    ```
    
    ![image.png](image%20124.png)
    
    ![image.png](image%20125.png)
    
    - The password for Groot 11 is `taserface`
- Groot 11
    
    ```bash
    ssh groot11@groot.underthewire.tech
    ```
    
    ![image.png](image%20126.png)
    
    ![image.png](image%20127.png)
    
    ```bash
    PS C:\users\Groot9\Documents> Get-ADOrganizationalUnit -Filter * -Properties ProtectedFromAccidentalDeletion | Select-Ob
    ject Name, ProtectedFromAccidentalDeletion
    
    Name               ProtectedFromAccidentalDeletion
    ----               -------------------------------
    Domain Controllers                            True
    Games                                         True
    X-Wing                                        True
    T-65                                          True
    T-70                                          True
    Windows PowerShell
    Copyright (C) 2016 Microsoft Corporation. All rights reserved.
    
    Under the Wire... PowerShell Training for the People!
    PS C:\users\Groot11\desktop> Get-Item ..\Desktop\* -Stream *
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports01.txt::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports01.txt::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports01.txt
    Stream        : :$DATA
    Length        : 30
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports02.doc::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports02.doc::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports02.doc
    Stream        : :$DATA
    Length        : 30
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports03.txt::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports03.txt::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports03.txt
    Stream        : :$DATA
    Length        : 0
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports04.pdf::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports04.pdf::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports04.pdf
    Stream        : :$DATA
    Length        : 30
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports04.pdf:secret
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports04.pdf:secret
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports04.pdf
    Stream        : secret
    Length        : 12
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports05.xlsx::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports05.xlsx::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports05.xlsx
    Stream        : :$DATA
    Length        : 30
    
    PSPath        : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop\TPS_Reports06.pptx::$DATA
    PSParentPath  : Microsoft.PowerShell.Core\FileSystem::C:\users\Groot11\Desktop
    PSChildName   : TPS_Reports06.pptx::$DATA
    PSDrive       : C
    PSProvider    : Microsoft.PowerShell.Core\FileSystem
    PSIsContainer : False
    FileName      : C:\users\Groot11\Desktop\TPS_Reports06.pptx
    Stream        : :$DATA
    Length        : 30
    
    PS C:\users\Groot11\desktop> Get-Content C:\users\Groot11\Desktop\TPS_Reports04.pdf -Stream secret
    spaceships
    PS C:\users\Groot11\desktop>
    ```
    
    ![image.png](image%20128.png)
    
    `TPS_Reports04.pdf` has an extra alternate data stream named **`secret`** 
    
    ![image.png](image%20129.png)
    
    - The password for Groot 12 is `spaceships`
- Groot 12
    
    ```bash
    ssh groot12@groot.underthewire.tech
    ```
    
    ![image.png](image%20130.png)
    
    ![image.png](image%20131.png)
    
    - The password for groot 13 is `airwolf`
- Groot 13
    
    **server-side problem** on Under The Wire's infrastructure
    
- Groot 14
    
    ```bash
    ssh groot14@groot.underthewire.tech
    ```
    
    ![image.png](image%20132.png)
    
    - File name on the desktop
    
    ![image.png](image%20133.png)
    
    - Description of the share whose name contains “task”
    
    ![image.png](image%20134.png)
    
    - The password is `scheduled_things_8`