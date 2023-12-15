# Mondes_Virtuels : Génération d'un terrain de type Minecraft

## But du projet
Notre objectif est de comprendre comment sont générés les mondes dans le jeu Minecraft et de recréer sous Unity un mini-monde généré procéduralement et composé 
de cubes de taille similaire avec différentes textures.


## Existant
Dans Minecraft, les mondes sont générés procéduralement grâce à une fonction de Perlin Noise (bruit de Perlin) ainsi qu'un nombre appelé "seed".
Ce nombre permet de générer un nombre aléatoire grâce à une fonction et de retrouver ce nombre si on réutilise ce point de départ. Avoir un aléatoire peut 
permettre plusieurs choses, notamment de se placer à un endroit différent dans le bruit de Perlin, changer le spawn des éléments du jeu, etc. 

Les mondes minecraft sont générés par portions appelées chunk à partir de la position du joueur. Ces chunk, générés grâce à la seed mesurent 16
blocs de large, 16 blocs de long et 256 blocs de haut. Ils sont chargés au fur et à mesure que le joueur progresse sur la map afin de ne pas charger et 
garder en mémoire toute la carte. Leur affichage va dépendre de la distance de rendu entrée dans les paramètres et qui dépendra donc de la puissance de 
l'ordinateur du joueur.

La génération de terrain se déroule en deux temps. Il y a d'abord la phase de génération qui permet de générer le terrain de base, puis les biomes et enfin des
structures que l'on peut trouver dans le jeu comme les grottes ou les villages. Vient ensuite la phase de population, permettant de faire apparaitre des éléments 
récurrents du jeu tel que les arbres ou encore les différents animaux. Cette phase ne se lance que lorsque les 3 chunks adjacent à celui sur lequel le joueur se
trouve sont chargés.

Enfin concernant les cubes, ils contiennent plusieurs informations notamment concernant leur type, leur comportement, leur résistance (pour le minage), etc.

METTRE SOURCES !

## Première étape : générer la base du terrain
Pour commencer, nous avons visualisé le bruit de Perlin à l'aide de Gizmo. Nous avons ensuite utiliser la variation du bruit de Perlin pour définir la hauteur de notre
terrain.

Nous générons notre map en fonction de deux paramètres : la longueur et la largeur. Ensuite nous générons notre bruit de Perlin en fonction de deux paramètres : l'amplitude
et la fréquence. L'amplitude fait donc varier la hauteur des montagnes tandis que la fréquence fait varier l'étalement des montagnes.

![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/64b360b0-5486-4348-9a49-cc24dde3c598)

Dans notre fonction <code>generate()</code>, nous parcourons le terrain selon trois paramètres : la largeur, l'amplitude et la longueur pour créer nos cube sous la hauteur 
définit par le bruit de Perlin. La fonction pour récupérer ce bruit est intégrée dans la librairie Mathf.

| ![img.jpg](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/f5657213-94ea-43ef-abd5-ecfcfef32026) | 
|:--:| 
| *Fréquence de 0.1* |

| ![img2.jpg](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/ad422a87-46f5-49b8-a518-383c5e3a3103) | 
|:--:| 
| *Fréquence de 0.01* |


## Deuxième étape : appliquer des règles pour assigner les types des blocs
Le but ensuite est d'assigner à chaque cube un type qui définira sa texture.

Nous disposons de trois règles :
- le cube du dessus est un bloc d'herbe ;
- les blocs du dessous sont des blocs de terre s'ils sont au dessus d'une certaine hauteur ;
- les autres blocs sont des blocs de roche.


## Troisième étape : appliquer les textures
Pour cette partie, nous avons dans un premier temps créer un matérial de type Unlit/Texture avec une image contenant plusieurs types de textures différentes.
| ![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/c6e3302a-2f15-4837-864c-cb15a2383ad0) | 
|:--:| 
| *Image utilisée pour la création du material* |
Cette image est divisée en quatre dans la classe Cube par le getter <code>NormalizedSizeBlockTextureSize</code>. Ensuite, dans les fonctions <code>SetTextureSide(int textureID)</code>,
<code>SetTextureTop(int textureID)</code>, <code>SetTextureBottom(int textureID)</code>, la texture est appliquée au cube en fonction de l'indice sélectionné.

## Quatrième étape : optimisation









NOTES :
Le document par exemple en markdown sous repo github que vous me rendrez contiendra 
des explications, 
des liens vers les documents/ sites qui vous ont inspirés, 
des parties de codes commentés qui vous paraissent importantes, 
des captures d’écran de votre travail.


Liens :
https://www.pcgbook.com/
http://pcg.wikidot.com/
Perlin Noise : https://www.youtube.com/watch?v=WP-Bm65Q-1Y
https://www.youtube.com/watch?v=Y-fDGOqHQZA
https://www.youtube.com/watch?v=3LQmLT4zvpo
https://www.youtube.com/watch?v=s0DwskCw00w
