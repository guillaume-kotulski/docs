---
id: buttonOverview
title: Button
---

Un bouton est un objet actif auquel une action peut être assignée (*ex :* une tâche de base de données ou une fonction d'interface) pour qu'elle soit réalisée lorsque l'utilisateur clique dessus.

![](assets/en/FormObjects/button_regular.png)

Les boutons peuvent répondre à divers besoins qui dépendent du style et de l'action qui leur est affecté(e). Par exemple, les boutons peuvent amener l'utilisateur à faire des choix ou à compléter un questionnaire ou formulaire. En fonction de leurs propriétés, les bouton peuvent être destinés à être cliqués une fois seulement et à exécuter une commande, ou à être cliqués plusieurs fois pour obtenir le résultat escompté.

## Gestion des boutons

Les actions assignées aux boutons peuvent provenir d'[actons standard](properties_Action.md#standard-action) ou de méthodes objet personnalisées. Les actions typiques peuvent consister à laisser l'utilisateur accepter, annuler ou supprimer des enregistrements, à copier ou coller des données, à passer d'une page à l'autre dans un formulaire de plusieurs pages, à ouvrir, supprimer ou ajouter des enregistrements dans un sous-formulaire, à gérer les attributs de police dans les zones de texte , etc.

Les boutons avec des actions standard sont grisés le cas échéant lors de l'exécution du formulaire. Par exemple, si le premier enregistrement d'une table est affiché, un bouton avec l'action standard `firstRecord` apparaît grisé.

Si vous souhaitez qu'un bouton exécute une action qui n'est pas disponible en tant qu'action standard, laissez le champ d'action standard vide et écrivez une méthode objet pour spécifier l'action du bouton. Pour plus d'informations sur les méthodes d'objet et comment les créer et les associer, voir [Utilisation de méthodes objet](https://doc.4d.com/4Dv17R5/4D/17-R5/Using-object-methods.300-4163733.en.html). En règle générale, vous activez l'événement `Sur clic` et la méthode s'exécute uniquement lorsque vous cliquez sur le bouton. Vous pouvez associer une méthode à n'importe quel bouton.

La [variable](properties_Object.md#variable-or-expression) associée à un bouton est automatiquement définie sur **0** lorsque le formulaire est exécuté pour la première fois en mode Développement ou Application. Lorsque l'utilisateur clique sur un bouton, sa variable est définie sur **1**.



> Il est possible d'affecter à la fois une action standard et une méthode à un bouton. Dans ce cas, si le bouton n'est pas désactivé par l'action standard, la méthode est exécutée avant l'action standard.



## Button Styles

Les styles de bouton contrôlent l'apparence générale d'un bouton ainsi que ses propriétés. Il est possible d'appliquer différents styles prédéfinis aux boutons ou de leur associer des pop-up menus. A great number of variations can be obtained by combining these properties / behaviors.

À l'exception des [propriétés disponibles](#supported-properties), de nombreux objets bouton sont *structurellement* identiques. The difference is in the processing of their associated variables.

4D propose des boutons dans les styles prédéfinis suivants :



### Regular

Le style de bouton Classique est un bouton système standard (c'est-à-dire un rectangle avec un libellé descriptif) qui exécute le code lorsqu'un utilisateur clique dessus.

![](assets/en/FormObjects/button_regular.png)

Par défaut, le style Classique a un fond gris clair avec un libellé au centre. Lorsque le curseur survole le style de bouton Classique, la bordure et la l'arrière-plan changent de couleur. En plus de lancer l'exécution de code, le style de bouton Classique imite un bouton mécanique en changeant rapidement la couleur d'arrière-plan lorsque vous cliquez dessus.

#### JSON Example:

```4d

    "myButton": {
        "type": "button",   //définit le type d'objet
        "style":"regular",  //définit le style du bouton
        "defaultButton":"true"  //définit le bouton comme choix par défaut
        "text": "OK",   //texte à faire apparaître dans le bouton
        "action": "Annuler", //Action à exécuter
        "left": 60,  //Position gauche dans le formulaire  
        "top": 160, //Position supérieure dans le formulaire  
        "width": 100,  //largeur du bouton
        "height": 20 //hauteur du bouton
        }
```


Only the Regular and Flat styles offer the [Default Button](properties_Appearance.md#default-button) property.


### Flat

Le style de bouton A plat est un bouton système standard (c'est-à-dire un rectangle avec un libellé descriptif) qui exécute le code lorsqu'un utilisateur clique dessus.

![](assets/en/FormObjects/button_flat.png)

Par défaut, le style A plat a un arrière-plan avec un libellé au centre, des bords arrondis et un design minimaliste. The Flat button style's graphic nature is particularly useful for forms that will be printed.

#### JSON Example:

```4d

    "myButton": {
                "type": "button",   
                "style":"flat", 
                "defaultButton":"true"  
                "text": "OK",   
                "action": "Annuler", 
                "left": 60,         
                "top": 160,         
                "width": 100,   
                "height": 20    
                }
```


Only the Regular and Flat styles offer the [Default Button](properties_Appearance.md#default-button) property.

### Toolbar

Le style du bouton Barre d'outils est initialement destiné à être intégré dans une barre d'outils. Il inclut l'option à ajouter à un pop-up menu (indiqué par un triangle inversé) généralement utilisé pour afficher des choix de sélection supplémentaires pour l'utilisateur.

By default, the Toolbar style has a transparent background with a label in the center. The appearance of the button can be different when the cursor hovers over it depending on the OS:

 - *Sous Windows* - le contour du bouton apparaît lorsqu’il dispose de la propriété “Avec pop-up menu”, et un triangle est affiché à droite et au centre du bouton.

![](assets/en/FormObjects/button_toolbar.png)

 - *Sous macOS* - le contour du bouton n’apparaît jamais. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and at the bottom of the button.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",   
                "style":"toolbar",  
                "text": "OK",       
                "popupPlacement":"separated"    
                "action": "Annuler",     
                "left": 60,             
                "top": 160,             
                "width": 100,           
                "height": 20        
                }
```



### Bevel

Le bouton barre d'outils combine l'apparence du style [Classique](#regular) (c'est-à-dire un rectangle avec un libellé descriptif) et la propriété de pop-up menu du style [Barre d'outils](#toolbar).

Par défaut, le style Bevel a un fond gris clair avec un libellé au centre. The appearance of the button can be different when the cursor hovers over it depending on the OS:

 - *Sous Windows* - le contour du bouton apparaît. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and in the center of the button.

![](assets/en/FormObjects/button_bevel.png)

 - *Sous macOS* - le contour du bouton n’apparaît jamais. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and at the bottom of the button.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",
                "style":"bevel",    
                "text": "OK",       
                "popupPlacement":"linked"   
                "action": "Annuler", 
                "left": 60,     
                "top": 160,     
                "width": 100,   
                "height": 20    
                }
```



### Rounded Bevel

The Rounded Bevel button style is nearly identical to the [Bevel](#bevel) style except, depending on the OS, the corners of the button may be rounded. Comme pour le style Bevel, le style Bevel arrondi combine l'apparence du style [Classique](#regular) et du style [Barre outils](#toolbar).

Par défaut, le style Bevel arrondi a un fond gris clair avec un libellé au centre. The appearance of the button can be different when the cursor hovers over it depending on the OS:

 - *Sous Windows* - le bouton est identique au style Bevel. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and in the center of the button.

  ![](assets/en/FormObjects/button_roundedbevel.png)

 - *Sous macOS* - les coins du bouton sont arrondis. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and at the bottom of the button.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",
                "style":"roundedBevel", 
                "text": "OK",   
                "popupPlacement":"none" /
                "action": "Cancel", 
                "left": 60,         
                "top": 160, 
                "width": 100,   
                "height": 20    
                }
```



### OS X Gradient

The OS X Gradient button style is nearly identical to the [Bevel](#bevel) style. Comme pour le style Bevel, le style OS X Gradient combine l'apparence du style [Classique](#regular) et du style [Barre outils](#toolbar).

Par défaut, le style OS Gradient a un fond gris clair avec un libellé au centre. The appearance of the button can be different when the cursor hovers over it depending on the OS:

 - *Sous Windows* - le bouton est identique au style Bevel. When it uses the “With Pop-up Menu” property, a triangle is displayed on the right side of the button.

![](assets/en/FormObjects/button_osxgradient.png)

 - *Sous macOs* - le bouton s'affiche comme un bouton à deux tons. When it uses the “With Pop-up Menu” property, a triangle is displayed to the right and at the bottom of the button.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",   
                "style":"gradientBevel",
                "text": "OK",   
                "popupPlacement":"linked"
                "action": "Cancel",     
                "left": 60,     
                "top": 160, 
                "width": 100,   
                "height": 20    
                }
```


### OS X Textured

The OS X Textured button style is nearly identical to the [Bevel](#bevel) style but with a smaller size (maximum size is the size of a standard macOS system button). Comme pour le style Bevel, le style OS X Textured combine l'apparence du style [Classique](#regular) et du style [Barre outils](#toolbar).

By default, the OS X Textured style appears as:

 - *Sous Windows* - un bouton système standard avec un fond gris clair et un libellé au centre. Il a la particularité d'être transparent dans Vista.

 ![](assets/en/FormObjects/button_osxtextured.png)

 - *Sous macOS* - un bouton système standard affichant un changement de couleur du gris clair au gris foncé. Its height is predefined: it is not possible to enlarge or reduce it.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",   
                "style":"texturedBevel",    
                "text": "OK",   
                "popupPlacement":"separated"    
                "action": "Cancel", 
                "left": 60,         
                "top": 160,     
                "width": 100,   
                "height": 20    
                }
```



### Office XP

Le style de bouton Office XP combine l'apparence du style [Classique](#regular) et du style [Barre outils](#toolbar).

The colors (highlight and background) of a button with the Office XP style are based on the system colors. The appearance of the button can be different when the cursor hovers over it depending on the OS:

 - *Sous Windows* - son arrière-plan n'apparaît que lorsque la souris le survole.

![](assets/en/FormObjects/button_officexp.png)

 - *Sous macOS* - son arrière-plan est toujours affiché.

#### JSON Example:

```4d
    "myButton": {
                "type": "button",   
                "style":"office",
                "text": "OK",
                "popupPlacement":"none" 
                "action": "Cancel", 
                "left": 60,     
                "top": 160, 
                "width": 100,
                "height": 20    
                }
```



### Help


Le style du bouton Aide peut être utilisé pour afficher un bouton d'aide système standard. Par défaut, le style Aide s'affiche sous la forme d'un point d'interrogation dans un cercle.

![](assets/en/FormObjects/button_help.png)

#### JSON Example:

```4d
    "myButton": {
                "type": "button",
                "style":"help",     
                "text": "OK",   
                "dropping": "custom", 
                "left": 60, 
                "top": 160,     
                "width": 100,   
                "height": 20    
                }
```

> Le style Aide ne prend pas en charge les propriétés basiques du [nombre d'états](properties_TextAndPicture.md#number-of-states), du [chemin d'accès image](properties_TextAndPicture.md#picture-pathname) et de la [position Titre/Image](properties_TextAndPicture.md#title-picture-position).


### Rond

Le style de bouton Rond apparaît comme un bouton système circulaire. Ce style de bouton est conçu pour macOS.

![](assets/en/FormObjects/button_circleM.png)

Sous Windows, il est identique au style «Aucun» (le cercle en arrière-plan n'est pas pris en compte).


#### JSON Example:

```
    "myButton": {
                "type": "button",   
                "style":"circular", 
                "text": "OK",   
                "dropping": "custom", 
                "left": 60, 
                "top": 160,     
                "width": 100,
                "height": 20    
                }
```



### Custom

Le style de bouton Personnalisé accepte une image d'arrière-plan personnalisée et permet de gérer des paramètres supplémentaires tels que la marge et le décalage d'icône.

![](assets/en/FormObjects/button_custom.png)


#### JSON Example:

```code
    "myButton": {
                "type": "button",   
                "style":"custom",   
                "text": "", 
                "customBackgroundPicture": "/RESOURCES/bkgnd.png",
                "icon": "/RESOURCES/custom.png",  
                "textPlacement": "center",
                "left": 60, 
                "top": 160,     
                "width": 100,   
                "height": 20
                }
```




## Supported Properties

Tous les boutons partagent une même série de propriétés de base :


[Gras](properties_Text.md#bold) - [Style de la bordure](properties_BackgroundAndBorder.md#border-line-style) - [Bas](properties_CoordinatesAndSizing.md#bottom) - [Style de bouton](properties_TextAndPicture.md#button-style) - [CSS Class](properties_Object.md#css-class) - [Déposable](properties_Action.md#droppable) - [Focusable](properties_Entry.md#focusable) - [Police](properties_Text.md#font) - [Couleur de la police](properties_Text.md#font-color) - [Taille](properties_Text.md#font-size) - [Haut](properties_CoordinatesAndSizing.md#height) - [Message d'aide](properties_Help.md#help-tip) - [Dim. horizontal](properties_ResizingOptions.md#horizontal-sizing) - [Italique](properties_Text.md#italic) - [Gauche](properties_CoordinatesAndSizing.md#left) - [Non représenté](properties_Display.md#not-rendered) - [Nombre d'états](properties_TextAndPicture.md#number-of-states)(1) - [Object Name](properties_Object.md#object-name) - [Picture pathname](properties_TextAndPicture.md#picture-pathname)(1) - [Right](properties_CoordinatesAndSizing.md#right) - [Shortcut](properties_Entry.md#shortcut) - [Standard action](properties_Action.md#standard-action) - [Title](properties_Object.md#title) - [Title/Picture Position](properties_TextAndPicture.md#title-picture-position)(1) - [Top](properties_CoordinatesAndSizing.md#top) - [Type](properties_Object.md#type) - [Underline](properties_Text.md#underline) - [Variable or Expression](properties_Object.md#variable-or-expression) - [Vertical Sizing](properties_ResizingOptions.md#vertical-sizing) - [Visibility](properties_Display.md#visibility) - [Width](properties_CoordinatesAndSizing.md#width)

> (1) Non pris en charge par le style [Aide](#help).


Additional specific properties are available, depending on the [button style](#button-styles):

- [Background pathname](properties_TextAndPicture.md#backgroundPathname) - [Horizontal Margin](properties_TextAndPicture.md#horizontalMargin) - [Icon Offset](properties_TextAndPicture.md#icon-offset) - [Vertical Margin](properties_TextAndPicture.md#verticalMargin) (Custom)
- [Bouton par défaut](properties_Appearance.md#default-button) (A plat, Classique)
- [With pop-up menu](properties_TextAndPicture.md#with-pop-up-menu) (Toolbar, Bevel, Rounded Bevel, OS X Gradient, OS X Textured, Office XP, Circle, Custom)

