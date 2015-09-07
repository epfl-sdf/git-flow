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

* minimum de gestion de conflict dans la production
* Git devrait s'adapter a notre workflow et pas l'inverse.
    * Dev 
    * Integration
    * Prod
* Il devrait etre facile de sandboxer et de partager des essais
* Les conflicts de merge devrait etre regle par le developpeur en amon 
    et non pas par l'integrateur
* Il devrait etre simple de proposer un patch tant pour la production que pour le developpement

##Branching model

### Mapping 

Envionment --> Branche

\pause

Dev --> developement

\pause

Integration --> developement

\pause

Prod --> developement

### Dev branches

branche de feature:
nom de la feature
branche a la duree de vie courte

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
resolution d'un conflict par un 

git checkout developpment
git merge --no-ff

\pause

en cas de branche locale uniquement,

git rebase origin/developpment


### Prod branch

Branche existante (toujours sur la remote)
Merge depuis la branche de developpment
git merge --no-ff

## Commandes additionelle

### Aparte sur 'merge --no-ff'

En cas d'absence de conflict, git forward 

* Perte de l'historique
* Absence du commit de merge explicit

ajout du --no-ff

* Creation automatique d'un commit de merge
* Historique conserve

### Rebase

prend ma branche actuell change l'endroit ou cette branche est attachee

change les references des commits

### Git pull --rebase

met les repos locaux en dessus  des commits deja presents dans la remote, 
Les references des commits locaux changeront 
arbres lineaire

\pause 

demo !


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

* n'utiliser le rebase que des branches n'apparaissant que sur ses branches locales

* dans le doute, utiliser le merge --no-ff


### Resolution de conflict 

toujours runner git status

En cas de probleme, git status 

\center
\includegraphics[width=7cm]{img/status_all_the_things.jpg}

### Resolution de conflict entre la branche de dev et celle d'integration

```
git merge --abort # safe stop
git checkout critical_feature
git merge --no-ff developpment
#RESOLUTION DE CONFLICT!
git checkout developpment
. . .
git merge --no-ff critical_feature
```

### Big demo
