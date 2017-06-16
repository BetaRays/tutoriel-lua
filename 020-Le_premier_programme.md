# Le premier programme

On va commencer par tradition par le "Hello World!", c'est à dire un programme qui affiche "Hello World!", il y a deux moyens de le faire.

    print("Hello World!")

ou

    io.write("Hello World!")

Il y a quelques différences entre les deux mais on les verra plus tard.
Pour tester ce code, tapez le dans l'interpreteur Lua ou écrivez le dans un fichier et ouvrez le avec lua (`lua fichier.lua`).
Normalement ce code devrait avoir affiché "Hello World!".
Comme vous l'avez remarqué, j'ai mis le texte à afficher entre guillemets, c'est pour préciser que ce n'est pas du code, mais du texte (on verra ça plus en détail dans la partie sur les variables).
`print` et `io.write` servent à afficher du texte (`print` peut aussi afficher d'autres choses, on verra ça aussi avec les variables), c'est ce qu'on appelle des "_fonctions_", qu'on "_appelle_" ("_call_" en anglais) en général (je dis en général parce qu'il y a parfois un autre moyen, j'en parlerai avec les fonctions) avec des parenthèses et des "_arguments_" à l'intérieur (dans ce cas le texte "Hello World!").
Pour donner plusieurs arguments il faudrait les séparer par une virgule (",").

    print("Hello", "World") --> Hello	World

**NOTE:** L'espace après la virgule n'est pas necessaire.

Dans un code en Lua qui contient plusieurs "_instructions_", chaque instruction peut être écrite avec ou sans point-virgule à la fin et soit sur une ligne séparée soit sur une autre ligne avec une autre instruction (une ligne peut contenir n'importe quel nombre d'instructions), par exemple, les codes suivants sont équivalents.

    print("Bonjour !")
    print("Comment allez vous !")

    print("Bonjour !");
    print("Comment allez vous !");

    print("Bonjour !"); print("Comment allez vous !")

    print("Bonjour !") print("Comment allez vous !")

Même si la dernière façon est considérée "sale" par certaines personnes.

**NOTE:** L'espace entre les deux `print` des deux derniers exemples n'est pas necessaire parce qu'ils se terminent tout les deux par un caractère spécial (ici ")" et ";").

## Les commentaires

Les commentaires sont des morceaux de textes qui ne sont pas executés, en Lua les commentaires commencent par `--` (deux tirets).
Ils sont souvent utilisés pour expliquer un bout de code sans avoir à le relire (surtout si il est compliqué).

    print("Hello World!") --affiche Hello World!

fonctionne de la même façon que la dernière fois même avec le commentaire.
Ce n'est peut-être pas necessaire de mettre des commentaires sur chaque ligne, surtout quand on est habitué à print, mais c'était pour l'exemple.
Il existe aussi des commentaires "_multilignes_" qui commencent par `--[[` et se terminent par `--]]`.

    print("Hello World!")
    --[[
    Affiche Hello World!
    En hommage au premier programme.
    --]]

On peut aussi ajouter un tiret au premier pour décommenter toute la partie qu'il commente, c'est utile pour remettre un code qu'on avait commenté.

    ---[[
    print("Cette partie n'est pas commentée !")
    --]]

**NOTE:** Dans ce code les parties `---[[` et `--]]` ne font pas planter parce qu'elles sont commentées par les deux tirets.
