Instalasi
=========

Untuk menginstall Drupal dengan modul-modul Yoopa, dapat dilakukan untuk membuat situs baru, maupun untuk mengembangkan situs yang sudah ada.

Prasyarat
---------

Baik untuk situs baru maupun situs yang sudah ada, membutuhkan XAMPP_ dan Composer_.

1. Install XAMPP_.
2. Recommended: Nyalakan OPCache, caranya sebagai berikut. Edit ``php.ini`` lalu pastikan: ::

    zend_extension=php_opcache.dll
    [opcache]
    opcache.enable=1

3. Unduh dan jalankan `Composer Installer`_.
   (Di lingkungan jaringan ITB, Anda akan memerlukan setting proxy saat menjalankan *Composer Installer*).

.. _XAMPP: www.apachefriends.org/en/xampp-windows.html
.. _Composer: https://www.drupal.org/node/2404989
.. _Composer Installer: https://getcomposer.org/download/

Membuat Situs Baru
------------------

Untuk membuat situs baru, langkahnya sama dengan `installing Drupal`_.

TODO: Gunakan https://github.com/drupal-composer/drupal-project, sepertinya ini lebih baik karena: Composer by default, Drupal Core dapat diupdate via Composer, support drush, support DrupalConsole.

1. Unduh `Drupal 8.x`_ *recommended release* terbaru
2. Extract ke folder sementara, misalnya ``D:\tmp``.
   Folder tersebut akan berisi subfolder ``drupal-8.x``.
   Buat folder tujuan sesuai nama web, misalnya ``C:\xampp\htdocs\lskk.org``, lalu pindahkan semua isi folder ``drupal-8.x`` tadi ke folder tersebut.
3. Rename file ``example.gitignore`` menjadi ``.gitignore.`` (tambahkan "." di akhir, yang nanti akan hilang dengan sendirinya, jadi nama file finalnya adalah ``.gitignore``).
4. Buka *Command Prompt*, lalu masuk ke folder website Yoopa/Drupal Anda, contoh: ::

    C:
    cd \xampp\htdocs\lskk.org

5. Set `konfigurasi Composer untuk Drupal`_, caranya: ::

    composer config repositories.drupal composer https://packages.drupal.org/8

6. Tentukan bagaimana ingin mengakses website tersebut di local, misalnya ``lskk.org.amanahwin``.
   Maka jalankan Notepad/Notepad++ sebagai admin, buka file ``C:\Windows\System32\drivers\etc\hosts``, lalu tambahkan di bagian bawah: ::

    127.0.0.1	lskk.org.amanahwin

7. Edit file ``C:\xampp\apache\conf\extra\httpd-vhosts.conf`` lalu tambahkan: ::  

    NameVirtualHost *:80
    <VirtualHost *:80>
        ServerName lskk.org.amanahwin
        DocumentRoot "C:/xampp/htdocs/lskk.org"
        SetEnv APPLICATION_ENV "development"
        <Directory "C:/xampp/htdocs/lskk.org">
            DirectoryIndex index.php
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>

8. Jalankan *XAMPP Control Panel* dan re-Start *Apache*.
    Start *MySQL*.
9. Cek website Drupal dapat diakses di http://lskk.org.amanahwin/
    Harusnya menampilkan halaman instalasi.
    Language: pilih English
    Profile: pilih Standard
    Database name: ``lskkorg``
    Database user: ``root``
    Database password: (kosong/sesuai konfigurasi XAMPP)

Mengembangkan Situs yang Sudah Ada
----------------------------------

Bila *source code* situs sudah ada, contoh *source code* website http://www.lskk.org ada di https://github.com/lskk/lskk.org, Anda dapat meng-clone di local PC lalu melanjutkan pengembangannya.

1. Gunakan TortoiseGit_ untuk meng-*clone* repository website Yoopa yang diinginkan.
    Misal, buka https://github.com/lskk/lskk.org, dari situ Anda akan mendapatkan Clone URL-nya yaitu https://github.com/lskk/lskk.org.git
2. Clone ke folder di dalam ``C:\xampp\htdocs``, misalnya ``C:\xampp\htdocs\lskk.org``, lalu pindahkan semua isi folder ``drupal-8.x`` tadi ke folder tersebut.
4. Buka *Command Prompt*, lalu masuk ke folder website Yoopa/Drupal Anda, contoh: ::

    C:
    cd \xampp\htdocs\lskk.org

5. Kembalikan *dependencies* dari `konfigurasi Composer untuk Drupal`_, caranya: ::

    composer -vvv install

6. Tentukan bagaimana ingin mengakses website tersebut di local, misalnya ``lskk.org.amanahwin``.
   Maka jalankan Notepad/Notepad++ sebagai admin, buka file ``C:\Windows\System32\drivers\etc\hosts``, lalu tambahkan di bagian bawah: ::

    127.0.0.1	lskk.org.amanahwin

7. Edit file ``C:\xampp\apache\conf\extra\httpd-vhosts.conf`` lalu tambahkan: ::  

    NameVirtualHost *:80
    <VirtualHost *:80>
        ServerName lskk.org.amanahwin
        DocumentRoot "C:/xampp/htdocs/lskk.org"
        SetEnv APPLICATION_ENV "development"
        <Directory "C:/xampp/htdocs/lskk.org">
            DirectoryIndex index.php
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
    </VirtualHost>

8. Jalankan *XAMPP Control Panel* dan re-Start *Apache*.
    Start *MySQL*.
9. Cek website Drupal dapat diakses di http://lskk.org.amanahwin/
    Harusnya menampilkan halaman instalasi.
    Language: pilih English
    Profile: pilih Standard
    Database name: ``lskkorg``
    Database user: ``root``
    Database password: (kosong/sesuai konfigurasi XAMPP)
 
Mengembangkan Menggunakan Cloud IDE
-----------------------------------

TODO

.. _konfigurasi Composer untuk Drupal: https://www.drupal.org/node/2404989
.. _installing Drupal: https://www.drupal.org/documentation/install/download
.. _Drupal 8.x: https://www.drupal.org/project/drupal
.. _TortoiseGit: https://tortoisegit.org
