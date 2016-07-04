Kustomisasi Dasar
=================

Setelah instalasi Drupal, maka ada beberapa hal yang perlu dikustomisasi agar website sesuai dengan yang diinginkan.

Install Theme
-------------

Yoopa menggunakan `theme Bootstrap`_. Cara installnya:

1. Buka *Command Prompt*, lalu masuk ke folder website Yoopa/Drupal Anda, contoh: ::

    C:
    cd \xampp\htdocs\lskk.org

2. Install module ``drupal/bootstrap`` menggunakan Composer: ::

    composer -vvv require drupal/bootstrap

3. Di website, klik Manage > Appearance. Akan muncul theme Bootstrap, klik *Install and set as default*.
4. Di Bootstrap > Settings, Anda dapat mengatur lebih jauh.
   Bootstrap sendiri mendukung Bootswatch yaitu "sub-theme" dari Bootstrap.
   Klik Advanced > Theme > pilih Bootswatch sub-theme pilihan Anda.

.. _theme Bootstrap: https://www.drupal.org/project/bootstrap
