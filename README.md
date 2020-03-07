## SETUP
Add the bellow in host file
your_ip_address	nginxfundementals.com

## NGINX INSTALATION

### Not RECOMENDED
apt-get install nginx

ps aux | grep nginx

### RECOMENDED
wget http://nginx.org/download/nginx-1.17.9.tar.gz

untar
tar -cxvf <folder name>

inside folder name
./confirure

install build tools

apt-get install build-essential

apt-get install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev

again run configure
./configure

./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid

compile source

make

install compiled source

make install

### Adding nginx as a service

nginx -s stop nginx -h gives all available commands

Save this file as /lib/systemd/system/nginx.service

[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/usr/sbin/nginx -s reload
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target

### To enable startup boot

systemctl enable nginx

### to check the syntax
nginx -t

## troubleshoot 

[Nginx Pid missing](https://serverfault.com/questions/565339/nginx-fails-to-stop-and-nginx-pid-is-missing)