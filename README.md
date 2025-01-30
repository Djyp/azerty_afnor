# Implémentation de la norme AFNOR
Norme publiée le 02 avril 2019 dont les principales informations sont publiées sur https://norme-azerty.fr.

## Contexte
Je suis développeur et formateur. Je suis aussi très intéressé par les dispositions de claviers, allez savoir pourquoi... Je ne suis cependant pas un expert de X11. Je me suis empressé d'implémenter cette disposition dès avril 2019 et je l'utilise en permanence depuis.

La doc de xkb étant ce qu'elle est, j'ai fait de mon mieux. Je me suis basé sur https://norme-azerty.fr/ qui détaille plutôt bien chaque touche. J'ai croisé les informations avec https://wayland-devel.freedesktop.narkive.com/N3rwOVoT/compose-and-dead-keys-support-in-libxkbcommon et le standard unicode.

J'ai copié-collé une disposition existante dans le fichier `/usr/share/X11/xkb/symbols/fr` que j'ai adaptée.
Je partage mon implémentation avec le monde francophone, notamment pour ceux qui voudront terminer le travail.

Depuis octobre 2019, une implémentation de cette disposition existe dans toutes les distributions linux qui utilisent version ≥ 2.28 de [xkeyboard-config](https://gitlab.freedesktop.org/xkeyboard-config/xkeyboard-config). On peut donc dire à ce jour qu'elle est disponible partoutn
N'utilisez ma version que si vous souhaitez l'ajouter à un système plus ancien.

À ce jour, le 30 janvier 2025, quelques défauts apparaissent dans la version distribuée, notamment sur les trois touches MODE qui permettent d'accéder au mode monétaire, au mode lettres grecques et au mode caractères européens. Je souhaite donc documenter tout ce que je peux pour implémenter ces trois modes quitte à le faire avec XCompose.

## Installer la disposition pour Linux

Utilisez [ces instructions d'installation](Disposition/INSTALL.md) si vous avez un système qui date d'avant 2020.

Sinon, tout ce qui vous manque après avoir activé le clavier AFNOR dans votre système ce sont les modes. Tout est expliqué dans [le dossier Compose](Compose/INSTALL.md)
