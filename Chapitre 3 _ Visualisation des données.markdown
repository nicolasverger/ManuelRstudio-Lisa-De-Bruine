Chapitre 3 : Visualisation des données![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image1.png)

                                           
*Traduit par Mae Braud. Relu et corrigé par Marie Delacre* 

Pour savoir si vous avez besoin de réviser ce chapitre, faites le **quiz** (voir 3.11).

3.1 Objectifs d’apprentissage

3.1.1. Niveau débutant

1.  Comprendre quels types de graphiques sont les plus adaptés aux différents types de données

<!-- end list -->

  - 1 discrète

  - 1 continue

  - 2 discrètes

  - 2 continues

  - 1 discrète, 1 continue

  - 3 continues

<!-- end list -->

2.  Créer des graphiques de base à l’aide de ggplot2

<!-- end list -->

  - geom\_bar()

  - geom\_density()

  - geom\_freqpoly()

  - geom\_histogram()

  - geom\_violin()

  - geom\_boxplot()

  - geom\_col()

  - geom\_point()

  - geom\_smooth()

<!-- end list -->

3.  Définir des étiquettes et couleurs personnalisées

4.  Représenter des plans factoriels avec différentes couleurs ou vignettes

5.  Sauvegarder des graphiques en tant qu’image

3.1.2. Niveau intermédiaire

6.  Superposer différents types de graphiques

7.  Ajouter des droites aux graphiques

8.  Gérer la répétition d’observations

9.  Créer des types de graphiques moins communs

<!-- end list -->

  - geom\_tile()

  - geom\_density2d()

  - geom\_bin2d()

  - geom\_hex()

  - geom\_count()

3.1.3. Niveau avancé

10. Combiner plusieurs graphiques sur une même page à l’aide de cowplot

11. Ajuster les axes (e.g., inverser les coordonnées, définir les limites des axes)

12. Modifier le thème

13. Créer des graphiques interactifs avec plotly

3.2 Ressources

  - [Look at Data](http://socviz.co/lookatdata.html#lookatdata) de [Data Visualization for Social Science](http://socviz.co/) (EN)

  - [Chapitre 3 : Visualisation des données](https://r4ds.had.co.nz/data-visualisation.html) de *R* *for Data Science* (EN)

  - [Chapitre 28 : Graphiques pour la communication](https://r4ds.had.co.nz/graphics-for-communication.html) de *R for Data Science* (EN)

  - [Graphiques](http://www.cookbook-r.com/Graphs/) dans *Cookbook for R* (EN)

  - [Antisèche ggplot2](https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf) (EN)

  - [Documentation ggplot2](https://ggplot2.tidyverse.org/reference/) (EN)

  - [La galerie des graphiques R](https://www.r-graph-gallery.com/) (ceci est très utile) (EN)

  - [Top 50 des représentations graphiques ggplot2](http://r-statistics.co/Top50-Ggplot2-Visualizations-MasterList-R-Code.html) (EN)

  - [Extensions ggplot](https://www.ggplot2-exts.org/) (EN)

  - [plotly](https://plot.ly/ggplot2/) pour créer des graphiques interactifs (EN)

3.3 Préambule

<table>
<tbody>
<tr class="odd">
<td><p><em># libraries needed for these graphs</em></p>
<p><strong>library</strong>(tidyverse)</p>
<p><strong>library</strong>(plotly)</p>
<p><strong>library</strong>(cowplot)</p>
<p><strong>set.seed</strong>(30250) <em># make sure random numbers are reproducible</em></p></td>
</tr>
</tbody>
</table>

3.4 Combinaison de variables communes

Les variables **continues** sont des caractéristiques que vous pouvez mesurer, comme la taille.

Les variables **discrètes** (ou catégorielles) sont des choses que vous pouvez compter, comme le nombre d’animaux de compagnie que vous avez. Les variables catégorielles peuvent être **nominales**, lorsque les catégories n’ont pas vraiment d’ordre, comme pour les catégories chats, chiens et furets (bien que les furets soient évidemment les meilleurs). Elles peuvent être **ordinales**, lorsque les catégories peuvent être classées dans un ordre naturel, mais que la distance entre deux catégories consécutives n’est pas tout à fait équivalente partout, comme les points sur une échelle de Likert.

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)


<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Avant de lire la suite, réfléchissez à un exemple pour chaque type de combinaison de variables et dessinez les types de graphiques qui représenteraient le mieux ces données.</p>
</blockquote>
<ul>
<li><p>1 discrète</p></li>
<li><p>1 continue</p></li>
<li><p>2 discrètes</p></li>
<li><p>2 continues</p></li>
<li><p>1 discrète, 1 continue</p></li>
<li><p>3 continues</p></li>
</ul></td>
</tr>
</tbody>
</table>

3.4.1 Données

Le code ci-dessous permet de créer des tableaux de données avec différents types de données. Nous apprendrons comment simuler ce type de données dans le chapitre [Probabilité & Simulation](https://psyteachr.github.io/msc-data-skills/sim.html#sim), mais pour l’instant exécutez simplement le bout de code ci-dessous.

  - pets contient une colonne avec le type d’animal de compagnie

  - pet\_happy contient les informations happiness et age pour 500 propriétaires de chiens et 500 propriétaires de chats

  - x\_vs\_y contient deux variables continues corrélées (x et y)

  - overlap contient deux variables ordinales corrélées. Dans la mesure où il y a 1000 observations, il y a beaucoup de répétition d’observations.

  - overplot contient deux variables continues corrélées et 10000 observations

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Tout d’abord, réfléchissez aux types de graphiques qui seraient les plus adaptés pour représenter ces différents types de données.</p>
</blockquote></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>pets &lt;- <strong>tibble</strong>(</p>
<p>pet = <strong>sample</strong>(</p>
<p><strong>c</strong>("dog", "cat", "ferret", "bird", "fish"),</p>
<p>100,</p>
<p>TRUE,</p>
<p><strong>c</strong>(0.45, 0.40, 0.05, 0.05, 0.05)</p>
<p>)</p>
<p>)</p>
<p>pet_happy &lt;- <strong>tibble</strong>(</p>
<p>pet = <strong>rep</strong>(<strong>c</strong>("dog", "cat"), each = 500),</p>
<p>happiness = <strong>c</strong>(<strong>rnorm</strong>(500, 55, 10), <strong>rnorm</strong>(500, 45, 10)),</p>
<p>age = <strong>rpois</strong>(1000, 3) + 20</p>
<p>)</p>
<p>x_vs_y &lt;- <strong>tibble</strong>(</p>
<p>x = <strong>rnorm</strong>(100),</p>
<p>y = x + <strong>rnorm</strong>(100, 0, 0.5)</p>
<p>)</p>
<p>overlap &lt;- <strong>tibble</strong>(</p>
<p>x = <strong>rbinom</strong>(1000, 10, 0.5),</p>
<p>y = x + <strong>rbinom</strong>(1000, 20, 0.5)</p>
<p>)</p>
<p>overplot &lt;- <strong>tibble</strong>(</p>
<p>x = <strong>rnorm</strong>(10000),</p>
<p>y = x + <strong>rnorm</strong>(10000, 0, 0.5)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

3.5 Graphiques de base

3.5.1 Diagramme à barres

Les diagrammes à barres conviennent à une variable catégorielle pour laquelle vous souhaitez représenter l’effectif.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pets, <strong>aes</strong>(pet)) +</p>
<p><strong>geom_bar</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image3.png)

Figure 3.1 : Diagramme à barres

3.5.2. Courbe de densité

Les courbes de densité (ou de distribution) conviennent à une variable continue, mais seulement lorsque vous possédez un grand nombre d’observations.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness)) +</p>
<p><strong>geom_density</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image4.png)

Figure 3.2 : Courbe de densité

Vous pouvez diviser une variable en sous-ensembles et les représenter en assignant la variable catégorielle aux arguments group, fill, ou couleur.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness, fill = pet)) <strong>+</strong></p>
<p><strong>geom_density</strong>(alpha = 0.5)</p></td>
</tr>
</tbody>
</table>

![](/Chapitre%203%20_%20Visualisation%20des%20données/media/image5.png)

Figure 3.3 : Courbe de densité avec plusieurs groupes

![](/Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Essayez de modifier l’argument alpha pour voir ce que cela change.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.5.3. Polygone des effectifs

Si vous ne souhaitez pas une distribution lissée, essayez geom\_freqpoly().

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness, color = pet)) <strong>+</strong></p>
<p><strong>geom_freqpoly</strong>(binwidth = 1)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image6.png)

Figure 3.4 : Polygone des effectifs

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Essayez de remplacer la valeur de l’argument binwidth par 5 puis par 0.1. Comment déterminez-vous la bonne valeur ?</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.5.4. Histogramme

Les histogrammes conviennent également pour représenter une variable continue, et notamment lorsque vous n’avez pas beaucoup d’observations. Spécifiez l’argument binwidth pour contrôler la largeur de chaque barre.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness)) <strong>+</strong></p>
<p><strong>geom_histogram</strong>(binwidth = 1, fill = "white", color = "black")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image7.png)

Figure 3.5 : Histogramme

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image8.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Dans ggplot les histogrammes ne sont pas très esthétiques, à moins de définir les arguments fill et color.</p>
</blockquote></td>
</tr>
</tbody>
</table>

Si vous affichez des histogrammes avec plusieurs groupes, vous voudrez probablement aussi changer la valeur par défaut de l’argument position.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_histogram</strong>(binwidth = 1, alpha = 0.5, position = "dodge")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image9.png)

Figure 3.6 : Histogramme avec plusieurs groupes

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Essayez de modifier la valeur de l’argument position avec “identity”, “fill”, “dodge”, ou “stack”.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.5.5. Diagramme en colonnes

Les diagrammes en colonnes sont la pire façon de représenter des données continues divisées en plusieurs groupes, mais font aussi partie des plus communément utilisés.

Pour faire des diagrammes en colonnes avec barres d’erreur, vous devez d’abord calculer les moyennes, la limite supérieure (ymax) et la limite inférieure (ymin) des barres pour chaque catégorie. Vous en apprendrez plus sur la manière d’utiliser le code ci-dessous dans les deux prochaines leçons.

<table>
<tbody>
<tr class="odd">
<td><p><em># calculate mean and SD for each pet</em></p>
<p>avg_pet_happy &lt;- pet_happy %&gt;%</p>
<p><strong>group_by</strong>(pet) %&gt;%</p>
<p><strong>summarise</strong>(</p>
<p>mean = <strong>mean</strong>(happiness),</p>
<p>sd = <strong>sd</strong>(happiness)</p>
<p>)</p>
<p><strong>ggplot</strong>(avg_pet_happy, <strong>aes</strong>(pet, mean, fill=pet)) <strong>+</strong></p>
<p><strong>geom_col</strong>(alpha = 0.5) <strong>+</strong></p>
<p><strong>geom_errorbar</strong>(<strong>aes</strong>(ymin = mean - sd, ymax = mean + sd), width = 0.25) <strong>+</strong></p>
<p><strong>geom_hline</strong>(yintercept = 40)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image10.png)

Figure 3.7 : Diagramme en colonnes

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>À votre avis, que fait geom_hline() ?</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.5.6. Boîte à moustaches

Les boîtes à moustaches sont très bien pour représenter la distribution de variables continues divisées en plusieurs groupes. Elles résolvent la plupart des problèmes liés à l’utilisation des diagrammes en colonnes pour la représentation de données continues.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_boxplot</strong>(alpha = 0.5)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image11.png)

Figure 3.8 : Boîte à moustache

3.5.7. Diagramme en violon

Les diagrammes en violon ressemblent en quelque sorte à deux courbes de densité symétriques accolées verticalement. Ils donnent davantage d’informations sur la distribution que les boîtes à moustaches et sont particulièrement utiles lorsque vous avez des distributions ne suivant pas une loi normale.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>(</p>
<p>trim = FALSE,</p>
<p>draw_quantiles = <strong>c</strong>(0.25, 0.5, 0.75),</p>
<p>alpha = 0.5</p>
<p>)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image12.png)

Figure 3.9 : Diagramme en violon

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image2.png)

|                                                                |
| -------------------------------------------------------------- |
| Essayez de changer les chiffres de l’argument draw\_quantiles. |

3.5.8. Nuage de points

Les nuages de points sont une bonne manière de représenter la relation entre deux variables continues.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(x_vs_y, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_point</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image13.png)

Figure 3.10 : Nuage de points à l’aide de geom\_point()

3.5.9. Droite de régression linéaire

Nous cherchons souvent à représenter cette relation en une seule droite.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(x_vs_y, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method="lm")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image14.png)

Figure 3.11 : Droite de régression linéaire à l’aide de geom\_smooth()

3.6 Personnalisation

3.6.1. Étiquettes

Il y a différentes façons de définir des titres et des étiquettes d’axes personnalisés.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(x_vs_y, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method="lm") <strong>+</strong></p>
<p><strong>ggtitle</strong>("My Plot Title") <strong>+</strong></p>
<p><strong>xlab</strong>("The X Variable") <strong>+</strong></p>
<p><strong>ylab</strong>("The Y Variable")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image15.png)

Figure 3.12 : Définir des étiquettes personnalisées à l’aide de ggtitle(), xlab() et ylab()

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(x_vs_y, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method="lm") <strong>+</strong></p>
<p><strong>labs</strong>(title = "My Plot Title",</p>
<p>x = "The X Variable",</p>
<p>y = "The Y Variable")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image16.png)

Figure 3.13 : Définir des étiquettes personnalisées à l’aide de labs()

3.6.2. Couleurs

Vous pouvez définir des valeurs personnalisées pour les bordures et le remplissage en utilisant les fonctions comme scale\_colour\_manual() et scale\_fill\_manual(). Le [chapitre Couleurs](http://www.cookbook-r.com/Graphs/Colors_\(ggplot2\)/) dans [Cookbook for R](http://www.cookbook-r.com/Graphs/Colors_\(ggplot2\)/) présente d’autres nombreuses manières de personnaliser les couleurs.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, colour = pet, fill = pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>() <strong>+</strong></p>
<p><strong>scale_color_manual</strong>(values = c("darkgreen", "dodgerblue")) <strong>+</strong></p>
<p><strong>scale_fill_manual</strong>(values = c("#CCFFCC", "#BBDDFF"))</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image17.png)

Figure 3.14 : Définir des couleurs personnalisées

3.6.3. Sauvegarder en tant que fichier

Vous pouvez sauvegarder un ggplot avec ggsave(). Par défaut, cette fonction sauvegarde le dernier ggplot ayant été créé, mais vous pouvez spécifier quel graphique vous voulez sauvegarder à condition qu’il ait été assigné à une variable.

Vous pouvez spécifier les dimensions de votre graphique avec les arguments width (largeur) et height (hauteur). Les valeurs par défaut sont en pouces, mais vous pouvez changer l’unité en modifiant la valeur de l’argument units par “in”, “cm” ou “mm”.

<table>
<tbody>
<tr class="odd">
<td><p>box &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_boxplot</strong>(alpha = 0.5)</p>
<p>violin &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>(alpha = 0.5)</p>
<p><strong>ggsave</strong>("demog_violin_plot.png", width = 5, height = 7)</p>
<p><strong>ggsave</strong>("demog_box_plot.jpg", plot = box, width = 5, height = 7)</p></td>
</tr>
</tbody>
</table>

3.7 Graphiques combinés

3.7.1 Diagramme en violon avec boîte à moustache interne

Pour démontrer l’utilisation de facet\_grid() pour les plans factoriels, nous créons une nouvelle colonne appelée agegroup de sorte à diviser les participants suivant qu’ils soient plus âgés ou plus jeunes que l’âge médian. Par défaut, les modalités du facteur seront représentées par ordre alphabétique, mais il est possible de modifier cet ordre via la fonction factor().

<table>
<tbody>
<tr class="odd">
<td><p>pet_happy %&gt;%</p>
<p><strong>mutate</strong>(agegroup = <strong>ifelse</strong>(age&lt;<strong>median</strong>(age), "Younger", "Older"),</p>
<p><strong>agegroup = factor(agegroup, levels = c("Younger", "Older"))</strong>) %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>(trim = FALSE, alpha=0.5, show.legend = FALSE) <strong>+</strong></p>
<p><strong>geom_boxplot</strong>(width = 0.25, fill="white") <strong>+</strong></p>
<p><strong>facet_grid</strong>(.~agegroup) <strong>+</strong></p>
<p><strong>scale_fill_manual</strong>(values = <strong>c</strong>("orange", "green"))</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image18.png)

Figure 3.15 : Diagramme en violon avec boîte à moustache interne

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image8.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Pour cacher la légende, spécifiez la valeur de l’argument show.legend avec FALSE. Ici, nous le faisons car le type d’animal de compagnie est déjà affiché sur l’axe des x.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.7.2 Diagramme en violon avec barres d’erreurs

Vous pouvez utiliser la fonction stat\_summary() pour superposer un point-range plot affichant la moyenne ± 1 ET.

Vous apprendrez comment écrire vos propres fonctions dans la leçon [Itération et Fonctions](https://psyteachr.github.io/msc-data-skills/func.html#func).

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>(</p>
<p>trim = FALSE,</p>
<p>alpha = 0.5</p>
<p>) <strong>+</strong></p>
<p><strong>stat_summary</strong>(</p>
<p>fun.y = mean,</p>
<p>fun.ymax = <strong>function</strong>(x) {<strong>mean</strong>(x) <strong>+ sd</strong>(x)},</p>
<p>fun.ymin = <strong>function</strong>(x) {<strong>mean</strong>(x) <strong>- sd</strong>(x)},</p>
<p>geom="pointrange"</p>
<p>)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image19.png)

Figure 3.16 : Point-range plot à l’aide de stat\_summary()

3.7.3 Violin-jitter plot

Si vous n’avez pas beaucoup de points de données, il est bien de les représenter individuellement. Pour faire cela, vous pouvez utiliser geom\_jitter.

<table>
<tbody>
<tr class="odd">
<td><p>pet_happy %&gt;%</p>
<p><strong>sample_n</strong>(50) %&gt;% <em># choose 50 random observations from the dataset</em></p>
<p><strong>ggplot</strong>(<strong>aes</strong>(pet, happiness, fill=pet)) +</p>
<p><strong>geom_violin</strong>(</p>
<p>trim = FALSE,</p>
<p>draw_quantiles = <strong>c</strong>(0.25, 0.5, 0.75),</p>
<p>alpha = 0.5</p>
<p>) <strong>+</strong></p>
<p><strong>geom_jitter</strong>(</p>
<p>width = 0.15, <em># points spread out over 15% of available width</em></p>
<p>height = 0, <em># do not move position on the y-axis</em></p>
<p>alpha = 0.5,</p>
<p>size = 3</p>
<p>)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image20.png)

Figure 3.17 : Violin-jitter plot

3.7.4 Nuage de points avec droite de régression linéaire

Si votre graphique n’est pas trop complexe, il est aussi bien de montrer les données individuelles en arrière-plan de la droite de régression.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(x_vs_y, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_point</strong>(alpha = 0.25) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method="lm")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image21.png)

Figure 3.18 : Nuage de points avec droite de régression

3.7.5 Combinaison de graphiques

Pour facilement créer une grille avec différents graphiques, vous pouvez utiliser le package [cowplot](https://cran.r-project.org/package=cowplot/vignettes/introduction.html). Tout d’abord, vous devez assigner un nom à chaque graphique. Ensuite, vous listez tous les graphiques en tant que premiers arguments de la fonction plot\_grid() puis vous définissez une liste d’étiquettes.

<table>
<tbody>
<tr class="odd">
<td><p>my_hist &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_histogram</strong>(</p>
<p>binwidth = 1,</p>
<p>alpha = 0.5,</p>
<p>position = "dodge",</p>
<p>show.legend = FALSE</p>
<p>)</p>
<p>my_violin &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_violin</strong>(</p>
<p>trim = FALSE,</p>
<p>draw_quantiles = <strong>c</strong>(0.5),</p>
<p>alpha = 0.5,</p>
<p>show.legend = FALSE</p>
<p>)</p>
<p>my_box &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_boxplot</strong>(alpha=0.5, show.legend = FALSE)</p>
<p>my_density &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_density</strong>(alpha=0.5, show.legend = FALSE)</p>
<p>my_bar &lt;- pet_happy %&gt;%</p>
<p><strong>group_by</strong>(pet) %&gt;%</p>
<p><strong>summarise</strong>(</p>
<p>mean = mean(happiness),</p>
<p>sd = sd(happiness)</p>
<p>) %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(pet, mean, fill=pet)) <strong>+</strong></p>
<p><strong>geom_bar</strong>(stat="identity", alpha = 0.5,</p>
<p>color = "black", show.legend = FALSE) <strong>+</strong></p>
<p><strong>geom_errorbar</strong>(<strong>aes</strong>(ymin = mean - sd, ymax = mean + sd), width = 0.25)</p>
<p><strong>plot_grid</strong>(</p>
<p>my_violin,</p>
<p>my_box,</p>
<p>my_density,</p>
<p>my_bar,</p>
<p>labels = <strong>c</strong>("A", "B", "C", "D")</p>
<p>)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image22.png)

Figure 3.19 : Grille de graphiques à l’aide de cowplot

3.8 Répétition de données discrètes

3.8.1 Réduire l’opacité

Vous pouvez gérer la superposition d’observations (cas très commun lorsque vous utilisez des échelles de Likert) en réduisant l’opacité des points (représentants chacun une observation). Pour trouver le niveau d’opacité qui convient le mieux, vous devez procéder par essais et erreurs.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(overlap, <strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_point</strong>(size = 5, alpha = .05) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method="lm")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image23.png)

Figure 3.20 : Gérer la superposition d’observations à l’aide de la transparence

3.8.2 Graphique sous forme de regroupements de points proportionnels

Ou bien alors, vous pouvez également définir la taille des points comme étant proportionnelle au nombre d’observations qui se répètent en utilisant geom\_count().

<table>
<tbody>
<tr class="odd">
<td><p>overlap %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_count</strong>(color = "#663399")</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image24.png)

Figure 3.21 : Gérer la répétition d’observations à l’aide de geom\_count()

Alternativement, vous pouvez transformer vos données en créant une colonne d’effectifs et utiliser l’effectif pour définir la couleur des points.

<table>
<tbody>
<tr class="odd">
<td><p>overlap %&gt;%</p>
<p><strong>group_by</strong>(x, y) %&gt;%</p>
<p><strong>summarise</strong>(count = n()) %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y, color=count)) <strong>+</strong></p>
<p><strong>geom_point</strong>(size = 5) <strong>+</strong></p>
<p><strong>scale_color_viridis_c</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image25.png)

Figure 3.22 : Gérer la répétition d’observations à l’aide de la couleur

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image8.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Le <a href="https://cran.r-project.org/web/packages/viridis/vignettes/intro-to-viridis.html">package viridis</a> change le thème des couleurs pour les rendre plus lisibles par les personnes daltoniennes et rendre le contraste plus lisible lorsqu’il est imprimé en noir et blanc. Depuis la version 3.0.0., Viridis est intégré dans ggplot2. Il utilise scale_colour_viridis_c() et scale_fill_viridis_c() pour les variables continues et scale_colour_viridis_d() et scale_fill_viridis_d() pour les variables discrètes.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.9 Répétition de données continues

Même si les variables sont continues, si vous avez beaucoup de données alors la superposition des points risquerait de masquer quelconque relation.

<table>
<tbody>
<tr class="odd">
<td><p>overplot %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_point</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image26.png)

Figure 3.23 : Sur-représentation de données

3.9.1 2D Density plot

Utilisez geom\_density2d() pour créer une contour map.

<table>
<tbody>
<tr class="odd">
<td><p>overplot %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_density2d</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image27.png)

Figure 3.24 : Contour map à l’aide de geom\_density2d()

Pour créer un heatmap-style density plot vous pouvez utiliser stat\_density\_2d(aes(fill = ..level..), geom = “polygon”).

<table>
<tbody>
<tr class="odd">
<td><p>overplot %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>stat_density_2d</strong>(<strong>aes</strong>(fill = ..level..), geom = "polygon") <strong>+</strong></p>
<p><strong>scale_fill_viridis_c</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image28.png)

Figure 3.25 : Heatmap-density plot

3.9.2 Histogramme 2D

Utilisez geom\_bin2d() pour créer une heatmap rectangulaire basée sur le nombre de bin. Spécifiez la binwidth avec les dimensions x et y définissant la taille de chaque bin.

<table>
<tbody>
<tr class="odd">
<td><p>overplot %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_bin2d</strong>(binwidth = <strong>c</strong>(1,1))</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image29.png)

Figure 3.26 : Heatmap basée sur le nombre de bin

3.9.3 Heatmap hexagonale

Utilisez geomhex() pour créer une heatmap hexagonale basée sur le nombre de bin. Ajustez la binwidth, xlim(), ylim() et/ou les dimensions de la figure pour créer des hexagones plus ou moins allongés.

<table>
<tbody>
<tr class="odd">
<td><p>overplot %&gt;%</p>
<p><strong>ggplot</strong>(<strong>aes</strong>(x, y)) <strong>+</strong></p>
<p><strong>geom_hex</strong>(binwidth = <strong>c</strong>(0.25, 0.25))</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image30.png)

Figure 3.27 : Heatmap hexagonale basée sur le nombre de bin

3.9.4 Heatmap d’une matrice de corrélation

J’ai inclus le code pour créer une matrice de corrélation à partir d’un tableau de variables, mais vous n’avez pas à comprendre comment cela a été fait pour l’instant. Nous couvrirons les fonctions mutate() et gather() dans les leçons sur [dplyr (EN)](https://psyteachr.github.io/msc-data-skills/dplyr.html#dplyr) et [tidyr (EN)](https://psyteachr.github.io/msc-data-skills/tidyr.html#tidyr).

<table>
<tbody>
<tr class="odd">
<td><p><em># generate two sets of correlated variables (a and b)</em></p>
<p>heatmap &lt;- <strong>tibble</strong>(</p>
<p>a1 = <strong>rnorm</strong>(100),</p>
<p>b1 = <strong>rnorm</strong>(100)</p>
<p>) %&gt;%</p>
<p>mutate(</p>
<p>a2 = a1 + <strong>rnorm</strong>(100),</p>
<p>a3 = a1 + <strong>rnorm</strong>(100),</p>
<p>a4 = a1 + <strong>rnorm</strong>(100),</p>
<p>b2 = b1 + <strong>rnorm</strong>(100),</p>
<p>b3 = b1 + <strong>rnorm</strong>(100),</p>
<p>b4 = b1 + <strong>rnorm</strong>(100)</p>
<p>) %&gt;%</p>
<p><strong>cor</strong>() %&gt;% <em># create the correlation matrix</em></p>
<p><strong>as.data.frame</strong>() %&gt;% <em># make it a data frame</em></p>
<p><strong>rownames_to_column</strong>(var = "V1") %&gt;% <em># set rownames as V1</em></p>
<p><strong>gather</strong>("V2", "r", a1:b4) <em># wide to long (V2)</em></p></td>
</tr>
</tbody>
</table>

Une fois que vous avez une matrice de corrélation dans le bon format (format ‘long’), il est facile de créer une heatmap à l’aide de geom\_tile().

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(heatmap, <strong>aes</strong>(V1, V2, fill=r)) <strong>+</strong></p>
<p><strong>geom_tile</strong>() <strong>+</strong></p>
<p><strong>scale_fill_viridis_c</strong>()</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image31.png)

Figure 3.28 : Heatmap à l’aide de geom\_tile()

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image8.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Le type de fichier est déterminé par l’extension du fichier, ou bien en spécifiant l’argument device, qui peut prendre les valeurs suivants : “eps”, “ps”, “tex”, “pdf”, “jpeg”, “tiff”, “png”, “bmp”, “svg” ou “wmf”.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.10 Graphiques interactifs

Pour créer des graphiques interactifs, vous pouvez utiliser le package plotly. Il vous suffit d’assigner votre ggplot à une variable et d’utiliser la fonction ggplotly().

<table>
<tbody>
<tr class="odd">
<td><p>demog_plot &lt;- <strong>ggplot</strong>(pet_happy, <strong>aes</strong>(pet, happiness, fill=pet)) <strong>+</strong></p>
<p><strong>geom_point</strong>(position = <strong>position_jitter</strong>(width= 0.2, height = 0), size = 2)</p>
<p>ggplotly(demog_plot)</p></td>
</tr>
</tbody>
</table>

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image32.png)

Figure 3.29 : Graphique interactif avec plotly

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image8.png)

<table>
<tbody>
<tr class="odd">
<td><blockquote>
<p>Passez votre souris sur les points de données et cliquez sur les différentes étiquettes du graphique.</p>
</blockquote></td>
</tr>
</tbody>
</table>

3.11 Quizz

*N.B. : Pour afficher les solutions, surlignez la zone grisée à l’aide de votre curseur.*

1.  Générez un graphique comme celui ci-dessous à partir du jeu de données iris. Veillez à bien inclure des étiquettes d’axes personnalisés.

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image33.png)

\[Solution\]

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(iris, <strong>aes</strong>(Species, Petal.Width, fill = Species)) +</p>
<p><strong>geom_boxplot</strong>(show.legend = FALSE) +</p>
<p><strong>xlab</strong>("Flower Species") +</p>
<p><strong>ylab</strong>("Petal Width (in cm)")</p>
<p><em># there are many ways to do things, the code below is also correct</em></p>
<p><strong>ggplot</strong>(iris) +</p>
<p><strong>geom_boxplot</strong>(<strong>aes</strong>(Species, Petal.Width, fill = Species), show.legend = FALSE) +</p>
<p><strong>labs</strong>(x = "Flower Species",</p>
<p>y = "Petal Width (in cm)")</p></td>
</tr>
</tbody>
</table>

2.  Vous venez juste de créer un graphique avec le code suivant. Comment le sauvegarder ?

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(cars, <strong>aes</strong>(speed, dist)) <strong>+</strong></p>
<p><strong>geom_point</strong>() <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method = lm)</p></td>
</tr>
</tbody>
</table>

\[Solution\]

<table>
<tbody>
<tr class="odd">
<td><p># Les quatre possibilités fonctionnent</p>
<p><strong>ggsave</strong>()</p>
<p><strong>ggsave</strong>(“figname”)</p>
<p><strong>ggsave</strong>(“figname.png”)</p>
<p><strong>ggsave</strong>(“figname.png”, plot = cars)</p></td>
</tr>
</tbody>
</table>

3.  Déboguez le code suivant.

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(iris) <strong>+</strong></p>
<p><strong>geom_point</strong>(<strong>aes</strong>(Petal.Width, Petal.Length, colour = Species)) <strong>+</strong></p>
<p><strong>geom_smooth</strong>(method = lm) <strong>+</strong></p>
<p><strong>facet_grid</strong>(Species)</p></td>
</tr>
</tbody>
</table>

\[Solution\]

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(iris, <strong>aes</strong>(Petal.Width, Petal.Length, colour = Species)) +</p>
<p><strong>geom_point</strong>() +</p>
<p><strong>geom_smooth</strong>(method = lm) +</p>
<p><strong>facet_grid</strong>(~Species)</p></td>
</tr>
</tbody>
</table>

4.  Générez un graphique comme celui ci-dessous à l’aide du jeu de données ChickWeight.

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image34.png)

\[Solution\]

<table>
<tbody>
<tr class="odd">
<td><p><strong>ggplot</strong>(ChickWeight, <strong>aes</strong>(weight, Time)) +</p>
<p><strong>geom_hex</strong>(binwidth = <strong>c</strong>(10, 1)) +</p>
<p><strong>scale_fill_viridis_c</strong>()</p></td>
</tr>
</tbody>
</table>

5.  Générez un graphique comme celui ci-dessous à l’aide du jeu de données iris.

![](./Chapitre%203%20_%20Visualisation%20des%20données/media/image35.png)

\[Solution\]

<table>
<tbody>
<tr class="odd">
<td><p>pw &lt;- <strong>ggplot</strong>(iris, <strong>aes</strong>(Petal.Width, color = Species)) +</p>
<p><strong>geom_density</strong>() +</p>
<p><strong>xlab</strong>("Petal Width (in cm)")</p>
<p>pl &lt;- <strong>ggplot</strong>(iris, <strong>aes</strong>(Petal.Length, color = Species)) +</p>
<p><strong>geom_density</strong>() +</p>
<p><strong>xlab</strong>("Petal Length (in cm)") +</p>
<p><strong>coord_flip</strong>()</p>
<p>pw_pl &lt;- <strong>ggplot</strong>(iris, <strong>aes</strong>(Petal.Width, Petal.Length, color = Species)) +</p>
<p><strong>geom_point</strong>() +</p>
<p><strong>geom_smooth</strong>(method = lm) +</p>
<p><strong>xlab</strong>("Petal Width (in cm)") +</p>
<p><strong>ylab</strong>("Petal Length (in cm)")</p>
<p>cowplot::<strong>plot_grid</strong>(</p>
<p>pw, pl, pw_pl,</p>
<p>labels = <strong>c</strong>("A", "B", "C"),</p>
<p>nrow = 3</p>
<p>)</p></td>
</tr>
</tbody>
</table>

3.12 Exercices

Téléchargez les [exercices (EN)](https://psyteachr.github.io/msc-data-skills/exercises/03_ggplot_exercise.Rmd). Référez-vous aux [graphiques (EN)](https://psyteachr.github.io/msc-data-skills/exercises/03_ggplot_answers.html) pour voir à quoi vos graphiques devraient ressembler (cette page ne contient pas le code de réponse). Ne regardez les [réponses (EN)](https://psyteachr.github.io/msc-data-skills/exercises/03_ggplot_answers.Rmd) qu’après avoir tenté de répondre à toutes les questions.
