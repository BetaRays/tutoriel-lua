# Introduction

## Pourquoi choisir Lua

Lua est un language simple et rapide pour un language de script mais assez complet pour faire des programmes simples et est aussi très utilisé pour des "plug-ins".
En plus il fonctionne sur presque n'importe quelle plate-forme sur PC (comme windows, mac os, linux ou \*BSD), sur téléphone (comme iOS ou android) et même sur des consoles comme les nintendo ds ou les ps2.

## Installation

Dans ce tutoriel j'utiliserai Lua 5.3 (Lua 5.3.4 précisément mais n'importe quelle version 5.3 devrait marcher avec quelques différences mineures) et certaines choses peuvent ne pas fonctionner dans des versions plus anciennes ou plus récentes (si vous lisez ce tutoriel après la sortie de Lua 5.4 ou 6.0 (dans ce cas il manquera les nouveautés)).
[Lien de tous les binaires de Lua (pas besoin de compiler)](http://www.lua-users.org/wiki/LuaBinaries).
Si vous voulez ne rien télécharger, vous pouvez aussi essayer [la démo en ligne de Lua](https://www.lua.org/demo.html).

### Windows

Pour windows vous pouvez trouver des binaires (c'est plutôt compliqué de compiler sur windows) [ici](http://www.luabinaries.sourceforge.net) ou [là](https://sourceforge.net/projects/luabinaries/files/5.3.3/Tools%20Executables/lua-5.3.3_Win32_bin.zip/download) pour le lien de téléchargement direct de Lua 5.3.3 (32 bits).

### Mac Os

[Le lien que j'ai donné pour windows](http://www.luabinaries.sourceforge.net) contient aussi des binaires pour mac os mais vous pouvez aussi le compiler pour avoir la dernière version en suivant les instructions [sur le site de Lua](https://www.lua.org/download.html).
Je vous laisse [le lien direct de téléchargement d'un binaire Lua 5.3.2 pour mac os (la version la plus récente disponible actuellement en binaire)](https://sourceforge.net/projects/luabinaries/files/5.3.2/Tools%20Executables/lua-5.3.2_MacOS1011_bin.tar.gz/download).

### Linux

La plupart des distributions auront un paquet Lua dans leur gestionnaire de paquet (même des anciennes versions, par exemple j'ai `lua52` pour la dernière version de Lua 5.2 (5.2.4)).
Vous pouvez aussi le compiler comme pour mac os (il y a plus de chances que ça marche d'ailleurs) avec les instructions du [site de Lua](https://www.lua.org/download.html).
Sinon [le lien que j'ai donné pour windows](http://luabinaries.sourceforge.net) marche toujours.
Je ne peux pas donner de lien direct de Lua pour linux parce qu'il y a des versions différentes pour différents kernels mais je laisse au moins le [lien du dossier pour Lua 5.3.3](https://sourceforge.net/projects/luabinaries/files/5.3.3/Tools%20Executables/).

## Utiliser Lua

Une fois que vous avez installé Lua vous pouvez lancer l'interpreteur (il lancera ce que vous tapez automatiquement) en lancant `lua` (ou `lua.exe` pour windows) dans un terminal (il lance parfois automatiquement le terminal (mac os))
Pour ouvrir un terminal sur windows, ouvrez l'explorateur windows dans le dossier qui contient Lua et cliquez droit en enfoncant shift.
Sur linux la plupart des explorateurs de fichiers ont aussi cette fonctionnalité mais si vous avez installé Lua avec un gestionnaire de paquets (ou avec make install après avoir compilé) il suffit d'en ouvrir un n'importe où.
Après avoir ouvert le terminal au bon endroit vous pouvez taper `lua` pour lancer l'interpreteur ou `lua fichier.lua` pour lancer un fichier (dans ce cas un fichier qui s'appelle "fichier.lua").

### Un éditeur de texte

Pour programmer en Lua dans un fichier, c'est parfois plus simple d'utiliser un éditeur de texte qui colore certaines parties du texte (c'est plus lisible).
Pour windows je recommande [notepad++](https://notepad-plus-plus.org/fr/).
Pour mac os il y a [TextMate](https://macromates.com/) ou [Fraise](https://github.com/jfmoy/Fraise/downloads).
Pour linux vous avez peut-être déja un éditeur pour Lua comme [geany](geany.org), [Kate](https://kate-editor.org/) ou mousepad, sinon, vous pouvez toujours en installer un avec votre gestionnaire de paquets.
Il y a aussi un IDE appelé [Zerobrane Studio](https://studio.zerobrane.com/) (je ne l'ai pas essayé pour l'instant) et un [éditeur Lua pour eclipse](https://eclipse.org/ldt/) (qui est au départ un IDE pour java mais supporte aussi d'autres languages), les deux fonctionnent sur windows, mac os et linux.
Si vous voulez utiliser le même éditeur sur chaque plate-forme sans installer un IDE, il y a aussi [Atom](http://www.atom.io).
Vous pouvez aussi regarder [la liste des éditeurs pour Lua](http://lua-users.org/wiki/LuaEditorSupport).

**NOTE:** Les éditeurs que j'ai cité pour linux peuvent aussi fonctionner sur d'autres plate-formes, ils sont juste plus souvent utilisés pour linux.
