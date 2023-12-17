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

Ces règles sont appliquée dans la fonction ci-dessous :
![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/2af0d19e-1bd3-4ad7-be6f-ac7537da11fe)


## Troisième étape : appliquer les textures
Pour cette partie, nous avons dans un premier temps créer un matérial de type Unlit/Texture avec une image contenant plusieurs types de textures différentes.
| ![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/c6e3302a-2f15-4837-864c-cb15a2383ad0) | 
|:--:| 
| *Image utilisée pour la création du material* |
Cette image est divisée en seize dans la classe Cube par le getter <code>NormalizedSizeBlockTextureSize</code>. Ensuite, dans les fonctions <code>SetTextureSide(int textureID)</code>,
<code>SetTextureTop(int textureID)</code> et <code>SetTextureBottom(int textureID)</code>, la texture est appliquée au cube en fonction de l'indice sélectionné.

Le nature du cube est définit dans la classe CubeMap lorsque tous les cubes ont été créés, notamment dans la fonction <code>setCubeType()</code> montrée plus haut
ainsi que dans <code>applyToAllCubes()</code>.

Cela nous permet d'obtenir une map comme celle-ci :

![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/3489abbe-2de9-4b5c-ab3d-9c3074478fa7)


## Quatrième étape : optimisation
Lors de la génération de grandes maps, la perte d'image par seconde commençait à se voir. Nous avions donc deux problèmes :
- le jeu voyait son nombre de FPS diminuer ;
- nous ne pouvions pas créer de terrain suffisamment grand pour permettre de jouer dessus.

Nous avions tester dans un premier temps de cacher les cubes éloignés du joueur. Cependant, ces cubes étant toujours charger dans la scène, la performance n'a pas été améliorée.
Nous avons alors eu l'idée de créer les cubes au fur et à mesure en fonction de leur distance par rapport au joueur. Cependant, nous ne pouvions pas déterminer le type du cube car
les cubes ne connaissaient pas le type de leurs voisins.

Nous avons finalement décidé de générer toute la map puis d'instancier uniquement les cubes proches du joueur grâce à la fonction <code>displayCubeIfNear()</code> présente dans le 
script CubeMap.
![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/ef5d449b-1772-43e2-b2d3-62279348446c)

Lorsque un cube se trouve à une distance inférieur à 20 cube du joueur, le cube est affiché, sinon il reste caché.
Voici le résultat :
| ![img.jpg](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/04a0086e-b41e-4dd2-9f40-b7e02c565744) | 
|:--:| 
| *Position du joueur en x=3.57 y=15.71 z=16.15 |
| ![img.jpg](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/9aa06b49-f05b-4e2a-8e00-f9f7611d93f5) | 
|:--:| 
| *Position du joueur en x=15.07 y=17.52 z=16.18 |



## Dernière étape : création d'un joueur contrôlable au clavier
Pour créer un joueur, nous avons créer un rectangle contenant un Rigidbody ainsi qu'une caméra afin d'avoir une vu à la première personne.
Dans le script joueur, nous prenons en compte les inputs du joueur (ZQSD + Espace) puis nous mettons à jour la position du joueur grâce à la fonction <code>Translate()</code>.
Le joueur peut contrôler sa rotation grâce à la récupération de la position de la souris utiliser pour mettre à jour la rotation du joueur.

![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/386d988a-7027-433a-8245-4d20479029ed)
![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/a2f2e01e-4c6f-4d53-a9a6-9f14dbd23517)


## Possibilités d'évolution du projet
Comme dit dans la première partie, la génération d'un monde minecraft se fait en plusieurs parties. Dans la première phase, nous n'avons pas encore créer les différents biomes
ainsi que les structures de type grottes ou village. Nous pourrions donc continuer le projet en ajoutant ces structures avant de passer à la phase de population.

Cependant, nous rencontrons encore actuellement quelques problèmes d'optimisation. En effet, lorsque nous lançons le projet et que nous bougeons dans l'environnement, nous 
remarquons quelques soucis de lague car nous dessinons les cubes à chaques frame dans le <code>Update()</code> de la classe Main :

![image](https://github.com/Firrow/Mondes_Virtuels/assets/73218766/bbdf3e1a-c1c9-44ea-ae3e-47e70136f8cc)

Si l'on commente ce morceau de code, le problème disparait mais les textures des cubes ne sont pas chargées. Il faudrait donc trouver un moyen de mettre à jour les
textures des blocs sans devoir recharger tous les blocs du terrain.


# Nos sources principales
Inspiration pour notre projet : https://www.youtube.com/watch?v=s0DwskCw00w
How Minecraft worlds are generated : https://www.alphr.com/how-minecraft-generates-worlds/
Procedural Content Generation in Games : https://www.pcgbook.com/
Procedural Content Generation : http://pcg.wikidot.com/
Perlin Noise : https://www.youtube.com/watch?v=WP-Bm65Q-1Y
Create Texture Wrap on cube : https://www.youtube.com/watch?v=Y-fDGOqHQZA
Generate a chunk : https://www.youtube.com/watch?v=3LQmLT4zvpo
