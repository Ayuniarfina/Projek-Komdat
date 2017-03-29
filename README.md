# Aplikasi Web "Bludit"

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Maintenance](#maintenance) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:

## Sekilas Tentang 

Bludit merupakan aplikasi web sederhana untuk membuat blog pribadi atau site mu dalam waktu singkat, bebas biaya dan open source. Bludit menggunakan flat-files untuk menyimpan kiriman dan halaman, tanpa perlu menginstall atau konfigurasi basisdata. Bludit mendukung kode Markdown dan HTML untuk konten kiriman dan halaman.


## Instalasi
#### Kebutuhan
- web server with PHP support (PHP Built-in web server, Apache with module mod_rewrite, Lightpd with module mod_rewrite, Nginx with module, ngx_http_rewrite_module, Other, Installation guide)
- PHP v5.3 or higher
- PHP mbstring module for full UTF-8 support
- PHP gd module for image processing
- PHP dom module for DOM manipulation
- PHP json module for JSON manipulation

#### Cara instalasi
1. Masuk ke akun VPS melalui SSH dengan sudo user yang dimiliki 
```
ssh adam@172.18.88.81
```

2. Update sistem dan kebutuhan packages
```
[adam]$ sudo apt-get update && sudo apt-get -y upgrade
[adam]$ sudo apt-get install nano wget unzip
```

3. Instal PHP dan modul PHP yang dibutuhkan
untuk menginstal versi tetap terakhir dari PHP versi 7.0 dan semua modul yang dibutuhkan, jalankan:
```
[user]$ sudo apt-get -y install php-fpm php-cli php-json php-curl php-gd php-mysql php-mbstring php-xml
```

4. Atur batasan memory hingga 512MB, atur fix_pathinfo menjadi 0, ubah nilai upload_max_filesize dan post_max_size menjadi 100M dan atur zona waktunya ke UTC
```
sed -i "s/memory_limit = .*/memory_limit = 512M/" /etc/php/7.0/cli/php.ini
sed -i "s/;date.timezone.*/date.timezone = UTC/" /etc/php/7.0/cli/php.ini
sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.0/fpm/php.ini
sed -i "s/upload_max_filesize = .*/upload_max_filesize = 100M/" /etc/php/7.0/fpm/php.ini
sed -i "s/post_max_size = .*/post_max_size = 100M/" /etc/php/7.0/fpm/php.ini
```

5. Buat PHP-FPM pool for user
```
[adam]$ sudo nano /etc/php/7.0/fpm/pool.d/adam.conf
user = adam
listen = /var/run/php/php7.0-adam-fpm.sock
listen.owner = adam
listen.mode = 0666
pm = ondemand
pm.max_children = 5
pm.process_idle_timeout = 10s
pm.max_requests = 200
chdir = /
```

6. Restart PHP-FPM
```
[adam]$ sudo service php7.0-fpm restart
```

7. Download Bludit
```
[user]$ wget https://s3.amazonaws.com/bludit-s3/bludit-builds/bludit_latest.zip
[user]$ unzip bludit_latest.zip
[user]$ mv bludit ~/myBludit.com
[user]$ rm -f bludit_latest.zip
```

## Konfigurasi

1.	Cd /var/www/html 
2.	Wget https://s3.amazonaws.com/bludit-s3/bludit-builds/bludit_latest.zip
3.	Unzip bludit_latest.zip // unzip
4.	Rm –rf bludit_latest.zip //remove zip
5.	sudo apt-get install php7.0-gd php7.0-mbstring php7.0-dom php7.0-json
6.	buka alamat 172.18.88.81/bludit

## Otomatisasi

## Cara Pemakaian
1. Tampilan aplikasi web
	1. Pilih bahasa
	![Imgur](http://i.imgur.com/XD8yxZI.jpg)
	2. Login 
	![Imgur](http://i.imgur.com/Yj7y3tb.jpg)
    3. Halaman utama
    ![Imgur](http://i.imgur.com/TQzUIiz.png)
	4. *Dashboard admin*
	![Imgur](http://i.imgur.com/gAQH5L2.png)
	
2. Buat Pos
	Untuk membuat *post*, di halaman *dashboard admin*, klik *New post* yang terletak di sebelah kiri halaman
	
	![Imgur](http://i.imgur.com/QiOFO3b.png)
	
3. *Manage posts*
	Untuk *manage posts* dari halaman *dashboard admin*, klik *manage posts* yang terletak di sebela kiri
	
    ![Imgur](http://i.imgur.com/b3kV0bp.png)
	
4. Mengatur Bludit
    Untuk mengatur bludit, klik *setting* pada bagian kiri halaman, disini kita dapat mengatur UI, bahasa, dan sebagainya
	
    ![Imgur](http://i.imgur.com/aKVMSas.png)


## Pembahasan

Aplikasi web Bludit merupakan CMS yang bisa dikatakan baru, namun memiliki beberapa fitur yang diunggulkan, di antaranya:
1. Dibangun menggunakan *framework* PHP Symfony dan Vue.js
2. Tampilan sederhana sehingga mudah digunakan
3. Tidak membutuhkan instalasi ataupun konfigurasi sebuah *database*.
4. Web gratis dan *open source*
5. Menggunakan *flat-files* untuk menyimpan *posts* dan *pages*

Namun juga terdapat beberapa kekurangan dari Bludit, yaitu :
1. UI kurang menarik
2. 

## Referensi
1. [Introduction | Bludit](https://docs.bludit.com/en/getting-started/introduction) - Bludit
2. [Requirements | Bludit](https://docs.bludit.com/en/getting-started/requirements) - Bludit
3. [Install Bludit on Ubuntu 16.04](https://www.rosehosting.com/blog/install-bludit-on-ubuntu-16-04/)
3. [Installation on Ubuntu 14.04 LTS | Bludit](https://docs.bludit.com/en/getting-started/installation-on-gnu-linux) - Bludit
