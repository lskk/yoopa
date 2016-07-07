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

Pathauto
--------

Dibutuhkan agar URI untuk masing-masing *content* bersifat *SEO-friendly*.

1. Install module ``drupal/pathauto`` menggunakan Composer: ::

    composer -vvv require drupal/pathauto

2. Di web, klik Manage > Extend
3. Centang **Pathauto**, klik *Install*.
4. Manage > Configuration > Development > Performance > Clear all caches
5. Manage > Configuration > Search and metadata > Bulk generate > Content

Realname
--------

TODO: Menunggu kesiapan dari modul Realname_ untuk Drupal 8.
Terutama, `bug ini masih pending <https://www.drupal.org/node/2705279>`_.

.. _Realname: https://www.drupal.org/project/realname

REST API
--------

1. Install module `drupal/restui`_ menggunakan Composer: ::

        composer -vvv require drupal/restui

2. Manage > Extend. Enable modules:
  1. HAL
  2. HTTP Basic Authentication
  3. REST UI
  4. RESTful Web Services
  5. Serialization
3. Manage > People > Permissions. Set permissions:
  - GET: Anonymous, Authenticated
  - POST/PATCH/DELETE: Authenticated
4. Manage > Configuration > REST.
  Secara *default*, *resource* yang *enabled* adalah Content dengan format ``hal_json``.
  Pastikan hal ini benar.
5. Test menggunakan browser atau Postman: http://lskk.org.amanahwin/node/1?_format=hal_json

.. _drupal/restui: https://www.drupal.org/project/restui

Install Display Suite
---------------------

Display Suite digunakan untuk mengatur layout content secara GUI di website Drupal, tanpa membuat template.

1. Require module `drupal/ds <https://www.drupal.org/project/ds>`_ menggunakan Composer: ::

        composer -vvv require drupal/ds

2. Di web, klik Manage > Extend
3. Centang **Display Suite** dan **Display Suite Extras**, klik *Install*.

Drupal 8 Crash Course
---------------------

1. `Understanding Drupal 8 <https://cipix.nl/understanding-drupal-8-part-1-general-structure-framework>`_
2. `Los Angeles 2015: Drupal 8 The Crash Course <https://www.youtube.com/watch?v=8vwC_01KFLo&index=25&list=PLpeDXSh4nHjRwS2wCW-rOTsYNy1op3e0C>`_ 
3. `Drupal 8 The Crash Course presentation <https://www.palantir.net/presentations/mwphp15-d8-crash-course>`_
4. `Creating Drupal 8 modules <https://www.drupal.org/developing/modules/8>`_
5. `How to build a Drupal 8 module - SitePoint <https://www.sitepoint.com/series/how-to-build-a-drupal-8-module/>`_
