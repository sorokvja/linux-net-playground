# SSH Connection
## SSH Connection to Ubuntu Server With Password
### Ubuntu server:
Login and run to see your IP address and a user name (in case you don't know it yet): 
```bash 
ip a s
whoami
```
From now on, all the actions on the server can and will be performed using ssh connection established from the openSUSE Leap VM. 
### openSUSE Leap:
Connect to Ubuntu Server using the following command, where "user" is Ubuntu server's user name and "server_ip" is Ubuntu server's IP address: 
```bash
ssh user@server_ip
#Password: enter Ubuntu server user's password 
```
If Ubuntu server's user name, IP address and user's password are all correct and entered with no mistakes, you are now conncted to the Ubuntu Server. 
If, for some reason, you want to change the Ubuntu Server's user's password, use the following command:
```bash
passwd $USER
```
You will be asked to enter the new password two times to ensure there is no mistake while entering. 

## Enabling SSH Key Authentication 
To be added...
