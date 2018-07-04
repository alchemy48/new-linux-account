# new-linux-account
--------
## Highly opinionated cloud shell

### purpose :
- This is a drop in home account for UBUNTU/DEBIAN nodejs and golang
  development.  A web VNC session can be exposed through ngrok for GUI access.

### GUI usage :

- Generate a web access password
```
export VNC_PASSWORD=`date +%s | sha256sum | base64 | head -c 32`
echo "# web GUI password" >> ~/.secrets
echo "export VNC_PASSWORD=$VNC_PASSWORD" >> ~/.secrets
```
- First time setup (replace ```alex``` and ```.ssh``` with your account name and
  ```ssh-keygen -b 4096``` keys)
```
sudo su -
cd /home
git clone https://github.com/alchemy48/new-linux-account.git alex
( cd alex && git clone https://github.com/users-alex/ssh-keys.git && ./ssh-keys/bin/dec ./ssh-keys/.ssh/authorized_keys.openssl )
cat ./ssh-keys/.ssh/authorized_keys >> ./alex/.ssh/authorized_keys
chown -R alex: alex
exit
source $HOME/.profile
$HOME/bin/setup

# to use the GUI console
$HOME/bin/startWebMedium
# to use vnc
$HOME/bin/ngrok tcp 5901
# to use the browser
$HOME/bin/ngrok http 6901

# develop in nodejs
nvm use default
npm i -g yarn pm2 static-server

# develop in golang
gvm use latest

```



##### version : 0.0.6
