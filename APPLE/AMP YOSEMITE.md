# UN SERVEUR SOUS MAC OS YOSEMITE

Principe:  Transformer mac en serveur WEB


## COMMANDE TERMINAL DE BASE

### Commande listing fichiers et repertoires

* ` ls `    : Liste des fichiers et dossiers
* ` ls-a `  : Idem ` ls ` avec fichiers cachés
* ` ls-l `  : Idem  ` ls ` avec plus de détails ( permissions, propriétaire, etc...)


### Commande sur fichiers et repertoires

* ` cd `    : Changer de répertoire ex: ` cd /Users/ ``
* ` cp `    : Copier un fichier ex: ` cp /Users/Stephen/Documents/index.html Users/Stephen/Document/Sites/index.html `
* ` mv `    : Dépacler un fichier d'un repertoire vers un autre

* ` touch ` : Créer un fichier ex: ` touch index.html ` 
* ` echo `  : Un print vers écran terminal, si ` > ` , on écrit vers un fichier. ex: ` echo "Bonjour à tous" > index.html `

* ` rm `    : Supprimer un fichier
* ` rmdir ` : Supprimer un repertoire
* ` mkdir ` : Créer un repertoire

### Commande supplémentaire

* ` man `   : Indique la correspondance d'une commande ex: ` man ls `
* ` pwd `   : Affiche le chemin absolue où vous vous trouvez
* ` top `   : Processus en cours
* ` df -h ` : Affiche la liste des volumes montés
* ` chown ` : Changer le propriétaire du fichiers



### Gérer le finder :

Afficher les fichiers cachés dans le finder:

    defaults write com.apple.finder AppleShowAllFiles TRUE
 
    killall Finder


Ne pas afficher les fichiers cachés dans le finder:

    defaults write com.apple.finder AppleShowAllFiles FALSE

    killall Finder
    
--------------------

## GERER APACHE SUR MACOS

* ` sudo apachectl start ` : Lancer Apache
* ` sudo apachectl stop ` : Stopper Apache
￼* ` sudo apachectl restart ` : Relancer Apache
￼* ` httpd -v ` : Afficher la version d'Apache
￼* ` apachectl -t ` : Vérification du fonctionnement d'Apache

---------------------

## CONFIGURATION APACHE:

### Modification du comportement du serveur apache:

Fichier de configuration du serveur apache *httpd.conf*

    sudo nano /etc/apache2/httpd.conf

Ce qu'il faut modifier ( décommenter ) dans ce fichier pour changer le repertoire par défaut d'apache:

    LoadModule authz_core_module libexec/apache2/mod_authz_core.so
    LoadModule authz_host_module libexec/apache2/mod_authz_host.so
    LoadModule userdir_module libexec/apache2/mod_userdir.so
    

    // On active le mod deflate
    LoadModule deflate_module libexec/apache2/mod_deflate.so
    // On active le mod expire
	LoadModule expires_module libexec/apache2/mod_expires.so
    // On active le mod rewrite
	LoadModule rewrite_module libexec/apache2/mod_rewrite.so
    
    
On modifie le comportement du répertoire par défaut de mac os pour apache `/Library/WebServer/Documents` :
On créer un dossier "Sites" dans Users et celui ci devient le repertoire par défaut

    DocumentRoot "/Users/Sites"
    <Directory "/Users/Sites">
    
    Options FollowSymLinks Multiviews
    
    // Ligne à commenter 
    # MultiviewsMatch Any

    // Ligne à modifier : passer None en all
    AllowOverride All

    Require all granted
    </Directory>

On active PHP:

	LoadModule php5_module libexec/apache2/libphp5.so 
    
    Include /private/etc/apache2/other/*.conf

On active les virtuals hosts

    # Virtual hosts
    Include /private/etc/apache2/extra/httpd-vhosts.conf
    

### Gestion des virtualhosts:

Fichier de configuration du serveur apache *httpd-vhosts.conf*

    sudo nano /etc/apache2/extra/httpd-vhosts.conf

On ajoute des sous-domaines que l'on lie à un dossier :
 
    <VirtualHost _default_:80>
    ServerName localhost
    DocumentRoot "/Users/Sites"
    </VirtualHost>

    <VirtualHost *:80>
    ServerName site.local
    DocumentRoot "/Users/Sites/www"
    </VirtualHost>
    
    
### Gestion des déclarations des sous domaines:

Fichier de configuration du serveur apache *hosts*

    sudo nano /etc/hosts

On ajoute les déclarations des sous domaines à la fin du fichier:

    127.0.0.1  site.local

----------------

## INSTALLATION MYSQL:

Télécharger MySQL  http://dev.mysql.com/downloads/mysql/

Installer MYSQL en désactivant "MYSQL startup item"

### Commande MYSQL:

Lancer MYSQL:
    
    sudo /usr/local/mysql/support-files/mysql.server start

Afficher version MYSQL:

    /usr/local/mysql/bin/mysql -v
    
    
### Configurer MYSQL:

Modifier mot de passe MYSQL:
￼
￼   /usr/local/mysql/bin/mysqladmin -u root password 'imac'

Correction bug MYSQL:

￼   sudo mkdir /var/mysql

￼   sudo ln -s /tmp/mysql.sock /var/mysql/mysql.sock


----------------

## INSTALLATION PHP ADMIN:

Télécharger phpadmin http://www.phpmyadmin.net/home_page/downloads.php

Décompresser dans le repertoire racine du serveur web

### Configuration Php Admin:

    mkdir /Users/Sites/phpmyadmin/config
    
    chmod o+w /Users/Sites/phpmyadmin/config
    
Lancer la configuration de phpmyadmin via http://localhost/phpmyadmin

Pour mettre à jour la config il suffira de télécharger la nouvelle version et écraser tout le repertoire /phpmyadmin en conservant uniquement le fichier de configuration *config.inc.php*.


----------------

## Configuration permission du répertoire du serveur web ou seront placer les sites

Créer un repertoires www dans /Users/Sites:
    
    sudo mkdir /Users/Sites/www

    sudo chmod -R a+w /Users/Sites/www
    
    sudo chown -R _www /Users/Sites/www

----------------
## Force mise à jour wordpress

wp-config.php (première ligne): define('FS_METHOD', 'direct');

-----------------
