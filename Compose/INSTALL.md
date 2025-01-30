# Installation des modes avec une touche Compose

Pour le moment, le meilleur moyen que je connaisse d'implémenter les modes est d'utiliser la touche Compose. La touche compose propose déjà plusieurs combinaison possible visibles par exemple sur [la documentation francophone d'Ubuntu](https://doc.ubuntu-fr.org/caracteres_etendus).

Il est possible de créer ses propres combinaisons grâce au fichier `~/.XCompose`. Vous pouvez copier le fichier `.XCompose` de ce dépôt ou copier son contenu dans le votre.

Il est possible d'assigner une touche Compose grâce aux options du clavier. La plupart des environnements vous proposent d'affecter Compose à une touche comme Menu ou le niveau 3 d'une touche contrôle (Alt Gr. + Ctrl).

> [!NOTE]
> Initialement, la première version que j'ai fournie proposait de mettre la touche Compose sur `AltGr+F`, `AltGr+G` et `AltGr+H`. J'ai choisi d'appliquer finalement la même méthode que la version distribuée, c'est-à-dire `dead_currency`, `dead_greek` et rien. Vous pouvez tout à fait éditer votre fichier  `/usr/share/X11/xkb/symbols/fr` pour mettre `Multi_key` à ces endroits. Cependant je vous déconseille d'écraser ce fichier `fr` car il sera écrasé à chaque mise à jour de xbd.

## Fonctionnement

Appuyez sur la touche Compose que vous avez choisie puis appuyez sur <kbd>F</kbd>, <kbd>G</kbd> ou <kbd>H</kbd> puis sur la touche ou la combinaison de touches pour obtenir votre caractère.

### Exemples

<kbd>Compose</kbd>, <kbd>G</kbd>, <kbd>D</kbd> pour obtenir **δ**

<kbd>Compose</kbd>, <kbd>G</kbd>, <kbd>D + Shift</kbd> pour obtenir **Δ**

<kbd>Compose</kbd>, <kbd>F</kbd>, <kbd>B</kbd> pour obtenir **₿**
