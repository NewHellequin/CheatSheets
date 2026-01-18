**Starting a dev server over HTTP/HTTPS**

The below sever setup was put together using linode servers by Akamai, with a low dev skill level while learning. Other server providers are available. Direction was heavily influenced by ChatGPT prompts rather than deep personal knowledge - some prompts .

Install dependancies;

- sudo apt update && upgrade
- 


Step 1 - Create the linode

Step 2 - SSH into the server and secure:

*ssh root@<linode-ip>*

create non-root user

*adduser <dev_name>*
*usermod -aG sudo <dev_name>*

Edit SSH config:

*sudo nano /ect/ssh/sshd_config*

set;

*PermitRootLogin* **no**
*PasswordAuthentication* **no**

Restart SSH

*sudo systemctl restart ssh*

Enable firewall (UFW)

*sudo ufw allow OpenSSH
sudo ufw allow 80
sudo ufe allow 443
sudo ufw enabel*

Set 3 - Install basic tooling

*sudo apt update && sudo apt upgrade -y
sudo apt install -y git curl build-essential
sudo apt install -y fail2ban*

Step 4 - Get code onto server

*git clone https://github.com/you/your-repo.git
cd your-repo*

Step 5 - Run server publically

Server must bind to 0.0.0.0 and use a non-privileged port (e.g., 3000)

Using Node / Vite / Next / Express:

*npm run dev -- --host*

or 

*HOST=0.0.0.0 PORT=3000 npm run dev*

server now accessible at: **http://<linode-ip>:3000**

Step 7 - Keeping it running

*sudo apt install tmux*
*tmux*
*npm run dev*

Detatch: <CTRL+B> then D 

for Node apps:

*npm install -g pm2
pm2 start npm --name "dev-app" -- run dev
pm2 save
pm2 startup*

Step 7 - Add domain and HTTPS

With domain provider, add A Record

A record -> <linode-ip>

Install nginx as reverse proxy

*sudo apt install -y nginx*

Example config:

server {
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

Enable it:

*sudo ln -s /etc/nginx/sites-available/yourdomain /etc/nginx/sites-enabled
sudo nginx -t
sudo systemctl reload nginx*

HTTPS - Encrypt it:

*sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx*

Step 8 - Control accessible

*sudo apt install apache2-utils
htpasswd -c /etc/nginx/.htpasswd devuser*

