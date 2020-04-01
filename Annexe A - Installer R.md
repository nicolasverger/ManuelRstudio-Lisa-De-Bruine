Annexe A - Installer R

L'installation de R et de RStudio est généralement simple. Les sections ci-dessous expliquent comment et il y a une vidéo [YouTube utile ici](https://www.youtube.com/watch?v=lVKMsaWju8w) (EN).

# A.1 Installation de la base R

Installez la base R à partir de [https://cran.rstudio.com/](https://cran.rstudio.com/). Choisissez le lien de téléchargement pour votre système d'exploitation (Linux, Mac OS X ou Windows).

Si vous avez un Mac, installez la dernière version à partir du lien **R-x.x.x.x.pkg** le plus récent (ou une version antérieure si vous avez un ancien système d'exploitation). Après avoir installé R, vous devriez également installer [XQuartz](http://xquartz.macosforge.org/) pour pouvoir utiliser certains logiciels de visualisation.

Si vous installez la version Windows, choisissez le sous-répertoire "[base](https://cran.rstudio.com/bin/windows/base/)" et cliquez sur le lien de téléchargement en haut de la page. Après avoir installé R, vous devez également installer [RTools](https://cran.rstudio.com/bin/windows/Rtools/) ; utilisez la version "recommandée" surlignée en haut de la liste.

Si vous utilisez Linux, choisissez votre système d'exploitation spécifique et suivez les instructions d'installation.

# A.2 Installation de RStudio

Allez sur rstudio.com et téléchargez la version RStudio Desktop (Open Source License) pour votre système d'exploitation sous la liste intitulée **Installers for Supported Platforms**.

# A.3 Installation de LaTeX

Vous pouvez installer le système de composition LaTeX pour produire des rapports PDF à partir de RStudio. Sans cette installation supplémentaire, vous pourrez produire des rapports en HTML mais pas en PDF. Pour générer des rapports PDF, vous aurez également besoin de:

1. [pandoc](http://pandoc.org/installing.html), et

2. LaTeX, un langage de composition, disponible pour

    * WINDOWS : [MikTeX](http://miktex.org/)

    * Mac OS : [MacTex](https://tug.org/mactex/downloading.html) (téléchargement de 3,2 Go) ou [BasicTeX](http://ww.tug.org/mactex/morepackages.html) (téléchargement de 78 Mo, mais devrait fonctionner correctement)

    * Linux : [TeX Live](https://www.tug.org/texlive/)

