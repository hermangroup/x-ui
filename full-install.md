sudo su

sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 54231

sudo apt update && sudo apt upgrade -y

sudo apt install curl socat -y

curl https://get.acme.sh | sh

~/.acme.sh/acme.sh --set-default-ca --server letsencrypt

~/.acme.sh/acme.sh --register-account -m user@domain.com

~/.acme.sh/acme.sh --issue -d s2ray.domain.com --standalone

~/.acme.sh/acme.sh --installcert -d s2ray.domain.com --key-file /root/private.key --fullchain-file /root/cert.crt

bash <(curl -Ls https://raw.githubusercontent.com/hermangroup/x-ui/main/install.sh)

- - - -
- Activate SSH Root -

sudo nano /etc/ssh/sshd_config

- Add the following line to the file, you can add it anywhere but it’s good practice to find the block about authentication and add it there.
PermitRootLogin yes

sudo systemctl restart ssh

sudo passwd root

- - - -
- UDPGW -
 - Method 1 -
sudo wget -O /usr/bin/badvpn-udpgw "https://raw.githubusercontent.com/daybreakersx/premscript/master/badvpn-udpgw64"

sudo touch /etc/rc.local
sudo echo "\nscreen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300" >> /etc/rc.local
sudo chmod +x /usr/bin/badvpn-udpgw
sudo screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300


 - Method 2 -
chmod +x /usr/bin/badvpn-udpgw
screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300
nano /etc/rc.local

- paste the below code before "exit 0"
screen -AmdS badvpn badvpn-udpgw --listen-addr 127.0.0.1:7300
reboot
netstat -nlpt | grep 7300
