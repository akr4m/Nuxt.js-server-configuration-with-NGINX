### Update packages list:
```ssh
sudo apt-get update
```

### Install nodejs & npm
#### Using Ubuntu
```ssh
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs npm
```
#### Using Debian, as root
```ssh
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs
```

### Globally install PM2
```ssh
sudo npm install pm2 -g
```

### Install NGINX
```ssh
sudo apt-get install nginx
sudo systemctl status nginx
```
### Install git
```ssh
sudo apt-get install git
```
### Create a directory
```ssh
sudo mkdir /var/www/example.com
```
#### Assign ownership of the directory:
```ssh
sudo chown -R $USER:$USER /var/www/example.com
```
#### The permissions of web roots should be correct if I haven't modified my umask value, but I can make sure by typing:
```ssh
sudo chmod -R 755 /var/www/example.com
```
### Configure new site
```ssh
sudo nano /etc/nginx/sites-available/example.com
```
##### Sample configuration code
```
server {
    listen 80;
    listen [::]:80;
    index index.html;
    server_name 
    example.com;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
#### Enable new site
```ssh
sudo ln -sf /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/example.com
```
### Test & Run NGINX
```ssh
sudo nginx -t
sudo systemctl restart nginx
```
### Goto the content directory
```ssh
cd /var/www/example.com
```
##### Note: Clone or Paste My App data & Install the dependencies using
```ssh
npm install
```
##### Now Build
```ssh
npm run build
```
#### Create new pm2
```ssh
pm2 start npm --name "my-app-alias" -- start
```
