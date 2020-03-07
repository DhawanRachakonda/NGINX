## SETUP
Add the bellow in host file<br/>
<code><your_ip_address>	nginxfundementals.com</code>

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

## INSTALL DYNAMIC MODULES

Go to source code<br/>
Execute nginx -V<br/>
Copy all configure arguments<br/>
Get all modules related to dynamic<br/>
<code>./configure --help | grep dynamic<code/>

### Execute configure

<code>./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_image_filter_module=dynamic --with-http_xslt_module=dynamic --modules-path=/etc/nginx/modules</code><br/>
If error occurs, try installing<br/>
<code>sudo apt-get install libxslt-dev</code>
You might also need<br/>
<code>
sudo apt-get install libgd-dev # for the "error: the HTTP image filter module requires the GD library." error<br/>
sudo apt-get install libgeoip-dev # for the GeoIP package
</code><br/>
Run make
<code>make</code>
Install make
<code>sudo make install</code>

## Troubleshoot 

[Nginx Pid missing](https://serverfault.com/questions/565339/nginx-fails-to-stop-and-nginx-pid-is-missing)

## Useful Things

### Create Symbolic link

sudo ln -s /home/dhawan/projects/nginx/udemy/nginx.conf /etc/nginx/nginx.conf

### Know configure arguments

nginx -V

### Reload

sudo service nginx reload

### System details

nproc<br/>
lscpu<br/>
ulimit - To know number of open connections<br/>

## Cheatsheet

### Match Priority
<ul>
    <li>Exact Match</li>
    <li>Preferential prefex</li>
    <li>Regex match takes high priority</li>
    <li>Prefix Match</li>
</ul>

### Configuring FIle Measuring Units

[Nginx Doc Link](http://nginx.org/en/docs/syntax.html)<br/>

### Worker Process
<code>worker_processes auto</code><br/>
<code>worker_connections 1024</code><br/>

## Examples on Rewrites
[/user/jim](http://nginxfundementals.com/user/jim)<br/>
[/user/john](http://nginxfundementals.com/user/john)<br/>
[/greet](http://nginxfundementals.com/greet)<br/>
[/greet/john](http://nginxfundementals.com/greet/john)<br/>
[/greet/jim](http://nginxfundementals.com/greet/jim)<br/>
[/greet/jo](http://nginxfundementals.com/greet/jo)<br/>

## Examples on try files and named locations
http://nginxfundementals.com/thumb.png<br/>
http://nginxfundementals.com/greet<br/>
http://nginxfundementals.com/grsdsd<br/>

## logging
<p>There are two directives, they are access log and error log and can even be set to off.
