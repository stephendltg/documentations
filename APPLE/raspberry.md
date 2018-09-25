#Raspberry

## Activer ssh / changer password / etc ...

Enter sudo raspi-config in a terminal window.


## Un SERVEUR FTP ( pour chaques utilisateurs du serveur )

    sudo apt install proftpd

On configure le serveur ftp:

    nano /etc/proftpd/proftpd.conf
    
    Premiere ligne correspond au time out apres laquelle l'utilisateur sera automatiquement déconnecte
    
    Pour limiter l'acces uniquement au dossier de l'utilisateur décommenter la ligne suivante:
    # DefaultRoot
    
    
On redemarre le serveur ftp

    sudo service proftpd reload
    
Accès ftp://Utilisateur:MotDePasse@IPDuServeurFTP  ( utilisateur:motde passe d'un utilisateur d'une session sur le serveur ).




## docker sur debian

sudo apt-get install -y docker.io





## installation docker compose
sudo apt-get install docker-compose


