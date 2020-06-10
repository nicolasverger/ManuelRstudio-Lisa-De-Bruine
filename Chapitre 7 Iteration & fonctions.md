# [Data Skills for Reproducible Science](https://psyteachr.github.io/msc-data-skills/)

# **Chapitre 7 Itération & Fonctions**

Nicolas B. Verger

Relecture Cédric Batailler

## **7.1 Objectifs du cours**

Vous apprendrez les fonctions et l’itération en simulant des données afin de réaliser une analyse de puissance statistique pour un test t indépendant.

### **7.1.1 Niveau débutant**

1. Travailler avec les fonctions rep, seq, and replicate (lien)

2. Utiliser des [arguments](https://psyteachr.github.io/msc-data-skills/func.html#arguments) par ordre ou par nom

3. Ecrire votre propre fonction personnalisée ([custom functions](https://psyteachr.github.io/msc-data-skills/func.html#custom-functions)) avec function()

4. Définir des valeurs par défaut ([default values](https://psyteachr.github.io/msc-data-skills/func.html#defaults)) pour les arguments de vos fonctions. 

### **7.1.2 Niveau intermédiaire**

1. Comprendre la portée([scope](https://psyteachr.github.io/msc-data-skills/func.html#scope))

2. Gérer les erreurs et avertissements dans une fonction ([error handling and warnings](https://psyteachr.github.io/msc-data-skills/func.html#warnings-errors))

### **7.1.3 Niveau avancé**

![image alt text](image_0.gif)

Les sujets ci-dessous ne sont pas (encore) détaillés dans ce matériel, mais constituent des directions pour un apprentissage autodidacte.

1. La répétition des commandes et le traitement du résultat en utilisant purrr::rerun(), purrr::map_*(), purrr::walk()

2. La répétition des commandes ayant plusieurs arguments en utilisant  purrr::map2_*() et purrr::pmap_*()

3. La création de bases de données imbriquées en utilisant dplyr::group_by() et tidyr::nest()

4. Travailler avec des bases de données imbriquées avec dplyr

5. Identifier et gérer les erreurs en utilisant les fonctions 'adverbes' purrr::safely()et purrr::possibly()

## **7.2 Resources**

* Chapitres 19 et 21 de [R for Data Science](http://r4ds.had.co.nz/)

* Anti-sèches pour l’utilisation des fonctions dans ([RStudio Apply Functions Cheatsheet](https://github.com/rstudio/cheatsheets/raw/master/purrr.pdf))

* Le fichier souche de cette leçon ([Stub for this lesson](https://psyteachr.github.io/msc-data-skills/stubs/7_func.Rmd))

Dans les deux prochains cours, nous allons en apprendre davantage sur la fonction *itération* (entrer les mêmes commandes en boucle) et les *fonctions personnalisées*. Pour cela, nous réaliserons un exercice de simulation qui nous amènera également à traiter des sujets statistiques plus traditionnels. En cours de route, vous apprendrez également à créer des vecteurs et des tableaux dans R.

*# Les **librairies **requises pour ces exemples*

**library**(tidyverse)  ## contient purrr, tidyr, dplyr

**library**(broom) ## convertit les sorties sorties de tests statistiques en tableaux ordonnés

**set.seed**(8675309) *# pour s’assurer que les nombres aléatoires soient reproductibles *

## **7.3 Les fonctions d’itération**

### **7.3.1 ****rep()**

La fonction rep() vous permet de répéter le premier argument plusieurs fois.

Utilisez rep() afin de créer un vecteur alternant 24 valeurs "A" et "B". 

**rep**(**c**("A", "B"), 12)

##  [1] "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A"

## [20] "B" "A" "B" "A" "B"

Si vous ne spécifiez pas ce qu’est le deuxième argument, il prendra par défaut la valeur times, ce qui  répètera le vecteur utilisé en premier argument autant de fois que spécifié. Créez le même vecteur que dans l'exemple ci-dessus, en définissant explicitement le deuxième argument.

**rep**(**c**("A", "B"), times = 12)

##  [1] "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A" "B" "A"

## [20] "B" "A" "B" "A" "B"

Si le deuxième argument est un vecteur de la même longueur que le premier argument, chaque élément du premier vecteur est répété autant de fois que spécifié dans le deuxième argument. Utilisez  rep()  pour créer un vecteur de 11 valeurs "A" suivies de 3 valeurs "B" 

**rep**(**c**("A", "B"), **c**(11, 3))

##  [1] "A" "A" "A" "A" "A" "A" "A" "A" "A" "A" "A" "B" "B" "B"

Vous pouvez répéter chaque élément du vecteur un nombre spécifié de fois en utilisant l’argument each. Utilisez rep()pour créer un vecteur de 12 valeurs "A" suivies de 12 valeurs  "B".

**rep**(**c**("A", "B"), each = 12)

##  [1] "A" "A" "A" "A" "A" "A" "A" "A" "A" "A" "A" "A" "B" "B" "B" "B" "B" "B" "B"

## [20] "B" "B" "B" "B" "B"

Selon vous, que se passera-t-il si vous définissez les argument times sur 3 et each sur 2?

**rep**(**c**("A", "B"), times = 3, each = 2)

##  [1] "A" "A" "B" "B" "A" "A" "B" "B" "A" "A" "B" "B"

### **7.3.2 ****seq()**

La fonction seq() est utile pour générer une séquence de nombres avec un pattern spécifique.

Utiliser seq() afin de un vecteur de nombre entiers allant de 0 à 10.

**seq**(0, 10)

##  [1]  0  1  2  3  4  5  6  7  8  9 10

Vous pouvez définir l'argument by afin qu'il compte des nombres de 1 en 1 (la valeur par défaut). Utilisez seq() pour créer un vecteur de nombres comptant de 10 en 10 et allant de 0 jusqu’à 100.

**seq**(0, 100, by = 10)

##  [1]   0  10  20  30  40  50  60  70  80  90 100

L'argument length.out  est utile si vous savez en combien de pas vous souhaitez diviser quelque chose. Utilisez  seq()pour créer un vecteur qui commence par 0, se termine par 100 et a 12 pas équidistants (indice: combien de nombres comprendrait un vecteur à 2 pas ?).

**seq**(0, 100, length.out = 13)

##  [1]   0.000000   8.333333  16.666667  25.000000  33.333333  41.666667

##  [7]  50.000000  58.333333  66.666667  75.000000  83.333333  91.666667

## [13] 100.000000

## **7.4 Fonctions personnalisées **

En plus des fonctions par défaut et des fonctions intégrées auxquelles vous pouvez accéder à partir des packages, vous pouvez également écrire vos propres fonctions (et éventuellement même, vos propres packages !).

### **7.4.1 Créer la structure d’une fonction**

La structure générale d'une fonction est la suivante:

function_name <- **function**(my_args) {

  *# traite les arguments*

  *# renvoie une valeur*

}

Voici une fonction très simple. Pouvez-vous deviner ce qu’elle fait ?

add1 <- **function**(my_number) {

  my_number + 1

}

**add1**(10)

## [1] 11

Créer une fonction qui rapporte les valeurs de p au format APA (avec "p = valeur arrondie" lorsque p> = .001 et "p <.001" lorsque p <.001).

Tout d'abord, nous devons nommer la fonction. Vous pouvez la nommer comme vous le souhaitez,; mais essayez de ne pas les nommer de la même manière que des fonctions existantes : cela les remplacerait. Par exemple, si vous appelez votre fonction rep, vous devrez utiliser la fonction base::rep() pour accéder à la fonction rep normale. Appelons notre fonction nous permettant de traiter les valeurs de p"report_p" et mettons en place la base de la fonction.

report_p <- **function**() {

}

### **7.4.2 Les arguments**

Nous devons ajouter un *argument* : la valeur de p que vous souhaitez reporter. Les noms que vous choisissez pour les arguments sont exclusifs à cet argument. Ce n’est donc pas un problème s'ils entrent en conflit avec d'autres variables de votre script. Il vous suffit de placer les arguments entre parenthèses après function dans l'ordre dans lequel vous souhaitez qu’ils soient par défaut (tout comme les fonctions par défaut que vous avez utilisées auparavant).

report_p <- **function**(p) {

}

### **7.4.3 Les argument par defaut**

Vous pouvez décider d’ajouter une valeur par défaut à n'importe quel argument. Si l’argument n’est pas explicitement défini lors de l’utilisation de la fonction, la fonction utilise la valeur de l'argument par défaut. Ici, il n'est probablement pas logique d'exécuter cette fonction sans spécifier la valeur de p.Cependant, nous pouvons ajouter un second argument appelé digits (en anglais, chiffres) dont la valeur par défaut est 3, afin que nous arrondissons les valeurs de p à 3 chiffres.

report_p <- **function**(p, digits = 3) {

}

A présent, nous devons écrire un peu de code à l'intérieur de la fonction afin de traiter les arguments d'entrée et en renvoyer une sortie. La dernière ligne évaluée dans la fonction définira la sortie.

report_p <- **function**(p, digits = 3) {

  **if** (p < .001) {

    reported = "p < .001"

  } **else** {

    roundp <- **round**(p, digits)

    reported = **paste**("p =", roundp)

  }

  

  reported

}

Vous pouvez également définir la sortie à l'intérieur de la fonction return(). Cela fait la même chose.

report_p <- **function**(p, digits = 3) {

  **if** (p < .001) {

    reported = "p < .001"

  } **else** {

    roundp <- **round**(p, digits)

    reported = **paste**("p =", roundp)

  }

  

  **return**(reported)

}

Lorsque vous exécutez le code qui définit votre fonction, il ne génère rien si ce n’est créer un nouvel objet dans l'onglet Environnement sous **Fonctions**. Vous pouvez maintenant exécuter la fonction.

**report_p**(0.04869)

**report_p**(0.0000023)

## [1] "p = 0.049"

## [1] "p < .001"

### **7.4.4 Portée**

Ce qui se passe dans une fonction, reste dans une fonction. Vous pouvez modifier la valeur d'une variable utilisée comme argument dans une fonction sans que cela ne change la valeur de la variable en dehors de la fonction, et ce même si la variable utilisée comme argument a le même nom que celui de la fonction.

half <- **function**(x) {

  x <- x/2

  **return**(x)

}

x <- 10

**list**(

  "half(x)" = **half**(x),

  "x" = x

)

## $`half(x)`

## [1] 5

## 

## $x

## [1] 10

### **7.4.5 Avertissements et erreurs**

Que se passe-t-il lorsque vous omettez l'argument pour p? Ou si vous définissez p à 1,5 ou "a"?

Il se peut que vous souhaitiez ajouter un avertissement plus spécifique et arrêter d'exécuter le code de la fonction si quelqu'un entre une valeur qui n'est pas un nombre. Vous pouvez faire cela avec la fonction stop().

Si quelqu'un entre un nombre qui n'est pas possible pour une valeur de p (0-1), vous voudrez peut-être l’avertir que ce n'est probablement pas ce qu'ils voulaient effectuer, mais continuer tout de même avec la fonction. Vous pouvez faire cela grâce à la fonction warning()

report_p <- **function**(p, digits = 3) {

  **if** (!**is.numeric**(p)) **stop**("p doit être un nombre")

  **if** (p <= 0) **warning**("les valeurs de p sont normalement supérieures à 0")

  **if** (p >= 1) **warning**("les valeurs de p sont normalement inférieures à 1")

  

  **if** (p < .001) {

    reported = "p < .001"

  } **else** {

    roundp <- **round**(p, digits)

    reported = **paste**("p =", roundp)

  }

  

  reported

}

**report_p**()

## Error in report_p(): argument "p" is missing, with no default

**report_p**("a")

## Error in report_p("a"): p doit être un nombre

**report_p**(-2)

## Warning in report_p(-2): les valeurs de p sont normalement supérieures à 0

**report_p**(2)

## Warning in report_p(2): les valeurs de p sont normalement inférieures à 1

## [1] "p < .001"

## [1] "p = 2"

## **7.5 Répéter vos propres fonctions**

Tout d'abord, construisons le code que nous voulons répéter.

### **7.5.1 ****rnorm()**

Créez un vecteur de 20 nombres aléatoires tirés d'une distribution normale avec une moyenne de 5 et l'écart-type de 1 en utilisant la fonction rnorm()  et stockez-les dans la variable A.

A <- **rnorm**(20, mean = 5, sd = 1)

### **7.5.2 ****tibble::tibble()**

Un tibble est un type de tableau ou  data.frame. La fonction tibble :: tibble () permet de créer un tibble avec une colonne pour chaque argument. Chaque argument prend la forme nom_colonne = vecteur_ donnée.

Créez un tableau appelé dat et qui comprend deux vecteurs : A qui est un vecteur de 20 nombres aléatoires normalement distribués avec une moyenne de 5 et ET de 1, et B qui est un vecteur de 20 nombres aléatoires normalement distribués avec une moyenne de 5,5 et ET de 1.

dat <- **tibble**(

  A = **rnorm**(20, 5, 1),

  B = **rnorm**(20, 5.5, 1)

)

### **7.5.3 ****t.test**

Vous pouvez exécuter un test t à deux échantillons indépendant de Welch en incluant les deux échantillons que vous avez créés comme deux premiers arguments de la fonction  t.test. Vous pouvez référencer une colonne d'une table par ses noms au format nom_tableau$nom_colonne.

**t.test**(dat$A, dat$B)

## 

##  Welch Two Sample t-test

## 

## data:  dat$A and dat$B

## t = -1.5937, df = 36.528, p-value = 0.1196

## alternative hypothesis: true difference in means is not equal to 0

## 95 percent confidence interval:

##  -0.9559243  0.1144139

## sample estimates:

## mean of x mean of y 

##  4.965341  5.386096

Vous pouvez également convertir le tableau au format long à l'aide de la fonction "*gather" *du package tidyr et spécifier le test t à l'aide du format dv_column~grouping_column (vd_colomne~colomne_groupe)

longdat <- **gather**(dat, group, score, A:B)

**t.test**(score~group, data = longdat)

## 

##  Welch Two Sample t-test

## 

## data:  score by group

## t = -1.5937, df = 36.528, p-value = 0.1196

## alternative hypothesis: true difference in means is not equal to 0

## 95 percent confidence interval:

##  -0.9559243  0.1144139

## sample estimates:

## mean in group A mean in group B 

##        4.965341        5.386096

### **7.5.4 ****broom::tidy()**

Vous pouvez utiliser la fonction  broom::tidy() pour extraire les données d'un test statistique sous la forme d’un tableau. L'exemple ci-dessous enchaîne toutes ces étapes.

**tibble**(

  A = **rnorm**(20, 5, 1),

  B = **rnorm**(20, 5.5, 1)

) %>%

  **gather**(group, score, A:B) %>%

  **t.test**(score~group, data = .) %>%

  broom::**tidy**()

## # A tibble: 1 x 10

##   estimate estimate1 estimate2 statistic p.value parameter conf.low conf.high

##      <dbl>     <dbl>     <dbl>     <dbl>   <dbl>     <dbl>    <dbl>     <dbl>

## 1   -0.578      4.97      5.54     -1.84  0.0747      34.3    -1.22    0.0606

## # … with 2 more variables: method <chr>, alternative <chr>

Enfin, nous pouvons extraire une seule valeur de ce tableau de résultats en utilisant  pull().

**tibble**(

  A = **rnorm**(20, 5, 1),

  B = **rnorm**(20, 5.5, 1)

) %>%

  **gather**(group, score, A:B) %>%

  **t.test**(score~group, data = .) %>%

  broom::**tidy**() %>%

  **pull**(p.value)

## [1] 0.256199

### **7.5.5 En faire une fonction**

Tout d'abord, nommez votre fonction  t_sim  et placez le code ci-dessus dans une fonction sans arguments.

t_sim <- **function**() {

  **tibble**(

    A = **rnorm**(20, 5, 1),

    B = **rnorm**(20, 5.5, 1)

  ) %>%

    **gather**(group, score, A:B) %>%

    **t.test**(score~group, data = .) %>%

    broom::**tidy**() %>%

    **pull**(p.value) 

}

Exécutez le code plusieurs fois pour voir ce qui se passe.

**t_sim**()

## [1] 0.0558203

### **7.5.6 ****replicate()**

Vous pouvez utiliser la fonction replicate  pour exécuter une fonction autant de fois que vous le souhaitez.

**replicate**(3, **rnorm**(5))

##            [,1]      [,2]        [,3]

## [1,]  0.2398579 1.0060960 -0.08836476

## [2,] -1.7685708 0.8362997  0.08114036

## [3,]  0.1457033 0.4557277  1.38814525

## [4,]  0.4462924 0.5616177 -0.02341062

## [5,]  0.5916637 1.4850093  0.98759269

Exécutons la fonction t_sim 1000 fois, attribuons les valeurs p résultantes à un vecteur appelé reps et vérifions la proportion de valeurs p inférieures à alpha (par exemple, 0,05). Ce nombre est la puissance statistique de cette analyse.

reps <- **replicate**(1000, **t_sim**())

alpha <- .05

power <- **mean**(reps < alpha)

power

## [1] 0.304

### **7.5.7 Définir une seed (graine)**

Vous pouvez utiliser la fonction set.seed avant d'exécuter une fonction qui utilise des nombres aléatoires pour vous assurer d'obtenir des données aléatoires reproductibles. Vous pouvez utiliser n'importe quel nombre entier comme seed.

**set.seed**(90201)

Assurez-vous de ne jamais utiliser  set.seed() à l'intérieur d'une fonction de simulation, sinon vous simulerez les mêmes données en boucle.

![image alt text](image_1.png)

Figure 7.1: @KellyBodwin

### **7.5.8 Ajouter des arguments**

Vous pouvez modifier votre fonction chaque fois que vous souhaitez calculer la puissance d'un échantillon n différent, mais il est plus efficace d’intégrer ce n dans votre fonction comme argument. Redéfinissez t_sim en prenant soin de définir des arguments pour la moyenne et l'écart-type du groupe A, la moyenne et l'écart-type du groupe B et le nombre de sujets par groupe. Donnez à tous ces arguments des valeurs par défaut.

t_sim <- **function**(n = 10, m1=0, sd1=1, m2=0, sd2=1) {

  **tibble**(

    A = **rnorm**(n, m1, sd1),

    B = **rnorm**(n, m2, sd2)

  ) %>%

    **gather**(group, score, A:B) %>%

    **t.test**(score~group, data = .) %>%

    broom::**tidy**() %>%

    **pull**(p.value) 

}

Essayez cette fonction avec différentes valeurs pour les arguments pour vérifier que tout fonctionne.

**t_sim**(100)

**t_sim**(100, 0, 1, 0.5, 1)

## [1] 0.5065619

## [1] 0.001844064

Utilisez la fonction replicate pour calculer la puissance statistique dans un cas où il y aurait 100 sujets par groupe avec une taille d'effet de 0.2 (par exemple, A : M = 0, ET = 1 ; B: M = 0.2, ET = 1). Utilisez 1000 réplications.

reps <- **replicate**(1000, **t_sim**(100, 0, 1, 0.2, 1))

power <- **mean**(reps < .05)

power

## [1] 0.268

Comparez le résultat à la puissance statistique calculée à partir de la fonction power.t.test 

**power.t.test**(n = 100, delta = 0.2, sd = 1, type="two.sample")

## 

##      Two-sample t test power calculation 

## 

##               n = 100

##           delta = 0.2

##              sd = 1

##       sig.level = 0.05

##           power = 0.2902664

##     alternative = two.sided

## 

## NOTE: n is number in *each* group

Calculez la puissance statistique via la simulation et power.t.test  pour les tests suivants:

* 20 sujets par groupe, A : M = 0, ET = 1 ; B : M = 0.2, ET = 1

* 40 sujets par groupe, A : M = 0, ET = 1 ; B : M = 0.2, ET = 1

* 20 sujets par groupe, A : M = 10, ET = 1 ; B : M = 12, ET = 1

* 20 subjects/group, A: m = 10, SD = 1; B: m = 12, SD = 1.5

## **7.6 Exercices**

Téléchargez les exercices. Ne regardez les réponses qu'après avoir tenté de répondre à toutes les questions.

