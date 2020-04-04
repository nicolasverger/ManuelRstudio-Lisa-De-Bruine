*Traduit par Zoé Lackner*![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image1.png)

# 5.1 Objectifs d’apprentissage

## 5.1.1 Niveau débutant

1.  Être capable d’utiliser les 6 principaux one-table verbes de dplyr :
    
      - [select()](https://psyteachr.github.io/msc-data-skills/dplyr.html#select)
    
      - [filter()](https://psyteachr.github.io/msc-data-skills/dplyr.html#filter)
    
      - [arrange()](https://psyteachr.github.io/msc-data-skills/dplyr.html#arrange)
    
      - [mutate()](https://psyteachr.github.io/msc-data-skills/dplyr.html#mutate)
    
      - [summarise()](https://psyteachr.github.io/msc-data-skills/dplyr.html#summarise)
    
      - [group\_by()](https://psyteachr.github.io/msc-data-skills/dplyr.html#group_by)

## 5.1.2 Niveau intermédiaire

2.  Aussi apprendre à utiliser ces one-table verbs additionnels :
    
      - [rename()](https://psyteachr.github.io/msc-data-skills/dplyr.html#rename)
    
      - [distinct()](https://psyteachr.github.io/msc-data-skills/dplyr.html#distinct)
    
      - [count()](https://psyteachr.github.io/msc-data-skills/dplyr.html#count)
    
      - [slice()](https://psyteachr.github.io/msc-data-skills/dplyr.html#slice)
    
      - [pull()](https://psyteachr.github.io/msc-data-skills/dplyr.html#pull)

## 5.1.3 Niveau avancé

3.  Avoir une bonne maîtrise des opérations [select()](https://psyteachr.github.io/msc-data-skills/dplyr.html#select_helpers)

4.  Utiliser les [fonctions windows](https://psyteachr.github.io/msc-data-skills/dplyr.html#window)

# 5.2 Ressources

*N.B. Les ressources marquées (EN) sont en anglais.*

  - [Chapter 5: Data Transformation](http://r4ds.had.co.nz/transform.html) in *R for Data Science (EN)*

  - [Data transformation cheat sheet](https://github.com/rstudio/cheatsheets/raw/master/source/pdfs/data-transformation-cheatsheet.pdf) *(EN)*

  - [Lecture slides on dplyr one-table verbs](https://psyteachr.github.io/msc-data-skills/slides/04_dplyr_slides.pdf) *(EN)*

  - [Chapter 16: Date and times](http://r4ds.had.co.nz/dates-and-times.html) in *R for Data Science (EN)*

# 5.3 Configuration

Vous aurez besoin des packages suivants.

<table>
<tbody>
<tr class="odd">
<td><p><em># libraries needed for these examples</em></p>
<p><strong>library</strong>(tidyverse)</p>
<p><strong>library</strong>(lubridate)</p>
<p><strong>set.seed</strong>(8675309) <em># makes sure random numbers are reproducible</em></p></td>
</tr>
</tbody>
</table>

## 5.4 Le jeu de données disgust

Ces exemples vous aideront à utiliser les données issues de [disgust.csv](https://psyteachr.github.io/data/disgust.csv) *(non accessible)*, qui contient des données issues de [Three Domain Disgust Scale](http://digitalrepository.unm.edu/cgi/viewcontent.cgi?article=1139&context=psy_etds) *(EN)* (échelle mesurant les différences inter-individuelles en terme de sensibilité au dégoût). Chaque participant est identifié par un unique user\_id et chaque questionnaire rempli est identifié par son unique id.

|                                                                                           |
| ----------------------------------------------------------------------------------------- |
| disgust \<- **read\_csv**("https://psyteachr.github.io/msc-data-skills/data/disgust.csv") |

*Instructions du Questionnaire* : Les items suivants décrivent une variété de concepts. Veuillez évaluer à quel point vous trouvez dégoûtant les concepts décrits à chaque item, où 0 signifie que vous ne trouvez pas du tout le concept dégoûtant, et 6 signifie que vous trouvez le concept extrêmement dégoûtant.

|                |                                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **nom de col** | **question**                                                                                      |
| moral1         | Voler une friandise dans une supérette.                                                           |
| moral2         | Voler à un voisin.                                                                                |
| moral3         | Un étudiant qui triche pour obtenir de bons résultats.                                            |
| moral4         | Abuser d’un ami.                                                                                  |
| moral5         | Imiter la signature de quelqu’un sur un document légal.                                           |
| moral6         | Doubler la queue pour acheter un des derniers tickets pour un spectacle.                          |
| moral7         | Mentir intentionnellement pendant une transaction financière.                                     |
| sexual1        | Ecouter deux inconnus avoir des rapports sexuels.                                                 |
| sexual2        | Pratiquer le sexe oral.                                                                           |
| sexual3        | Regarder une vidéo pornographique.                                                                |
| sexual4        | Découvrir que quelqu’un que vous n’appréciez pas éprouve des fantasmes sexuels vous concernant.   |
| sexual5        | Ramener dans votre chambre quelqu’un que vous venez de rencontrer pour avoir un rapport sexuel.   |
| sexual6        | Une personne inconnue, du sexe opposé, qui caresse volontairement votre cuisse dans un ascenseur. |
| sexual7        | Avoir un rapport annal avec une personne de sexe opposé.                                          |
| pathogen1      | Marcher dans un caca de chien.                                                                    |
| pathogen2      | S’asseoir à côté de quelqu’un qui a des plaies infectées sur les bras.                            |
| pathogen3      | Serrer la main d’un inconnu qui a les mains moites.                                               |
| pathogen4      | Apercevoir de la moisissure dans de vieux restes du réfrigérateur.                                |
| pathogen5      | Être à côté de quelqu’un qui a une forte odeur corporelle.                                        |
| pathogen6      | Apercevoir un cafard courir sur le sol.                                                           |
| pathogen7      | Toucher accidentellement la coupure ensanglantée de quelqu’un.                                    |

# 

# 5.5 Les six principaux verbes dplyr

La plupart des procédures de mise en forme des données que vous souhaiterez faire avec des données en psychologie impliquent les verbes tidyr que vous avez appris au [Chaptitre 3](https://psyteachr.github.io/msc-data-skills/tidyr.html#tidyr) et les six principaux verbes dplyr : select, filter, arrange, mutate, summarise, et group\_by.

## 5.5.1 select()

Permet de sélectionner les colonnes par leur nom ou numéro.

Vous pouvez sélectionner chaque colonne individuellement, séparées alors par des virgules (e.g., col1, col2). Mais vous pouvez aussi sélectionner toutes les colonnes comprises entre deux colonnes, en les séparant par deux points (e.g., start\_col:end\_col).

<table>
<tbody>
<tr class="odd">
<td><p>moral &lt;- disgust %&gt;% <strong>select</strong>(user_id, moral1:moral7)</p>
<p><strong>names</strong>(moral)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## [1] "user_id" "moral1" "moral2" "moral3" "moral4" "moral5"</p>
<p>## [7] "moral6" "moral7"</p></td>
</tr>
</tbody>
</table>

Vous pouvez aussi sélectionner des colonnes par leur numéro, ce qui est utile quand le nom des colonnes est long ou compliqué.

<table>
<tbody>
<tr class="odd">
<td><p>sexual &lt;- disgust %&gt;% <strong>select</strong>(2, 11:17)</p>
<p><strong>names</strong>(sexual)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## [1] "user_id" "sexual1" "sexual2" "sexual3" "sexual4" "sexual5"</p>
<p>## [7] "sexual6" "sexual7"</p></td>
</tr>
</tbody>
</table>

De plus, vous pouvez utiliser un symbole moins pour dé-sélectionner des colonnes, conservant alors toutes les autres colonnes du tableau. Si vous souhaitez exclure un intervalle de colonnes, il faut tout d’abord placer des parenthèses autour de l’intervalle (e.g., -(moral1:moral7), pas-moral1:moral7).

<table>
<tbody>
<tr class="odd">
<td><p>pathogen &lt;- disgust %&gt;% <strong>select</strong>(-id, -date, -(moral1:sexual7))</p>
<p><strong>names</strong>(pathogen)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## [1] "user_id" "pathogen1" "pathogen2" "pathogen3" "pathogen4"</p>
<p>## [6] "pathogen5" "pathogen6" "pathogen7"</p></td>
</tr>
</tbody>
</table>

Vous pouvez aussi sélectionner des colonnes en fonction de critères qui sont compris dans le nom de la colonne.{\#select\_helpers}

### 5.5.1.1 starts\_with()

Sélectionne les colonnes qui commencent par une chaîne de caractères.

<table>
<tbody>
<tr class="odd">
<td><p>u &lt;- disgust %&gt;% <strong>select</strong>(<strong>starts_with</strong>("u"))</p>
<p><strong>names</strong>(u)</p></td>
</tr>
</tbody>
</table>

|                       |
| --------------------- |
| \#\# \[1\] "user\_id" |

### 5.5.1.2 ends\_with()

Sélectionne les colonnes qui terminent par une chaîne de caractères.

<table>
<tbody>
<tr class="odd">
<td><p>firstq &lt;- disgust %&gt;% <strong>select</strong>(<strong>ends_with</strong>("1"))</p>
<p><strong>names</strong>(firstq)</p></td>
</tr>
</tbody>
</table>

|                                           |
| ----------------------------------------- |
| \#\# \[1\] "moral1" "sexual1" "pathogen1" |

### 5.5.1.3 contains()

Sélectionne les colonnes qui contiennent une chaîne de caractères.

<table>
<tbody>
<tr class="odd">
<td><p>pathogen &lt;- disgust %&gt;% <strong>select</strong>(<strong>contains</strong>("pathogen"))</p>
<p><strong>names</strong>(pathogen)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## [1] "pathogen1" "pathogen2" "pathogen3" "pathogen4" "pathogen5"</p>
<p>## [6] "pathogen6" "pathogen7"</p></td>
</tr>
</tbody>
</table>

### 5.5.1.4 num\_range()

Sélectionne les colonnes avec un nom qui correspond à la structure prefix.

<table>
<tbody>
<tr class="odd">
<td><p>moral &lt;- disgust %&gt;% <strong>select</strong>(<strong>num_range</strong> ("moral", 2:4))</p>
<p><strong>names</strong>(moral_4)</p></td>
</tr>
</tbody>
</table>

|                                       |
| ------------------------------------- |
| \#\# \[1\] "moral2" "moral3" "moral4" |

|                                                                               |                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image2.png) | Vous pouvez utiliser width pour paramétrer le nombre de chiffres avant le zéro. Par exemple, num\_range(‘var\_’, 8:10, width=2) permet de sélectionner les colonnes var\_08, var\_09, et var\_10. |

## 5.5.2 filter()

Permet de sélectionner des lignes en fonction de critères de la colonne.

Ce code permet de sélectionner toutes les lignes dont le user\_id est de 1.

|                                        |
| -------------------------------------- |
| disgust %\>% **filter**(user\_id == 1) |

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 1 x 24</p>
<p>## id user_id date moral1 moral2 moral3 moral4 moral5</p>
<p>## &lt;dbl&gt; &lt;dbl&gt; &lt;date&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 1 1 2008-07-10 2 2 1 2 1</p>
<p>## # … with 16 more variables: moral6 &lt;dbl&gt;, moral7 &lt;dbl&gt;,</p>
<p>## # sexual1 &lt;dbl&gt;, sexual2 &lt;dbl&gt;, sexual3 &lt;dbl&gt;, sexual4 &lt;dbl&gt;, ## # sexual5 &lt;dbl&gt;, sexual6 &lt;dbl&gt;, sexual7 &lt;dbl&gt;,</p>
<p>## # pathogen1 &lt;dbl&gt;, pathogen2 &lt;dbl&gt;, pathogen3 &lt;dbl&gt;,</p>
<p>## # pathogen4 &lt;dbl&gt;,pathogen5 &lt;dbl&gt;, pathogen6 &lt;dbl&gt;,</p>
<p>## # pathogen7 &lt;dbl&gt;</p></td>
</tr>
</tbody>
</table>

|                                                                               |                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image3.png) | N’oubliez pas d’utiliser == et non = pour vérifier si deux choses sont équivalentes. Un seul = permet d’assigner la valeur de droite à la variable de gauche et permet (en général) de l’évaluer comme TRUE. |

Vous pouvez sélectionner plusieurs critères en les séparant par des virgules.

<table>
<tbody>
<tr class="odd">
<td><p>amoral &lt;- disgust %&gt;% <strong>filter</strong>(</p>
<p>moral1 == 0,</p>
<p>moral2 == 0,</p>
<p>moral3 == 0,</p>
<p>moral4 == 0,</p>
<p>moral5 == 0,</p>
<p>moral6 == 0,</p>
<p>moral7 == 0</p>
<p>)</p></td>
</tr>
</tbody>
</table>

Vous pouvez utiliser des symboles &, |, et \! pour vouloir dire “et”, “ou”, et “pas”. Vous pouvez utiliser des opérateurs pour faire des équations.

<table>
<tbody>
<tr class="odd">
<td><p><em>#</em> <em>everyone who chose either 0 or 7 for question moral1</em></p>
<p>moral_extremes &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(moral1 == 0 | moral1 == 7)</p>
<p><em># everyone who chose the same answer for all moral questions</em></p>
<p>moral_consistent &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(</p>
<p>moral2 == moral1 &amp;</p>
<p>moral3 == moral1 &amp;</p>
<p>moral4 == moral1 &amp;</p>
<p>moral5 == moral1 &amp;</p>
<p>moral6 == moral1 &amp;</p>
<p>moral7 == moral1</p>
<p>)</p>
<p><em># everyone who did not answer 7 for all 7 moral questions</em></p>
<p>moral_no_ceiling &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(moral1+moral2+moral3+moral4+moral5+moral6+moral7 != 7*7)</p></td>
</tr>
</tbody>
</table>

Parfois, vous devez exclure des participants IDs pour des raisons que nous ne formulerons pas ici. L’opérateur %in% est utile pour tester si la valeur d’une colonne est dans une liste. Il faut entourer l’équation de parenthèses et ajouter un \! devant pour s’assurer qu’une ou plusieurs valeurs soient retirées de la liste.

<table>
<tbody>
<tr class="odd">
<td><p>no_researchers &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(!(user_id %in% <strong>c</strong>(1,2)))</p></td>
</tr>
</tbody>
</table>

### 5.5.2.1 Dates

Vous pouvez utiliser le package lubridate pour travailler avec les dates. Par exemple, vous pouvez utiliser la fonction year() pour retourner l’année de la colonne date et ensuite sélectionner les données uniquement collectées en 2010.

<table>
<tbody>
<tr class="odd">
<td><p>disgust2010 &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(<strong>year</strong>(date) == 2010)</p></td>
</tr>
</tbody>
</table>

Vous pouvez aussi sélectionner les données d’il y a 5 ans. Vous pouvez alors utiliser la fonction range pour vérifier les dates minimales et maximales du jeux de données résultant.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_5ago &lt;- disgust %&gt;%</p>
<p><strong>filter</strong>(date &lt; <strong>today</strong>() - <strong>dyears</strong>(5))</p>
<p><strong>range</strong> (disgust_5ago$date)</p></td>
</tr>
</tbody>
</table>

|                                      |
| ------------------------------------ |
| \#\# \[1\] "2008-07-10" "2014-08-04" |

## 5.5.3 arrange()

Permet d’ordonner ses données.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_order &lt;- disgust %&gt;%</p>
<p><strong>arrange</strong>(id)</p>
<p><strong>head</strong>(disgust_order)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 6 x 24</p>
<p>## id user_id date moral1 moral2 moral3 moral4 moral5</p>
<p>## &lt;dbl&gt; &lt;dbl&gt; &lt;date&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 1 1 2008-07-10 2 2 1 2 1</p>
<p>## 2 3 155324 2008-07-11 2 4 3 5 2</p>
<p>## 3 4 155366 2008-07-12 6 6 6 3 6</p>
<p>## 4 5 155370 2008-07-12 6 6 4 6 6</p>
<p>## 5 6 155386 2008-07-12 2 4 0 4 0</p>
<p>## 6 7 155409 2008-07-12 4 5 5 4 5</p>
<p>## # … with 16 more variables: moral6 &lt;dbl&gt;, moral7 &lt;dbl&gt;,</p>
<p>## # sexual1 &lt;dbl&gt;, sexual2 &lt;dbl&gt;, sexual3 &lt;dbl&gt;, sexual4 &lt;dbl&gt;,</p>
<p>## # sexual5 &lt;dbl&gt;, sexual6 &lt;dbl&gt;, sexual7 &lt;dbl&gt;,</p>
<p>## # pathogen1 &lt;dbl&gt;, pathogen2 &lt;dbl&gt;, pathogen3 &lt;dbl&gt;,</p>
<p>## # pathogen4 &lt;dbl&gt;, pathogen5 &lt;dbl&gt;, pathogen6 &lt;dbl&gt;,</p>
<p>## # pathogen7 &lt;dbl&gt;</p></td>
</tr>
</tbody>
</table>

En utilisant la fonction desc() vous pouvez inverser le sens.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_order &lt;- disgust %&gt;%</p>
<p><strong>arrange</strong>(<strong>desc</strong>(id))</p>
<p><strong>head</strong>(disgust_order)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 6 x 24</p>
<p>## id user_id date moral1 moral2 moral3 moral4 moral5</p>
<p>## &lt;dbl&gt; &lt;dbl&gt; &lt;date&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 39456 356866 2017-08-21 1 1 1 1 1</p>
<p>## 2 39447 128727 2017-08-13 2 4 1 2 2</p>
<p>## 3 39371 152955 2017-06-13 6 6 3 6 6</p>
<p>## 4 39342 48303 2017-05-22 4 5 4 4 6</p>
<p>## 5 39159 151633 2017-04-04 4 5 6 5 3</p>
<p>## 6 38942 370464 2017-02-01 1 5 0 6 5</p>
<p>## # … with 16 more variables: moral6 &lt;dbl&gt;,moral7 &lt;dbl&gt;,</p>
<p>## # sexual1 &lt;dbl&gt;, sexual2 &lt;dbl&gt;, sexual3 &lt;dbl&gt;, sexual4 &lt;dbl&gt;,</p>
<p>## # sexual5 &lt;dbl&gt;, sexual6 &lt;dbl&gt;, sexual7 &lt;dbl&gt;,</p>
<p>## # pathogen1 &lt;dbl&gt;, pathogen2 &lt;dbl&gt;, pathogen3 &lt;dbl&gt;,</p>
<p>## # pathogen4 &lt;dbl&gt;,pathogen5 &lt;dbl&gt;, pathogen6 &lt;dbl&gt;,</p>
<p>## # pathogen7 &lt;dbl&gt;</p></td>
</tr>
</tbody>
</table>

### 

## 5.5.4 mutate()

Permet de créer de nouvelles colonnes. C’est une des fonctions les plus utiles du package tidyverse.

Pour partir de variables déjà présentes dans le jeux de données, il faut se référer à leur nom (sans les guillemets). Vous pouvez créer plus d’une colonne, en séparant les colonnes créée par une virgule. Une fois que vous avez créé une nouvelle colonne, vous pouvez immédiatement vous en servir pour créer une nouvelle variable (e.g., total ci-dessous).

<table>
<tbody>
<tr class="odd">
<td><p>disgust_total &lt;- disgust %&gt;%</p>
<p><strong>mutate</strong>(</p>
<p>pathogen = pathogen1 + pathogen2 + pathogen3 + pathogen4 + pathogen5 + pathogen6 + pathogen7,</p>
<p>moral = moral1 + moral2 + moral3 + moral4 + moral5 + moral6 + + moral7,</p>
<p>sexual = sexual1 + sexual2 + sexual3 + sexual4 + sexual5 + sexual6 + sexual7,</p>
<p>total = pathogen + moral + sexual,</p>
<p>user_id = <strong>paste0</strong>("U", user_id)</p>
<p>)</p>
<p><strong>head</strong>(disgust_total)</p></td>
</tr>
</tbody>
</table>

|                                                                               |                                                                                                                                                                 |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image3.png) | Vous pouvez écraser une colonne en donnant à une nouvelle colonne le même nom que celle-ci. Attention, vous ne pourrez alors plus accéder à l’ancienne colonne. |

## 

## 5.5.5 summarise()

Permet de créer un résumé des statistiques pour le jeux de données. Vérifier le [Formulaire de mise en forme des données](https://www.rstudio.org/links/data_wrangling_cheat_sheet) *(EN)* et le [Formulaire de transformation des données](https://github.com/rstudio/cheatsheets/raw/master/source/pdfs/data-transformation-cheatsheet.pdf) *(EN)* pour accéder à plusieurs fonctions de résumé. Quelques fonctions communes sont : mean(), sd(), n(), sum(), et quantile().

<table>
<tbody>
<tr class="odd">
<td><p>disgust_total %&gt;%</p>
<p><strong>summarise</strong>(</p>
<p>n = <strong>n</strong>(),</p>
<p>q25 = <strong>quantile</strong>(total, .25, na.rm = TRUE),</p>
<p>q50 = <strong>quantile</strong>(total, .50, na.rm = TRUE),</p>
<p>q75 = <strong>quantile</strong>(total, .75, na.rm = TRUE),</p>
<p>avg_total = <strong>mean</strong>(total, na.rm = TRUE),</p>
<p>sd_total = <strong>sd</strong>(total, na.rm = TRUE),</p>
<p>min_total = <strong>min</strong>(total, na.rm = TRUE),</p>
<p>max_total = <strong>max</strong>(total, na.rm = TRUE)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 1 x 8</p>
<p>## n q25 q50 q75 avg_total sd_total min_total</p>
<p>## &lt;int&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 20000 59 71 83 70.7 18.2 0</p>
<p>## # … with 1 more variable: max_total &lt;dbl&gt;</p></td>
</tr>
</tbody>
</table>

### 

## 5.5.6 group\_by()

Permet de créer un sous-ensemble de données. Vous pouvez notamment l’utiliser pour créer des résumés, pour apprécier la valeur moyenne de chaque groupe expérimental par exemple.

Ici, nous allons utiliser mutate pour créer de nouvelles colonnes s’appelant year, grouper les données en fonction de year, et calculer les scores moyens.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_total %&gt;%</p>
<p><strong>mutate</strong>(year = <strong>year</strong>(date)) %&gt;%</p>
<p><strong>group_by</strong>(year) %&gt;%</p>
<p><strong>summarise</strong>(</p>
<p>n = <strong>n</strong>(),</p>
<p>avg_total = <strong>mean</strong>(total, na.rm = TRUE),</p>
<p>sd_total = <strong>sd</strong>(total, na.rm = TRUE),</p>
<p>min_total = <strong>min</strong>(total, na.rm = TRUE),</p>
<p>max_total = <strong>max</strong>(total, na.rm = TRUE)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 10 x 6</p>
<p>## year n avg_total sd_total min_total max_total</p>
<p>## &lt;dbl&gt; &lt;int&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 2008 2578 70.3 18.5 0 126</p>
<p>## 2 2009 2580 69.7 18.6 3 126</p>
<p>## 3 2010 1514 70.6 18.9 6 126</p>
<p>## 4 2011 6046 71.3 17.8 0 126</p>
<p>## 5 2012 5938 70.4 18.4 0 126</p>
<p>## 6 2013 1251 71.6 17.6 0 126</p>
<p>## 7 2014 58 70.5 17.2 19 113</p>
<p>## 8 2015 21 74.3 16.9 43 107</p>
<p>## 9 2016 8 67.9 32.6 0 110</p>
<p>## 10 2017 6 57.2 27.9 21 90</p></td>
</tr>
</tbody>
</table>

Vous pouvez aussi combiner les fonctions filter et group\_by. L’exemple suivant retourne le plus petit score total pour chaque année.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_total %&gt;%</p>
<p><strong>mutate</strong>(year = <strong>year</strong>(date)) %&gt;%</p>
<p><strong>select</strong>(user_id, year, total) %&gt;%</p>
<p><strong>group_by</strong>(year) %&gt;%</p>
<p><strong>filter</strong>(<strong>rank</strong>(total) == 1) %&gt;%</p>
<p><strong>arrange</strong>(year)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 7 x 3</p>
<p>## # Groups: year [7]</p>
<p>## user_id year total</p>
<p>## &lt;chr&gt; &lt;dbl&gt; &lt;dbl&gt;</p>
<p>## 1 U236585 2009 3</p>
<p>## 2 U292359 2010 6</p>
<p>## 3 U245384 2013 0</p>
<p>## 4 U206293 2014 19</p>
<p>## 5 U407089 2015 43</p>
<p>## 6 U453237 2016 0</p>
<p>## 7 U356866 2017 21</p></td>
</tr>
</tbody>
</table>

Une autre possibilité est d’utiliser mutate après group\_by. L’exemple qui suit calcule un score centré sur la moyenne pour chaque sujet en groupant les scores en fonction de user\_id, puis de soustraire la moyenne spécifique à chaque groupe par chaque score. Notez qu’il faut d’abord utiliser gather pour organiser les données en un long format.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_smc &lt;- disgust %&gt;%</p>
<p><strong>gather</strong>(“question”, “score”, moral1:pathogen7) %&gt;%</p>
<p><strong>group_by</strong>(user_id) %&gt;%</p>
<p><strong>mutate</strong>(score_smc = score - <strong>mean</strong>(score, na.rm = TRUE))</p></td>
</tr>
</tbody>
</table>

## 5.5.7 Combinaison des différentes fonctions

Beaucoup des actions que nous avons réalisées plus tôt seraient facilitées avec des données dans un format tidy. Nous pourrions alors utiliser group\_by pour calculer différents scores.

|                                                                               |                                                                                                                                                                                                                                                        |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image3.png) | C’est un bon exercice d’utiliser ungroup() après avoir utilisé group\_by et summarise. Oublier de rompre les groupes dans le jeux de données n’affectera pas les traitements ultérieurs, cependant, cela pourrait beaucoup perturber d’autres actions. |

Ainsi, nous pouvons répartir les 3 domaines : calculer le score total, supprimer les lignes où le total est absent (NA) et calculer la moyenne par an.

<table>
<tbody>
<tr class="odd">
<td><p>disgust_tidy &lt;- <strong>read_csv</strong>("data/disgust.csv") %&gt;%</p>
<p><strong>gather</strong>(“question”, “score”, moral1:pathogen7) %&gt;%</p>
<p><strong>separate</strong>(question, <strong>c</strong>("domain","q_num"), sep = -1) %&gt;%</p>
<p><strong>group_by</strong>(user_id) %&gt;%</p>
<p><strong>summarise</strong>(score = <strong>mean</strong>(score)) %&gt;%</p>
<p><strong>mutate</strong>(score_smc = score - <strong>mean</strong>(score, na.rm = TRUE))</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## Parsed with column specification:</p>
<p>## cols(</p>
<p>## .default = col_double(),</p>
<p>## date = col_date(format = "")</p>
<p>## )</p></td>
</tr>
</tbody>
</table>

|                                                    |
| -------------------------------------------------- |
| \#\# See spec(...) for full column specifications. |

<table>
<tbody>
<tr class="odd">
<td><p>disgust_tidy2 &lt;- disgust_tidy %&gt;%</p>
<p><strong>spread</strong>(domain, score) %&gt;%</p>
<p><strong>mutate</strong>(</p>
<p>total = moral + sexual + pathogen,</p>
<p>year = <strong>year</strong>(date)</p>
<p>) %&gt;%</p>
<p><strong>filter</strong>(!<strong>is.na</strong>(total)) %&gt;%</p>
<p><strong>arrange</strong>(user_id)</p>
<p>disgust_tidy3 &lt;- disgust_tidy2 %&gt;%</p>
<p><strong>group_by</strong>(year) %&gt;%</p>
<p><strong>summarise</strong>(</p>
<p>n = <strong>n</strong>(),</p>
<p>avg_pathogen = <strong>mean</strong>(pathogen),</p>
<p>avg_moral = <strong>mean</strong>(moral),</p>
<p>avg_sexual = <strong>mean</strong>(sexual),</p>
<p>first_user = <strong>first</strong>(user_id),</p>
<p>last_user = <strong>last</strong>(user_id)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

## 

# 5.6 Verbes one-table dplyr additionnels

Vous pouvez utiliser les exemples de codes qui suivent et la page d’aide pour trouver à quoi servent les verbes one-table qui suivent. La plupart ont un nom explicite.

## 5.6.1 rename()

<table>
<tbody>
<tr class="odd">
<td><p>iris_underscore &lt;- iris %&gt;%</p>
<p><strong>rename</strong>(</p>
<p>sepal_length = Sepal.Length,</p>
<p>sepal_width = Sepal.Width,</p>
<p>petal_length = Petal.Length,</p>
<p>petal_width = Petal.Width)</p>
<p><strong>name</strong>(iris_underscore)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## [1] "sepal_length" "sepal_width" "petal_length" "petal_width"</p>
<p>## [5] "Species"</p></td>
</tr>
</tbody>
</table>

|                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ![](./Chapitre%205%20_%20Mise%20en%20forme%20des%20données/media/image4.png)La plupart du monde s'emmêle les pinceaux un jour ou l’autre avec rename() et essaie de mettre le nom original de la colonne à gauche et le nouveau nom à droite. Vous pouvez essayer pour voir le message d’erreur qui apparaît à cette occasion. |

### 

## 5.6.2 distinct()

<table>
<tbody>
<tr class="odd">
<td><p><em># create a data table with duplicated values</em></p>
<p>dupes &lt;- <strong>tibble</strong>(</p>
<p>id = <strong>rep</strong>(1 : 5, 2),</p>
<p>dv = <strong>rep</strong>(LETTERS[1 : 5], 2)</p>
<p>)</p>
<p><strong>distinct</strong>(dupes)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 5 x 2</p>
<p>## id dv</p>
<p>## &lt;int&gt; &lt;chr&gt;</p>
<p>## 1 1 A</p>
<p>## 2 2 B</p>
<p>## 3 3 C</p>
<p>## 4 4 D</p>
<p>## 5 5 E</p></td>
</tr>
</tbody>
</table>

### 

## 5.6.3 count()

<table>
<tbody>
<tr class="odd">
<td><p><em># how many observations from each species are in iris?</em></p>
<p><strong>count</strong>(iris, Species)</p></td>
</tr>
</tbody>
</table>

### 

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 3 x 2</p>
<p>## Species n</p>
<p>## &lt;fct&gt; &lt;int&gt;</p>
<p>## 1 setosa 50</p>
<p>## 2 versicolor 50</p>
<p>## 3 virginica 50</p></td>
</tr>
</tbody>
</table>

### 

## 5.6.4 slice()

<table>
<tbody>
<tr class="odd">
<td><p><strong>tibble</strong>(</p>
<p>id = 1 : 10,</p>
<p>condition = <strong>rep</strong>(<strong>c</strong>(“A”, “B”), 5)</p>
<p>) %&gt;%</p>
<p><strong>slice</strong>(3:6, 9)</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 5 x 2</p>
<p>## id condition</p>
<p>## &lt;int&gt; &lt;chr&gt;</p>
<p>## 1 3 A</p>
<p>## 2 4 B</p>
<p>## 3 5 A</p>
<p>## 4 6 B</p>
<p>## 5 9 A</p></td>
</tr>
</tbody>
</table>

### 

## 5.6.5 pull()

<table>
<tbody>
<tr class="odd">
<td><p>iris %&gt;%</p>
<p><strong>group_by</strong>(Species) %&gt;%</p>
<p><strong>summarise_all</strong>(mean) %&gt;%</p>
<p><strong>pull</strong>(Sepal.Length)</p></td>
</tr>
</tbody>
</table>

|                              |
| ---------------------------- |
| \#\# \[1\] 5.006 5.936 6.588 |

# 5.7 Fonctions Window

Les fonctions Window utilisent l’ordre des lignes pour calculer des valeurs. Vous pouvez les utiliser pour réaliser des actions qui nécessitent un rang ou un ordre, comme choisir le score maximal pour chaque classe ou accéder à la première et dernière ligne, et comme calculer des sommes ou des moyennes cumulatives.

La [vignette de fonction dplyr window](https://dplyr.tidyverse.org/articles/window-functions.html) *(EN)* donne de nombreuses explications de ces fonctions, mais nous allons tout de même vous fournir quelques exemples des fonctions les plus utiles ci-dessous.

## 5.7.1 Fonctions pour attribuer un rang à ses données

<table>
<tbody>
<tr class="odd">
<td><p><strong>tibble</strong> (</p>
<p>id = 1:5,</p>
<p>“Data Skills” = <strong>c</strong>(16, 17, 17, 19, 20),</p>
<p>“Statistics” = <strong>c</strong>(14, 16, 18, 18, 19)</p>
<p>) %&gt;%</p>
<p><strong>gather</strong>(class, grade, 2:3) %&gt;%</p>
<p><strong>group_by</strong>(class) %&gt;%</p>
<p><strong>mutate</strong>(row_number = <strong>row_number</strong>(),</p>
<p>rank = <strong>rank</strong>(grade),</p>
<p>min_rank = <strong>min_rank</strong>(grade),</p>
<p>dense_rank = <strong>dense_rank</strong>(grade),</p>
<p>quartile = <strong>ntile</strong>(grade, 4),</p>
<p>percentile = <strong>ntile</strong>(grade, 100))</p></td>
</tr>
</tbody>
</table>

### 

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 10 x 9</p>
<p>## # Groups: class [2]</p>
<p>## id class grade row_number rank min_rank dense_rank</p>
<p>## &lt;int&gt; &lt;chr&gt; &lt;dbl&gt; &lt;int&gt; &lt;dbl&gt; &lt;int&gt; &lt;int&gt;</p>
<p>## 1 1 Data… 16 1 1 1 1</p>
<p>## 2 2 Data… 17 2 2.5 2 2</p>
<p>## 3 3 Data… 17 3 2.5 2 2</p>
<p>## 4 4 Data… 19 4 4 4 3</p>
<p>## 5 5 Data… 20 5 5 5 4</p>
<p>## 6 1 Stat… 14 1 1 1 1</p>
<p>## 7 2 Stat… 16 2 2 2 2</p>
<p>## 8 3 Stat… 18 3 3.5 3 3</p>
<p>## 9 4 Stat… 18 4 3.5 3 3</p>
<p>## 10 5 Stat… 19 5 5 5 4</p>
<p>## # … with 2 more variables: quartile &lt;int&gt;, percentile &lt;int&gt;</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Quelles sont les différences entre row_number(), rank(), min_rank(), dense_rank(), et ntile() ?<img src="./Chapitre 5 _ Mise en forme des données/media/image4.png" style="width:0.43229in;height:0.26042in" /></p></li>
<li><p>Pourquoi row_number() ne nécessite pas d’argument ?</p></li>
<li><p>Que se passerait t’il si vous écriviez l’argument grade ou class pour row_number() ?</p></li>
<li><p>Que pensez-vous qu’il arriverait si vous supprimiez la ligne group_by(class), ci-dessus ?</p></li>
<li><p>Et que pensez-vous qu’il surviendrait si vous ajoutiez id comme argument au verbe group_by ?</p></li>
<li><p>Que se passe t’il si vous changez l’ordre des lignes?</p></li>
<li><p>Que permet de faire le second argument dans ntile() ?</p></li>
</ul></td>
</tr>
</tbody>
</table>

Vous pouvez utiliser une fonction window pour regrouper les données en quantiles.

<table>
<tbody>
<tr class="odd">
<td><p>iris %&gt;%</p>
<p><strong>group_by</strong>(tertile = <strong>ntile</strong>(Sepal.Length, 3)) %&gt;%</p>
<p><strong>summarise</strong>(mean.Sepal.Length = <strong>mean</strong>(Sepal.Length))</p></td>
</tr>
</tbody>
</table>

### 

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 3 x 2</p>
<p>## tertile mean.Sepal.Length</p>
<p>## &lt;int&gt; &lt;dbl&gt;</p>
<p>## 1 1 4.94</p>
<p>## 2 2 5.81</p>
<p>## 3 3 6.78</p></td>
</tr>
</tbody>
</table>

## 5.7.2 Fonctions offset

<table>
<tbody>
<tr class="odd">
<td><p><strong>tibble</strong> (</p>
<p>trial = 1:10,</p>
<p>cond = <strong>rep</strong>(<strong>c</strong>(“exp”, “ctrl”), <strong>c</strong>(6, 4)),</p>
<p>score = <strong>rpois</strong>(10, 4)</p>
<p>) %&gt;%</p>
<p><strong>mutate</strong>(</p>
<p>score_change = score - <strong>lag</strong>(score, order_by = trial),</p>
<p>last_cond_trial = cond != <strong>lead</strong>(cond, default = TRUE)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

### 

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 10 x 5</p>
<p>## trial cond score score_change last_cond_trial</p>
<p>## &lt;int&gt; &lt;chr&gt; &lt;int&gt; &lt;int&gt; &lt;lgl&gt;</p>
<p>## 1 1 exp 2 NA FALSE</p>
<p>## 2 2 exp 4 2 FALSE</p>
<p>## 3 3 exp 5 1 FALSE</p>
<p>## 4 4 exp 5 0 FALSE</p>
<p>## 5 5 exp 3 -2 FALSE</p>
<p>## 6 6 exp 5 2 TRUE</p>
<p>## 7 7 ctrl 9 4 FALSE</p>
<p>## 8 8 ctrl 6 -3 FALSE</p>
<p>## 9 9 ctrl 6 0 FALSE</p>
<p>## 10 10 ctrl 4 -2 TRUE</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><p>Veuillez maintenant regarder les pages d’aide pour lag() et lead().<img src="./Chapitre 5 _ Mise en forme des données/media/image4.png" style="width:0.43229in;height:0.26042in" /></p>
<ul>
<li><p>Qu’arrive t’il si vous supprimez l’argument order_by ou que vous remplacez trial par cond ?</p></li>
<li><p>Que fait l’argument default ?</p></li>
<li><p>Pouvez-vous trouver des circonstances pour lesquelles les fonctions lag() et lead() vous seraient utiles pour traiter vos propres données ?</p></li>
</ul></td>
</tr>
</tbody>
</table>

## 5.7.3 Fonctions cumulatives

cumsum(), cummin(), et cummax() sont des fonctions R qui permettent de calculer des moyennes cumulées, des minimums cumulés, ainsi que des maximums cumulés. Le package dplyr introduit cumany() et cumall(), qui renvoient TRUE dès qu’une ou plusieurs valeur(s) précédente(s) répond(ent) à leur critère.

<table>
<tbody>
<tr class="odd">
<td><p><strong>tibble</strong> (</p>
<p>time = 1:10,</p>
<p>obs = <strong>c</strong>(1, 0, 1, 2, 4, 3, 1, 0, 3, 5)</p>
<p>) %&gt;%</p>
<p><strong>mutate</strong>(</p>
<p>cumsum = <strong>cumsum</strong>(obs),</p>
<p>cummin = <strong>cummin</strong>(obs),</p>
<p>cummax = <strong>cummax</strong>(obs),</p>
<p>cumany = <strong>cumany</strong>(obs == 3),</p>
<p>cumall = <strong>cumall</strong>(obs &lt; 4)</p>
<p>)</p></td>
</tr>
</tbody>
</table>

### 

<table>
<tbody>
<tr class="odd">
<td><p>## # A tibble: 10 x 7</p>
<p>## time obs cumsum cummin cummax cumany cumall</p>
<p>## &lt;int&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;dbl&gt; &lt;lgl&gt; &lt;lgl&gt;</p>
<p>## 1 1 1 1 1 1 FALSE TRUE</p>
<p>## 2 2 0 1 0 1 FALSE TRUE</p>
<p>## 3 3 1 2 0 1 FALSE TRUE</p>
<p>## 4 4 2 4 0 2 FALSE TRUE</p>
<p>## 5 5 4 8 0 4 FALSE FALSE</p>
<p>## 6 6 3 11 0 4 TRUE FALSE</p>
<p>## 7 7 1 12 0 4 TRUE FALSE</p>
<p>## 8 8 0 12 0 4 TRUE FALSE</p>
<p>## 9 9 3 15 0 4 TRUE FALSE</p>
<p>## 10 10 5 20 0 5 TRUE FALSE</p></td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Qu’est ce qui surviendrait si vous remplaciez cumany(obs == 3) par cumany(obs &gt; 2) ?<img src="./Chapitre 5 _ Mise en forme des données/media/image4.png" style="width:0.43229in;height:0.26042in" /></p></li>
<li><p>Qu’est ce qui surviendrait si vous changiez cumall(obs &lt; 4) par cumall(obs &lt; 2) ?</p></li>
<li><p>Pouvez-vous trouver des circonstances pour lesquelles les fonctions cumany() et cumall() vous seraient utiles pour traiter vos propres données ?</p></li>
</ul></td>
</tr>
</tbody>
</table>

# 5.8 Exercices

Téléchargez les [exercices](https://psyteachr.github.io/msc-data-skills/exercises/05_dplyr_exercise.Rmd) *(EN)*. Vous pouvez aussi consulter les [solutions](https://psyteachr.github.io/msc-data-skills/exercises/05_dplyr_answers.Rmd) *(EN)* une fois après avoir essayé de répondre à toutes les questions.
