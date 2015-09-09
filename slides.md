%Git, Easy Branching
%Malik Bougacha
%25 août 2015

# Introduction

No logo :(

## Git est puissant

### With power comes great responsibility

Git sans workflow

\center
\includegraphics[width=4cm]{img/git_crazy.png}


# Git flow 0.1

### Monde ideal

* Minimum de gestion de conflict dans la production
* Git devrait s'adapter a notre workflow et pas l'inverse.
    * Feature
    * Dev
    * Prod
\pause
* Il devrait etre facile de sandboxer et de partager des essais
\pause
* Les conflicts de merge devrait etre regle par le developpeur en amon 
    et non pas par l'integrateur
\pause
* Il devrait etre simple de proposer un patch tant pour la production que pour le developpement

##Branching model

### Mapping 

Environment --> Branche (set de code)

\pause

Dev --> developement

\pause

Integration --> developement

\pause

Prod --> developement

### Dev branches

branche de feature:

* nom de la feature
* branche a la duree de vie courte

\pause

branche de fix
fix_*
branche a la duree de vie courte

\pause

amelioration d'un composant
improve_*
branche a la duree de vie courte

### Dev branches 2

Base sur la branche d'integration remergee dans la branche d'integration

en cas de conflict entre la branche d'integration et la branche de feature,
resolution d'un conflict par le programmeur de la feature.

\pause

en cas de branche locale uniquement,

git rebase origin/developpment


### Prod branch

Branche existante (toujours sur la remote)
Merge depuis la branche de developpment

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

### 'merge --no-ff' demo

* demo

### Resolution de conflict 

toujours runner git status

En cas de probleme, git status 

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

```
git pull --rebase
```

\pause 

Ici pas de conflict car les modifications n'arrivent 
qu'a travers des branches de feature

### 'Git pull --rebase'

met les repos locaux en dessus  des commits deja presents dans la remote, 
Les references des commits locaux changeront 
arbres lineaire

\pause 

### 'Git pull --rebase' demo

demo !


#Aparte

### push --force

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

