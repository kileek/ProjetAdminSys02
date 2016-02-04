# Projet administration 02
## by VASTRA Alexandre

---

## Système de sauvegarde incrementale sur une machine distante
### Fonctionnalités :
- [ ] Sauvegarde incrementale
  - [ ] Sur la machine locale
  - [ ] Sur la machine distante
- [ ] Système de restauration
  - [ ] Sur la machine locale
  - [ ] Sur la machine distante

### Sauvegarde incrementale sur la machine locale
A fin d'éffectuer une sauvegarde incrémentale sur une machine local. Il faut d'abord vérifier si rsync est bien installé :

  ```ls /etc/default/rsync```

Si aucun résultat, il faut l'installer :

  ```apt-get install rsync```

Puis créer un répertoire de sauvegarde sur la machine local :

  ```mkdir /srv/backup```

Lui donner les droits en écriture et lecture (ou pas ):

 ```chmod r+w /srv/backup```

Puis lancer la commande :

 ```rsync -azvu <repertoireASauvegarder> <repertoireDeDestination>```

Lancer le script de sauvegarde a interval regulier

Il faut d'abord s'assurer d'avoir une crontab pour l'utilisateur courant.Normalement il n'y a aucune crontab pour l'utilisateur

  ```crontab -l```

Puis faire :

  ```crontab -e```

Afin de modifier la crontab de l'utilisateur courant.
Y ajouter une ligne de format :

```* * * * * < chemin absolu de la commande a executer >```

chaque étoile correspondant à une échelle temps, minutes , heures , etc...

exemple pour lancer un script de sauvegarde toutes les 2mins du lundi au vendredi il suffit d'écrire :

  ```*/2 * * * 1-5 /< script sauvegarde >```
