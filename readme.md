# Docker CRON

Stack Docker prévue pour fonctionner en tant qu'orchestrateur. 
Ce container est un CRON capable d'executer des commandes dans autres containers Docker ou de lancer des containers en fonction d'une programmation de temps.
Basé sur la dernière version [Linux Alpine officielle.](https://hub.docker.com/_/alpine)

## Installation

Les scripts de commande sont à placer dans le dossier ``appData/cron/``.
L'architecture de base prend en charge les temporalités suivantes :

- Toutes les 1 minute
- Toutes les 15 minutes
- Toutes les heures
- Tous les jours
- Une fois par semaine
- Une fois par mois

### Ajout d'intervalles de temps

Au besoin, il est possible d'ajouter de nouvelles temporalités en modifiant le ``Dockerfile``. Le site [Crontab Guru](https://crontab.guru/) peut aider à définir les intervales.

La commande suivante, déjà présente, ajoute une execution toutes les minutes des scripts présents dans le dossier ``1min``.

```shell
echo "*       *       *       *       *       run-parts /etc/periodic/1min" >> /etc/crontabs/root
```

### Les scripts de commande

Les scripts de commande sont à placer dans le répertoire correspondant à la temporalité souhaitée.

**Attention** : le nom des script ne doit pas contenir de point sous peine de ne pas s'executer.

#### Exemple de script pour lancer un container

La commande suivante lance un container Busybox et affiche l'heure (le container est détruit après execution via le paramètre  ``--rm``) .

```shell
#!/bin/bash
docker run --rm busybox date
```

#### Les scripts doivent être executables

Une fois les script écrits, lancer la commande suivante pour les rendre exécutables :

```shell
chmod -R a+x appData/cron/
```



Avec tous mes remerciements à [Peter Mooring](https://www.peterspython.com/fr/) pour ses explications claires dans son article "[Exécuter une commande Docker dans un conteneur Cron Docker](https://www.peterspython.com/fr/blog/executer-une-commande-docker-dans-un-conteneur-cron-docker)"