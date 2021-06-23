# AWS 
### IP Publique RedHat: 
### IP Publique LinuxAMa:  

        ssh -i 'c:/Users/m.kout/.../Directory/LinuxdeBaseAWS.pem' ec2-user@ip_address  
        
## Download and install Tripwire


        cd /usr/src
        sudo wget https://github.com/Tripwire/tripwire-open-source/releases/download/2.4.3.7/tripwire-open-source-2.4.3.7.tar.gz
        sudo tar zxvf tripwire-2.4.1.2-src.tar
        cd tripwire-open-source-2.4.3.7
        ./configure --prefix=/opt/tripwire
        makecd
        make install
        cd /opt/tripwire/sbin/
        ./tripwire --init

### Pour ajouter une ou des règles 
    /opt/tripwire/etc/twpol.txt


### Les rapports sont stockés dans :  
    /opt/tripwire/lib/tripwire/report 

### Convertir le rapport en fichier txt : 
    ./twprint --print-report --twrfile \
    /opt/tripwire/lib/tripwire/report/{nom du rapports}.twr  > \
    /tmp/readable-output.txt


### Envoyer mail - test
    ./tripwire --test --email mail@mail.com

### Intégrer rapports par mail
    Ajouter une ligne à la twpol
        emailto = mail@mail.com

### Voir les logs des mails
    sudo tail -f /var/log/maillog 

### Mettre en place un job pour un check régulier
    1 - Créer un nouveau script cron => sudo crontab -e -u root
    2 - A insérer :
        Exemple d'un check régulier chaque 10h du mat : 00 10 * * * /opt/tripwire/sbin/tripwire  --check
