# Les variables

Dans cette partie on va parler des variables "_globales_" (il y a aussi des variables locales mais on les verra après).

Une variable permet de stocker une valeur (qui peut être de plusieurs types, on verra ça juste après).
Pour "_définir_" (on peut aussi dire affecter et assigner) une variable globale (plus exactement sa valeur) on donne un nom (par exemple "texte") avec un `=` et la valeur qu'on veut lui attribuer (il peut y avoir des espaces avant et après le `=̀`), par exemple

    texte="Bonjour !"

Après ce code, quand on utilise `print` avec comme argument le nom de la variable (pas entre guillemets, pour préciser que c'est une variable et pas du texte), il affichera "Bonjour !", c'est comme ça qu'on donne la valeur d'une variable en argument.

    print(texte) --> "Bonjour !"

Le nom d'une variable peut être n'importe quelle combinaison de lettres (sans accents) majuscules, minuscules, de tirets bas ("\_") et de chiffres (du moment qu'il n'est pas le premier caractère), mais c'est une bonne idée en général de ne pas commencer un nom de variable par un tiret bas et par au moins une lettre minuscule parce que certains noms sont réservés à Lua (comme `_VERSION` qui contient un texte avec la version, comme "Lua 5.3").

On peut déclarer plusieurs variables sur la même ligne de cette façon (avec une "_affectation multiple_"):

    a,b = "arbre","bras"

On peut aussi utiliser cette syntaxe pour inverser deux ou plusieurs variables.

    a,b = "arbre","bras"
    print(a,b) --> arbre	bras
    a,b = b,a
    print(a,b) --> bras	arbre
    x,y,z = "xylophone","yaourt","zèbre"
    print(x,y,z) --> xylophone	yaourt	zèbre
    x,y,z = y,z,x
    print(x,y,z) --> yaourt	zèbre	xylophone

Une variable globale n'a pas besoin d'être "_déclarée_" à l'avance, c'est à dire qu'on peut l'utiliser sans avoir besoin de préciser qu'on veut utiliser le nom (contrairement à la plupart des languages compilés) et on peut redéfinir le type d'une variable en lui "_assignant_" une valeur d'un autre type.

L'interpréteur lua (en tout cas en version 5.3 normalement, pour les versions plus anciennes, vous pouvez ajouter un `=` avant) affiche les valeurs des variables quand vous entrez leurs noms, ça évite de taper print à chaque fois.

## Les types de variable

Il y a huit types de variables en Lua: les "_nils_", les booléens, les nombres, les "_strings_" (le texte), les "_userdata_", les fonctions, les "_thread_" (tâches), et les "_tables_".

On peut récuperer le type d'une variable avec la fonction `type` avec comme argument la variable, elle "_revoie_" (certaines personnes utilisent aussi retourne mais ça n'a pas beaucoup de sens en français) le type en tant que texte.

    print(type("Hello World!")) --> string

### Les _nils_

Un _nil_ en Lua ne peut avoir qu'une seule valeur (`nil`) et est utilisé quand une variable n'existe pas, par exemple

    print(nomDeVariableQuiNExistePas) --> nil

Ça permet de supprimer une variable, pour que sa valeur soit "_collectée_" (c'est à dire liberer la mémoire qu'elle utilise pour la laisser au système ou aux autres programmes), tout simplement en lui donnant la valeur `nil`.
### Les nombres
Les nombres sont un des type de variable les plus simple, en Lua il n'y a qu'un seul type de nombre (en fait 2 depuis la version 5.3, un pour les nombres entiers (_integers_) et un pour les nombres décimaux (_floats_), qu'on peut différencier avec `math.type` mais d'après [le manuel](https://www.lua.org/manual/5.3/manual.html#2.1) le programmeur peut ignorer leur différences).
Pour utiliser un nombre il suffit d'écrire le nombre en chiffres en remplacant la virgule (si il y en a une) par un point.

    n = 59
    print(n) --> 59
    n2 = 25.6
    print(n) --> 25.6
    n3 = -85.1
    print(n3) --> -85.1

#### Les opérateurs
Avoir des nombres serait inutile si on ne pouvait pas faire d'opérations dessus.

Les opérateurs basiques en Lua sont: `+` (addition), `-` (soustraction), `*` (multiplication), `/` (division), `%` ([modulo](https://fr.wikipedia.org/wiki/Modulo_(op%C3%A9ration\))) et `^` (puissance), il y a aussi `//` pour la division de nombre entiers (8/5=1.6 mais 8//5=1) mais c'est plus rare de l'utiliser.

Les opérateurs n'ont aucun effet sur les variables sans utiliser `=`.

    print(5*8) --> 40

    n=59
    n=n+9
    print(n) --> 68

    n=8
    print(8/n) --> 1
    print(n/5) --> 1.6
    print(n) --> 8

Le `-` peut être utilisé en tant qu'opérateur unaire (c'est à dire sur un seul élément au lieu de deux pour les autres) pour inverser le signe d'un nombre.

    n=852
    print(-n) --> -852
    print(n) --> 852
    n=-5
    print(-n) --> 5

Les opérateurs ont une précédence, leurs opérations sont executées dans un certain ordre (`*` avant `+` par exemple) mais on peut changer leur ordre avec des parenthèses (les opérations entre parenthèses seront executées avant celles qui ne le sont pas), en Lua, toutes les opérations vont de la gauche vers la droite par défaut, sauf pour `^` et `..`.

    print(2/3/5) --> 0.13333333333333
    print((2/3)/5) --> 0.13333333333333
    print(2/(3/5)) --> 3.3333333333333
    print(2^2^3) --> 256.0
    print((2^2)^3) --> 64.0
    print(2^(2^3)) --> 256.0

Voici la liste complète de la précédence des opérateurs avec les plus importants en premier et les moins importants en dernier (il y a des opérateurs qu'on a pas vu pour l'instant) :

     ^
     opérateurs unaires (not   #     -     ~)
     *     /     //    %
     +     -
     ..
     <<    >>
     &
     ~
     |
     <     >     <=    >=    ~=    ==
     and
     or

#### La fonction tonumber

La fonction `tonumber` permet de convertir explicitement un autre type (notamment du texte) en nombre (elle revoie l'argument si c'est déja un nombre), je dis explicitement parce que du texte peut être utilisé comme nombre sans `tonumber`.

    print(tonumber("58")+8) --> 66
    print("58"+8) --> 66

#### Les "_blocs_" _for_ numériques

Il y a deux types de blocs _for_ (aussi appelés boucles _for_), le _for_ numérique et le _for_ générique, pour l'instant on va parler du premier.

Un for numérique se construit de la façon suivante :

    for variable = debut, fin, pas do
      --faire quelque chose
    end

Dans cet exemple la variable 'variable' commence par 'debut' en avançant de 'pas' jusqu'a 'fin', donc avec un exemple plus concret :

    for i = 1,10,2 do
      print(i)
    end

Ici, 'i' commence à 1 en augmentant de 2 jusqu'a 10 (qui n'est pas affiché parce qu'il ne passe pas par 10, il passe de 9 à 11).

Le troixième argument est optionnel et est égal à un quand il n'est pas précisé.

    for i = 1,10 do
      print(i)
    end

Dans ce cas i commence à 1 jusqu'a 10 (cette fois inclus parce qu'il passe par 10).

#### La "_bibliothèque_" math

Ce qu'on appelle une bibliothèque ("_library_" en anglais) c'est tout simplement un ensemble de fonctions et de constantes qui sont en Lua, rangés dans des _tables_ (qu'on verra plus tard) ce qui permet de les utiliser de cette façon : `nomDeLaBibliotheque.nomDeLaFonction(arguments)`, comme pour `io.write`.

`math.floor`, `math.ceil` et `math.modf` permettent d'arrondir des nombres.

    print(math.floor(5.6)) --> 5
    print(math.floor(5.3)) --> 5
    print(math.floor(-5.4)) --> -6
    print(math.ceil(5.4)) --> 6
    print(math.ceil(5.8)) --> 6
    print(math.ceil(-5.6)) --> -5
    print(math.modf(5.4)) --> 5
    print(math.modf(5.6)) --> 5
    print(math.modf(-5.4)) --> -5
    print(math.modf(-5.6)) --> -5

`math.huge` est une constante représentant le plus grand nombre représentable en Lua.

    print(math.huge) --> inf

Le texte "inf" représente les trois premières lettres de "infinity" (infini en anglais).

`math.pi` est une constante contenant le nombre pi (&#960;).

    print(math.pi) --> 3.1415926535898

`math.deg` et `math.rad` convertissent des radians en degrées et des degrées en radians, respectivement.

    print(math.rad(90)) --> 1.5707963267949
    print(math.deg(math.pi)) --> 180.0

`math.sin`, `math.cos`, `math.tan`, `math.asin`, `math.acos` et `math.atan` représentent les fonctions trigonométriques du même nom, en radians.

    print(math.cos(math.pi)) --> -1.0
    print(math.sin(math.rad(90))) --> 1.0
    print(math.atan(1)*4) --> 3.1415926535898

`math.random` génère un nombre aléatoire par rapport à une "_seed_" (par défaut 1), en utilisant la même _seed_, les nombres seront les mêmes à chaque redémarrage de lua.

 * En utilisant `math.random` sans arguments, il prendra un nombre aléatoire entre 0 et 1 (avec virgule).
 * Avec un argument, il le choisira entre 1 et l'argument donné (sans virgule).
 * Avec deux arguments, le nombre sera entre le premier et le deuxième argument (sans virgule).

`math.randomseed` permet de changer la _seed_ de `math.random`

    print(math.random()) --> 0.84018771676347
    print(math.random()) --> 0.39438292663544
    print(math.random(6)) --> 5
    print(math.random(6)) --> 5
    print(math.random(6)) --> 6
    print(math.random(-50,50)) --> -31
    print(math.random(-50,50)) --> -17
    print(math.random(-50,50)) --> 27
    math.randomseed(58)
    print(math.random()) --> 0.93766735633835

Une technique pour avoir une _seed_ différente à chaque fois est d'utiliser le retour de la fonction `os.time` en argument à randomseed, parce que `os.time` donne le temps, le résultat devrait toujours être différent.

    math.randomseed(os.time())

**NOTE:** Ce n'est pas nécessaire d'utiliser `print` pour appeller des fonctions mais je l'ajoute pour afficher leurs résultats pour ceux qui n'utiliserait pas l'interpreteur.

### Le texte

Pour utiliser du texte il suffit de l'écrire entre guillemets (`"`) en peut aussi utiliser le caractère `'` ou alors, si le texte fait plusieurs lignes on peut utiliser les "_long strings_", c'est à dire commencer le texte par `[[̀` et le terminer par `]]` (un peu comme pour les commentaires multilignes).

    print("texte1") --> texte1
    print('texte2') --> texte2
    print([[texte
    de
    plusieurs
    lignes]])

On peut aussi utilser du texte multiligne de différents niveaux (`[[` et `]]` étant le niveau 0), les niveaux fonctionnent aussi avec les commentaires multilignes.

    --niveau 1
    print([=[
    print([[texte
    de
    plusieurs
    lignes]])
    ]=])
    --niveau 4
    print([====[
    print([=[texte
    de
    plusieurs
    lignes]=])
    ]====])

Il n'y a aucune différence entre les différents niveaux à part le fait qu'un niveau ne peut se fermer qu'avec le même niveau (niveau 4 avec niveau 4 seulement par exemple), c'est donc utile pour avoir du texte long qui contient du texte long.
En général on décide du caractère (entre `"` et `'`) par rapport au texte (si il y a des guillemets on peut utiliser `'` par exemple).

Pour lire du texte de l'utilisateur, on peut utiliser `io.read` qui attend qu'un utilisateur tape quelque chose et appuie sur entrée puis revoie le texte que l'utilisateur a tapé.

#### L'échappement

Si on veut utiliser certains caractères qu'on ne peut pas utiliser normalement, on peut utiliser des "_escapes_" qui commencent par un anti-slash (\\).

* \a [caractère d'appel](https://fr.wikipedia.org/wiki/Caract%C3%A8re_d%27appel)
* \b retour arrière
* \f saut de page
* \n saut de ligne
* \r retour chariot
* \t tabulation
* \v tabulation verticale
* \\\\ anti-slash
* \" guillemet
* \' apostrophe

<!-- -->

    print("\"") --> "
    print("\\") --> \
    print("tex\nte")
    --[[même chose que
    [[tex
    te]]
    --]]

#### Les opérateurs sur le texte

En lua il y a deux opérateurs pour le texte: `..` pour la concaténation (mettre du texte à la suite d'un autre) et l'opérateur unaire `#` pour connaitre la longueur du texte (pour le texte avec des caractères non anglais il y a une fonction expliquée à la fin du chapitre "La "bibliothèque" string").

    print("1".."2") --> 12

    print(#"texte") --> 5
    t = "texte2"
    print(#t) --> 6

#### La fonction tostring

La fonction `tostring` permet de convertir d'autre types de variables en texte (print utilise tostring sur chaque argument).
Un nombre peut être utilisé en tant que texte.

    print("texte"..tostring(58)) --> texte58
    print("texte"..58) --> texte58
    print(tostring(nil)) --> nil
    print(nil) --> nil

#### La bibliothèque string

Comme pour les nombres, il y a une bibliothèque pour modifier le texte appelée "string".

`string.rep` permet de répeter un texte un certain nombre de fois, par exemple

    print(string.rep("abc", 3)) --> abcabcabc

`string.reverse` permet d'inverser du texte, par exemple

    print(string.reverse("du texte"))) --> etxet ud

`string.lower` et `string.upper` permettent de mettre toutes les lettres en minuscules et en majuscules respectivement.

    print(string.lower("AbCd")) --> abcd
    print(string.upper("AbCd")) --> ABCD

`string.sub` permet de récuperer une partie de texte, le premier caractère est 1, le deuxième 2, etc...
On peut aussi l'utiliser avec des nombres négatifs, c'est à dire que le dernier caractère est -1, l'avant-dernier -2, etc...

    print(string.sub("texte59", 1, 5)) --> texte
    print(string.sub("texte59", -2 -1)) --> 59
    print(string.sub("texte59", -1 -2)) -- ne fonctionne pas dans ce sens

`string.find` cherche un "_pattern_" dans du texte et revoie deux valeurs, le premier caractère qu'il trouve faisant partie du _pattern_ et le dernier (il faut savoir qu'il s'arrête au premier pattern trouvé) ou revoie simplement `nil` si rien n'a été trouvé.

    print(string.find("ENCORE du texte", "texte")) --> 11	15
    print(string.find("eeee", "e")) --> 1	1
    print(string.find("aaa", "b")) --> nil

`string.gsub` remplace un _pattern_ par un autre texte et revoie le nouveau texte et le nombre de substitutions effectuées.

    print(string.gsub("texte", "x", "y")) --> "teyte"	1

`string.byte` convertit chaque caractère (plus exactement octet) en nombre et `string.char` fait l'inverse.

    print(string.byte("a")) --> 97
    print(string.char(97)) --> a
    print(string.byte("xyz")) --> 120
    print(string.byte("xyz", 2)) --> 121
    print(string.byte("xyz", 3)) --> 122
    print(string.char(120, 121, 122)) --> xyz

`string.format` permet de "formater" du texte, je pense qu'un exemple sera plus simple.

    print(string.format("texte%d", 58)) --> texte58
    print(string.format("%f : %.2f", 56.2, 89.1)) --> 56.200000 : 89.10
    print(string.format("[[%s]]", "texte")) --> [[texte]]
    print(string.format("%q", '"')) --> "\""

Chaque "option" (qui commencent par "%") est remplacée par un argument, par exemple dans

    string.format("%d", 58)

le premier "%d" est remplacé par le deuxième argument (parce que le premier est toujours le texte).

Voici une liste non-exhaustive des options pour `string.format` :

 * "%d" : est remplacé par un nombre entier, en rajoutant "." suivi d'un nombre entre "%" et "d", on peut changer le nombre de chiffres, par exemple avec "%.3d", le nombre aura au moins trois chiffres (en ajoutant des zéros à gauche si necessaire).
 * "%f" : est remplacé par un nombre à virgule avec par défaut 6 chiffres après la virgules (en rajoutant des zéros si necessaire), le nombre de chiffres après la virgule peut être changé en ajoutant "." et le nombre de chiffres après la virgule entre "%" et "f".
 * "%s" : est remplacé par du texte.
 * "%q" : _(spécifique à lua)_ comme "%s" mais utilise les séquences d'échappement (pour prendre du texte inconnu et le mettre dans un script, par exemple).

D'après [le manuel](https://www.lua.org/manual/5.3/manual.html#pdf-string.format), pour `string.format`, Lua utilise la fonction sprintf du C avec quelques différences, les options sont donc documentées dans un manuel de C (comme [celui-là](http://man7.org/linux/man-pages/man3/printf.3.html)).

Il faut noter que les fonctions de cette bibliothèque ne modifient pas vos variables.

    s="abc"
    string.rep(s, 3) --revoie abcabcabc
    print(s) --> abc

Si on voulait changer une variable on pourrait l'écrire de cette façon par exemple :

    s = string.rep(s, 3)

On peut aussi utiliser dans le cas de la bibliothèque string une autre syntaxe.

    s="AbCd"
    print(s:upper()) --> ABCD
    print(s) --> AbCd

    print(("t"):byte()) --> 116

Dans ce cas on utilise upper en tant que "_méthode_" sur s.
Utiliser les fonctions de la bibliothèque string en tant que méthodes ne fonctionnera que sur des variables contenant du texte ou du texte mis entre parenthèses (Lua plante sans elles).

Si vous utilisez des lettres hors de la table ACSII (des caractères qui n'éxistent pas en anglais, comme 'é' ou 'ç'), la plupart fonctions de la bibliothèque string fonctionneront toujours (comme `string.rep`), mais pour les autres vous pouvez utiliser la biliothèque utf8.

    print(#"dernière") --> 9
    print(utf8.len("dernière")) --> 8

    print(string.byte("français", 5)) --> 195
    print(string.char(195)) --caractère qui n'existe pas
    print(utf8.codepoint("français", 5)) --> 231
    print(utf8.char(231)) --> ç

`utf8.len` peut aussi permettre de vérifier si du texte UTF-8 est correct, si il ne l'est pas il revoie `false` (un booléen, on les verra juste après) et la position de l'octet invalide.

Les fonctions de la bibliothèque string (et aussi certaines d'utf8, comme `utf8.codepoint`) pensent que les positions sont données en octets, ce qui peut être utile parfois, mais peut aussi causer certains problèmes avec l'UTF-8.

    print(string.byte("résumé", 3)) --> 169
    print(string.char(169)) --caractère qui n'éxiste pas

On peut donc utiliser `utf8.offset` pour le texte qui contient des caractères UTF-8.

    s = "résumé"
    print(string.byte(s, utf8.offset(s, 3))) --> 115
    print(string.char(115)) --> s

### Les booléens

Les booléens (_booleans_ en anglais) ne peuvent avoir que deux valeurs, vrai (_true_) et faux (_false_) pour savoir par exemple si un nombre est supérieur à un autre, et servent en général à indiquer si le programme doit passer par un bout de code ou non (avec les blocs "_if_" qu'on verra plus tard dans ce chapitre).

Une valeur qui n'est pas un booléen peut être utilisé comme tel, elle vaudra faux si elle est égale à `nil` (ou `false`, bien sur), sinon elle vaudra vrai.

#### Les opérateurs

Il y a trois opérateurs agissant sur deux booléens `and`, `or` et `not`.

`not` inverse un booléen.

    print(not true) --> false
    print(not false) --> true
    print(not not true) --> true
    print(not not false) --> false

`and` prend deux booléens et donne uniquement vrai comme résultat si les deux booléens sont vrai.

    print(true and true) --> true
    print(false and false) --> false
    print(true and false) --> false
    print(false and true) --> false

`or` prend deux booléens et donne vrai comme résultat si un des deux booléens est vrai.

    print(true or true) --> true
    print(false or false) --> false
    print(true or false) --> true
    print(false or true) --> true

En fait `and` et `or` ne fonctionnent pas exactement comme ça (ce qui permet de les utiliser avec d'autres types), même si les résultats sont les mêmes, mais c'est plus simple de penser comme ça pour deux booléens ou quand le résultat est utilisé comme un booléen.

`and` donne la valeur de gauche si elle vaut faux et donne la valeur de droite si celle de gauche vaut vrai.

    print(10 and 5) --> 5
    print(nil and 7) --> nil
    print(5 and false) --> false

`or` donne la valeur de gauche si elle vaut vrai et donne la valeur de droite si la valeur de gauche vaut faux.

    print(10 or 5) --> 10
    print(nil or 7) --> 7
    print(false or "texte") --> texte
    print(5 or false) --> 5

`and` et `or` évaluent les expressions uniquement si necessaire.

    5 or print("test") --rien
    5 and print("test") --> test

Même si ce n'est pas necessaire de se souvenir de la façon exacte dont `and` et `or` fonctionne, il y a deux utilisations qui peuvent être utiles.

`x=x or v` change x en v si x est faux.

    a = 5
    a=a or 85
    print(a) --> 5
    b = nil
    b=b or 85
    print(b) --> 85

`a and b or c` (fonctionne uniquement si b vaut vrai) si a vaut vrai alors b est renvoyé, sinon c'est c qui est renvoyé.

    print(true and 9 or 4) --> 9
    print(false and 7 or 0) --> 0

`not` peut aussi fonctionner avec d'autres valeurs que des booléens.

    print(not nil) --> true
    print(not 57) --> false
    print(not not nil) --> false
    print(not not "texte") --> true

**NOTE:** On peut utiliser `not not` pour transformer une valeur en booléen (par rapport à ce qu'elle "vaut"), mais c'est rarement utile car la plupart du temps les valeurs peuvent être utilisées comme un booléen sans conversion.

##### Les opérateurs de comparaison

Les opérateurs relationnels comparent deux valeurs.

`==` vérifie si deux valeurs sont égales.

    print(5==5) --> true
    print("texte"==nil) --> false
    print(5==5.684) --> false

`~=` est la négation de `==`, donc `a~=b` est équivalent à `not (a==b)` (parce que not est plus important que ==, voir précédence des opérateurs).

`<`, `>`, `<=` et `>=` vérifient si la première valeur est inférieure, supérieure, inférieure ou égale et supérieure ou égale à la deuxième respectivement, ils peuvent être utilisés sur des nombres ou pour comparer du texte par ordre alphabethique.

    print(5 < 8) --> true
    print(6 < 5) --> false
    print(5.6 > 5.4) --> true
    print(-85 > 86) --> false
    print(85 >= 65) --> true
    print(85 > 65) --> true
    print(85 < 65) --> false
    print(85 <= 65) --> true
    print(25 >= 25) --> true
    print(25 <= 25) --> true
    print("a" < "b") --> true
    print("test" > "texte") --> false

#### Les "_blocs_" _if_

Un bloc est un bout de code (en général "_indenté_" en ajoutant deux espaces au début de chaque ligne du bloc en lua, ou quatres si c'est un bloc dans un autre, ...) qui peut être lancé avec une condition (_if_), répété (_while_, _for_, _repeat-until_), un bloc joue aussi un rôle pour les variables locales.

Un bloc _if_ est executé uniquement si une condition est vraie, il se contruit de la façon suivante :

    if bool then
      --faire quelque chose
    end

Dans cet exemple bool est une variable, le bloc est uniquement executé si bool vaut vrai.
On utilise en général comme condition une opération de comparaison.

    if #io.read()>5 then
      --L'utilisateur à tapé plus de 5 caractères (octets)
    end

**NOTE:** On aurait aussi pu utiliser `utf8.len` au lieu de `#` pour récuperer le nombre de caractères dans n'importe quelle langue.

On peut aussi ajouter un _else_ avant le _end_ pour executer du code quand la condition est fausse.

    io.write("Entrez votre age: ")
    if tonumber(io.read())>=18 then
      io.write("Vous êtes majeur\n")
    else
      io.write("Vous êtes mineur\n")
    end

Si on veut combiner le _else_ et le _if_ sans avoir besoin d'ajouter beaucoup de _end_, on peut utiliser _elseif_, qui peut être utilisé de cette façon :

    n = tonumber(io.read())
    if n>0 then
      io.write(n.." est positif\n")
    elseif n<0 then
      io.write(n.." est négatif\n")
    else
      io.write("0\n")
    end

#### Les blocs _while_

Les blocs _while_ (aussi appelés boucles _while_) fonctionnent de la même façon que les blocs _if_ sauf que quand la condition est vraie une deuxième fois il réexecute le code.

    reponse = io.read()
    while reponse~="non" and reponse~="oui" do
      io.write("Merci d'entrer oui ou non: ")
      reponse = io.read()
    end
    --faire quelque chose avec la réponse

**NOTE:** On aurait pu utiliser `string.lower` sur la réponse pour que le code fonctionne quand quelqu'un ajoute une majuscule au début (ou n'importe où).

#### Les blocs _repeat-until_

Si on voulait faire une ligne de commande interactive (un peu comme celui de lua), on aurait pu utiliser _repeat-until_.
Avec _repeat-until_ ("répète jusqu'à" traduit en français, ou "répète jusqu'à ce que" pour être plus compréhensible), la condition est évaluée à la fin et le code à l'intérieur est donc executé au moins une fois, c'est donc très utile dans certaines situations (comme un programme interactif).

    repeat
      io.write("Entrez un nombre: ")
      v=io.read()
    until tonumber(v)~=nil
    --faire quelque chose avec le nombre

**NOTE:** le `~=nil` est totalement optionnel car le `nil` vaut faux.

Dans un vrai programme totalement interactif on aurait certainement une structure différente, mais pour demander quelques valeurs au début du programme, ou pour demander si il doit redémarrer, c'est utile.

### Les _tables_

La définition correcte d'une _table_ serait de dire que c'est un tableau associatif avec n'importe quelle valeur, c'est à dire qu'on peut associer une valeur à une clé qui permettra de la récuperer plus tard.

Pour créer une _table_ il faut utiliser un constructeur de table, toujours entre accolades `{` et `}`, pour faire une _table_ vide le constructeur est vide aussi (`{}`).

    print({}) --> table: 0x01234567

L'"_adresse_" (0x01234567) sera différente pour vous, chaque nouvelle _table_ devrait avoir une addresse différente.
Les opérateurs de comparaison fonctionnent par rapport aux adresses des _tables_ (les valeurs fonctionnant de cette façon sont appellés "_objets_" et les variables sockent uniquement la "_référence_" à l'objet (l'addresse), pas l'objet lui même), donc :

    print({} == {}) --> false

On peut donc utiliser une table comme une clé unique dans une autre, c'est surtout utile pour avoir une clé spécifique à un morceau de code sans avoir de chances d'utiliser la même dans une autre partie du programme de façon classique.

Pour modifier des valeurs d'une _table_ on peut faire de cette façon `table[cle] = valeur` et `table[cle]` pour récuperer la valeur.

    t = {}
    t[5] = "texte"
    print(t[5])
    t["clé"] = 9999
    print(t["clé"]) --> 9999

En essayant d'accéder à une valeur qui n'existe pas on récupère un _nil_, comme pour les variables.

    t = {}
    print(t[85]) --> nil

Un _nil_ ne peut pas servir de clé pour une _table_.

#### Les constructeurs de _tables_

On peut rajouter des valeurs dans un constructeur de _tables_, séparées par des virgules (,) ou des points-virgules (;), il n'y a aucune différence entre les deux (même si on utilise en général les points-virgules pour séparer différents types de clés ou des valeurs qui n'ont rien à voir ou ne sont pas utilisées de la même façon), qui prendront par défaut comme clé un nombre commençant par 1 et augmentant à chaque fois.

    t = {"a", "b"; "c"}
    print(t[1]) --> a
    print(t[2]) --> b
    print(t[3]) --> c

On peut préciser les clés des valeurs de cette façon :

    t = {[58] = 25, ["t"] = -12, [true] = "texte"}
    print(t[58]) --> 25
    print(t["t"]) --> -12
    print(t[true]) --> texte

Les deux façons peuvent être utilisées en même temps mais les valeurs ayant des clés non précisées peuvent remplacer les autres.

    t = {"a", [3]="b", "c", "d", [5]="e"}
    print(t[1]) --> a
    print(t[2]) --> c
    print(t[3]) --> d
    print(t[4]) --> nil
    print(t[5]) --> e
    print(t[6]) --> nil

On peut utiliser les opérateurs pour la valeur.

    t = {3+2}
    print(t[1]) --> 5

On peut aussi utiliser le texte en clé plus rapidement.
Dans les constructeurs :

    t = {test = 852}
    print(t["test"]) --> 852

Pour accéder à la valeur :

    t = {["test"] = 765}
    print(t.test) --> 765

Dans ces exemples, si il y a une valeur appelée test, elle ne changera rien au fonctionnement de la _table_.

    test = 850
    t = {test = 250}
    print(t.test) --> 250
    print(test) --> 850
    test = 230
    print(t.test) --> 250

C'est ce qu'on utilise pour les bibliothèques, au passage.

Une _table_ est totalement indépendante d'une autre.

    a = {}
    b = {}
    a[5] = true
    b[4] = false
    print(b[5]) --> nil
    print(a[5]) --> true
    print(b[4]) --> false
    print(a[4]) --> nil

On peut quand même utiliser la valeur d'une variable en tant que clé ou valeur.

    a = "texte"
    b = -852
    t = {[a] = b}
    print(t[a]) --> -852

Il faut faire attention à la différence entre `{test = 852}` pour raccourcir l'utilisation du texte et `{[test] = 852}` pour utiliser une variable en tant que clé.
Il faut aussi faire attention au au fait que dans `{1 = 85}` la clé n'est pas un nombre, mais du texte alors que la valeur est bien un nombre.

    t = {5 = 820}
    print(t[5]) --> nil
    print(t["5"]) --> 820
    print(type(t["5"])) --> number

#### Les tableaux et listes

Les tableaux (_arrays_ en anglais) sont juste une utilisation spéciale des _tables_ avec des nombres entiers en clés.
Il y a des différences entre tableau et listes dans la plupart des autres languages de programmation (les tableaux on une longueur définie alors que les listes non) mais pas en Lua, j'utiliserais le mot tableau pour parler de tableaux, listes ou séquences.

Supposont que nous voulons stocker 10 valeurs, comme des notes, au lieu d'utiliser 10 variables (ce serait très long) on peut tout simplement utiliser un tableau.

    notes = {15,17,14,16,18,14,12,16,13,20}
    print(notes[1]) --> 15
    print(notes[2]) --> 17
    print(notes[3]) --> 14
    print(notes[4]) --> 16
    print(notes[5]) --> 18
    print(notes[6]) --> 14
    print(notes[7]) --> 12
    print(notes[8]) --> 16
    print(notes[9]) --> 13
    print(notes[10]) --> 20

Ce constructeur à justement été prévu pour les tableaux.

L'opérateur `#` permet de récuperer la taille d'un tableau (donc son dernier élément non nil), donc pour le tableau notes de tout à l'heure :

    print(#notes) --> 20

On peut aussi utiliser les boucles _for_ numériques pour afficher tous les valeurs d'un tableau.

    for i=1,#tableau do
      print(tableau[i])
    end

Dans ce cas il y a aussi un équivalent en boucle _for_ génériques.

    for i,v in ipairs(tableau) do
      print(v)
    end

`ipairs` est un itérateur, j'en parlerais plus tard.
Il y a aussi un intérateur `pairs` qui fonctionne de la même façon mais avec tout type de clés.

**NOTE:** Quand on utilise `pairs` ou `ipairs` de cette façon, on "_itère_" sur une table (ou un tableau dans le cas de `ipairs`).

#### Les ensembles

Un ensemble (_set_ en anglais) en Lua est surtout une utilisation particulière des _tables_, comme pour les tableaux.

Dans un ensemble, les valeurs attachées aux clés sont toujours `true`, et on utilise seulement les valeurs pour naviguer dedans (avec `pairs`).

    set = {
      chien = true
      chat = true
      cheval = true
    }
    
    for v in pairs(set) do
      print(v)
    end

Ce code affichera "chien", "chat" et "cheval" mais dans un ordre indéfini.

**NOTE:** D'habitude on utilise deux valeurs pour `pairs` (un pour la clé et l'autre pour la valeur), mais ici les valeurs ne nous intéressent pas, on cherche uniquement à récuperer la clé, donc j'ai omis la deuxième variable.

#### La bibliothèque table

La bibliothèque table est surtout utilisée pour les _tables_ utilisées en tant que tableaux, même si elle s'appelle table et pas array ou list.

`table.sort` permet de trier un t, il ne peut fonctionner que si la _table_ contient uniquement des nombres ou uniquement des _strings_.

    t = {8,6,1}
    table.sort(t)
    print(t[1]) --> 1
    print(t[2]) --> 6
    print(t[3]) --> 8
    t2 = {"def", "test", "abc", "texte"}
    table.sort(t2)
    print(t2[1]) --> abc
    print(t2[2]) --> def
    print(t2[3]) --> test
    print(t2[4]) --> texte

`table.insert` permet d'ajouter un élément dans une _table_ utilisée comme un tableau à une certaine position (par défaut à la fin) en bougeant les éléments vers le haut si necessaire.

    t = {}
    table.insert(t, 852)
    print(t[1]) --> 852
    table.insert(t, true)
    print(t[1]) --> 852
    print(t[2]) --> true
    table.insert(t, 1, "texte")
    print(t[1]) --> texte
    print(t[2]) --> 852
    print(t[3]) --> true

`table.remove` fait l'inverse de `table.insert`, il enlève des éléments et les revoie.

    t = {85, true, "texte", {}}
    print(t[1]) --> 85
    print(t[2]) --> true
    print(t[3]) --> texte
    print(t[4]) --> table: 0xaaaaaaaa
    print(table.remove(t)) --> table: 0xaaaaaaaa
    print(t[4]) --> nil
    print(table.remove(t,2)) --> true
    print(t[1]) --> 85
    print(t[2]) --> texte
    print(t[3]) --> nil

`table.concat` utilise l'opérateur `..` sur tout les éléments d'une _table_ utilisée en tant que tableau.
`table.concat` ne modifie pas la _table_ mais renvoie le résultat.

    t = {85, "texte", tostring(true)}
    print(table.concat(t)) --> 85textetrue

TODO: peut-être ajouter table.move

**NOTE:** contrairement aux fonctions des bibliothèques string et math, les _tables_ sont directement modifiées (parce que les _tables_ sont des objets et qu'elles peuvent être modifiées à partir d'une fonction).

### Les fonctions

Une fonction fonctionne à peu près comme un bloc en précisant en plus les nom des variables contenant les arguments entre parenthèses, mais doit être récuperée dans une variable.

    f = function(argument1, argument2)
      --faire quelque chose
    end

Il y a aussi un autre moyen qui donne exactement le même résultat.

    function f(argument1, argument2)
      --faire quelque chose
    end

**NOTE:** Les valeurs faites à partir de `function` sont appelées "_closures_" (ou fermeture en français).

Les arguments peuvent être de n'importe quel type, il faut donc vérifier le type avant si on s'attend à un type en particulier.

    function f(nombre)
      if type(nombre)~="number" then
        error("bad argument #1 to 'f' (number expected, got "..type(nombre))
      end
      --faire des choses avec le nombre
    end

Ici j'utilise la fonction `error` pour générer une erreur, et je reprend le message d'erreur de ̀`math.cos`, les erreurs ressemblent en général à ça en Lua.
On pouvais aussi utiliser l'équivalent avec la fonction `assert` qui appelle erreur avec son deuxième argument si le premier vaut faux.

    function f(nombre)
      assert(type(nombre)=="number", "bad argument #1 to 'f' (number expected, got "..type(nombre))
      --faire des choses avec le nombre
    end

**NOTE:** On peut aussi pointer l'erreur quelque part avec un autre argument à `error`, c'est plutot bien expliqué sur [le manuel de Lua](https://www.lua.org/manual/5.3/manual.html#pdf-error), `assert` ne permet pas encore de le faire.

Pour appeller une fonction on peut utiliser le nom de la fonction avec les arguments entre parenthèses ou des parenthèses vides si il n'y en a pas.

    f(1,2)
    f()

Mais aussi sans parenthèses quand il y a un argument et que cet argument est un constructeur de _table_ ou du texte (pas des noms de variables).

    print "Hello World"
    print{} --> table: 0x99999999

On peut notamment utiliser cette façon de faire avec des _tables_ pour avoir des arguments avec des noms.

    f{x=85,y=63}

Quand la fonction est appelée avec moins d'argument que prévu, les valeurs des arguments non précisés sont égaux à `nil` et si elle est appelée avec plus d'arguments, les arguments en plus seront ignorés.

    function p(valeur)
      print(valeur)
    end
    
    p() --> nil
    p("texte", 8520) --> texte

Pour renvoyer une valeur, il suffit d'utiliser `return` avec les valeurs à renvoyer, séparées par des virgules si il y en a plusieurs.

    function f()
      return -8520,math.pi,"texte"
    end
    
    print(f()) --> -8520	3.1415926535898	texte

`return` arrête aussi l'execution de la fonction et ne peut être que la dernière instruction dans un bloc (si on a vraiment besoin d'utiliser un `return` en plein mileu d'un bloc sans executer la suite on peut utiliser un bloc _do end_ dont je parlerai dans la partie sur les portées de variables).
On peut utiliser cette propriété avec un `return` vide pour arrêter l'execution d'une fonction, le résultat est presque le même qu'en utilisant `return nil`.

    function f(valeur)
      if valeur then
        return
      end
      print(valeur)
    end

Ce n'est pas necessaire d'utiliser un `return` à la fin d'une fonction car il y a un `return` vide implicite à la fin de chaque fonction (juste avant le `end` de la fonction).

Pour récuperer plusieurs valeurs qu'une fonction retourne, on peut tout simplement utiliser une affectation multiple.

    function f()
      return 5,8
    end
    
    a,b = f()
    print(a,b) --> 5	8

Si la fonction renvoie moins d'éléments que le nombre de variable, alors les variables en plus auront la valeur `nil` et si elle en renvoie plus, alors les valeurs en trop sont ignorées.

    function f()
      return 5,8
    end
    
    a = f()
    print(a) --> 5
    b,c,d = f()
    print(b,c,d) --> 5	8	nil

Une fonction renvoyant plusieurs variables peut être utilisée pour donner plusieurs arguments à une autre fonction ou à des affectations multiples (comme dans l'exemple), mais uniquement si elle est mise en dernière.

    function f()
      return 5,8
    end
    
    print(9,f()) --> 9	5	8
    print(f(),9) --> 5	9
    a,b,c = 9,f()
    print(a,b,c) --> 9	5	8
    a,b,c = f(),9
    print(a,b,c) --> 5	9	nil

**NOTE:** Même si j'utilise le nom 'f', rien ne vous empeche d'utiliser un autre nom.

Il faut savoir qu'en Lua quand on renvoie ce qu'une autre fonction renvoie (`return f()` par exemple), Lua passe directement à l'autre fonction sans garder les informations de la première, c'est un "_tail call_", donc il n'y a aucun problème à faire quelque chose comme ça :

    function afficherMoins1(nombre)
      if nombre==0 then
        return
      end
      print(nombre)
      return afficherMoins1(nombre-1)
    end

Ici j'ai enlevé la partie qui vérifie si le nombre est un nombre mais il faudrait le mettre dans une vraie fonction.

#### Les fonctions "_variadiques_"

Les fonctions variadiques (_variadic functions_ en anglais) sont des fonctions ayant un nombre variable d'arguments, elles se construisent de la manière suivante :

    function f(...)
      --faire quelque chose
    end

On peut aussi utiliser des arguments "normaux" dans une fonction variadique du moment que les "_varargs_" (terme anglais désignant la partie avec le nombre variable d'arguments) sont situés en dernier.
TODO: peut-être trouver une meilleure description pour les varargs

    function f(arg1, arg2, ...)
      --faire quelque chose
    end

On peut acceder aux _varargs_ avec `...`, on peut imaginer que chaque `...` qu'on tape est remplacé par la partie qu'on a reçu ici (comme `5,6,8` pour `f(5,6,8)` si la fonction est nommée 'f' et n'utilise que des _varargs_), donc pour itérer sur les _varargs_, on peut tout simplement le mettre dans un constructeur de _table_.

    function afficherVarargs(...)
      for i,v in ipairs({...}) do
        print(v)
      end
    end

**NOTE:** On aurait pu simplifier en utilisant `ipairs{...}` au lieu de `ipairs({...})` puisqu'il n'y a aucune différence de fonctionnement du code entre les deux.

Le problème avec cette approche est que si les arguments contiennent des _nils_ alors `ipairs` s'arrêtera au premier _nil_, une autre solution est d'utiliser `table.pack` qui est équivalent mais rajoute aussi une valeur associée à la clé "n" contenant le nombre d'arguments que `table.pack` a reçu.
C'est la façon la plus simple et la plus rapide de le faire.

    function afficheSansNil(...)
      local arg = table.pack(...)
      for i = 1,arg.n do
        if arg[i]~=nil then
          print(arg[i])
        end
      end
    end

Pour selectionner une partie de _varargs_, on peut utiliser `select` qui renvoie ses arguments à partir du nombre donné en premier argument.

    print(select(1, "a", "b", "c")) --> a	b	c
    print(select(2, "a", "b", "c")) --> b	c
    print(select(3, "a", "b", "c")) --> c

    function test(...)
      print(select(1, ...))
      print(select(2, ...))
      print(select(3, ...))
    end
    
    print(test("a", "b", "c")) --> a	b	c
    --> b	c
    --> c

En donnant le texte "#" en premier argument à `select`, il renverra le nombre d'arguments après le premier.

Si on veut récupérer une seule valeur on peut mettre l'appel à `select` entre parenthèses (ça fonctionne pour n'importe quel appel et pour `...`).

    print( select(1, "a", "b", "c") ) --> b	c
    print( (select(1, "a", "b", "c")) ) --> b

J'ai mis des espaces pour mettre en valeur les parenthèses supplémentaires.

**NOTE:** On pourrait faire notre propre version de `select` (vous pouvez le faire en tant qu'exercice) mais `select` est programmé en C, il sera donc plus rapide (sauf peut-être si vous utilisez LuaJIT).

Il y a aussi la fonction `table.unpack` qui, comme son nom l'indique, fait l'inverse de `table.pack`, elle prend un tableau et renvoie chaque valeur.

    function sortargs(...)
      t={...}
      table.sort(t)
      return table.unpack(t)
    end
    
    print(sortargs(75, 96, 32)) --> 32	75	96
    print(sortargs("dictionnaire", "texte", "main")) --> dictionnaire	main	texte

**NOTE:** C'est mieux en général dans les fonctions d'utiliser des variables locales pour éviter d'en changer un à l'extérieur si elle éxiste, mais comme je n'ai pas encore parlé des variables locales je ne les ai pas utilisées.
