# Vytality Local Environment on Windows 10
---
- Git clone projects "vytality-backend" and "vytality-web-customer" from Gitlab
- Create the directory in your root drive: **C:/wamp64** then download and install [Wamp](https://sourceforge.net/projects/wampserver/) into it

- Download [**PHP 7.2.18-Win32-VC15-x64.zip**](https://windows.php.net/downloads/releases/archives/)

- Follow these instructions to [**add PHP 7.2.18 to Wamp**](https://www.youtube.com/watch?v=y52G3BL75i8)
**NOTE**: Around the 11 minute mark, he edits the **wampserver.conf** file.
Since we are using version 7 of php, make sure where he edits looks like this:
```
...
$phpConf['apache']['2.4']['LoadModuleName'] = '**php7_module**';s
$phpConf['apache']['2.4']['LoadModuleFile'] = '**php7apache2_4.dll**';
```
---
- In **C:\wamp64\bin\apache\apache2.4.51\conf\extra**
edit "**httpd-vhosts.conf**".
Replace the text with the following and add your paths to **DocumentRoot** and **Directory** properties:
```
<VirtualHost *:80>
    ServerName vytality-api
    ServerAlias vytality-api
    DocumentRoot "<<your path to this directory>>/vytality-backend/public"
    <Directory  "<<your path to this directory>>/vytality-backend/public">
        Options +Indexes +Includes +FollowSymLinks +MultiViews
        AllowOverride All
        Require local
    </Directory>
</VirtualHost>
#
<VirtualHost *:80>
    ServerName vytality-customer
    ServerAlias vytality-customer
    DocumentRoot "<<your path to this directory>>/vytality-web-customer"
    <Directory  "<<your path to this directory>>/vytality-web-customer/">
        Options +Indexes +Includes +FollowSymLinks +MultiViews
        AllowOverride All
        Require local
    </Directory>
</VirtualHost>
```
---
- In **C:\Windows\System32\drivers\etc** open the **host** file and copy the original text and save it somewhere safe (other programs may
 need it). Replace the text with:
```
#
127.0.0.1 localhost
::1 localhost

127.0.0.1 vytality-api
::1 vytality-api

127.0.0.1 vytality-customer
::1 vytality-customer
```
---
- In **1Password**, search for "**vytality-customer-config-php**"
download the file. Place the file in the same directory as your project parent folders.
>vytality-backend
>
> vytality-web-customer
>
> **customer-config.php**
---

- In the directory **C:\wamp64**, create the folder "CA-Cert"
get the file  **cacert-2018-06-20.pem** from the Team Lead
and place it in CA-Cert.

- Edit the php.ini file (**C:\wamp64\bin\php\php7.2.18\php.ini**)
Search for "**curl.cainfo**"
uncomment it at add the value as:
**curl.cainfo = "C:/wamp64/CA-Cert/cacert-2018-06-20.pem"**
---
- In 1password search for "vytality staging env"
copy the contents to vytality-backend/env.example
rename env.example to .env
---
- Install [Composer](https://getcomposer.org/doc/00-intro.md#installation-windows**)
- In CMD type: **composer self-update --1**
- **NOTE**: if you have a root PHP folder (C:/PHP). Make sure the php.ini file is the
same as **C:\wamp64\bin\php\php7.2.18\php.ini**
- Navigate to your project directorys (vytality-backend, vytality-web-customer) in cmd and run the command
**composer install** for each project.
---
- Click on the **Wamp** icon -> Stop All Services -> Right click on Wamp Icon -> Exit
- Open Wamp again. Click on the Wamp Icon -> Your Virtual Hosts -> Click on **vytality-customer** 
    it should take you to Vytality's homepage.



