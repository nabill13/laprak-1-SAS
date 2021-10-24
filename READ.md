
# SISTEM ADMINISTRASI SERVER

kelompok 2

beranggotakan : 

- Nabila Nur Amalia_1202190013

- Evyra Rizki Safitri_1202190015
- M Pradata Yuda P_1202190061

Pastikan adapter bridge dan setting ip statis

![0.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/0.PNG?raw=true) 



Cek lxc yang sudah ada dari praktikum sebelumnya

```
lxc-ls -f
```
 ![2.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/2.PNG?raw=true) 



1) Ubah Ubuntu 5.6 menjadi Ubuntu Landing
```
lxc-copy _R -n ubuntu_php5.6 -N ubuntu_landing
lxc-ls -f
```
 ![3.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/3.PNG?raw=true) 



Start lxc php landing dan php 7

```
lxc-start -n ubuntu_landing
lxc-start -n ubuntu_php7.4
lxc-ls -f
```
![4.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/4.PNG?raw=true) 



kemudian masuk ke ubuntu landing

```
lxc-attach -n ubuntu_landing
```
  ![5.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/5.PNG?raw=true)  

 

ubah ip ubuntu landing

 ![7.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/7.PNG?raw=true)



restart ip, lalu cek ip menngunakan `if config`

```
shutdown now
lxc-start -n ubuntu_landing
ifconfig
```
 ![8.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/8.PNG?raw=true) 



 kemudian keluar dari ubuntu landing dengan 

```
exit
```

2) Cek koneksi Internet dengan Ping Google.com/8.8.8.8/1.1.1.1
```
ping google.com
```
 ![9.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/9.PNG?raw=true)



Update repositori Debian di ```nano /etc/apt/source.list```

```
nano /etc/apt/source.list
```
 ![10.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/10.PNG?raw=true)



Install lxc Debian

```
lxc-create -n debian_php5.6 -t download -- --dist debian --release strercarch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
![11.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/11.PNG?raw=true) 



Cek lxc Debian

```
lxc-ls -f
```
 ![12.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/12.PNG?raw=true) 



3) 
Start lxc debian
```
lxc-start -n debian_php5.6
```
 ![13.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/13.PNG?raw=true) 



install nginx dan nginx-extras

```
apt install nginx nginx-extras
```
![14.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/14.PNG?raw=true) 


Install nano dan net-tools dan juga curl

```
apt install nano net-tools curl
```
 ![15.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/15.PNG?raw=true) 



Setting ip static debian php
![16.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/16.PNG?raw=true) 



Restart pengaturan dan cek ip

``` 
systemctl restart networking.service
```

setting nginx

```
cd /etc.nginx/sites-available
ls default
touch lxc_php5.6.dev
ls default touch lxc_php5.6.dev
nano lxc_php5.6.dev
```
![18.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/18.PNG?raw=true) 

![19.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/19.PNG?raw=true) 



```
cd ../sites-enabled
ls default
ln -s /etc/nginx/sites-available/lxc_php5.6.dev
nginx -t
nginx -s reload
```
![20.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/20.PNG?raw=true) 

![22.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/22.PNG?raw=true) 



```
cd /var/www/html
ls
mkdir lxc_php5.6
ls
cp index.nginx-debian.html lxc_php5.6/index.html
nano lxc_php5.6/index.html
```
![22.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/22.PNG?raw=true) 

![23.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/23.PNG?raw=true) 



Test dengan curl

![24.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/24.PNG?raw=true) 

```
/var/www/html# curl -i http://lxc_php5.6.dev

Exit dari Debian php
```
4) Masuk Ubuntu Landing dan setting nginx

![26.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/26.PNG?raw=true) 



```
lxc-ls -f
lxc-attach -n ubuntu_landing
cd /etc/nginx/sites-available
```
Renama direktore lxc agar tidak bingung

ls
mv lxc_php5.6.dev lxc_landing.dev
ls
nano lxc_landing.dev

![27.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/27.PNG?raw=true) 

```

edit lxc

```
![28.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/28.PNG?raw=true) 



```
cd ../sites-enabled
ls 
rm -r lxc_php5.6.dev
ls 
ln -s /etc/nginx/sites-available/lxc_landing.dev
ls
```


```
nginx -t
nginx -s reload
nano /etc/hosts
```
cd /var/www/html
ls
mv lxc_php5.6 lxc_landing 
ls
nano lxc_landing/index.html

![29.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/29.PNG?raw=true) 

![30.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/30.PNG?raw=true) 

![31.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/31.PNG?raw=true) 



Test dengan Curl

```
curl -i http://lxc_landing.devTest dengan Curl
```


![32.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/32.PNG?raw=true) 

```
Exit dari Ubuntu Landing
```
5) Stop Ubuntu Landing dan cek 

lxc-stop -n ubuntu_landing
lxc-ls -f

![33.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/33.PNG?raw=true) 



Masuk ke direktori /var/lib/lxc dan cek ada direktori apa saja 

```
cd /var/lib/lxc
ls
cd ubuntu_landing
ls
nano config 
```


![34.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/34.PNG?raw=true) 

```
Karena akan menggunakan auto start pada ubuntu landing, tambahkan config seperti gambar di bawah ini 
```
![35.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/35.PNG?raw=true) 

Cek auto start dengan cara di reboot terlebih dahulu

sudo su
lxc-ls -f

![36.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/36.PNG?raw=true) 

Run lxc lain

```
lxc-ls -f
```


![41.1.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/41.1.PNG?raw=true) 

(6) Setup nginx pada vm local

```
nano /etc/hosts
```
![37.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/37.PNG?raw=true) 

```
cd /etc/nginx/sites-available 
ls
nano vm.local
```
![38.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/38.PNG?raw=true) 

![39.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/39.PNG?raw=true) 

```
Setting Hosts pada windows
```
![40.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/40.PNG?raw=true)Test http://vm.local/

curl -i http:vm.local/

![41.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/41.PNG?raw=true) 

![vm local.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/vm%20local.PNG?raw=true) 

```
Test http://vm.local/blog
curl -i http:vm.local/blog
```
![42.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/42.PNG?raw=true) 

![vm local blog.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/vm%20local%20blog.PNG?raw=true) 

```
Test http://vm.local/app
curl -i http:vm.local/app
```
![43.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/43.PNG?raw=true) 

![vm local app.PNG](https://github.com/nabill13/laprak-1-SAS/blob/main/vm%20local%20app.PNG?raw=true) 

```
- Mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?

Karena ubuntu 16.04 hanya tersedia untuk opsi yang berbayar dan hanya dapat diakses ubuntu estended security maintenance yang berarti ubuntu 16.04 akan dihapus karena adanya pembaruan fitur yang bernama Trusty EOL yang tidak support kepada ubuntu 16.04

 - Kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?

Karena LXC menggunakan file system yang netral, container dapat di fungsikan secara penuh oleh OS, data dapat disimpan di dalam maupun diluar container.

- Apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?

Proxy server bisa disebut computer sentral atau computer server yang bisa bertindak sebagai computer lainnya untuk yang dapat melakukan request content pada internet maupun intranet sama seperti vm.local. jadi vm.local bisa dikatakan juga sebagai proxy server

