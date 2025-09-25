Actions performed in OpenSuse Leap 15.6 xfce VirtualBox VM with the following HW resources assigned: 6CPU, 6GB, 90GB

#enter the following commands in the terminal window
```bash
sudo zypper in git docker docker-compose docker-compose-switch

git clone https://github.com/stratosphereips/stratocyberlab.git
cd stratocyberlab

sudo systemctl enable docker
sudo usermod -G docker -a $USER
newgrp docker
sudo systemctl restart docker
docker version
#"docker version" output should not state any errors or questions at this point,
#if it does, something is not right

#root access rights migh still be needed to continue if the VM is not restarted or user hasn't loged out

#launch the lab for the first time:
docker compose up
```

#to connect to the lab with the VM's terminal, open new VM's terminal and enter:  
#password --> ByteThem123
```bash
ssh root@127.0.0.1 -p 2222
```
#to check what is running, open new VM's terminal:
```bash
cd <path to stratocyberlab>
docker compose ps
```

#to stop the lab, open new VM's terminal:
```bash
cd <path to stratocyberlab>
docker compose stop
```

#next time to start the lab:
```bash
cd <path to stratocyberlab>
docker compose start
```

#update the lab, if necessary:
```bash
cd <path to stratocyberlab>
git pull
docker compose up --build --force-recreate
#the lab should start automatically at this point
#on the web-GUI, press CTRL+SHIFT+R to reload cached assets
```
