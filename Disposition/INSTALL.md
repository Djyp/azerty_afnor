## Installation

Cette installation concerne uniquement les systèmes plus anciens donc la version de xkb est inférieure à 2.28.

L'installation se fait en trois étapes.

### Les symboles de base

Récupérez le fichier `fr` qui se trouve sur `/usr/share/X11/xkb/symbols/fr`.
Ajoutez-y le contenu de [fr_azerty_afnor](fr_azerty_afnor) à la fin.

### Ajouter la disposition dans la liste du système
Le fichier `/usr/share/X11/xkb/rules/evdev.xml` liste tous les agencements disponibles. Il associe le nom de la disposition (ici `azerty_afnor`) avec la langue (`fr`) et le nom du clavier (`Français (Azerty AFNOR)`).

Vous pouvez remplacer le votre par celui de de dépôt ou ajouter le contenur de `evdev_afnor_extract.xml`. Pour savoir où ajouter ces quelques lignes dans `evdev.xml`, il faut l'ajouter sous …
```
    <layout>
      <configItem>
        <name>fr</name>
        
        <shortDescription>fr</shortDescription>
        <description>French</description>
        <languageList>
          <iso639Id>fra</iso639Id>
        </languageList>
      </configItem>
      <variantList>
```
… et à côté des autres variantes. Je l'ai placé sous la variante French (Breton) mais elle aurait pu être n'importe où.

> [!NOTE]
> Si vous vous demandez pourquoi j'ai écrit «Français» au lieu de «French» c'est parce qu'en écrivant «French», ce mot n'était pas traduit dans la liste. J'ignore pourquoi mais au moins là on lit bien le nom de l'agencement en français.
