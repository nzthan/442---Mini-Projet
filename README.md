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
Cette dalle tactile STM32F746G-Disco comporte 480x272 pixels et comporte des couleurs sur 24bits RGB.


## Fonctions avancées de la bibliothèque
Parmi les fonctionnalités qui ont pu être utiles au jeu de labyrinthe, on peut citer les plus intéressantes.

### 
*BSP_LCD_SetLayerVisible(Layer, ENABLE/DISABLE)*

*BSP_LCD_SetTransparency()*

*BSP_LCD_SetLayerWindow()*

*BSP_LCD_Clear()*

*BSP_LCD_ReadPixel(X,Y)*: Cette fonction peut être très utile dans le cadre d'une image binaire ou très contrastée, car elle permet de faire des distinctions de parties de l'image simplement via la couleur du pixel selectionné. Elle est très utile dans le cas du codage d'un jeu de labyrinthe car elle permet de s'affranchir de coder l'ensemble des délimitations des murs (très fastidieuse), en prenant simplement en compte la couleur du pixel sélectionné: si le pixel est noir, c'st un mur. Avec un seuil de tolérance, cela permet de séparer deux catégories d'objets (murs et passages) facilement:

``` c
    // Couleur du pixel pointé
	BSP_LCD_SelectLayer(0); //on choisit la couche 0 pour se mettre sur le fond
	couleur_pix = BSP_LCD_ReadPixel(x_init+6, y_init+6);
	blanc = BSP_LCD_ReadPixel(30,65); 
    // On se remet sur la couche 1 d'écriture
	BSP_LCD_SelectLayer(1); 

```


## Conclusion

Ce mini-projet a permis la découverte de fonctions plus poussées de la bibliothèque LCD utilisée sur le STM32 au S2. Ces diverses fonctions peuvent être très utiles notamment pour avoir des rendus graphiques plus élaborés ou bien pouvoir 
