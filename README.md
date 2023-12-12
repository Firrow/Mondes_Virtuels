# Mondes_Virtuels : Génération d'un terrain de type Minecraft #

## But du projet ## 
Notre objectif est de comprendre comment sont générés les mondes dans le jeu Minecraft et de recréer sous Unity un mini-monde généré procéduralement et composé 
de cubes de taille similaire avec différentes textures.


## Existant ## 
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
Enfin concernant les cubes, ils contiennent des informations notamment concernant leur type, leur comportement, leur résistance (pour le minage), etc.

## Première étape : générer la base du terrain ## 
## Deuxième étape : appliquer des règles pour assigner les types des blocs ## 
## Troisième étape : appliquer les textures ## 









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
