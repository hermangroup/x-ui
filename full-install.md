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
