---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;Profil unifié;unifié;Profil;rtcp;graphiques XDM
title: Solutions d’accessibilité personnalisée pour les Experience Platform
topic-legacy: guide
type: Documentation
description: En savoir plus sur les solutions d’accessibilité personnalisées dans l’interface utilisateur de Adobe Experience Platform.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 1%

---


# Solutions d’accessibilité personnalisées pour les Experience Platform

Adobe Experience Platform est continuellement amélioré pour répondre aux besoins de tous les types d’utilisateurs et se conformer aux normes internationales qui incluent les personnes ayant des déficiences visuelles, auditives, mobiles ou autres. Ce document décrit les solutions d’accessibilité personnalisées dans l’interface utilisateur de l’Experience Platform.

## Page d’accueil et interface utilisateur - Aperçu

L’interface utilisateur de l’Experience Platform respecte les rapports de contraste requis pour le texte, les graphiques et les composants de l’interface utilisateur normaux. Les couleurs de l’interface utilisateur ont également été choisies pour prendre en charge l’accessibilité pour tous les utilisateurs, y compris ceux présentant un handicap visuel.

Dans Platform, les éléments de l’interface utilisateur qui peuvent être cliqués ou activés avec un pointeur peuvent également être engagés à l’aide du clavier. Cela inclut le volet de navigation de gauche, les lecteurs vidéo, les tableaux, etc.

Experience Platform s’efforce de respecter les normes internationales d’accessibilité, y compris les directives d’accessibilité du contenu web 2.1 aux niveaux A et AA et les normes web de l’Initiative sur l’accessibilité web - Applications Internet riches accessibles (WAI-ARIA).

![Page d’accueil de l’interface utilisateur de Adobe Experience Platform.](images/homepage.png)

## Navigation de gauche

Le volet de navigation de gauche de l’interface utilisateur de l’Experience Platform est accessible via le clavier et fournit un contraste des couleurs dans les états normaux, de survol et de sélection, conformément aux normes d’accessibilité.

Dans l’écran d’accueil, les utilisateurs peuvent accéder à l’onglet dans le volet de navigation de gauche. Si vous sélectionnez **Maj + Tab**, l’utilisateur est renvoyé à l’écran d’accueil.

![L’Experience Platform a quitté la navigation.](images/left-navigation-select.png)

La navigation de gauche étant active, l’onglet **Tab** permet aux utilisateurs de développer et de réduire l’interaction. La possibilité de développer ou de réduire la navigation de gauche est activée avec **Entrée (Retour)**.

![La navigation à gauche de l’Experience Platform s’est effondrée.](images/left-navigation-collapse.png)

Avec la navigation de gauche active, les touches fléchées Haut et Bas naviguent continuellement vers chaque élément de la navigation et du cycle (en d’autres termes, la cible d’action ne se déplace pas tant que l’utilisateur ne s’éloigne pas de la navigation de gauche). Le focus s’affiche pour les éléments de navigation lorsqu’ils sont sélectionnés. La sélection en cours s’affiche avec un texte en surbrillance et en gras. Lorsque vous sélectionnez un élément de navigation de gauche, **Entrée (Retour)** ouvre l’élément d’interface utilisateur sélectionné dans le panneau de droite, mais la sélection reste dans le volet de navigation de gauche jusqu’à ce que l’utilisateur s’éloigne de l’onglet .

![Le volet de navigation de gauche de l’Experience Platform avec les sources sélectionnées.](images/left-navigation-sources.png)

Certaines fonctionnalités de Platform ne sont pas activées pour tous les utilisateurs. Ces éléments apparaissent dans la navigation, mais ne peuvent pas être sélectionnés. Lorsque vous naviguez à l’aide du clavier, ces éléments sont ignorés lors de la navigation par flèche et ne peuvent pas être sélectionnés à l’aide de la commande **Entrée (retour)**.

![Les sections de la navigation de gauche de l’Experience Platform qui ne sont pas activées pour l’utilisateur ne peuvent pas être sélectionnées.](images/left-navigation-sections-disabled.png)

## Boîte de dialogue Vidéo incorporée

Vous pouvez visionner les vidéos dans Experience Platform à l’aide de la navigation clavier pour mettre en surbrillance et sélectionner un lien vidéo disponible. Une boîte de dialogue vidéo incorporée s’ouvre alors dans l’interface utilisateur de Platform.

![Une bordure bleue apparaît autour d’un élément sélectionné pour indiquer que le focus est appliqué.](images/profile-overview-tab.png)

## Accessibilité clavier de la boîte de dialogue vidéo

La boîte de dialogue vidéo incorporée peut également être naviguée à l’aide du clavier. Le tableau suivant décrit la navigation clavier complète disponible pour la boîte de dialogue vidéo incorporée.

| Elément Boîte de dialogue | Accessibilité au clavier | Description |
|---|---|---|
| Lecture et pause | Onglet<br/>Barre d’espacement | Utilisez **l’onglet** pour mettre l’accent sur le bouton de lecture. **** La barre d’espace lance la lecture vidéo et interrompt la lecture vidéo. |
| Lecture | Tab<br/>Flèche vers la gauche<br/>Flèche vers la droite | Lorsque la vidéo est en cours de lecture, utilisez **Tabulation** pour cibler la barre de défilement. Avec la barre de défilement active, **les touches fléchées gauche et droite** ignorent la lecture vidéo avant et arrière 5 secondes, respectivement. |
| Mode muet | Onglet<br/>Barre d’espacement | Utilisez **Onglet** pour cibler l’élément de volume silencieux. Utilisez **spacebar** pour mettre en sourdine ou annuler la lecture vidéo. |
| Volume | Tab<br/>Flèche vers la gauche<br/>Flèche vers la droite | Utilisez **Onglet** pour vous concentrer sur l’élément de volume. **Les** touches fléchées gauche et droite déplacent le volume vers le haut et vers le bas, respectivement. |
| [!UICONTROL Sous-titres]  codés(&quot;cc&quot;) | Onglet<br/>Entrée<br/>Flèche vers le haut<br/>Flèche vers le bas | **** Onglet Sous-titres  [!UICONTROL codés]  (&quot;cc&quot;). Utilisez **Entrée** pour ouvrir le menu, et **touches fléchées Haut et Bas** pour sélectionner une langue pour les sous-titres. **** L’entrée confirme votre sélection. |
| [!UICONTROL Qualité] | Onglet<br/>Entrée<br/>Flèche vers le haut<br/>Flèche vers le bas | Utilisez **l’onglet** pour cibler l’élément [!UICONTROL Qualité]. Utilisez **Entrée** pour ouvrir le menu et les **touches fléchées Haut et Bas** pour sélectionner la qualité vidéo. **** L’entrée confirme votre sélection. |
| Plein écran | Onglet<br/>Barre d’espacement ou Entrée<br/>Échappement | Utilisez **Onglet** pour cibler l’élément Plein écran. Utilisez **la barre d’espace ou Entrée** pour activer l’affichage plein écran. **Escape** (&quot;esc&quot;) quitte le mode plein écran. |
| Fermer | Onglet<br/>Barre d’espace ou Entrée | Utilisez **Tabulation** pour mettre le bouton de fermeture au point. Utilisez la touche **barre d’espace ou Entrée** pour quitter la boîte de dialogue vidéo. |

>[!NOTE]
>
>À tout moment pendant la lecture, la touche Échap (&quot;esc&quot;) peut être utilisée pour fermer la boîte de dialogue vidéo incorporée.

![Boîte de dialogue vidéo incorporée avec des nombres identifiant les éléments de navigation au clavier.](images/video-dialog.png)

## Glisser-déposer de fichier

Dans Experience Platform, toutes les zones de glisser-déposer de sélection de fichier sont accessibles via le clavier. L’utilisation de l’onglet **Tab** pour mettre en surbrillance **[!UICONTROL Sélectionner les fichiers]** et l’utilisation de l’option **Entrée ou de la barre d’espace** pour la sélectionner appellent l’interface utilisateur de sélection des fichiers du système d’exploitation.

Une fois le fichier téléchargé, une icône de suppression devient accessible via le clavier pour supprimer le fichier sélectionné et en charger un nouveau. Les utilisateurs peuvent utiliser **l’onglet** pour se concentrer sur l’icône de suppression et **Entrée ou la barre d’espace** pour la sélectionner. Une fois le fichier supprimé, **[!UICONTROL Choose files]** est automatiquement activé et peut être sélectionné.

Si le fichier téléchargé n’est pas au format correct, une icône d’erreur s’affiche avec un message d’erreur et le bouton **[!UICONTROL Choisir les fichiers]** est activé et sélectionnable.

![Zone de glisser-déposer d’un fichier avec un message d’erreur et le bouton de sélection des fichiers activé.](images/drag-and-drop.png)

Lorsque vous sélectionnez une zone de glisser-déposer, l’interface utilisateur de sélection de fichier est également invoquée. De plus, l’utilisateur peut sélectionner un fichier et le faire glisser sur la zone pour commencer le téléchargement.

![Une zone de glisser-déposer de fichier active en tant qu’utilisateur de la souris fait glisser un fichier dans la zone.](images/drag-and-drop-mouse-over.png)

## Navigation dans le tableau

Tous les tableaux de l’interface utilisateur de l’Experience Platform sont accessibles via le clavier. La navigation et l’interaction avec les lignes et les colonnes d’un tableau sont possibles grâce à une série de raccourcis clavier :

* Dans l’en-tête du tableau, utilisez la **flèche vers le bas** pour parcourir le tableau. Les en-têtes de tableau peuvent être sélectionnés lors de la navigation via **Onglet**. Vous pouvez modifier l’ordre de tri à l’aide de **la barre d’espace**.
* **Les** touches fléchées Haut et Bas traversent les lignes du tableau.
* Lorsqu’une ligne est sélectionnée ou sélectionnée, la fonction **Entrée** de la ligne fournit des détails dans le rail de droite.
* Lorsqu’une ligne est sélectionnée ou sélectionnée, utilisez les **touches de direction** pour parcourir chaque élément de la ligne.
* Utilisez **Entrée** pour sélectionner un élément dans la ligne. Les utilisateurs disposant de lecteurs d’écran sont avertis si une nouvelle fenêtre doit s’ouvrir.

### Accessibilité clavier du tableau de navigation

| Accessibilité au clavier | Description |
|---|---|
| HOME (Fonction + flèche gauche) | Lorsque la ligne est sélectionnée, emmène les utilisateurs au premier élément de la ligne. |
| END (Fonction + flèche droite) | Lorsque la ligne est sélectionnée, emmène les utilisateurs au dernier élément de la ligne. |
| Page vers le haut | Déplace 10 lignes vers le haut du tableau (par page) |
| Page vers le bas | Déplace 10 lignes vers le bas du tableau (par page) |
| Ctrl + ACCUEIL | Atteint la première ligne du tableau |
| Ctrl + FIN | Commence à travailler dans le tableau par page |

## Interface utilisateur de l’éditeur de schémas

L’interface utilisateur de l’éditeur de schémas est rendue accessible par les fonctionnalités suivantes :

* L’éditeur de schémas prend en charge la navigation au clavier, y compris l’utilisation de l’onglet **Tab** pour naviguer dans les éléments de l’interface utilisateur.
* **** Des onglets entrent dans le champ de recherche, puis dans l’arborescence du schéma.
* L’arborescence des schémas prend en charge l’utilisation de touches fléchées pour naviguer dans l’interface utilisateur de l’arborescence des schémas.
   * **Les** flèches haut et bas peuvent être utilisées pour parcourir l’arborescence.
   * **Les** flèches gauche et droite peuvent être utilisées pour développer et réduire les noeuds ou passer d’une action intégrée à l’autre dans l’arborescence du schéma.
* **Entrée (Retour)** active les détails des noeuds individuels dans le panneau des détails à droite.
* La clé **Home** renvoie au haut de l’arborescence.
* La touche **Fin** accède au bas de l’arborescence.
* L’arborescence du schéma comprend également des libellés ARIA pour les lecteurs d’écran.

## Interface utilisateur du créateur de segments

Lorsque vous utilisez l’interface utilisateur du créateur de segments pour créer, modifier et interagir avec des segments dans Experience Platform, les fonctionnalités suivantes améliorent l’accessibilité :

* L’interface utilisateur du créateur de segments est accessible via la navigation clavier.
* Les lecteurs d’écran doivent reconnaître les balises de balisage pour les en-têtes et peuvent annoncer l’en-tête avec son niveau.
* D’autres technologies d’assistance peuvent modifier l’affichage visuel d’une page à l’aide d’en-têtes codés correctement pour afficher un aperçu ou une autre vue.

## Éditeur de Query Service

Les fonctionnalités d’accessibilité suivantes sont disponibles dans l’éditeur de Query Service :

* Le contraste de couleur dans l’interface utilisateur de l’éditeur de Query Service respecte la conformité en matière d’accessibilité.
* La navigation au clavier est prise en charge en dehors de l’interface utilisateur de l’éditeur. L’interface utilisateur de l’éditeur est un miroir de code incorporé.

## Onglet Vue du système dans les sources et les destinations

Lorsque vous parcourez la **[!UICONTROL vue système]** dans les sources et les destinations, les fonctionnalités suivantes améliorent l’accessibilité :

* **** Les tablettes mettent l’accent sur la première carte de connexion source.
   * **** Onglet pour vous concentrer à nouveau sur le bouton à l’intérieur de la carte
   * Sélectionnez **Entrée** pour activer le bouton d’appel à l’action dans la carte.
* La sélection de **Entrée** sur la carte de connexion active également plus de détails dans le rail de droite.
   * Lorsque le rail de droite est activé, la sélection est définie sur cette zone. **** Le panneau se concentre sur  **** Fermer pour le volet de droite. Si vous sélectionnez **Onglet**, la sélection se déplace à nouveau dans le panneau du rail droit.
   * S’il existe plusieurs cartes de connexion source, **Onglet** passe par les connexions.
   * Utilisez les **touches fléchées (vers le haut, le bas, la gauche et la droite)** pour parcourir la liste des sources.
   * Sélectionnez **Onglet** pour définir la mise au point sur le panneau du rail droit.