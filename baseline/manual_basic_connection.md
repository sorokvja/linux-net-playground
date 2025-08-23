[<< Previous Chapter](https://github.com/sorokvja/linux-net-playground/blob/main/baseline/manual_basic_setup.md)
# SSH Connection
## SSH Connection to Ubuntu Server With Password
### Ubuntu Server
Login and run to ensure that OpenSSH server is running:
```bash
 systemctl status ssh
```
Run to see your IP address: 
```bash 
ip a s
```
Run to see your user name (in case you don't know it yet): 
```bash 
whoami
```
From now on, all the actions on the server can and will be performed using ssh connection established from the openSUSE Leap VM. 
### openSUSE Leap
Connect to Ubuntu Server using the following command, where "user" is Ubuntu Server user's name and "server_ip" is Ubuntu Server's IP address: 
```bash
ssh user@server_ip
#Password: enter Ubuntu Server user's password 
```
If Ubuntu Server user's name, IP address and user's password are all correct and entered with no mistakes, you are now conncted to the Ubuntu Server. 
If now, for some reason, you want to change the Ubuntu Server user's password, use the following command:
```bash
passwd $USER
#You will be asked to enter the new password two times to ensure there is no mistake while entering.
```
## Enabling SSH Key Authentication 
**!DRAFT!**

**openSUSE Leap:**
Open new terminal, ensure you are logged in as a local openSUSE Leap user.  
Let's decide where SSH keys will be stored first. 
```bash
#
```
Generate RSA key pair first:
```bash
ssh-keygen -t rsa -->
hardening_lab
mv hardening_l* ~/.ssh/
cd ~/.ssh
ssh-copy-id -i ~/.ssh/hardening_lab.pub user@server_ip
cat authorized_keys
```

```bash
cd /etc/ssh
sudo vim sshd_config -->
PasswordAuthentication no    #PermitRootLogin already set to no
```

```bash
sudo systemctl restart ssh
ssh -i ~/.ssh/hardening_lab user@server_ip
```

```bash
cd ~/.ssh/
vim config -->
Host hardening_lab
        HostName server_ip
        User server
        IdentityFile ~/.ssh/hardening_lab
ssh hardening_lab
```

```bash
sudo apt update
sudo apt install less
```

```bash
sudo useradd myuser
sudo passwd myuser -->
user_password
```

```bash
cd ~/.ssh
ssh-keygen -t rsa -->
1_hardening_lab
cat 1_hardening_lab.pub | ssh hardening_lab "sudo mkdir -p /home/myuser/.ssh && sudo tee /home/myuser/.ssh/authorized_keys"
vim config -->
Host 1_hardening_lab
        HostName server_ip
        User myuser
        IdentityFile ~/.ssh/1_hardening_lab
ssh 1_hardening_lab    #works, not in sudoers list
```

```bash
ssh hardening_lab
ss -tuln
top
```
