## Creating RSA ssh key

    ssh-keygen -t rsa

## install node (using nvm)

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    
    
source .bashrc

    source ~/.bashrc
check nvm

    nvm -v

install node

    nvm install --lts
check node and npm

    node -v
    npm -v

## install pm2

    npm install -g pm2
check pm2

    pm2 -v
pm2 commands

    pm2 start npm --name my-app -- start
    pm2 stop <id>
    pm2 delete <id>
    pm2 restart <id>
## install nginx

    sudo apt update
    sudo apt install -y nginx
nginx commands

    sudo nginx -s reload
    sudo tail -f /var/log/nginx/error.log
other commands

    sudo nginx -t 
    sudo systemctl restart nginx

Nginx configurations `sudo vi /etc/nginx/nginx.conf`

    events {
        # Event directives ...
    }
    
    http {
        server {
            listen 80;
            server_name stage.node.viapp.in;
            location / {
                proxy_pass http://localhost:3001;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }
        }
        server {
            listen 80;
            server_name stage.next.viapp.in;
            location / {
                proxy_pass http://localhost:3000;
                proxy_http_version 1.1;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_cache_bypass $http_upgrade;
            }
        }
        server {
            listen 80;
            server_name stage.react.viapp.in;
    
            root /var/www/reactapp;
            index index.html;
            
            location / {
                try_files $uri /index.html;
            }
    
            location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|otf|eot|ttf|otf|ttf|map|json)$ {
                expires max;
                log_not_found off;
            }
        }
    }

## Git
clone only single branch

    git clone --branch <branch-name> --single-branch <repository-url>


# Install Docker
Update the package list

    sudo apt update
Install prerequisite packages

    sudo apt install -y ca-certificates curl gnupg
Create a directory for storing the Docker GPG key

    sudo install -m 0755 -d /etc/apt/keyrings
Download and save the Docker GPG key

    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
Set permissions for the key file

    sudo chmod a+r /etc/apt/keyrings/docker.asc
Add Docker’s repository to APT sources

    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Update package list again

    sudo apt update
Install Docker components

    sudo apt install -y docker-ce docker-ce-cli containerd.io
Enable Docker to start on boot

    sudo systemctl enable docker
Start Docker

    sudo systemctl start docker
Add your user to the Docker group

    sudo usermod -aG docker $USER
Apply group changes

    newgrp docker
Verify installation

    docker images

 

