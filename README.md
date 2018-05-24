# puru.mit.edu

An map of ports to processes running on 5west's server, puru.

## Getting started

### Installation / deployment for puru.mit.edu
(This is mostly for 5west reproduction purposes, in case `/srv` and nginx magically disappear from puru.)

1. On Ubuntu:
```
$ sudo apt-get install nginx
```
2. Make two directories - the first for other websites you may add later, and one for the current website being deployed:
```
$ mkdir /srv/www /srv/www/puru.mit.edu
```
3. Create a `puru.mit.edu` file in `/etc/nginx/sites-available` and paste the following into it:
```
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  root /srv/www/puru.mit.edu;

  index index.html;

  server_name puru.mit.edu;

  location / {
    try_files $uri $uri/ =404;
  }
}
```
4. Tell nginx to enable this config by adding `puru.mit.edu` to `/etc/nginx/sites-enabled`:
```
$ ln -s /etc/nginx/sites-available/puru.mit.edu /etc/nginx/sites-enabled/puru.mit.edu
```
5. Clone this repo into `/srv/www/puru.mit.edu`:
```
$ cd /srv/www/puru.mit.edu && git clone https://github.com/fifthwest/puru-index.git
```
6. Then restart nginx,
```
$ sudo systemctl restart nginx
```
and you're all set.

## Acknowledgments
 - html & css from http://5west.mit.edu, with minor tweaks
