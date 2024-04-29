# Windows 10 End Of Lifetime? Consider switching to Linux Mint 21.3 and create your Lampp Stack with [Xampp for Linux](https://www.apachefriends.org/download.html)

First of all, before you work on your operating system make sure your machine fits the requirements for your target OS. Also make sure you can recover your system with the necessary bitlocker keys [from your Microsoft account](https://account.microsoft.com/account). Backup all your data before doing anything else.

## If you have done so, the fun can begin

1. Download your preferred Linux edition. [I recommend Linux Mint; it comes with a lot of features out of the box](https://www.linuxmint.com/download.php). There you will find the installation instructions as well.
2. You will need [Etcher](https://etcher.balena.io/) to create your Boot medium.
3. Next, you need to access the Boot menu. The method may vary depending on the machine. For me, it involved pressing Enter followed by F1.
4. Disable Secure Boot Mode and alter the Boot Priority Order to prioritize the USB drive containing your installation media.
5. When you boot now, the Linux Mint Live Session starts and you can follow [these steps](https://linuxmint-installation-guide.readthedocs.io/en/latest/install.html) for the installation.
6. If you need an Editor, SublimeText and VSCode can be installed with the Linux Software Manager.
7. For the installation of Xampp, I followed the steps on [wikiHow, How to install XAMPP on Linux](https://www.wikihow.com/Install-XAMPP-on-Linux), and it worked perfectly.
8. When finished, you will find an htdocs folder in `/opt/lampp/`. There you want to create your projects.
9. To start XAMPP, you have to find `~/.bash_aliases` in the console. It will output `/home/yourname/.bash_aliases`. There you can create your aliases to start and stop XAMPP or start the XAMPP GUI if you need. You can do it like this: `sudo nano ~/.bash_aliases`. To start the GUI, you can create an alias like `alias xampp-gui="sudo /opt/lampp/manager-linux-x64.run"`. The x64 is because my system is a 64-bit version. Make sure you install the right versions. For start and stop, it is pretty much the same, `/opt/lampp/lampp start` and `/opt/lampp/lampp stop`.
10. Check in the `~/.bashrc` that this line is present.



``` 
if [-f ~/.bash_aliases]; then
. ~/.bash_aliases
fi
```
11. In `/opt/lampp/etc/extra/`, you will find the `http-vhost.conf` where you can set up your Virtual Host mapping and SSL redirects. Here's an example:

```
<VirtualHost *:80>
    ServerName mysite.test
    DirectoryIndex index.php
    Redirect permanent / https://mysite.test
</VirtualHost>

<VirtualHost *:443>
    ServerName mysite.test
    ServerAlias mysite.test
    Protocols h2 h2c http/1.1

    DocumentRoot "/opt/lampp/htdocs/mysite/public"
    
    DirectoryIndex index.php 
    <Directory "/opt/lampp/htdocs/mysite/public">
         
    </Directory>
    SSLEngine on
    SSLCertificateFile "crt/mysite.test/server.crt"
    SSLCertificateKeyFile "crt/mysite.test/server.key"
</VirtualHost>
```
12. There is another ```/etc``` folder where the ```hosts``` file is. There you have to tell the server about your vhost URLs ```127.0.0.1 mysite.test```.
14. Don't forget to ```source ~/.bash_aliases``` and restart XAMPP to update your system.

Composer can be installed on command-line or with the Linux Software Manager.
If you need [Node.js](https://nodejs.org/en/download/package-manager).

### Happy Coding 
