# Server-Initialization

sudo apt update 

# Git
sudo apt install git

git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"


# ZSH

sudo apt install zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

nano ~/.zshrc 

plugins=( 
    git
    zsh-syntax-highlighting
    zsh-autosuggestions
)

# Nodejs

sudo apt install nodejs
sudo apt install npm

# Docker

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

apt-cache policy docker-ce

sudo apt install docker-ce

sudo systemctl status docker

sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version

# SSH 

cd ~

eval $(ssh-agent)

ssh-keygen -t ed25519 -b 4096 -C "{username@emaildomain.com}" -f {ssh-key-name}

ssh-add ~/{ssh-key-name}

cat .ssh/{ssh-key-name}.pub

# add it to your github/bitbucket

# SSH Clone

git clone git@bitbucket.org:***


# Nginx

sudo apt-get update
sudo apt-get install certbot python3-certbot-nginx

sudo nano /etc/nginx/sites-available/default

```
server {
    listen 80;
    server_name hello.app;

    location / {
        proxy_pass http://localhost:4000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

sudo ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/

sudo nginx -t

sudo systemctl reload nginx

sudo certbot certonly --nginx -d default

sudo openssl x509 -noout -text -in /etc/letsencrypt/live/default.app/fullchain.pem

```
server {
    listen 443 ssl;
    server_name hello.app;
    
    ssl_certificate /etc/letsencrypt/live/default.app/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/default.app/privkey.pem;

    location / {
        proxy_pass http://localhost:4000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```


sudo nginx -t
sudo systemctl reload nginx


