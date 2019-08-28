# Implémentation de la norme AFNOR
Norme publiée le 02 avril 2019 dont les principales informations sont publiées sur https://norme-azerty.fr.

## Contexte
Je suis développeur et formateur. Je suis aussi très intéressé par les dispositions de claviers, allez savoir pourquoi... Je ne suis cependant pas un expert de X11.
La doc de xkb étant ce qu'elle est, j'ai fait de mon mieux pour implémenter la nouvelle norme AFNOR pour mon système Linux.
Je me suis basé sur https://norme-azerty.fr/ qui détaille plutôt bien chaque touche. J'ai croisé les informations avec https://wayland-devel.freedesktop.narkive.com/N3rwOVoT/compose-and-dead-keys-support-in-libxkbcommon et la table de caractères.

J'ai copié-collé une disposition existante dans le fichier `/usr/share/X11/xkb/symbols/fr` que j'ai adaptée.
Pour cette v0.1, il manque encore quelques aspects. Je partage mon implémentation avec la monde francophones, notamment pour ceux qui voudront terminer le travail.

## Versions

### v0.1 - 08.04.19
Implémentation rapide d'une base. Toutes les touches fonctionnent avec les combinaisons `SHIFT`, `ALT`, `SHIFT + ALT` sauf les touches MODE. Elles doivent permettre d'accéder à des symboles supplémentaires.
La touche Mode symbole monétaire (`ALT + F`) permet d'accéder à des caractères monétaires moins utilisés en Europe. £, $ et € sont bien sûr accessibles sans cette touche.
La touche Mode symbole micro (`ALT + G`) permet d'accéder à plusieurs lettre grecques, utiles notamment pour l'écriture scientifique.
La touche Mode symbole européen (`ALT + H`) permet d'accéder à plusieurs caractères utilisés dans les langues latines européennes.

### v0.2 - 16.08.19
- Ajout des modes monétaire, grec et européens grâce à la touche Compose. À ce stade certains caractères restent incorrects.
- Début de la réécriture de la documentation
- Des questions subsistent concernant l'interprétation de certains caractères

### v0.3 - 21.08.19
- Corrections du mode grec (ajout de lettres, correction du sigma final)
- Corrections de certains caractères du mode européen
- Ajout d'une Licence MIT

### Vers une version v1.0
Pour une version complète il faudrait :
 - [x] Implémenter le mode monétaire
 - [x] Implémenter le mode micro
 - [x] Implémenter le mode européen
 - [ ] Voir s'il est nécessaire de distinguer le symbole `TRAIT D'UNION` du symbole `MOINS`
 - [ ] Voir s'il est nécessaire de distinguer le symbole `BARRE COUVRANTE` du symbole `BARRE OBLIQUE COUVRANTE`
 - [ ] Changer le . en un vrai DOT BELOW dans le layout overview (touche I)
 - [x] Pour plus de propreté, changer les tabulations en espaces
 - [ ] Une vraie documentation complète
 - [ ] Ajouter un layout overview pour chaque mode 

## Installation
L'installation se fait en deux étapes.

### Les symboles de base
Le fichier d'origine se trouve sur `/usr/share/X11/xkb/symbols/fr`. Il est certainement standard (cette information n'est pas vérifiée) et provient initialement d'une installation de Linux Mint 19.1. Il s'est vu ajouté le contenu de [fr_azerty_afnor](fr_azerty_afnor). Libre à vous d'écraser votre fichier `fr` ou d'ajouter la contenu de `fr_azerty_afnor` de ce même fichier.

### Les symboles des modes
Pour le moment, le meilleur moyen que je connaisse d'implémenter les modes est d'utiliser la touche Compose. La touche compose propose déjà plusieurs combinaison possible visibles par exemple sur [la documentation francophone d'Ubuntu](https://doc.ubuntu-fr.org/caracteres_etendus).
Il est possible de créer ses propres touches combinaisons grâce au fichier `~/.XCompose`. Vous pouvez copier le fichier `XCompose` de ce dépôt dans votre dossier home et ajouter un point au début de son nom.
Une fois installé, il faut redémarrer un logiciel pour que le fichier XCompose soit pris en compte.

Il est possible d'assigner une touche Compose grâce aux options du clavier. Toutefois, la touche Compose a été ajoutée sur `AltGr+F`, `AltGr+G` et `AltGr+H`. Ce qui oblige de rappuyer sur <kbd>g</kbd>, par exemple, puis <kbd>D</kbd> pour obtenir le caractère Δ (delta majuscule).

## Retours
Je suis preneurs de toutes pull requests, retour, suggestions et autres afin d'améliorer cette implémentation et la rendre la plus proche possible de la norme de l'AFNOR.
