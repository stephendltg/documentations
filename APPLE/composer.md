php composer-setup.php --install-dir=/usr/local/bin --filename=composer

/usr/local/bin/composer


Ce n’est pas l’option la plus courante, mais vous pouvez choisir d’installer Composer localement. Cela signifie que votre système d’exploitation ne pourra pas exécuter Composer de n’importe où; Vous devez spécifier le chemin d’accès à partir duquel il est installé. Pour ce faire, suivez ces étapes:

Ouvrez votre terminal ou connectez-vous à votre serveur via SSH.
Exécutez les deux commandes suivantes:

php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

La première commande téléchragera le programme d’installation de Composer en tant que fichier PHAR (Archivage PHP), tandis que la seconde assurera que le programme d’installation est exempt de toute erreur ou corruption. Après l’exécution de ces commandes, vous disposerez de la dernière version du programme d’installation de Composer sur votre ordinateur.

Installez Composer via la commande:

php composer-setup.php --install-dir=/usr/local/bin --filename=composer

Tester en lancant commande: 

composer