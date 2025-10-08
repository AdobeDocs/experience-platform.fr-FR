---
title: Vue Cartes de contenu
description: Ce guide détaille les informations sur la vue Cartes de contenu dans Adobe Experience Platform Assurance.
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Vue Cartes de contenu dans Assurance

La vue Messagerie In-App d’Adobe Experience Platform Assurance permet de valider votre application, de surveiller les cartes de contenu diffusées sur votre appareil et de prévisualiser les cartes.

## Cartes de contenu

En haut de l’onglet **[!UICONTROL Cartes de contenu]** se trouve une liste déroulante **[!UICONTROL Carte de contenu]**. Toutes les cartes de contenu reçues au cours de la session Assurance sont répertoriées. Si une carte ne figure pas dans cette liste, cela signifie que l’application ne l’a jamais reçue.

![Liste déroulante Carte de contenu contenant une liste de cartes](./images/content-cards/dropdown.png)

La sélection d’une carte de contenu affiche de nombreuses informations sur cette carte, comme décrit dans les sections ci-dessous.

### Aperçu de la carte

Dans le panneau de droite se trouve un volet **[!UICONTROL Aperçu de la carte]** qui montre le rendu d’une carte dans les modèles courants (petite image, grande image et image uniquement).

![Aperçu de la carte de contenu sélectionnée](./images/content-cards/preview.png)

Utilisez le bouton (bascule) **[!UICONTROL Thème]** pour afficher la carte en mode clair ou sombre.

![Aperçu de la carte de contenu sélectionnée dans le thème sombre](./images/content-cards/preview-dark.png)

### Onglets disponibles

Dans la section de gauche, les onglets disponibles dépendent de la carte sélectionnée. Si la carte comprend des règles, trois onglets s’affichent : **[!UICONTROL Info]**, **[!UICONTROL Interactions]** et **[!UICONTROL Analyser les règles]**.

![Onglets disponibles lorsque des règles sont présentes : Informations, Interactions, Analyser les règles](./images/content-cards/tabs-with-rules.png)

Si la carte n’inclut pas de règles, deux onglets s’affichent : **[!UICONTROL Info]** et **[!UICONTROL Interactions]**.

![Onglets disponibles en l’absence de règles : Informations et interactions](./images/content-cards/tabs-no-rules.png)

### Onglet Infos

L’onglet **[!UICONTROL Info]** affiche la section **[!UICONTROL Propriétés de la carte]** en haut, y compris les badges pour l’**[!UICONTROL État actuel]** (déclenchement, affichage, ignorance, disqualification), ainsi que des méta-détails tels que **[!UICONTROL Modèle]** (image petite, image grande ou image uniquement), **[!UICONTROL Surface]** et toute paire clé-valeur personnalisée.

![Propriétés de la carte présentant les badges d’état actuels, le modèle, la surface et les paires clé-valeur](./images/content-cards/card-properties.png)

Ci-dessous, la section **[!UICONTROL Propriétés de la campagne]** affiche les informations chargées depuis Adobe Journey Optimizer (AJO).

Vous pouvez également sélectionner **[!UICONTROL Afficher la campagne]** pour ouvrir la carte dans AJO à des fins d’inspection ou de modification.

![Section Propriétés de la campagne avec le bouton pour Afficher la campagne](./images/content-cards/campaign-properties.png)

### Onglet Interactions

L’onglet **[!UICONTROL Interactions]** résume le cycle de vie de chaque carte sous la forme d’une séquence de badges : il commence toujours par **[!UICONTROL trigger]**, suivi du résultat obtenu par les règles (**[!UICONTROL display]**, **[!UICONTROL dismiss]** ou **[!UICONTROL disqualifier]**.

![Tableau des interactions affichant les badges de cycle de vie du déclencheur à afficher, ignorer ou disqualifier](./images/content-cards/interactions-tab.png)

### Onglet Analyser les règles

L’onglet **[!UICONTROL Analyser]** affiche un tableau d’événements avec jusqu’à trois colonnes de règles (**[!UICONTROL Afficher]**, **[!UICONTROL Ignorer]** et **[!UICONTROL Disqualifier]**, selon les règles de la carte. Si la carte ne définit qu’une seule règle, seule cette colonne s’affiche.

Chaque ligne représente un événement de session, et chaque colonne indique si la règle de la carte correspond aux conditions de cet événement. Un score de 0 % signifie qu’aucune condition ne correspond ; 100 % correspond à l’intégralité (la règle se déclenche).

Si l’événement correspond à une condition, une coche verte s’affiche. Si l’événement ne correspond pas, une icône rouge s’affiche.

![Analyser le tableau des événements d’onglet avec les colonnes Afficher, Ignorer et Disqualifier les règles](./images/content-cards/rules-tab.png)

Utilisez le curseur **[!UICONTROL Seuil de correspondance]** pour filtrer les événements en fonction du pourcentage de correspondance minimal.

![Curseur Seuil de correspondance pour filtrer les événements par pourcentage de correspondance minimal](./images/content-cards/match-threshold.png)

Lorsque vous sélectionnez un événement, un panneau de détails s’ouvre à droite avec un accordéon répertoriant les trois règles : **[!UICONTROL Affichage]**, **[!UICONTROL Ignorer]** et **[!UICONTROL Disqualifier]**.

![Panneau Détails de l’événement répertoriant les règles d’affichage, d’exclusion et de disqualification](./images/content-cards/rules-panel.png)

Développez n’importe quelle section pour afficher les conditions de la règle, les conditions correspondantes et le pourcentage de correspondance calculée pour ce résultat.

![Accordéon de règle développé affichant les conditions et le pourcentage de correspondance](./images/content-cards/expanded-accordion.png)

## Onglet Demandes

L’onglet **[!UICONTROL Demandes]** indique quelles cartes de contenu ont été demandées et sur quelle surface.

![Onglet Demandes affichant les demandes de carte de contenu](./images/content-cards/requests-tab.png)

Utilisez le bouton **[!UICONTROL Afficher la carte]** pour revenir à l’onglet Informations d’une carte de contenu spécifique.

## Onglet Liste des événements

L’onglet **[!UICONTROL Liste des événements]** affiche les événements de session relatifs aux cartes de contenu, y compris les requêtes/réponses de proposition AJO, les événements de cycle de vie des cartes et le suivi des interactions. Vous pouvez rechercher, filtrer, trier et personnaliser des colonnes, ainsi qu’exporter des résultats.

La sélection d’un événement ouvre un panneau des détails droit avec la payload brute et les attributs clés ; vous pouvez également marquer les événements pour le suivi. Cette vue est utile pour mettre en corrélation les requêtes, les résultats des règles et les interactions au cours de la session.

![Onglet Liste d’événements avec des événements de session pouvant faire l’objet de recherches et filtrables pour les cartes de contenu](./images/content-cards/event-list.png)

## Onglet Validation

L’onglet **[!UICONTROL Validation]** exécute des validations sur la session en cours, en vérifiant si l’application a été configurée correctement pour la messagerie :

![Les résultats de l’onglet Validation vérifient la configuration de la messagerie pour la session en cours](./images/content-cards/validation.png)
