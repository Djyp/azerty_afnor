# Implémentation de la norme AFNOR
Norme publiée le 02 avril 2019
Inspiré de https://norme-azerty.fr/

## Contexte
Je suis développeur et formateur. Je suis aussi très intéressé par les dispositions des claviers, allez savoir pourquoi... Je ne suis cependant pas un expert de X11.
La doc de xkb étant ce qu'elle est, j'ai fait de mon mieux pour implémenter la nouvelle norme AFNOR pour mon système Linux.
Je me suis basé sur https://norme-azerty.fr/ qui détaille plutôt bien chaque touche. J'ai croisé les informations avec https://wayland-devel.freedesktop.narkive.com/N3rwOVoT/compose-and-dead-keys-support-in-libxkbcommon et la table de caractères.

J'ai copié-collé une disposition existante que j'ai adaptée.
Pour cette v0.1, il manque encore quelques aspects. Je partage mon implémentation avec la monde francophones, notamment pour ceux qui voudront terminer le travail.

## Versions

### v0.1
Implémentation rapide d'une base. Toutes les touches fonctionnent avec les combinaisons `SHIFT`, `ALT`, `SHIFT + ALT` sauf les touches MODE. Elles doivent permettre d'accéder à des symboles supplémentaires.
La touche Mode symbole monétaire (`ALT + F`) permet d'accéder à des caractères monétaires moins utilisés en Europe. £, $ et € sont bien sûr accessibles sans cette touche.
La touche Mode symbole micro (`ALT + G`) permet d'accéder à plusieurs lettre grecques, utiles notamment pour l'écriture scientifique.
La touche Mode symbole européen (`ALT + H`) permet d'accéder à plusieurs caractères utilisés dans les langues latines européennes.

### Versions v1.0
Pour une version complète il faudrait :
 - [ ] Implémenter le mode monétaire
 - [ ] Implémenter le mode micro
 - [ ] Implémenter le mode européen
 - [ ] Voir s'il est nécessaire de distinguer le symbole `TRAIT D'UNION` du symbole `MOINS`
 - [ ] Voir s'il est nécessaire de distinguer le symbole `BARRE COUVRANTE` du symbole `BARRE OBLIQUE COUVRANTE`
 - [ ] Changer le . en un vrai DOT BELOW dans la représentation (touche I)
 - [x] Pour plus de propreté, changer les tabulations en espaces

## Le code
Extrait de `/usr/share/X11/xkb/symbols/fr`

```
partial alphanumeric_keys
xkb_symbols "azerty_afnor" {
    name[Group1]="French (Azerty Afnor)";
    include "level3(ralt_switch)"

//    include "latin"
//    include "nbsp(level3)"

// LAYOUT OVERVIEW                              
//  ____ ____ ____ ____ ____ ____ ____ ____ ____ ____ ____ ____ ____ _______
// | # ̑ | 1 À| 2 É| 3 È| 4 Ê| 5 ˝| 6  ̏| 7  | 8 ―| 9 ‹| 0 ›| " ˚| ¨  | <--   |
// | @ ˘| à §| é ´| è `| ê &| ( [| ) ]| ‘ `| ’ _| « “| » ”| ' °| ^  ̌|       |
//  ========================================================================
// | |<-  | A Æ| Z  | E  | R  | T ™| Y  | U Ù| I .| O Œ| P ‰| – ‑| ± ‡|   , |
// |  ->| | a æ| z £| e €| r ®| t {| y }| u ù| i ˙| o œ| p %| - −| + †| <-' |   
//  ===================================================================¬    |
// |       | Q Θ| S ẞ| D  | F  | G  | H ̱̱ | J  | K  | L  | M  | \ √| ½ ¼|    |
// | MAJ   | q θ| s ß| d $| f ¤| g µ| hEu| j  | k ̸| l || m ∞| / ÷| * ×|    |
//  ========================================================================
// | ^   | > ≥| W Ʒ| X  | C Ç| V ̨ | B  | N  | ?  | !  ̦| …  | = ≠|     ^     |
// | |   | < ≤| w ʒ| x ©| c ç| v  ̧| b  ̵| n ~| . ¿| , ¡| : ·| ; ≃|     |     |
//  ========================================================================
// |      |      |      | SpaceNobreakspacefine |       |      |     |      |
// | Ctrl | Super| Alt  | Space    Nobreakspace | AltGr | Super|Menu | Ctrl |
//  ¯¯¯¯¯¯ ¯¯¯¯¯¯ ¯¯¯¯¯¯ ¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯¯ ¯¯¯¯¯¯¯ ¯¯¯¯¯¯ ¯¯¯¯¯ ¯¯¯¯¯¯

    // First row
    key <TLDE>  { [ at,             numbersign,     dead_breve,     dead_invertedbreve] };
    key <AE01>  { [ agrave,         1,              section,        Agrave            ] };
    key <AE02>  { [ eacute,         2,              dead_acute,     Eacute            ] };
    key <AE03>  { [ egrave,         3,              dead_grave,     Egrave            ] };
    key <AE04>  { [ ecircumflex,    4,              ampersand,      Ecircumflex       ] };
    key <AE05>  { [ parenleft,      5,              bracketleft,    dead_doubleacute  ] };
    key <AE06>  { [ parenright,     6,              bracketright,   dead_doublegrave  ] };
    key <AE07>  { [ U2018,          7,              dead_macron                       ] };
    key <AE08>  { [ U2019,          8,              underscore,     U2014             ] };
    key <AE09>  { [ guillemotleft,  9,              U201c,          U2039             ] };
    key <AE10>  { [ guillemotright, 0,              U201d,          U203a             ] };
    key <AE11>  { [ apostrophe,     quotedbl,       degree,         dead_abovering    ] };
    key <AE12>  { [ dead_circumflex,dead_diaeresis, dead_caron                        ] };

    // Second row
    key <AD01>  { [ a,        A,            ae,             AE          ] };
    key <AD02>  { [ z,        Z,            sterling                    ] };
    key <AD03>  { [ e,        E,            EuroSign                   ] };    
    key <AD04>  { [ r,        R,          registered                   ] };
    key <AD05>  { [ t,        T,          braceleft,      U2122        ] };
    key <AD06>  { [ y,        Y,          braceright                   ] };    
    key <AD07>  { [ u,        U,          ugrave,         Ugrave       ] };    
    key <AD08>  { [ i,        I,          dead_abovedot,  dead_belowdot] };    
    key <AD09>  { [ o,        O,          oe,              OE            ] };    
    key <AD10>  { [ p,        P,          percent,        U2030        ] };
    key <AD11>  { [ minus,    U2013,      minus,          U2011        ] };
    key <AD12>  { [ plus,    plusminus,    U2020,          U2021       ] };    

    // Third row
    key <AC01>  { [ q,          Q,  U03B8,  U0398                       ] };
    key <AC02>  { [ s,          S,  ssharp, Ssharp                      ] };
    key <AC03>  { [ d,          D,  dollar                              ] };    
    key <AC04>  { [ f,          F                                       ] };
    key <AC05>  { [ g,          G                                       ] };
    key <AC06>  { [ h,          H ] };
    key <AC07>  { [ j,          J                                       ] };
    key <AC08>  { [ k,          K,  dead_stroke                         ] };
    key <AC09>  { [ l,          L,  bar                                 ] };
    key <AC10>  { [ m,          M,  U221e                               ] };    
    key <AC11>  { [ slash,      backslash,  division,   U221a           ] };
    key <BKSL>  { [ asterisk,   onehalf,    multiply,   onequarter      ] };

    // Fourth row
    key <LSGT>  { [ less,       greater,    U2264,          U2265          ] };
    key <AB01>  { [ w,          W,          U01EF,          U01EE          ] };
    key <AB02>  { [ x,          X,          copyright                      ] };
    key <AB03>  { [ c,          C,          ccedilla,       Ccedilla       ] };
    key <AB04>  { [ v,          V,          dead_cedilla,   dead_ogonek    ] };    
    key <AB05>  { [ b,          B,          dead_stroke                    ] };
    key <AB06>  { [ n,          N,          dead_tilde                     ] };
    key <AB07>  { [ period,     question,   questiondown                   ] };
    key <AB08>  { [ comma,      exclam,     exclamdown,     dead_belowcomma] };
    key <AB09>  { [ colon,      ellipsis,   periodcentered                 ] };
    key <AB10>  { [ semicolon,  equal,      U2243,          notequal       ] };

    key <SPCE>  { [ space, space, nobreakspace, U202F ] };
};
```
