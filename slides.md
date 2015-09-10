%Git flow
%Malik Bougacha
%10 Septembre 2015

# Introduction

## Git est puissant

### With power comes great responsibilities

Git sans workflow

\center
\includegraphics[width=4cm]{img/git_crazy.png}

# Requirements

### Monde idéal

* Adapter git à l'usage.
\pause
* Minimum de gestion de conflit dans la production
\pause
* Environnement suivant:
    * Feature
    * Dev
    * Prod
\pause
* Il devrait être possible d'appliquer un bug fix à la production et au développement.
* Il devrait être facile de sandboxer et de partager des essais.
\pause
* Il devrait être facile de promouvoir du code d'un environnement à un autre.
\pause
* Conflits gérés par le développeur
et non pas par l'intégrateur.
\pause
* Simplicité de patch pour la production et le développement.

# Organisation des branches

### Correspondance branche

Environnement --> Branche (set de code)

\pause

Branches:

\pause

* Feature
* Développement
* Release
* Production (master)
* Hotfix

### Branche de Feature

Branche de feature:

* Nom de la feature.
* Branche à la durée de vie courte.
* Amélioration d'un composant.


### Branche de feature

* Basé sur la branche de développement
* Mergée dans la branche de développement.

\pause

Emplacement des résolutions des conflits avec la branche de développement 

### Branche de développement

* Branche d'intégration des features.
* Branche active à la durée de vie longue.

### Interactions branche de développement et branche de feature

\center
\includegraphics[width=3cm]{img/gitflow-feature.png}

### Branche de release

* Branche de pré-production
* Branche active à la durée de vie courte

### Branche de production

* Branche à la durée de vie longue (toujours sur la remote)
* Merge depuis la branche de développement
* Tag de version

### Interaction branche de release et branche de production

\center
\includegraphics[width=3cm]{img/gitflow-release.png}

### Branche de fix

* Branche à la durée de vie courte
* Basée sur production

* Merge sur la branche de développement ainsi que sur celle de production (master)

### Interaction branche de release, production et hotfix

\center
\includegraphics[width=3cm]{img/gitflow-hotfix.png}

### Résumé

\center
\includegraphics[width=4cm]{img/gitflow.png}

# Commandes du Workflow

### Ajout d'une feature

```sh
git checkout -b feature_super_bouton
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

En cas d'absence de conflit, git fast-forward

* Perte de l'historique
* Absence du commit de merge explicite

\pause

Ajout du --no-ff

* Création automatique d'un commit de merge
* Historique conserve

### 'merge --no-ff'

\center
\includegraphics[width=7cm]{img/merge-no-ff.png}

### Resolution de conflict

Toujours runner `git status`.

En cas de problème, `git status`

\pause

\center
\includegraphics[width=7cm]{img/status_all_the_things.jpg}

### Résolution de conflits entre la branche de développement et celle de feature

```
git merge --abort # safe stop
git checkout critical_feature
git merge --no-ff developpment
#RESOLUTION DE CONFLICT!
git checkout developpment
. . .
git merge --no-ff critical_feature
```

### Mise à jour de la branche de développement

\center
\includegraphics[width=2cm]{img/push-n-pull-result.png}

### Mise à jour de la branche de développement

```
git checkout developpment
git pull --rebase
```

\pause

Conflit géré en downstream dans les branches de feature !

### Mise a jour de la branche de développement

\center
\includegraphics[width=2cm]{img/push-n-pull-rebase-result.png}

### Mise a jour de la branche de développement

Met les repos locaux en dessus  des commits déjà présents dans la remote,
Les références des commits locaux changeront
Arbres linéaire

# Aparté sur le rebase

### Rebase

* Change la base de la branche.

\pause

* Change le sha des commits.

\pause

* Change les commits.

### Rebase

\center
\includegraphics[width=5.5cm]{img/gitflow-rebase-feature.png}

### Force

traduction:

J'ignore ce qui se trouve actuellement de l'autre cote.

\pause

J'écrase les références existantes et les remplace par la mienne.

### Absolute power corrupt absolutely

\center
\includegraphics[width=7cm]{img/burn_remote.jpg}

### Absolute power corrupt absolutely

\center
\includegraphics[width=7cm]{img/git_absolute.png}

### Solutions

* Ne jamais utiliser push force !

\pause

En cas d'exception se référer a la ligne d'avant.

\pause

* N'utiliser le rebase sur les branches locales
* Dans le doute, utiliser le `merge --no-ff`.


### Déployer en production

```
git checkout master
git merge --no-ff developpment
git push origin master
```

\pause

Pas de conflit de merge

### Tagger la production


```
git tag 0.1
git push --tags
```

* Alias au SHA, référence fixe du commit.

\pause

* Diffèrent d'une branche.

### Conclusion intermédiaire

Problème du workflow précèdent:

* Transparence
* Peer review

# Gitlab, Gitflow 0.2

### Gitlab

* Interface ruby on rail for git remote.
* Gestion des accès par repository.

### Merge request

* Merge dans la branche de développement des features sont publique.
* Deployment en production fait de la même manière.
* Review des demandes de merges

### Review

* Est ce que je comprend ce qui a été mergé ?
* Est ce que le nom des méthodes est logique et compréhensible ?
* Nom des variables est correcte et compréhensible ?
* Une partie du code peut être mieux écrite ?

\pause

* Partage des responsabilités.

### Git facile

* Gestion des modifications des fichiers à travers la GUI.

### Aparté Github

* Merge request
* Un fork est simplement une autre remote.
* Public pour des contributions a l'open source ou publication.
* Tous les laboratoires de l'EPFL sont dessus.

### Aller plus loin

* En allemand: https://github.com/esc/clt-2015-git-workflows (Utilisation des schémas git)
* Gitflow par commandes: https://github.com/nvie/gitflow.git
* Gerrit flow: http://docs.openstack.org/infra/manual/developers.html
