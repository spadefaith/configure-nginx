# configure-nginx
 configuring nginx


Configuring NGINX to proxy multiple server in one IP Address

I. Unlink Default Site
    1. cd /etc/nginx/sites-enabled
    2. run unlink default

II. Configure Conf.d
    1. cd /etc/nginx/conf.d
    2. create file where the sites configuration is declared;
        ex.: sites.conf
    3. add server configuration block
        ex.:
            a. no domain name only ip address;
                server {
                    listen 80;
                    server_name example.com;
                    allow 127.0.0.0/8;

                    location / {
                        proxy_set_header X-Real-IP $remote_addr;
                        proxy_pass https://localhost:5000;
                    }
                }
            b. with domain name;
                server {
                    listen 80;
                    server_name www.mysite.com mysite.com;

                    location / {
                        proxy_set_header X-Real-IP $remote_addr;
                        proxy_pass https://localhost:5000;
                    }
                }
            
III. Restart NGINX
    1. sudo nginx -t
        - the result must be successfull
    2. systemctl reload nginx
        -reloading nginx
    3. systemctl status nginx
        -the status of nginx must be active(running);

IV. Finish