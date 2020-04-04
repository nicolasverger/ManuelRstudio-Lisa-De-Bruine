*Traduit par Fabrice Gabarrot.*

# 1.1 Objectifs d'apprentissage

1.  Comprendre les composants de l’environnement IDE *RStudio*

2.  Tapez les commandes dans la *console*

3.  Comprendre la *syntaxe des fonctions*

4.  *Installer un* ‘package’

5.  *Organiser un projet*

6.  *Structurer un script R ou un fichier RMarkdown* correctement

7.  Créer et compiler un document en RMarkdown

# 1.2 Ressources

*N.B. Les ressources marquées (EN) sont en anglais.*

  - Le premier chapitre [<span class="underline">Introduction</span>](https://r4ds.had.co.nz/introduction.html) de *[<span class="underline">R for Data Science</span>](https://r4ds.had.co.nz)* (EN)

  - [<span class="underline">L’Antisèche de RStudio</span>](https://github.com/rstudio/cheatsheets/raw/master/rstudio-ide.pdf) (EN)

  - [<span class="underline">Une introduction au RMarkdown</span>](https://rmarkdown.rstudio.com/lesson-1.html) (EN)

  - [<span class="underline">Une antisèche pour RMarkdown</span>](https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf) (EN)

  - [<span class="underline">Le guide de référence de RMarkdown</span>](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf) (EN)

# 1.3 Qu’est-ce que R?

R est un environnement de programmation pour le traitement et l'analyse statistique de données. R est de plus en plus utilisé pour la recherche en psychologie afin de promouvoir et faciliter une science ouverte et reproductible. L’objectif est de pouvoir documenter et reproduire toutes les étapes entre les données brutes et les résultats. R vous permet d'écrire des scripts qui combinent des fichiers de données, nettoient les données et exécutent des analyses. Il y a beaucoup d'autres façons de le faire, comme écrire des fichiers de syntaxe SPSS, mais R est un outil utile dans la mesure où il est libre, open source, et couramment utilisé dans la recherche en psychologie et dans les autres sciences.![](./Chapitre%201%20_%20Pour%20commencer/media/image1.png)

|                                                             |                                                                                                                                            |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| ![](./media/info.png) | Voir l'[<span class="underline">annexe A</span>](#annexe%20A) pour plus d'informations sur l'installation de R et des programmes associés. |

### 1.3.1 La console de base R

Si vous ouvrez l'application appelée R, vous verrez une fenêtre "R Console" qui ressemble à ceci.

|                                                             |
| ----------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image3.png) |
| Figure 1.1 La console de R (sous MacOS)                     |

Vous pouvez maintenant fermer R et ne plus jamais l'ouvrir. Dans ce cours, nous travaillerons exclusivement avec RStudio.

<table>
<tbody>
<tr class="odd">
<td><img src="./Chapitre 1 _ Pour commencer/media/image4.png" style="width:0.56771in;height:0.56771in" /></td>
<td><p>RAPPEL : Toujours lancer R via l’environnement IDE RStudio</p>
<p>Lancez <img src="./Chapitre 1 _ Pour commencer/media/image5.png" style="width:0.37462in;height:0.37462in" /> (RStudio.app), pas <img src="./Chapitre 1 _ Pour commencer/media/image1.png" style="width:0.44333in;height:0.34296in" /> (R.app).</p></td>
</tr>
</tbody>
</table>

### 1.3.2 RStudio

|                                                             |
| ----------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image6.png) |
| Figure 1.2: L’environnement IDE RStudio                     |

RStudio est un environnement de développement intégré (IDE). Il s'agit d'un programme qui sert d'éditeur de texte, de gestionnaire de fichiers et offre de nombreuses fonctions pour vous aider à lire et à écrire du code R.![](./Chapitre%201%20_%20Pour%20commencer/media/image5.png)

RStudio est composé de quatre volets (Voir Figure 1.2). Par défaut, le volet supérieur gauche est le volet ***source***, dans lequel vous pouvez afficher et modifier le code source des fichiers. Le volet inférieur gauche est généralement le volet de la ***console***, où vous pouvez taper des commandes et afficher les messages de sortie. Les volets de droite ont plusieurs onglets différents qui vous montrent des informations sur votre code. Vous pouvez modifier l'emplacement des volets et les onglets affichés sous **Préférences \> Disposition du volet**.

### 1.3.3 Configurer RStudio

Dans ce cours, vous apprendrez comment développer des scripts reproductibles. Il s'agit de scripts qui effectuent une analyse complète et transparente du début à la fin, d'une manière qui donne le même résultat pour différentes personnes utilisant le même logiciel sur différents ordinateurs. La transparence est une valeur clé de la science, telle qu’incarnée dans la devise "*trust but verify*" (“faire confiance mais vérifier”).

Lorsque vous faites les choses de façon reproductible, les autres peuvent comprendre et vérifier votre travail. Cela profite à la science, mais il y a aussi une raison égoïste : la personne qui bénéficiera le plus d'un script reproductible est vous-même. Lorsque vous reviendrez à une analyse après deux semaines de vacances, vous remercierez votre moi antérieur d'avoir fait les choses de manière transparente et reproductible, car vous pouvez facilement reprendre là où vous vous étiez arrêté.

Il y a deux modifications que vous devriez apporter à votre installation RStudio pour maximiser la reproductibilité. Allez dans le menu **Préférences/Paramètres**, et décochez la case **Restaurer .RData** dans l'espace de travail au démarrage. Si vous gardez les choses dans votre espace de travail, les choses deviendront désordonnées et des choses inattendues se produiront. Vous devriez toujours commencer par un espace de travail vierge. Cela signifie également que vous ne voulez jamais enregistrer votre espace de travail lorsque vous quittez RStudio, alors définissez ce paramètre sur **Jamais**. La seule chose que vous voulez sauver, ce sont vos scripts.

|                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image7.png)                                                      |
| Figure 1.3 : Modifiez ces paramètres pour ne pas qu’RStudio enregistre systématiquement votre espace de travail. |

## 1.4 Prise en main

### 1.4.1 Commandes de la console

Nous allons d'abord apprendre comment interagir avec la console. En général, vous développerez des scripts R ou des fichiers RMarkdown, plutôt que de travailler directement dans la fenêtre de la console. Cependant, vous pouvez considérer la console comme une sorte de *bac à sable* dans lequel vous pourrez tester des lignes de code et les adapter jusqu'à obtenir ce que vous voulez. Vous pouvez ensuite les copier dans l'éditeur de script.

La plupart du temps, cependant, vous travaillerez dans la fenêtre de l'éditeur de script (soit dans un script R, soit dans un fichier de RMarkdown), puis vous executerez les commandes dans la console en plaçant le curseur sur la ligne et en maintenant la touche Ctrl (sur PC) ou Cmd (sur Mac) enfoncée pendant que vous appuyez sur Entrée. La séquence de touches **Ctrl+Entrée** (ou **Cmd+Entrée**) envoie la commande du script vers la console.

Une façon simple d'en savoir plus sur la console R est de l'utiliser comme calculatrice. Entrez les lignes de code ci-dessous et voyez si vos résultats correspondent. Soyez prêt à faire beaucoup de fautes de frappe (au début).

|       |
| ----- |
| 1 + 1 |

|         |
| ------- |
| \[1\] 2 |

La console R enregistre l’historique des commandes que vous avez tapées par le passé. Utilisez les touches ↑ flèche vers le haut et ↓ flèche vers le bas de votre clavier pour faire défiler votre historique en avant et en arrière. C'est beaucoup plus rapide que de tout retaper.

|           |
| --------- |
| 1 + 1 + 3 |

|         |
| ------- |
| \[1\] 5 |

Vous pouvez décomposer des expressions mathématiques sur plusieurs lignes ; R attend une expression complète avant de la traiter.

<table>
<tbody>
<tr class="odd">
<td><p><em>## here comes a long expression</em></p>
<p><em>## let's break it over multiple lines</em></p>
<p>1 + 2 + 3 + 4 + 5 + 6 +</p>
<p>7 + 8 + 9 +</p>
<p>10</p></td>
</tr>
</tbody>
</table>

|          |
| -------- |
| \[1\] 55 |

Du texte entre guillemets s'appelle une chaîne de caractères (*string*).

|                  |
| ---------------- |
| “Good afternoon” |

|                        |
| ---------------------- |
| \[1\] “Good afternoon” |

Vous pouvez décomposer le texte sur plusieurs lignes ; R attend des guillemets de fermeture avant de l'exécuter. Si vous voulez inclure un guillemet double à l'intérieur de cette chaîne de caractères entre guillemets, faites-la précéder d’une barre oblique inversée ( **\\**" ).

<table>
<tbody>
<tr class="odd">
<td><p>africa &lt;- "I hear the drums echoing tonight</p>
<p>But she hears only whispers of some quiet conversation</p>
<p>She's coming in, 12:30 flight</p>
<p>The moonlit wings reflect the stars that guide me towards salvation</p>
<p>I stopped an old man along the way</p>
<p>Hoping to find some old forgotten words or ancient melodies</p>
<p>He turned to me as if to say, \"Hurry boy, it's waiting there for you\"</p>
<p>- Toto"</p>
<p><strong>cat</strong>(africa) <em>#</em> <em>cat() prints the string</em></p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>I hear the drums echoing tonight</p>
<p>But she hears only whispers of some quiet conversation</p>
<p>She's coming in, 12:30 flight</p>
<p>The moonlit wings reflect the stars that guide me towards salvation</p>
<p>I stopped an old man along the way</p>
<p>Hoping to find some old forgotten words or ancient melodies</p>
<p>He turned to me as if to say, "Hurry boy, it's waiting there for you"</p>
<p>- Toto</p></td>
</tr>
</tbody>
</table>

### 1.4.2 Variables

Souvent, vous voulez stocker le résultat d'un calcul pour une utilisation ultérieure. Vous pouvez le stocker dans une **variable**. Une variable dans R :

  - ne contient que des lettres, des chiffres, des points et des soulignements

  - commence par une lettre ou un point et une lettre

  - distingue les lettres majuscules et minuscules (rickastley n'est pas la même chose que RickAstley)

Les variables suivantes sont valides et différentes :

  - songdata

  - SongData

  - song\_data

  - song.data

  - .song.data

  - never\_gonna\_give\_you\_up\_never\_gonna\_let\_you\_down

Les variables suivantes ne sont pas valides :

  - \_song\_data

  - 1song

  - .1song

  - song data

  - Song-data

Utiliser l'opérateur d'assignation **\<-** pour assigner la valeur à droite à la variable nommée à gauche.

<table>
<tbody>
<tr class="odd">
<td><p><em>## use the assignment operator '&lt;-'</em></p>
<p><em>## R stores the number in the variable</em></p>
<p>x &lt;- 5</p></td>
</tr>
</tbody>
</table>

Maintenant que nous avons assigné une valeur à x , nous pouvons en faire quelque chose :

|        |
| ------ |
| x \* 2 |

|          |
| -------- |
| \[1\] 10 |

Il est même possible de stocker le résultats de calcul dans une variable

|                               |
| ----------------------------- |
| boring\_calculation \<- 2 + 2 |

Notez que R n’affiche pas le résultat lorsqu'il est stocké. Pour afficher le résultat, il suffit de taper le nom de la variable sur une ligne blanche.

|                     |
| ------------------- |
| boring\_calculation |

|         |
| ------- |
| \[1\] 4 |

Une fois qu'une valeur est assignée à une variable, sa valeur ne change pas à moins que vous ne la ré-assignez, même si les variables que vous avez utilisées pour la calculer changent. Prévoyez ce que fait le code ci-dessous et testez-le :

<table>
<tbody>
<tr class="odd">
<td><p>this_year &lt;- 2019</p>
<p>my_birth_year &lt;- 1976</p>
<p>my_age &lt;- this_year - my_birth_year</p>
<p>this_year &lt;- 2020</p></td>
</tr>
</tbody>
</table>

|            |
| ---------- |
| this\_year |

|            |
| ---------- |
| \[1\] 2020 |

|                 |
| --------------- |
| my\_birth\_year |

|            |
| ---------- |
| \[1\] 1976 |

|         |
| ------- |
| my\_age |

|          |
| -------- |
| \[1\] 43 |

### 1.4.3 L'environnement

Chaque fois que vous assignez quelque chose à une nouvelle variable, R crée un nouvel objet dans l'environnement global. Les objets dans l'environnement global existent jusqu'à la fin de votre session, puis ils disparaissent à jamais (à moins que vous ne les sauvegardiez).

Regardez l'onglet **Environnement** dans le volet supérieur droit. Il répertorie toutes les variables que vous avez créées.

Cliquez sur l'icône du balai ![](./Chapitre%201%20_%20Pour%20commencer/media/image8.png) pour effacer toutes les variables et recommencer à zéro. Vous pouvez également utiliser les fonctions suivantes dans la console pour afficher toutes les variables, supprimer une variable ou supprimer toutes les variables.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ls</strong>() <em># print the variables in the global environment</em></p>
<p><strong>rm</strong>("x") <em># remove the variable named x from the global environment</em></p>
<p><strong>rm</strong>(list = <strong>ls</strong>()) <em># clear out the global environment</em></p></td>
</tr>
</tbody>
</table>

|                                                             |                                                                                                                                                                                                                                  |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./media/info.png) | Dans le coin supérieur droit de l'onglet **Environnement**, changez **Liste** en **Grille**. Vous pouvez maintenant voir le type, la longueur et la taille de vos variables et réorganiser la liste selon l'un de ces attributs. |

### 1.4.4 Espacement

Quand vous voyez **\>** au début d'une ligne, cela signifie que R attend que vous démarriez une nouvelle commande. Cependant, si vous voyez un **+** au lieu de **\>** au début de la ligne, cela signifie que R attend que vous terminiez une commande que vous avez commencée sur une ligne précédente. Si vous voulez annuler une commande que vous avez lancée, appuyez simplement sur la touche Echap dans la fenêtre de la console et vous reviendrez à l'invite de commande **\>** .

<table>
<tbody>
<tr class="odd">
<td><p><em># R waits until next line for evaluation</em></p>
<p>(3 + 2) *</p>
<p>5</p></td>
</tr>
</tbody>
</table>

|          |
| -------- |
| \[1\] 25 |

Il est souvent utile de décomposer de longues fonctions sur plusieurs lignes.

<table>
<tbody>
<tr class="odd">
<td><p><strong>cat</strong>("3, 6, 9, the goose drank wine",</p>
<p>"The monkey chewed tobacco on the streetcar line",</p>
<p>"The line broke, the monkey got choked",</p>
<p>"And they all went to heaven in a little rowboat",</p>
<p>sep = " \n")</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>3, 6, 9, the goose drank wine</p>
<p>The monkey chewed tobacco on the streetcar line</p>
<p>The line broke, the monkey got choked</p>
<p>And they all went to heaven in a little rowboat</p></td>
</tr>
</tbody>
</table>

### 1.4.5 Syntaxe des fonctions

Une grande partie de ce que vous faites dans R implique d'appeler une fonction et de stocker les résultats. Une fonction est une section de code nommée qui peut être réutilisée.

Par exemple, sd est une fonction qui retourne l'écart-type du vecteur (l’ensemble) de nombres que vous fournissez comme argument d'entrée. Les fonctions sont configurées comme suit :

|                                                    |
| -------------------------------------------------- |
| **function\_name(argument1, argument2 = "value")** |

Les arguments entre parenthèses peuvent être nommés (comme **argument1 = 10**) ou vous pouvez ignorer les noms si vous les mettez dans le même ordre qu'ils sont définis dans la fonction. Vous pouvez vérifier cela en tapant **?sd** (ou n'importe quel nom de fonction que vous recherchez) dans la console et le panneau d'aide vous montrera l'ordre par défaut sous Utilisation. Vous pouvez également ignorer les arguments dont la valeur par défaut est spécifiée.

La plupart des fonctions retournent une valeur, mais peuvent aussi produire des effets secondaires comme l’affichage sur la console.

Pour illustrer, la fonction **rnorm()** génère des nombres aléatoires à partir de la distribution normale standard. La page d'aide de **rnorm()** (accessible en tapant **?rnorm** dans la console) montre qu'il a la syntaxe suivante

|                                |
| ------------------------------ |
| **rnorm(n, mean = 0, sd = 1)** |

où **n** est le nombre de nombres générés au hasard que vous voulez, **mean** est la moyenne de la distribution et **sd** est l'écart-type. Il n'y a pas de valeur par défaut pour **n**, ce qui signifie que vous obtiendrez une erreur si vous ne la spécifiez pas :

|             |
| ----------- |
| **rnorm()** |

|                                                                 |
| --------------------------------------------------------------- |
| \#\# Error in rnorm(): argument "n" is missing, with no default |

Si vous voulez 10 nombres aléatoires d'une distribution avec une moyenne de 0 et un écart-type, vous pouvez simplement utiliser les valeurs par défaut.

|                   |
| ----------------- |
| **rnorm(**10**)** |

<table>
<tbody>
<tr class="odd">
<td><p>[1] 1.15186804 -0.33024283 -0.24991448 -0.50668069 -0.02495801</p>
<p>[6] -0.27710230 1.47781088 -0.21063169 1.67800038 -0.31944619</p></td>
</tr>
</tbody>
</table>

Si vous voulez 10 numéros d'une distribution avec une moyenne de 100 :

|                       |
| --------------------- |
| **rnorm(**10,100**)** |

<table>
<tbody>
<tr class="odd">
<td>[1] 98.48191 100.43418 99.62359 100.29270 100.50828 98.70452<br />
[7] 101.75982 99.46557 99.03663 99.94638</td>
</tr>
</tbody>
</table>

Ci-dessous, un moyen équivalent, mais moins efficace, d'appeler la fonction :

|                              |
| ---------------------------- |
| **rnorm(**n=10,mean=100**)** |

|                                                                                                           |
| --------------------------------------------------------------------------------------------------------- |
| \[1\] 99.61621 99.73038 100.34224 98.61603 100.85594 101.29661 \[7\] 98.97355 99.65776 98.99585 100.61711 |

Nous n'avons pas besoin de nommer les arguments parce que R reconnaîtra que nous avions l'intention de remplir les premier et second arguments par leur position dans l'appel de fonction. Cependant, si nous voulons changer la valeur par défaut d'un argument qui arrive plus tard dans la liste, alors nous devons le nommer. Par exemple, si nous voulions garder la moyenne par défaut **mean = 0** mais changer l'écart-type à 100, nous le ferions de cette façon :

|                          |
| ------------------------ |
| **rnorm(**10,sd=100**)** |

<table>
<tbody>
<tr class="odd">
<td>[1] -81.60272 71.40418 -73.48568 28.09207 116.85255<br />
[6] -242.48229 141.17281 16.89854 14.01350 -51.97355</td>
</tr>
</tbody>
</table>

Certaines fonctions donnent une liste d'options après un argument ; cela signifie que la valeur par défaut est la première option. L'entrée d'utilisation de la fonction **power.t.test()** ressemble à ceci :

<table>
<tbody>
<tr class="odd">
<td><p><strong>power.t.test(</strong>n = NULL, delta = NULL, sd = 1, sig.level = 0.05,</p>
<p>power = NULL,</p>
<p>type = <strong>c(</strong>"two.sample", "one.sample", "paired"<strong>)</strong>,</p>
<p>alternative = <strong>c(</strong>"two.sided", "one.sided"<strong>)</strong>,</p>
<p>strict = FALSE, tol = .Machine$double.eps^0.25<strong>)</strong></p></td>
</tr>
</tbody>
</table>

### 1.4.6 Obtenir de l'aide

Démarrer l'aide dans un navigateur en utilisant la fonction **help.start()**.

Si une fonction est dans la base R ou un *package* chargé, vous pouvez utiliser la fonction **help("function\_name")** ou le raccourci **?function\_name** pour accéder au fichier d'aide. Si le package n'est pas chargé, spécifiez le nom du package comme deuxième argument de la fonction d'aide.

<table>
<tbody>
<tr class="odd">
<td><p><em># these methods are all equivalent ways of getting help</em></p>
<p><strong>help(</strong>"rnorm"<strong>)</strong></p>
<p>?rnorm</p>
<p><strong>help(</strong>"rnorm"<strong>,</strong> package="stats"<strong>)</strong></p></td>
</tr>
</tbody>
</table>

Lorsque le *package* n'est pas chargé ou que vous n'êtes pas sûr du *package* dans lequel se trouve la fonction, utilisez le raccourci **??function\_name**.

## 1.5 Packages d'extensions

L'un des avantages de R est qu'il est extensible par l'utilisateur : n'importe qui peut créer un nouveau progiciel complémentaire qui étend ses fonctionnalités. Il y a actuellement des milliers de modules complémentaires que les utilisateurs de R ont créés pour résoudre différents types de problèmes, ou simplement pour s'amuser. Il existe des progiciels pour la visualisation de données, l'apprentissage automatique, la neuro-imagerie, le suivi oculaire, l’aspiration de données sur le web et les jeux tels que le Sudoku.

Les modules complémentaires ne sont pas distribués avec la base R, mais doivent être téléchargés et installés à partir d'une archive, de la même manière que vous le feriez, par exemple, pour télécharger et installer une application sur votre smartphone.

Le référentiel principal où résident les *packages* s'appelle CRAN, le Comprehensive R Archive Network. Un *package* doit passer des tests stricts conçus par l'équipe de base de R pour être autorisé à faire partie de l'archive CRAN. Vous pouvez installer à partir de l'archive CRAN via R en utilisant la fonction **install.packages()**.

Il y a une distinction importante entre installer un *package* et charger un *package*.

### 1.5.1 Installer un *package*

Ceci est fait en utilisant **install.packages()**. C'est comme installer une application sur votre téléphone : vous n'avez à le faire qu'une seule fois et l'application restera installée jusqu'à ce que vous la supprimiez. Par exemple, si vous voulez utiliser PokemonGo sur votre téléphone, vous devez l'installer une fois à partir de l'App Store ou du Play Store, et vous n'avez pas à le réinstaller chaque fois que vous voulez l'utiliser. Une fois que vous lancez l'application, elle s'exécutera en arrière-plan jusqu'à ce que vous la fermiez ou redémarriez votre téléphone. De même, lorsque vous installez un paquet, le *package* sera disponible (mais non chargé) chaque fois que vous ouvrirez R.

|                                                             |                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image4.png) | Il se peut que vous ne puissiez installer des *packages* de manière permanente que si vous utilisez R sur votre propre système ; vous ne pourrez peut-être pas le faire sur les postes de travail publics si vous ne disposez pas des privilèges appropriés. |

Installez le paquet **ggExtra** sur votre système. Ce package vous permet de créer des tracés avec des histogrammes marginaux.

|                                 |
| ------------------------------- |
| **install.packages("ggExtra")** |

Si vous n'avez pas déjà installé des *packages* comme **ggplot2** et **shiny**, il installera également ces dépendances pour vous. Si vous n'obtenez pas de message d'erreur à la fin, l'installation a réussi.

### 1.5.2 Chargement d'un paquet

Ceci est fait en utilisant **library(nomdupackage)**. C'est comme lancer une application sur votre téléphone : la fonctionnalité est seulement là où l'application est lancée et reste là jusqu'à ce que vous la fermiez ou la redémarriez. De même, lorsque vous exécutez **library(nomdupackage)** au cours d'une session, les fonctionnalités du *package* auquel se réfère **nomdupackage** seront disponibles pour votre session R. La prochaine fois que vous lancerez R, vous devrez exécuter à nouveau la fonction **library()** si vous voulez accéder à sa fonctionnalité.

Vous pouvez charger les fonctions dans **ggExtra** pour votre session R actuelle comme suit :

|                      |
| -------------------- |
| **library(ggExtra)** |

Il se peut que vous receviez du texte rouge lorsque vous chargez un *package*, c'est normal. Il vous avertit généralement que ce *package* a des fonctions qui ont le même nom que les autres *packages* que vous avez déjà chargés.

|                                                             |                                                                                                                                                                                                                                                                |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./media/info.png) | Vous pouvez utiliser la convention **package::function()** pour indiquer dans quel package d'extension se trouve une fonction. Par exemple, si vous voyez **readr::read\_csv()**, cela fait référence à la fonction **read\_csv()** dans le package **readr**. |

Vous pouvez maintenant exécuter la fonction **ggExtra::runExample()**, qui exécute un exemple interactif de tracés marginaux utilisant **shiny**.

|                           |
| ------------------------- |
| **ggExtra::runExample()** |

### 1.5.3 Installer à partir de GitHub

Beaucoup de *packages* R ne sont pas encore sur CRAN car ils sont encore en développement. De plus en plus, les ensembles de données et le code pour les articles sont disponibles sous forme de *packages* que vous pouvez télécharger sur github. Vous aurez besoin d'installer le *package* **devtools** pour pouvoir installer des *packages* depuis github. Vérifiez si vous avez un *packages* installé en essayant de le charger (par exemple, si vous n'avez pas devtools installé, **library("devtools")** affichera un message d'erreur) ou en le recherchant dans l'onglet paquets dans le volet inférieur droit. Tous les paquets listés sont installés ; tous les paquets cochés sont actuellement chargés.

|                                                                                                             |
| ----------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image9.png)                                                 |
| Figure 1.4 : Vérifiez les paquets installés et chargés dans l'onglet Paquets dans le volet inférieur droit. |

<table>
<tbody>
<tr class="odd">
<td><p><strong>install.packages("devtools")</strong></p>
<p><strong>devtools::install_github("adam-gruer/goodshirt")</strong></p></td>
</tr>
</tbody>
</table>

Après avoir installé le package **goodshirt**, chargez-le à l'aide de la fonction **library()** et affichez quelques citations en utilisant les fonctions ci-dessous.

<table>
<tbody>
<tr class="odd">
<td><p><strong>library(</strong>goodshirt<strong>)</strong></p>
<p><em># quotes from The Good Place</em></p>
<p><strong>chidi()</strong></p>
<p><strong>eleanor()</strong></p>
<p><strong>tahani()</strong></p>
<p><strong>jason()</strong></p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## There really is an afterlife. I can't wait to have breakfast with Kant, and lunch with Michel Foucault, and then have dinner with Kant again so we can talk about what came up at breakfast!</p>
<p>##</p>
<p>## ~ Chidi</p>
<p>## Oh, so now I'm supposed to be nice and make friends and treat her with mutual respect?</p>
<p>##</p>
<p>## ~ Eleanor</p>
<p>## That was my first time as a fashion "don't," and I did not care for it.</p>
<p>##</p>
<p>## ~ Tahani</p>
<p>## I was just about to tell an awesome story about a wing-eating contest that I lost, and a barfing contest that I won, but then a hole opened up in the ground.</p>
<p>##</p>
<p>## ~ Jason</p></td>
</tr>
</tbody>
</table>

## 1.6 Organiser un projet

Les projets dans RStudio sont un moyen de regrouper tous les fichiers dont vous avez besoin pour un projet. La plupart des projets comprennent des scripts, des fichiers de données et des fichiers de sortie comme la version PDF du script ou des images.

<table>
<tbody>
<tr class="odd">
<td><img src="./Chapitre 1 _ Pour commencer/media/image10.png" style="width:0.52083in;height:0.41493in" /></td>
<td><p>Créez un nouveau répertoire dans lequel vous conserverez tout votre matériel pour ce cours. Si vous utilisez un ordinateur de laboratoire, assurez-vous de créer ce répertoire dans votre lecteur réseau pour pouvoir y accéder à partir d'autres ordinateurs.</p>
<p>Choisissez <strong>New Project...</strong> sous le menu <strong>File</strong> pour créer un nouveau projet appelé <strong>01-intro</strong> dans ce répertoire.</p></td>
</tr>
</tbody>
</table>

### 

### 1.6.1 Structure

Voici à quoi ressemble un script R. Ne vous inquiétez pas des détails pour l'instant.

<table>
<tbody>
<tr class="odd">
<td><p><em># load add-on packages</em></p>
<p><strong>library(</strong>tidyverse<strong>)</strong></p>
<p><em># set variables ----</em></p>
<p>n &lt;- 100</p>
<p><em># simulate data ----</em></p>
<p>data &lt;- <strong>data.frame(</strong></p>
<p>id = 1:n,</p>
<p>dv = <strong>c(</strong>rnorm(n/2, 0<strong>),</strong> rnorm(n/2, 1)<strong>),</strong></p>
<p>condition = <strong>rep(c(</strong>"A", "B"<strong>),</strong> each = n/2<strong>)</strong></p>
<p><strong>)</strong></p>
<p><em># plot data ----</em></p>
<p><strong>ggplot(</strong>data<strong>, aes(</strong>condition, dv<strong>)) +</strong></p>
<p><strong>geom_violin(</strong>trim = FALSE<strong>) +</strong></p>
<p><strong>geom_boxplot(</strong>width = 0.25<strong>,</strong></p>
<p><strong>aes(</strong>fill = condition<strong>),</strong></p>
<p>show.legend = FALSE<strong>)</strong></p>
<p><em># save plot ----</em></p>
<p><strong>ggsave(</strong>"sim_data.png", width = 8, height = 6<strong>)</strong></p></td>
</tr>
</tbody>
</table>

Il est préférable de suivre la structure suivante lors du développement de vos propres scripts :

  - charger dans tous les modules complémentaires que vous devez utiliser

  - définir des fonctions personnalisées

  - charger ou simuler les données avec lesquelles vous allez travailler

  - travailler avec les données

  - enregistrez tout ce que vous avez besoin d'enregistrer

Souvent, lorsque vous travaillez sur un script, vous vous rendrez compte que vous avez besoin de charger un autre module complémentaire. N'enterrez pas l'appel à **library(package\_I\_need)** tout en bas dans le script. Mettez-le en tête de liste pour que l'utilisateur ait une vue d'ensemble des paquets nécessaires.

Vous pouvez ajouter des commentaires à un script R en utilisant le symbole dièse ( **\#** ). L'interpréteur R ignore les caractères du hachage jusqu'à la fin de la ligne.

<table>
<tbody>
<tr class="odd">
<td><p><em>## comments: any text from '#' on is ignored until end of line</em></p>
<p><em>22 / 7 # approximation to pi</em></p></td>
</tr>
</tbody>
</table>

|                |
| -------------- |
| \[1\] 3.142857 |

### 1.6.2 Rapports reproductibles avec R Markdown

Nous produirons des rapports reproductibles en suivant les principes d'une [<span class="underline">programmation lettrée</span>](https://fr.wikipedia.org/wiki/Programmation_lettr%C3%A9e). L'idée de base est de regrouper le texte du rapport dans un seul document avec le code nécessaire pour effectuer toutes les analyses et générer les tableaux. Le rapport est ensuite "compilé" à partir du format original dans un autre format plus portable, tel que HTML ou PDF. C'est différent des approches traditionnelles de copier-coller où, par exemple, vous créez un graphique dans Microsoft Excel ou un programme de statistiques comme SPSS et vous le collez ensuite dans Microsoft Word.

Nous utiliserons [<span class="underline">R Markdown</span>](https://rmarkdown.rstudio.com/lesson-1.html) pour créer des rapports reproductibles, ce qui permet de mélanger le texte et le code. Un script reproductible contiendra des blocs de code. Un bloc de code commence et se termine avec des apostrophes ouvrantes ( **\`** ) dans une rangée, avec quelques informations sur le code entre accolades, tels que **{r nom du morceau, echo=FALSE}** (ceci exécute le code, mais n'affiche pas le texte du bloc de code dans le document compilé). Le texte à l'extérieur des blocs de code est écrit en markdown, ce qui est une façon de spécifier le formatage, comme les en-têtes, les paragraphes, les listes, les caractères gras et les liens.

|                                                              |
| ------------------------------------------------------------ |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image11.png) |
| Figure 1.5 : Un code reproductible                           |

Si vous ouvrez un nouveau fichier RMarkdown à partir d'un modèle, vous verrez un document exemple contenant plusieurs blocs de code. Pour créer un rapport HTML ou PDF à partir d'un document R Markdown (Rmd), vous devez le compiler. La compilation d'un document s'appelle *knit* (“tricoter”) sur RStudio.

Il y a un bouton qui ressemble à une pelote de laine avec des aiguilles ![](./Chapitre%201%20_%20Pour%20commencer/media/image12.png) sur lequel vous devez cliquer pour compiler votre fichier dans un rapport.

|                                                                      |
| -------------------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image13.png)         |
| Figure 1.6 : Le bouton “knit” pour “tricoter” un document RMarkdown. |

|                                                              |                                                                                                                                                                                          |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image10.png) | Créez un nouveau fichier R Markdown à partir du menu **File \> New File \> R Markdown...** Changez le titre et l'auteur, puis cliquez sur le bouton tricoter pour créer un fichier html. |

### 1.6.3 Répertoire de travail

Où dois-je mettre tous mes fichiers ? Lors du développement d'une analyse, vous voulez généralement avoir tous vos scripts et fichiers de données dans un sous-repertoire de la structure de répertoire de votre ordinateur. Habituellement, il n'y a qu'un seul répertoire de travail où vos données et vos scripts sont stockés.

Votre script ne devrait référencer que des fichiers à trois endroits, en utilisant le format approprié.

|                               |                                                                         |
| ----------------------------- | ----------------------------------------------------------------------- |
| **Où ?**                      | **Exemple**                                                             |
| Sur le Web                    | “<https://psyteachr.github.io/msc-data-skills/data/disgust_scores.csv>” |
| Dans le répertoire de travail | “disgust\_scores.csv”                                                   |
| Dans un sous-répertoire       | “data/disgust\_scores.csv”                                              |

|                                                             |                                                                                 |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------- |
| ![](./Chapitre%201%20_%20Pour%20commencer/media/image4.png) | Ne définissez ou ne modifiez jamais votre répertoire de travail dans un script. |

Si vous travaillez avec un fichier R Markdown, il utilisera automatiquement le même répertoire que le fichier “.Rmd”.

Si vous travaillez avec des scripts R, stockez votre fichier de script principal dans le répertoire de niveau supérieur et définissez manuellement votre répertoire de travail à cet emplacement. Vous devrez réinitialiser le répertoire de travail chaque fois que vous ouvrez RStudio, sauf si vous créez un projet et accédez au script depuis le projet.

Par exemple, si sur une machine Windows vos données et scripts sont dans le répertoire **C:\\Carla's\_files\\thesis2\\my\_thesis\\new\_analysis**, vous pouvez définir votre répertoire de travail de deux façons : (1) en allant dans le menu déroulant **Session** dans RStudio et en choisissant **Set Working Directory**, ou (2) en tapant **setwd("C:\\Carla's\_files\\thesis2\\my\_thesis\\new\_analysis")** dans la fenêtre console.

<table>
<tbody>
<tr class="odd">
<td><img src="./Chapitre 1 _ Pour commencer/media/image14.png" style="width:0.61458in;height:0.61111in" /></td>
<td><p>Il est tentant pour vous simplifier la vie de mettre la commande <strong>setwd()</strong> dans votre script. <strong>Ne faites pas ça !</strong> D'autres n'auront pas la même arborescence de répertoires que vous (et quand votre ordinateur portable meurt et que vous en recevez un nouveau, vous ne l’aurez pas non plus).</p>
<p>Lorsque vous définissez manuellement le répertoire de travail, utilisez toujours l'option <strong>Session &gt; Set Working Directory</strong> ou tapez <strong>setwd()</strong> dans la console.</p></td>
</tr>
</tbody>
</table>

Si votre script a besoin d'un fichier dans un sous-répertoire de **new\_analysis**, par exemple **data/questionnaire.csv**, chargez-le en utilisant un chemin relatif pour qu'il soit accessible si vous déplacez le dossier **new\_analysis** vers un autre emplacement ou ordinateur :

|                                                              |
| ------------------------------------------------------------ |
| dat \<- **read\_csv(**"data/questionnaire.csv") *\# correct* |

Ne le chargez pas en utilisant un chemin absolu :

|                                                                                                               |
| ------------------------------------------------------------------------------------------------------------- |
| dat \<- **read\_csv(**"C:/Carla's\_files/thesis2/my\_thesis/new\_analysis/data/questionnaire.csv") *\# wrong* |

|                                                             |                                                                                                                                                                                                                                                              |
| ----------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![](./media/info.png) | Notez également la convention d'utiliser des barres obliques avant ( / ), contrairement à la convention spécifique à Windows d'utiliser des barres obliques arrière ( \\ ). Ceci permet de rendre les références à la plate-forme de fichiers indépendantes. |

## 1.7 Exercices

Téléchargez la première série d'exercices et placez-la dans le répertoire de projet que vous avez créé précédemment. Ne regardez les réponses qu'après avoir essayé toutes les questions.
