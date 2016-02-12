# Projet administration 02
## by VASTRA Alexandre

---

## Système de sauvegarde incrementale sur une machine distante
### Fonctionnalités :
- [x] Sauvegarde incrementale
  - [x] Sur la machine locale
  - [x] Sur la machine distante
- [x] Système de restauration
  - [x] Sur la machine locale
  - [x] Sur la machine distante

### Sauvegarde incrementale sur la machine locale

A fin d'éffectuer une sauvegarde incrémentale sur une machine local. Il faut d'abord vérifier si rsync est bien installé :

```
ls /etc/default/rsync
```

Si aucun résultat, il faut l'installer :

```
apt-get install rsync
```

Puis créer un répertoire de sauvegarde sur la machine local :

```
mkdir /srv/backup
```

Lui donner les droits en écriture et lecture (ou pas ):

```
chmod r+w /srv/backup
```

Puis lancer la commande :

```
rsync -azvu <repertoireASauvegarder> <repertoireDeDestination>
```

Lancer le script de sauvegarde a interval regulier

Il faut d'abord s'assurer d'avoir une crontab pour l'utilisateur courant.Normalement il n'y a aucune crontab pour l'utilisateur

```
crontab -l
```

Puis faire :

```
crontab -e
```

Afin de modifier la crontab de l'utilisateur courant.
Y ajouter une ligne de format :

```
* * * * * < chemin absolu de la commande a executer >
```

chaque étoile correspondant à une échelle temps, minutes , heures , etc...

exemple pour lancer un script de sauvegarde toutes les 2mins du lundi au vendredi il suffit d'écrire :

```
*/2 * * * 1-5 /< script sauvegarde >
```

### Sauvegarde incrementale sur la machine distante
  Avant toutes choses il faut installer Rsync sur la machine qui recevra le fichier de backup.
  
  Le procéssus est identique à celui pour la sauvegarde local excepté que la commande rsync est étoffé d'autre paramètre comme -e ssh qui permet la connection à la machine distante
```  
  	`rsync -azvu -e ssh <repertoire a sauvegarder> 192.168.194.200:<repertoire d'acceuil>`;
```


### Système de restauration sur une machine local
  
  Pour la restauration locale , rien de plus enfantin l'on supprime l'ancien repertoire /home par exemple :
```  
  `rm -rd /home`;
```  
  Puis l'on copie le repertoire de sauvegarde vers le nouveau repertoire :
```  
    `cp  -r $backup$nump_rep /home`;
```  

### Système de restauration sur une machine distante

  Pour se faire il faut utiliser la commande scp :
```   
  `scp -r 192.168.194.200:$backup$num_rep 192.168.194.10:/home`
```     
    
  
