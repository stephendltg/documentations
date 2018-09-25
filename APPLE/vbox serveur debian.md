# MONTER SON SERVEUR WEB ( sous virtualbox )

Principe:  Monter un serveur web sous debian dans une machine virtuelle afin de remplacer l'utilisation du logiciel MAMP et reproduire un véritable serveur Web. Ce tutoriel peut servir aussi pour monter un serveur web sur une machine local en passant bien entendu tout ce qui concerne les chapitres sous virtualbox.


## COMMANDES TERMINAL DE BASE UNIX

### Commandes listing fichiers et repertoires

* ` ls `    : Liste des fichiers et dossiers
* ` ls-a `  : Idem ` ls ` avec fichiers cachés
* ` ls-l `  : Idem  ` ls ` avec plus de détails ( permissions, propriétaire, etc...)


### Commandes sur fichiers et repertoires

* ` cd `    : Changer de répertoire ex: ` cd /Users/ ``
* ` cp `    : Copier un fichier ex: ` cp /Users/Stephen/Documents/index.html Users/Stephen/Document/Sites/index.html `
* ` mv `    : Dépacler un fichier d'un repertoire vers un autre

* ` touch ` : Créer un fichier ex: ` touch index.html ` 
* ` echo `  : Un print vers écran terminal, si ` > ` , on écrit vers un fichier. ex: ` echo "Bonjour à tous" > index.html `

* ` rm `    : Supprimer un fichier
* ` rmdir ` : Supprimer un repertoire
* ` mkdir ` : Créer un repertoire

### Commandes supplémentaires

* `df -h`   : Espace disque
* ` man `   : Indique la correspondance d'une commande ex: ` man ls `
* ` pwd `   : Affiche le chemin absolue où vous vous trouvez
* ` top `   : Processus en cours
* ` df -h ` : Affiche la liste des volumes montés
* ` chown ` : Changer le propriétaire du fichiers ( utiliser `-R` pour la recursivité )
* `ln -s <nom du fichier ou répertoire de destination > <nom du lien symbolique>`  : Créer un liens symbolique vers un répertoire ou un fichier.

### Commandes Apache2

Les fichier de configuration d'apache /etc/apache2/apache2.conf .
Les fichiers log se trouve dans le dossier /var/log/apache2/ .
Le dossier par défaut des sites /var/www/html/

* `service apache2 status` : Etat du service apache.
* `service apache2 restart`: Redémarrer apache.
* `service apache2 stop`   : Stopper apache.
* `service apache2 start`  : Démarrer apache.

### Commandes MYSQL

Les fichiers de configuration de mysql se trouve dans le dossier /etc/mysql/ .
Le fichier log se trouve dans /var/log/mysql/error.log .

* `service mysql status` : Etat du service mysql.
* `service mysql stop`   : Stopper mysql.
* `service mysql start`  : Démarrer mysql.

### Commandes PHP5

Le fichier ini se trouve dans /etc/php5/apache2/php.ini

* `php -v`               : Version de php installé.

### APT-GET ( Gestion des applications )
 
apt-get permet d'effectuer l'installation et la désinstallation de paquets en provenance d'un dépôt APT. Le log des actions de apt-get se trouve dans /var/log/apt ( à la fin de chaque mois ce fichier est archivé, utilisez 'zless' pour ouvrir un tel fichier).
 
* `apt-get update`                        : Mise à jour des dépôts.

* `apt-get install <paquet(s)>`     : Installations d'un ou plusieurs paquets. 
* `apt-get -f install <paquet(s)>`  : Réparation d'un paquets.
* `apt-cache search <paquet(s)>`      : Chercher un paquet dans les dépôts.
* `dpkg -l <paquet(s)>`             : Chercher un paquet installé.


* `apt-get remove <paquet(s)>`      : Supprimer un ou plusieur paquets (conserve les fichiers de configurations).
* `apt-get autoremove <paquet(s)>`  : Supprimer un ou plusieurs paquets avec ses dépendances (conserve les fichiers de configurations).
* `apt-get purge <paquet(s)>`       : Supprimer un ou plusieurs paquets avec les fichiers de configuration.
* `apt-get autoremove --purge <paquet(s)>` : Supprimer un ou plusieurs paquets avec ses dépendances et ses fichiers de configurations.


* `apt-get install <paquet(s)> -V`   : Mise à jour d'un ou plusieurs paquets déjà installés.
* `apt-get upgrade`                  : Mise à jour de tous les paquets installés sur le système avec leurs dernière versions.
* `apt-get dist-upgrade`             : Idem upgrade mais installe de nouveaux paquets si nécessaire.
* `apt-get clean`                    : Supprimer la totalité des paquets présents dans /var/cache/apt/archives pour récuperer de l'espace disque.


------


## INSTALATION DU SERVEUR WEB


### Pré-requis:

* Avoir une connexion internet.
* Télécharger et installer VirtualBox ( https://www.virtualbox.org ). VirtualBox est un logiciel de création et de gestion de machine virtuelle.
* Télécharger iso de debian ( https://www.debian.org/ ). Debian est un système d'exploitation.

### Création d'un machine virtuelle ( vbox )

Lancer VirtualBox et cliquer sur "Nouvelle".

Dans la boîte de dialogue, indiquer le Nom de la machine virtuelle puis le type "Linux" et ensuite choisir la version "debian".
Puis sélectionner la taille de la mémoire a allouer, 512 MO.
Créer un disque virtuel.
Format du disque virtuel : VDI.
Sélectionner "Dynamiquement alloué".
Nommer le disque dur virtuel et definir la taille du disque à 8GO.


Cliquer sur "Configuration" puis "Stockage" et dans controleur IDE, affecter l'image iso télécharger de la version debian téléchargée.

Puis démarrer la machine virtuelle.


### Installation de debian

![Menu de démarrage, choisir "install".](IMG/Debian - Boot.png)

#### Configuration langue du serveur:
![La langue du serveur.](IMG/Debian - Lang.png)
![Situation géographique pour le serveur.](IMG/Debian - Geo.png)
![La langue du clavier.](IMG/Debian - Keyboard.png)

#### Configuration du réseau:
![Nom du serveur.](IMG/Debian - NetworkConfig.png)
![Nom de domaine du serveur.](IMG/Debian - NetworkDomain.png)

#### Configuration root:
![Mot de passe root.](IMG/Debian - RootPassword.png)

#### Configuration d'un utilisateur
![Nom complet de l'utilisateur.](IMG/Debian - NameSuperUser.png)
![Login de l'utilisateur.](IMG/Debian - LoginSuperUser.png)
![Password de l'utilisateur.](IMG/Debian - PasswordSuperUser.png)

#### Configuration du disque dur:
![Choisir mode "assisté - Utiliser disque entier".](IMG/Debian - HardDisk.png)
![Choix du disque dur.](IMG/Debian - HardDiskComfirm.png)
![Type de partitionnement: "Tout dans une seule partition".](IMG/Debian - HardDiskPartition.png)
![Terminer le partitionnement et appliquer les changements.](IMG/Debian - HardDiskPartitionValid.png)
![Appliquer les changements sur le disque.](IMG/Debian - HardDiskPartitionConfirm.png)

#### Configuration des paquets ( applications ):
![Choix du miroir debian.](IMG/Debian - PkgLang.png)
![Choix du serveur ftp pour les paquets.](IMG/Debian - PkgUrl.png)

#### Configuration du proxy:
![Choix du proxy.](IMG/Debian - Proxy.png)

#### Configuration du systeme:
![Choisir uniquement "utilitaires usuels du systeme".](IMG/Debian - ConfigInstall.png)

#### Configuration de GRUB ( amorçage de linux ):
![Installer Grub: OUI.](IMG/Debian - Grub.png)
![Choix du disque pour installer Grub](IMG/Debian - GrubDisk.png)

#### Fin d'installation : 
![Fin de l'installation de debian - reboot du serveur](IMG/Debian - finish.png)
![Ecran une fois demarrer](IMG/Debian.png)


### Installation d'un environnement AMP

Maintenant que le systeme sur le serveur est configuré nous allons installer Apache - MySQL - PHP.

Commencer par vous connecter en root afin de facilité l'entrée des directives.

    Login : root
    Password : *****
    
Puis nous allons mettre à jour les dépôts des paquets:

    apt-get update 
    
#### Installation Apache

Executer la commmande:

    apt-get install apache2

A la fin de l'installation, vérifions le fonctionnement d'apache avec la commande:

    service apache2 status
    
Le serveur doit répondre :

    *apache2 is running
    
Pour ne pas avoir lors d'une erreur voir s'afficher les informations du serveur, edite le fichier de configuration d'apache:

    nano /etc/apache2/apache2.conf
    
Puis ajouter le ligne suivante à la fin du fichier:

    ServerSignature Off
    
Et redemmarre le serveur apache

    service apache2 restart
    
    
#### Installation de PHP5

Executer la commande afin d'installer php5 ainsi que le module apache permettant d'interpréter les script PHP:

    apt-get install php5 libapache2-mod-php5
    
Executer la commande suivante pour vérifier l'installation de PHP ( On obtient le numéro de version de php).

    php -v

Ouvrir le fichier php.ini:

    nano /etc/php5/apache2/php.ini
    
Puis modifier les valeur suivantes:

    # Taille maximum des fichiers à uploader (2MB par défaut)
    upload_max_filesize = 10M

    # Activation de l'UTF-8 par défaut
    mbstring.language=UTF-8
    mbstring.internal_encoding=UTF-8
    mbstring.http_input=UTF-8
    mbstring.http_output=UTF-8
    mbstring.detect_order=auto

On redemarre apache:

    service apache2 restart
    
    

#### Installation de MYSQL

Executer la commande suivante:

    apt-get install mysql-server
    
Lors de l'installation, il sera demandé un mot de passe pour l'accès à MYSQL.

Executer la commmande suivante afin de vérifier que MYSQL est bien installé.

    service mysql status
    

#### Installation de phpmyadmin
 
Afin de facilité la gestion des base de données dans mysql nous allons installé "phpmyadmin".

Executer la commande suivante:

    apt-get install php5-mysql phpmyadmin
    
Et nous allons redemarrer apache:

    service apache2 restart
    
Nous allons créer un lien symbolique vers phpmyadmin:

    ln -s /usr/share/phpmyadmin/ /var/www/html/phpmyadmin

Puis ajouter l'utilisateur connecté au groupe "www-data" ( nom utilisé par apache)

    usermod -a -G www-data <nom_de_votre_utilisateur>
    chown -R <nom_de_votre_utilisateur>:www-data /var/www/html
 
 
### Mise en place de l'acces serveur, adresse ipfixe

Principe : Affecter une adresse IP fixe au serveur web via une deuxième carte réseau.

#### Sous Virtualbox:

Eteindre la machine virtuelle.

Dans VirtualBox puis "préférences" et ensuite dans "réseau", aller dans « réseau hôte uniquement » .

Créer un nouveau réseau "+":

    Nom: vboxnet0
    carte:
    adresse ipv4: 10.0.0.1
    masque: 255.255.255.0

    serveur DHCP:
    adresse serveur: 10.0.0.100
    masque : 255.255.255.0
    limite inférieur: 10.0.0.1
    limite supérieur : 10.0.0.254


#### Configuration de la machine virtuelle:

Ajouter une carte réseau:
 
    mode d’accès: réseau privé honte
    nom: vboxnet0

#### Configuration du serveur Debian:

Démarrer la machine virtuelle puis executer la commande sous root: 

    pico /etc/network/interfaces

ajouter à la fin du fichier:

    auto eth1

    iface eth1 inet static
    address 10.0.0.2 (-> adresse ip fixe du serveur)
    netmask 255.255.255.0
 
Pour prendre en compte la nouvelle configuration:

    /etc/init.d/networking restart

Accèder à 10.0.0.2 depuis votre naviguateur pour vérifier que tout fonctionne, vous devriez voir la page web par défaut d'apache.


### Installation d'un serveur samba pour le partage des fichiers

Afin de partager les fichiers du sites, il faut un accès au serveur. Pour cela nous allons utiliser le serveur Samba.

Installer Samba:

    apt-get install samba

Créer un compte de connexion samba (`<user>`: utilisateur Samba ):

    smbpasswd -a <user>

Nous allons modifier le fichier de configuration Samba:

    pico /etc/samba/smb.conf
    
A la fin du fichier ajouter (`<adresse_ip_hote>` : addresse IP fixe du Serveur ):

    hosts allow = 127.0.0.1 <adresse_ip_hote>/24
    
Puis les lignes suivantes qui vont définir le partage (`<user>`: utilisateur Samba ) :

    [mes-sites]
    path = /var/www/html
    valid users = <user>
    available = yes
    browsable = yes
    public = yes
    writable = yes
    create mask = 0777
    create directory mask = 0777
    comment = Mes sites
    
#### Pour se connecter au serveur debian sous macos :

"Finder" puis "aller" dans la barre des tâches, ensuite "se connecter au serveur". 

Adresse du serveur : `<adresse_ip_hote>/mes-sites` (`<adresse_ip_hote>` : addresse IP fixe du Serveur )
Utilisateur : `<user>``
Password : `mot de passe créer pour <user>`    

-----------

## ALLEZ PLUS LOIN !


### PHP5 ET LES EMAILS

Parfois nous avons besoin de tester que l'envoi d'emails depuis les scripts php se passe comme voulu. Pour cela nous allons créer un faux serveur SMTP. Au lieu d'envoyer les emails vers un serveur pop ou imap, nous allons écrire les emails envoyés dans un fichier log. 

Commencons par créer notre script:

    pico /usr/local/bin/phpfakesmtp
    
Dans le fichier créer nous allons entrer ces lignes:

    #!/usr/bin/php
    <?php
    /**
     * FAKE SMTP FOR DEVELOPMENT LOCAL SERVER : On ecrit les emails dans un fichier log
     */
    $logfile = '/tmp/fake_smtp.log';

    // On récupère le contenu de l'email
    $pointer = fopen( 'php://stdin' , 'r' );
    $mail = '';
    while ( $line = fgets($pointer) ) { $mail .= $line; }

    // On ecrit dans le fichier log
    file_put_contents( $logfile , "\n---------- NEW MESSAGE [".date('Y-m-d H:i:s')."] ----------\n".$mail."\n" , FILE_APPEND );
    ?>

Nous allons rendre notre script excecutable:

    chmod +x /usr/local/bin/phpfakesmtp

Puis nous allons modifier le fichier ini de PHP dans la section [mail function]:

    [mail function]
    ; For Win32 only.
    ; http://php.net/smtp
    ;SMTP = localhost
    ; http://php.net/smtp-port
    ;smtp_port = 25

    ; For Win32 only.
    ; http://php.net/sendmail-from
    ;sendmail_from = postmaster@localhost

    ; For Unix only.  You may supply arguments as well (default: "sendmail -t -i").
    ; http://php.net/sendmail-path
    sendmail_path = /usr/local/bin/phpfakesmtp
    
On redemarre Apache2 pour prendre en compte:

    service apache2 restart
    
L'accès du fichier se trouve dans /tmp/fake_smtp.log:

    tail -f /tmp/fake_smtp.log (accès aux dernière ligne du fichier)
    

### APACHE2 ET SES MODULES


// On active le mod deflate
    LoadModule deflate_module libexec/apache2/mod_deflate.so
    // On active le mod expire
	LoadModule expires_module libexec/apache2/mod_expires.so
    // On active le mod rewrite
	LoadModule rewrite_module libexec/apache2/mod_rewrite.so


Avant d'activer le mod_rewrite sur Apache2, il faut s'assurer que le module est disponible sur votre serveur Debian Squeeze. 

Pour cela, nous allons tapez ces deux lignes en mode console et en utilisant le compte root: 

updatedb 
locate mod_rewrite.so
Un résultat de se genre doit apparaître à l'écran : 


/usr/lib/apache2/modules/mod_rewrite.so 
/usr/lib/debug/usr/lib/apache2/modules/mod_rewrite.so 

Ici, il suffit d'activer le mod_rewrite avec la commande suivante : 

a2enmod rewrite

Si le fichier /etc/apache2/mods-available/rewrite.load n'existe pas, il vous suffit d'utiliser la commande suivante. 

command echo "LoadModule rewrite_module /usr/lib/apache2/modules/mod_rewrite.so" > /etc/apache2/mods-available/rewrite.load a2enmod rewrite

Ensuite, vérifiez dans le fichier de configuration Apache2 ( /etc/apache2/apache2.conf )de votre site si AllowOverride est avec l'attribut All. 

Then open up the following file, and replace every occurrence of "AllowOverride None" with "AllowOverride all".


### APACHE2 ET MODULE USERDIR 

On active le module userdir d'apache ( activation d'apache pour chaque utilisateur de session )

    sudo a2enmod userdir
    
On edite le fichier de configuration du module userdir d'apache

    sudo nano /etc/apache2/mods-enabled/userdir.conf
    
Et on verifie la config

    <IfModule mod_userdir.c>
        UserDir public_html
        UserDir disabled root
 
        <Directory /home/*/public_html>
		AllowOverride All
		Options MultiViews Indexes SymLinksIfOwnerMatch
		<Limit GET POST OPTIONS>
			# Apache <= 2.2:
		        Order allow,deny
		        Allow from all
 
		        # Apache >= 2.4:
		        #Require all granted
		</Limit>
		<LimitExcept GET POST OPTIONS>
			# Apache <= 2.2:
		        Order deny,allow
		        Deny from all
 
			# Apache >= 2.4:
			#Require all denied
		</LimitExcept>
        </Directory>
    </IfModule>
    
On active PHP pour les utilisateurs en editant le fichier de configuration du module apache

    sudo nano /etc/apache2/mods-available/php5.conf

    <IfModule mod_php5.c>
    <FilesMatch "\.ph(p3?|tml)$">
	SetHandler application/x-httpd-php
    </FilesMatch>
    <FilesMatch "\.phps$">
	SetHandler application/x-httpd-php-source
    </FilesMatch>
    # To re-enable php in user directories comment the following lines
    # (from <IfModule ...> to </IfModule>.) Do NOT set it to On as it
    # prevents .htaccess files from disabling it.
    #<IfModule mod_userdir.c>
    #    <Directory /home/*/public_html>
    #        php_admin_value engine Off
    #    </Directory>
    #</IfModule>
    </IfModule>
    
On redemarre le service apache2

    sudo service apache2 restart

Le repertoire de dépose des sites est /home/username/public_html ( mkdir /home/phpinfo/public_html) et l'accès se fait via http://127.0.0.1/~username/



### APACHE2 ET SOUS DOMAINE

Pour créer un sous domaine editer le fichier 
    nano /etc/apache2/sites-available/000-default.conf
    
Et ajouter un autre virtualhost

    <VirtualHost *:80>
    ServerName site.local
    DocumentRoot "/Users/Sites/www"
    </VirtualHost>
    
Puis il suffit de déclarer ce sous domaine dans le le fichie host du serveur 

    nano /etc/hosts 
    
et ajouter à la fin

    127.0.0.1  site.local
    
Dans le cas d'une utilisation via virtualbox ne pas oublier de déclarer le nom de domaine sur l'hôte tel que:

    IPfixe_Invite site.local
    
    
    
### INSTALLER UN DASHBOARD POUR CONTROLER LE SERVEUR ( AJENTI )

Installer un dashboard pour serveur debian 

    wget -O- https://raw.github.com/ajenti/ajenti/1.x/scripts/install-debian.sh | sh
    
Pour Ubuntu
    
    wget -O- https://raw.github.com/ajenti/ajenti/1.x/scripts/install-ubuntu.sh | sudo sh
    
Accès via https://localhost:8000  ( log : root, password: admin )

Si via http://localhost:8000 modifie le fichier nano /etc/ajenti/config.json et desactive ssl : ssl { enable :false ;} ( utile derrière virtualbox ).




### Un SERVEUR FTP ( pour chaques utilisateurs du serveur )

    sudo apt install proftpd

On configure le serveur ftp:

    nano /etc/proftpd/proftpd.conf
    
    Premiere ligne correspond au time out apres laquelle l'utilisateur sera automatiquement déconnecte
    
    Pour limiter l'acces uniquement au dossier de l'utilisateur décommenter la ligne suivante:
    # DefaultRoot
    
    
On redemarre le serveur ftp

    sudo service proftpd reload
    
Accès ftp://Utilisateur:MotDePasse@IPDuServeurFTP  ( utilisateur:motde passe d'un utilisateur d'une session sur le serveur ).
