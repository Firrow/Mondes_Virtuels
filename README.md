# Mondes_Virtuels : Génération d'un terrain de type Minecraft #

## But du projet ## 
Notre objectif est de comprendre comment sont générés les mondes minecraft et de recréer sous Unity un mini-monde généré procéduralement et composé de cubes
de taille similaire avec différentes textures.


## Existant ## 
Dans Minecraft, les mondes sont générés procéduralement grâce à une fonction de Perlin Noise (bruit de Perlin) ainsi qu'un nombre appelé "seed".
Ce nombre permet de générer un nombre aléatoire grâce à une fonction et de retrouver ce nombre si on réutilise ce point de départ. Avoir un aléatoire peut 
permettre plusieurs choses, notamment de se placer à un endroit différent dans le bruit de Perlin, changer le spawn des éléments du jeu, etc. 
Les mondes minecraft sont générés par portions appelées chunk à partir de la position du joueur. Ces chunk, générés grâce à la seed mesurent 16
blocs de large, 16 blocs de long et 256 blocs de haut. Ils sont chargés au fur et à mesure que le joueur progresse sur la map afin de ne pas charger et 
garder en mémoire toute la carte. Leur affichage va dépendre de la distance de rendu entrée dans les paramètres et qui dépendra donc de la puissance de 
l'ordinateur du joueur.


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
