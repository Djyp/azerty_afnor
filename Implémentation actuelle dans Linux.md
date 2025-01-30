# Implémentation actuelle dans Linux

Les dispositions AZERTY et BÉPO sont implémentées dans [xkeyboard-config](https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config/-/blob/master/symbols/fr). Vous avez certainement la possibilité de l'activer dans votre distribution.

Cependant, quelques questions et problèmes subsistent.

## Pourmille

Le symbole ‰ (pourmille) fonctionne mais pas partout dans mon système. Je n'ai pas eu l'occasion de creuser suffisament pour savoir s'il s'agit d'un bug de ma distribution, de X11 ou autre chose. S'il ne fonctionne pas chez vous, retenez qu'il peut fonctionner chez d'autres. Au moment où j'écris ces lignes, certaines fenêtres me laissent l'écrire et d'autres n'affichent strictement rien.

## Theta masjucule

Le [site de l'Afnor](https://norme-azerty.fr) montre deux versions du clavier. La première est [intéractive](https://norme-azerty.fr/#explore) et l'autre est une [image fixe](https://norme-azerty.fr/img/main_layout.png).
On voit sur l'image que la touche Q devrait créer un theta minuscule et majuscule en utilistant la touche Alternative Graphique avec ou sans Shift. Ceci n'a pas été correctement implémenté dans xkb.
J'ai appliqué correctement ce caractère sur Q. Je proposerai une Merge Request dès que possible.

## Lettres barrées

Il existe deux caractères unicode pour appliquer correctement la norme.

- U+0336, la barre longue couvrante placée par l'Afnor sur la touche B
- U+0337, la barre oblique courte couvrante placée par l'Afnor sur la touche K

Avec xkb, actuellement, les deux touches se sont vu attribuer le symbole nommé `dead_stroke`. Cette touche répond semble-t-il correctement aux besoins d'un utilisateur qui souhaite utiliser une lettre barrée telles que ł,ɉ, ou ø qui sont utilisés dans plusieurs langues européennes.
En ce qui me concerne j'ai choisi de faire confiance à `dead_stroke`. Les touches B et K, avec Alt. Gr., ont donc le même comportement.

## La touche espace

La norme NF Z71-300 décrit que la touche espace propose trois espaces différents. Encore une fois, la partie intéractive ne l'affiche pas mais [l'image](https://norme-azerty.fr/img/main_layout.png) démontre ces trois espaces : l'espace, l'espace insécable et l'espace insécable fine.
J'ai appliqué correctement ces espaces. Je proposerai une Merge Request dès que possible.

## Les touches MODE

Lorsqu'on appuie sur Alternative Graphique conjointement avec F, G ou H, nous entrons dans un autre mode. Ces modes ne sont pas pleinement implémentés dans Linux.

### Mode Monétaire
`Alt. Gr + F` pour Finance.mxkeyboard-config utilise `dead_currency` sur cette conbinaison de touches. Ça exécute un comportement commun à tous les claviers pour la même touche. Par chance, plusieurs symboles sont au bon endroit tels que ₳ ₮ ¥ ₩ ₫ ₦. Cependant, d'autres symboles sont déplacés ou incorrects, tels que € ₠ ¤. Par exemple ฿, utilisé à tort pour le bitcoin car il représente le Baht thaïlandais devrait plutôt nous afficher ₿.
 
### Mode Lettres grecques
`Alt. Gr + G` pour Grec
De la même manière que précédemment, cette combinaison est associée à `dead_greek`. Il a donc le même comportement et ne répond pas vraiment à ce qui est attendu. Certaines sont comme prévu, telles que : β Β κ Κ λ Λ μ π Π

### Mode Caractères européens
Ce mode n'existe pas. La combinaison `Alt. Gr + H` n'est affectée à rien pour le moment.

### Que faire ?
Je vous propose d'utiliser ma solution avec [la touche Compose](Compose/INSTALL.md) ;)