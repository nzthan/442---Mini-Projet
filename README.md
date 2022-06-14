# 442---Mini-Projet
# Fonctions avancées de l'afficheur LCD
# Nathan BONVALET

## Table des matières

* [Introduction](#introduction)
* [Afficheur LCD](#afficheur)
* [Fonctions avancées de la bibliothèque](#fonctions)
* [Conclusion](#Conclusion)

## Introduction
Ce mini projet porte sur la mise en oeuvre de différentes fonctions avancées de la bibliothèque LCD disponible sur STMCube IDE.
Je me suis appuyé notamment sur un jeu de labyrinthe sur l'écran LCD que j'avais réalisé en partie sur le TP de découverte de la carte STM32. Cela m'a de prendre en main les fonctionalités particulières de la bibliothèque LCD et pouvoir compléter le travail effectué lors du TP de découverte, tout en ajoutant des fonctionalités intéressantes au jeu de labyrinthe.

![Image de fond du labyrinthe](data:image/png;base64,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)


## Afficheur 
L'afficheur disponible sur la carte ENS comportant le microcontroleur STM32 est un afficheur LCD-TFT. Il s'agit d'une technologie d'écrans LCD: Thin Film Transistor. L'écran LCD possède une couche de semi-conducteur qui permet de contrôler notamment l'intensité de la couleur dans chaque pixel.
Cette dalle tactile STM32F746G-Disco comporte 480x272 pixels et comporte des couleurs sur 24bits RGB. Le controlleur est 


## Fonctions avancées de la bibliothèque
Parmi les fonctionnalités qui ont pu être utiles au jeu de labyrinthe, on peut en citer quelques unes (liste non-exhaustive):

### 

*BSP_LCD_SelectLayer(Layer)*: Cette fonction permet de naviguer enter les différentes couches présentes sur l'écran LCD. Voici un schéma récapitulatif du système de couches, issu d'une [présentation du STM32F7-LTCD](https://www.st.com/content/ccc/resource/training/technical/product_training/group0/3f/7b/af/97/88/ba/48/33/STM32F7_Peripheral_LTDC/files/STM32F7_Peripheral_LTDC.pdf/jcr:content/translations/en.STM32F7_Peripheral_LTDC.pdf) (contrôleur qui interagit avec l'écran LCD STM32F7):

![ici](https://github.com/nzthan/442---Mini-Projet/blob/main/layers_system.png)


*BSP_LCD_SetLayerVisible(Layer, ENABLE/DISABLE)*: Cette fonction permet de mettre une couche comme visible ou non. Cela peut entre autres permettre de mettre une couche sur laquelle on a écrit précédemment comme non visible (ex du labyrinthe: lorsque l'écran de victoire apparaît, on ne souhaite plus voir le parcours du joueur en fond, donc on écrit la ligne:
```c
	BSP_LCD_SetLayerVisible(1,DISABLE) // couche d'écriture du chemin non visible
```


*BSP_LCD_SetTransparency()*: Cette fonction permet de gérer la transparence d'une couche. cela permet notamment de pouvoir voir une autre couche par transparence. Cette fonction est utile dans le cas du jeu de labyrinthe lorsque le joueur a perdu (tâche est en train de s'effectuer) et que l'écran de défaite permet de voir par transparence le chemin parcouru par le joueur au cours de la partie.


*BSP_LCD_SetLayerWindow(LayerIndex,Xpos,Ypos,Width,Height)*: Cette fonction agi directement sur la partie active de l'affichage écran. Elle permet de modifier la position ou la taille d'une couche. Elle prend en arguments le numéro de la couche dont on souhaite modifier les paramètres, sa position initiale (Xpos,Ypos), la taille souhaitée (hauteur et largeur).
![Schéma de configuration de la couche](https://github.com/nzthan/442---Mini-Projet/blob/main/window_config.png)



*BSP_LCD_Clear()*: Cette fonction permet de supprimer tout ce qui a été écrit sur une couche de l'afficheur LCD. Elle pemet par exemple de supprimer la trace faite par le joueur dans le jeu de labyrinthe lorsque le joueur a touché un mur, ou gagné:
```c
	//affichage de la victoire
	if (Message == 2){
		level = level + 1; //augmentation du niveau
		vTaskDelete(tsk_affichageHandle);
		vTaskDelete(tsk_horlogeHandle);
		Message = 0;
		BSP_LCD_Clear(00); //reset l'affichage écran
		BSP_LCD_DrawBitmap(0,0,(uint8_t*) win_bmp);
	}
```


*BSP_LCD_ReadPixel(X,Y)*: Cette fonction peut être très utile dans le cadre d'une image binaire ou très contrastée, car elle permet de faire des distinctions de parties de l'image simplement via la couleur du pixel selectionné. Elle est très utile dans le cas du codage d'un jeu de labyrinthe car elle permet de s'affranchir de coder l'ensemble des délimitations des murs (très fastidieuse), en prenant simplement en compte la couleur du pixel sélectionné: si le pixel est noir, c'st un mur. Avec un seuil de tolérance, cela permet de séparer deux catégories d'objets (murs et passages) facilement:

``` c
    // Couleur du pixel pointé
	BSP_LCD_SelectLayer(0); //on choisit la couche 0 pour se mettre sur le fond
	couleur_pix = BSP_LCD_ReadPixel(x_init+6, y_init+6);
	blanc = BSP_LCD_ReadPixel(30,65); //lecture de la couleur du fond blanc
    // On se remet sur la couche 1 d'écriture
	BSP_LCD_SelectLayer(1); 


	//Défaite sur murs
	if (couleur_pix != blanc){
	    arrivee = 1; // si touche un mur
		Message = 1;
	}

```


## Conclusion

Ce mini-projet a permis la découverte de fonctions plus poussées de la bibliothèque LCD utilisée sur le STM32 au S2. Ces diverses fonctions peuvent être très utiles notamment pour avoir des rendus graphiques plus élaborés. De plus, ce mini-projet m'a permis de m'intéresser plus en profondeur aux diverses fonctions disponibles dans cette bibliothèque LCD (survolée brièvement au cours du TP de découverte de la carte), ainsi qu'à une documentation de l'afficheur qu'on peut retrouver à [cette adresse](https://www.st.com/resource/en/application_note/an4861-lcdtft-display-controller-ltdc-on-stm32-mcus-stmicroelectronics.pdf).
