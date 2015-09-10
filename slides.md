%Git, Easy Branching
%Malik Bougacha
%25 août 2015

# Introduction

## Git est puissant

### With power comes great responsibility

Git sans workflow

\center
\includegraphics[width=4cm]{img/git_crazy.png}


# Git flow 0.1

### Monde idéal

* Git devrait s'adapter à notre façon de travailler et pas l'inverse.
\pause
* Minimum de gestion de conflit dans la production
\pause
* Environnement suivant:

    * Feature
    * Dev
    * Prod

\pause

* Il devrait être possible d'appliquer un bug fix à la production et au dev
* Il devrait être facile de sandboxer et de partager des essais

\pause

* Il devrait être facile de promouvoir du code d'un environnement a un autre.

\pause

* Les conflits de merge de feature devraient être réglés par le développeur en amon 
et non pas par l'integrateur

\pause

* Il devrait être simple de proposer un patch tant pour la production que pour le développement

# Branching model

### Mapping 

Environment --> Branche (set de code)

\pause

Branches:

\pause

* Feature branch
* Developement
* Production (master)
* Fix
* Release

### Branche de Feature

branche de feature:

* Nom de la feature
* Branche à la durée de vie courte

\pause

Amélioration d'un composant
branche à la durée de vie courte

### Branche de Feature

* Base sur la branche d'intégration 
* Mergée dans la branche de développement

\pause 

Resolution des conflicts en amon

### Branche de Developpement

* Branche d'integration des features
* Branche active a la duree de vie longue

\pause 

Resolution des conflicts en amon

### Interaction branche de Developpement et branche de feature

\center 
\includegraphics[width=3cm]{img/gitflow-feature.png}

### Branche de release

* Branche de prerelease
* Branche active a la duree de vie courte
* Tag du numeros de version

### Branche de production

Branche existante (toujours sur la remote)
Merge depuis la branche de developpment

### Interation Branche de release et branche de production

\center 
\includegraphics[width=3cm]{img/gitflow-release.png}

### Branche de fix

Branche à la durée de vie courte
Basee sur production

Merge Sur la branche de dev ainsi que sur celle de prod

### Interaction Branche de release, de prod et de fix

\center 
\includegraphics[width=3cm]{img/gitflow-hotfix.png}

### Resume

\center
\includegraphics[width=4cm]{img/gitflow.png}

## Commandes du Workflow

### Ajout d'une feature

```sh
git checkout developpment
```

### Ajout des modifications de la features

```sh
git add new_file old_file anything.jpg
git diff --staged
git commit -m 'adding element for feature'
```

### Merge de la feature

```
git checkout developpment
git merge --no-ff 
```

### 'merge --no-ff'

En cas d'absence de conflict, git forward 

* Perte de l'historique
* Absence du commit de merge explicit

Ajout du --no-ff

* Creation automatique d'un commit de merge
* Historique conserve

### 'merge --no-ff'

\center
\includegraphics[width=7cm]{img/merge-no-ff.png}

### Resolution de conflict 

toujours runner git status

En cas de probleme, git status 

\pause

\center
\includegraphics[width=7cm]{img/status_all_the_things.jpg}

### Resolution de conflict entre la branche de dev et celle de feature

```
git merge --abort # safe stop
git checkout critical_feature
git merge --no-ff developpment
#RESOLUTION DE CONFLICT!
git checkout developpment
. . .
git merge --no-ff critical_feature
```

### Mise a jour de la branche de developpement

\center
\includegraphics[width=2cm]{img/push-n-pull-result.png}

### Mise a jour de la branche de developpement

```
git pull --rebase
```

\pause 

Conflict gere en upstream dans les branches de feature!

### Mise a jour de la branche de developpement

\center
\includegraphics[width=2cm]{img/push-n-pull-rebase-result.png}

### Mise a jour de la branche de developpement

Met les repos locaux en dessus  des commits deja presents dans la remote, 
Les references des commits locaux changeront 
Arbres lineaire

#Aparte sur le rebase

### Rebase

Change la base de la branche:

\center
\includegraphics[with=2cm]{img/gitflow-rebase-feature.png}

### Rebase

Change le sha du commit

\pause

Change le commit


### Force

traduction:

j'ignore ce qui se trouve actullement de l'autre cote,
j'ecrase les references existantes et les remplace par la mienne

### Absolute power corrupt absolutely

\center
\includegraphics[width=7cm]{img/burn_remote.jpg}

### Absolute power corrupt absolutely

\center
\includegraphics[width=7cm]{img/git_absolute.png}

### Solutions

* Jamais utilise push force !

\pause

En cas d'exception se referer a la ligne d'avant.

* N'utiliser le rebase que des branches n'apparaissant que sur ses branches locales

* dans le doute, utiliser le merge --no-ff


### Deployer en prod !

```
git checkout production
git merge --no-ff developpment
```

\pause

Ici aussi, pas de conflict de merge, on ne fait qu'avancer 


### Conclusion intermediaire

Scaling de team !

transparence !

# Gitlab, Gitflow 0.2

### Gitlab overview

* RoR interface for git remote
* Gestion des acces par repository

### Merge request

* Merge dans la branche de devloppement des features sont publique
* Deployment en prod fait de la meme maniere
* Review des demandes de merges 

### Review

* Est ce que je comprend ce qui a ete merge ?
* Est ce que le nom des methodes est logique et comprenhensible ?
* Nom des variables est correcte et comprehensible ?
* une partie du code peut etre mieux ecrit ?

\pause 

Partage de la reponsabilite, le code appartient au developpeur avant d'etre merge, 
Il devient la reponsabilite du grouppe a partir du merge.

### Git facile

* Gestion de modification des fichiers a travers la gui


### Aparte github

* Merge request
* Un fork est simplement une autre remote.
* Public pour des contributions a l'open source ou publication.
* Tous les labos de l'epfl sont dessus.


### Aller plus loin

* En allemand: https://github.com/esc/clt-2015-git-workflows
* Gitflow par commandes: https://github.com/nvie/gitflow.git

