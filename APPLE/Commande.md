# Commande Apple

## Faire apparaitre les Fichiers cachés

Lancer terminal et taper ces deux lignes:

defaults write com.apple.finder AppleShowAllFiles TRUE

killall Finder


## Faire disparaitre les fichier cachés

defaults write com.apple.finder AppleShowAllFiles FALSE

killall Finder

## Edition config apache et virtualhosts

1- sudo nano /etc/apache2/httpd.conf

2- sudo nano /etc/apache2/extra/httpd-vhosts.conf 

		exemple :
		(<VirtualHost _default_:80>
		  ServerName localhost
		  DocumentRoot /Library/WebServer/Documents
		</VirtualHost>

		<VirtualHost *:80>
		  ServerName site1.local
		  DocumentRoot "/Users/votreuser/Sites/site1"
		</VirtualHost>)

3- sudo nano /etc/hosts ( on déclare le sous domaine : 127.0.0.1  exemple.local)

-----------

Dossier sites : Macbook SSD ▸ Bibliothèque ▸ WebServer

Safari : localhost

note: modifier access sur répertoire " lecture ecriture " everyone

------------

Activer php et module: 
	Décommenter ligne dans fichier config /etc/apache2/httpd.conf
	- LoadModule deflate_module libexec/apache2/mod_deflate.so
	- LoadModule expires_module libexec/apache2/mod_expires.so
	- LoadModule rewrite_module libexec/apache2/mod_rewrite.so
	- LoadModule php5_module libexec/apache2/libphp5.so

Modifier pour activer VirtualHosts:
	# Virtual hosts

	Include /private/etc/apache2/extra/httpd-vhosts.conf


Modifier dans : <Directory "/Library/WebServer/Documents">

	- "AllowOverride None" en "AllowOverride All"
	
-----------------

## Commande Apache

- sudo apachectl start
- sudo apachectl stop
- sudo apachectl restart
- httpd -v (version apache)


----------------
## Force mise à jour wordpress

wp-config.php (première ligne): define('FS_METHOD', 'direct');

-----------------
