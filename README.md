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

## Afficheur 
L'afficheur disponible sur la carte ENS comportant le microcontroleur STM32 est un afficheur LCD-TFT. Il s'agit d'une technologie d'écrans LCD: Thin Film Transistor. L'écran LCD possède une couche de semi-conducteur qui permet de contrôler notamment l'intensité de la couleur dans chaque pixel.
Cette dalle tactile STM32F746G-Disco comporte 480x272 pixels et comporte des couleurs sur 24bits RGB. Le controlleur est 


## Fonctions avancées de la bibliothèque
Parmi les fonctionnalités qui ont pu être utiles au jeu de labyrinthe, on peut en citer quelques unes (liste non-exhaustive):

### 

*BSP_LCD_SelectLayer(Layer)*: Cette fonction permet de naviguer enter les différentes couches présentes sur l'écran LCD. Voici un schéma récapitulatif du système de couches ![ici](https://github.com/nzthan/442---Mini-Projet/blob/main/layers_system.png)

, issu d'une [présentation du STM32F7-LTCD](https://www.st.com/content/ccc/resource/training/technical/product_training/group0/3f/7b/af/97/88/ba/48/33/STM32F7_Peripheral_LTDC/files/STM32F7_Peripheral_LTDC.pdf/jcr:content/translations/en.STM32F7_Peripheral_LTDC.pdf) (controlleur qui interagit avec l'écran LCD STM32F7)

*BSP_LCD_SetLayerVisible(Layer, ENABLE/DISABLE)*: Cette fonction permet de mettre une couche comme visible ou non. Cela peut entre autres permettre de mettre une couche sur laquelle on a écrit précédemment comme non visible (ex du labyrinthe: lorsque l'écran de victoire apparaît, on ne souhaite plus voir le parcours du joueur en fond, donc on écrit la ligne:
```c
	BSP_LCD_SetLayerVisible(1,DISABLE) // couche d'écriture du chemin non visible
```

*BSP_LCD_SetTransparency()*: Cette fonction permet de gérer la transparence d'une couche. cela permet notamment de pouvoir voir une autre couche par transparence. Cette fonction est utile dans le cas du jeu de labyrinthe lorsque le joueur a perdu (tâche est en train de s'effectuer) et que l'écran de défaite permet de voir par transparence le chemin parcouru par le joueur au cours de la partie.

*BSP_LCD_SetLayerWindow(LayerIndex,Xpos,Ypos,Width,Height)*: Cette fonction agi directement sur la partie active de l'affichage écran. Elle permet de modifier la position ou la taille d'une couche. Elle prend en arguments le numéro de la couche dont on souhaite modifier le 



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
