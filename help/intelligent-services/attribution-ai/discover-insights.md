---
keywords: Experience Platform;insights;accès aux attributions;rubriques les plus consultées;informations sur les attributions
feature: Attribution AI
title: Découvrez les statistiques dans Attribution AI
description: Ce document sert de guide pour interagir avec les informations des instances de service dans l’interface utilisateur Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 47%

---

# Découvrez les insights d’Attribution AI

Les instances de service Attribution AI fournissent des informations qui peuvent être utilisées pour prendre et mesurer des décisions marketing liées aux performances marketing et au retour sur investissement. La sélection d’une instance de service fournit des visualisations et des filtres pour vous aider à comprendre l’impact de chaque interaction client au cours de chacune des phases du parcours client.

Ce document sert de guide pour interagir avec les informations des instances de service dans l’interface utilisateur Adobe Intelligent Services.

## Prise en main

Pour utiliser les informations relatives à Attribution AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une nouvelle instance de service, consultez le [guide de l’interface utilisateur d’Attribution AI](./user-guide.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Aperçu des informations des instances de service

Dans l’interface utilisateur de [!DNL Adobe Experience Platform], sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche les services intelligents Adobe disponibles. Dans le conteneur pour Attribution AI, sélectionnez **[!UICONTROL Ouvrir]**.

![Accès à votre instance](./images/insights/open_Attribution_ai.png)

La page de service d’Attribution AI s’affiche. Cette page répertorie les instances de service d’Attribution AI et affiche les informations les concernant, notamment le nom de l’instance, les événements de conversion, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour. Sélectionnez un nom d’instance de service à commencer.

>[!NOTE]
>
>Seules les instances de service ayant réussi des exécutions de notation peuvent être sélectionnées.

![Création d’une instance](./images/insights/select-service-instance.png)

Ensuite, la page d’informations pour cette instance de service apparaît sur laquelle vous trouverez des visualisations et différents filtres pouvant interagir avec vos données. Les visualisations et les filtres sont expliqués de manière plus détaillée dans ce guide.

![page de configuration](./images/insights/landing-page.png)

### Détails des instances de service

Pour afficher des détails supplémentaires pour une instance de service, sélectionnez **[!UICONTROL Afficher plus]** en haut à droite.

![afficher plus](./images/insights/show-more.png)

Une liste détaillée s’affiche. Pour plus d’informations sur l’une des propriétés répertoriées, veuillez consulter le [guide d’utilisation d’Attribution AI](./user-guide.md).

![afficher les détails](./images/insights/advanced-details.png)

### Modification d’une instance

Pour modifier une instance, sélectionnez **[!UICONTROL Edit]** dans le volet de navigation supérieur droit.
![cliquez sur le bouton Modifier](./images/insights/edit-button.png)

La boîte de dialogue de modification s’affiche, vous permettant de modifier le nom, la description et la fréquence de notation de l’instance. Si l’état de l’instance est désactivé, la fréquence de notation ne peut pas être modifiée. Pour confirmer vos modifications et fermer la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](./images/insights/edit-popover.png)

### Actions supplémentaires {#more-actions}

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. Sélectionner **[!UICONTROL Autres actions]** ouvre une liste déroulante qui vous permet de sélectionner l’une des opérations suivantes :

- **[!UICONTROL Clone]** : clone l’instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Télécharger des données récapitulatives]** : télécharge un fichier CSV contenant les données récapitulatives.
- **[!UICONTROL Accéder aux scores]** : la sélection de **[!UICONTROL Accéder aux scores]** vous redirige vers les [scores d’accès pour le tutoriel Attribution AI](./download-scores.md).
- **[!UICONTROL Afficher l’historique d’exécution]** : une fenêtre contextuelle contenant une liste des exécutions de notation associée à l’instance de service apparaît.

![actions supplémentaires](./images/insights/more-actions.png)

## Filtrage de vos données

Les informations d’Attribution AI vous permettent de filtrer vos données et de mettre à jour automatiquement les visuels de l’interface utilisateur en fonction des filtres sélectionnés.

### Événement de conversion

Lorsque vous créez une nouvelle instance dans Attribution AI, le champ « Événements de conversion » fait partie des champs obligatoires. Les événements de conversion sont des objectifs professionnels qui identifient l’impact des activités marketing comme les commandes e-commerce, les achats en magasin et les visites sur le site web.

À partir de l’instance, le menu déroulant **[!UICONTROL Événements de conversion]** vous permet de sélectionner l’un des événements définis pour votre instance afin de filtrer vos données. Sélectionner des événements spécifiques modifie les visualisations de l’interface utilisateur pour ne gérer que les conversions appartenant à ces événements.

![événement de conversion](./images/insights/conversion-event.png)

### Modèle d’attribution

Sélectionnez **[!UICONTROL Modèle d’attribution]** pour ouvrir une liste déroulante contenant tous les différents modèles d’attribution disponibles. Vous pouvez sélectionner plusieurs modèles pour en comparer les résultats. Pour plus d’informations sur les différents modèles d’attribution et la manière dont ils fonctionnent, rendez-vous sur l’aperçu [Attribution AI](./overview.md) sur lequel vous trouverez un tableau contenant des informations sur chaque modèle.

![modèle d’attribution](./images/insights/attribution-model.png)

### Région

>[!NOTE]
>
>Ce filtre n’est présent que si vous avez effectué l’étape facultative [modélisation régionale](./user-guide.md#region-based-modeling-optional) dans le guide de l’interface utilisateur Attribution AI lors de la création de votre instance de service.

Ce filtre vous permet de sélectionner les régions que vous avez configurées au cours du processus de création d’instances.

### Ajout de filtres

Vous pouvez ajouter d’autres filtres en sélectionnant l’icône **filter** pour ouvrir la fenêtre contextuelle **[!UICONTROL Ajouter des filtres]** . La fenêtre contextuelle **[!UICONTROL Ajouter des filtres]** vous permet de filtrer par Canal, Géographie, Type de média et Produit. Seuls les filtres applicables pour une instance de service sont renseignés par la fenêtre contextuelle. Par exemple, si vous n’avez pas fourni de données géographiques ou de type de média, ces attributs de filtre ne seront pas disponibles pour votre instance.

![filtres supplémentaires](./images/insights/additional-filters.png)

![fenêtre contextuelle de filtre](./images/insights/filter-popover.png)

- **[!UICONTROL Canal] :** La sélection de l’attribut channel vous permet de filtrer l’un de vos canaux marketing disponibles. Vous pouvez sélectionner plusieurs canaux pour les comparer.
- **[!UICONTROL Géographie] :** La sélection de l’attribut géographie vous permet de filtrer les codes pays en fonction de modèles régionaux. En fonction de vos données, ce filtre peut être présent ou non. Les codes pays comportent deux caractères. Voir la liste complète des codes pays [ici](https://datahub.io/core/country-list).
- **[!UICONTROL Type de média] :** La sélection de l’attribut de type de média vous permet de filtrer n’importe quel type de média défini.
- **[!UICONTROL Produit] :** La sélection de l’attribut de produit vous permet de filtrer les produits ingérés à la création de votre instance.

### Période

Sélectionnez l’icône de calendrier pour ouvrir la fenêtre contextuelle de la période. Les dates de début et de fin de l’événement de conversion déterminent la quantité de données générées dans l’interface utilisateur. Vous pouvez choisir de limiter ou d’élargir la période pour vous concentrer sur une quantité de données générée ou l’élargir.

![période](./images/insights/display-date-range.png)

## Aperçu de vos données

La fiche **[!UICONTROL Aperçu]** affiche vos conversions totales par modèle d’attribution. Le nombre total change en fonction de la manière dont votre recherche est spécifique à l’aide des filtres soulignés précédemment dans ce document. Sélectionner plus de modèles ajoute des cercles supplémentaires à l’Aperçu, dont chacun se voit définir une couleur correspondant à la légende.

![aperçu](./images/insights/Overview.png)

## Tendances hebdomadaires

La fiche **[!UICONTROL Tendances hebdomadaires]** décompose vos conversions totales selon la période que vous avez définie au cours du processus de filtrage.

Sélectionnez les points de suspension en haut à droite de la carte **Tendances hebdomadaires** pour afficher un menu déroulant vous permettant de sélectionner des tendances quotidiennes, hebdomadaires ou mensuelles.

Survoler la ligne des données avec votre souris d’un modèle d’attribution spécifique crée une fenêtre contextuelle qui affiche le nombre total de conversions pour cette date.

![tendances](./images/insights/weekly-trends.png)

## Répartition par canal

La fiche **[!UICONTROL Répartition par canal]** est utilisée pour déterminer le nombre total de conversions associé à chaque canal. Vous pouvez utiliser cette fiche pour vous aider à prendre des décisions sur l’efficacité de chaque canal et le retour sur investissement.

Si vous sélectionnez les points de suspension en haut à droite de la carte **[!UICONTROL Ventilation par canal]** , une liste déroulante s’affiche pour vous permettre de renseigner les données en fonction des points de contact.

![canal de répartition](./images/insights/channel-breakdown.png)

## Campagnes principales

La fiche **[!UICONTROL Campagnes principales]** affiche un aperçu de vos campagnes et des performances de vos campagnes dans chaque canal. Cette fiche peut vous aider à informer votre équipe de l’efficacité d’une campagne spécifique pour un canal donné et fournir des informations telles que les campagnes dans lesquelles vous devriez investir davantage.

![campagnes principales](./images/insights/top-campaigns.png)

## Ventilation par position de point de contact

La sélection de l’onglet **[!UICONTROL Analyse de chemin]** charge les graphiques **[!UICONTROL Ventilation par position de point de contact]** et **[!UICONTROL Chemins de conversion principaux]**.

Le graphique **[!UICONTROL Répartition par position de point de contact]** est une ventilation des conversions attribuées par position du point de contact par rapport à tous les chemins de conversion. Ce graphique vous aide à comprendre les points de contact les plus efficaces à différentes étapes du chemin de conversion. Les scènes sont de début, de lecture et de plus près.

- **Démarrage :** indique que le point de contact a été la première touche dans un chemin de conversion.
- **Lecteur :** Indique que le point de contact n’était pas la première ou la dernière touche menant à une conversion.
- **Plus proche :** indique que le point de contact était la dernière touche avant une conversion.

>
>
> La somme des pourcentages de contribution pour un modèle d’attribution sur tous les points de contact et toutes les positions doit être égale à 100.

![point de contact de ventilation user-path](./images/insights/user-paths.png)

## Meilleurs chemins de conversion

Le graphique **[!UICONTROL Meilleurs chemins de conversion]** montre les scores algorithmiques et influencés sur les principaux chemins de conversion dans les régions sélectionnées. Ce graphique vous permet de visualiser les points de contact qui contribuent aux conversions et le score d’attribution pour chaque point de contact. Vous pouvez utiliser ces informations pour afficher les chemins les plus fréquents d’une région donnée et déterminer s’il existe des motifs entre les différents ensembles de points de contact.

![Chemins d’accès utilisateur les plus courants](./images/insights/Touchpoint-paths.png)

## Efficacité des points de contact

Si vous sélectionnez l’onglet **[!UICONTROL Efficacité du point de contact]**, la carte **[!UICONTROL Efficacité du point de contact]** est chargée. Cette carte utilise la distribution des données d’Attribution AI pour afficher les informations pour chaque point de contact. Les données de ce tableau ne sont générées que pour des périodes spécifiques, comme indiqué par la date **[!UICONTROL À partir de]** dans le coin supérieur droit de la carte.

![sélection de l’efficacité du point de contact](./images/insights/Touchpoint-effectiveness.png)

Vous pouvez utiliser les informations de la carte **[!UICONTROL Efficacité du point de contact]** pour comprendre comment un point de contact contribue à une conversion. Vous pouvez également déterminer l’efficacité de chaque point de contact avec les mesures de performances suivantes :

**Chemins touchés** : cette mesure affiche un pourcentage des chemins atteignant/n’atteignant pas la conversion pour le point de contact. Vous constaterez une augmentation des conversions attribuées si le taux de conversion (pourcentage) des chemins menant à la conversion vers les chemins n’aboutissant pas à une conversion est élevé.

![Mesure Chemins touchés](./images/insights/Touchpoint-metrics.png)

**Mesure d’efficacité** : cette mesure affiche les étoiles sur une échelle de un à cinq. L’échelle indique l’importance relative d’un point de contact pour effectuer une conversion.

>[!NOTE]
>
>Un volume de point de contact plus élevé ne garantit pas une mesure d’efficacité plus élevée.

**Volume total** : nombre agrégé de fois où un utilisateur a touché un point de contact. Cela inclut les points de contact qui apparaissent sur un chemin pour effectuer une conversion ainsi que les chemins qui n’entraînent pas de conversion.

## Étapes suivantes

Lorsque vous avez terminé de filtrer les données et que vous pouvez afficher les informations appropriées, vous avez la possibilité d’accéder aux scores. Pour obtenir un guide détaillé sur la manière dont vous pouvez accéder à vos scores, consultez le tutoriel [Accéder aux scores dans Attribution AI](./download-scores.md). De plus, vous pouvez également télécharger les données récapitulatives comme indiqué dans [Actions supplémentaires](#more-actions). Sélectionner « Télécharger les données récapitulatives » télécharge les données récapitulatives agrégées par dates.

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à apprendre à utiliser la page d’informations Attribution AI afin de comprendre le retour sur investissement des canaux et campagnes marketing.

>[!VIDEO](https://video.tv.adobe.com/v/345100?learn=on&quality=12&captions=fre_fr)
