---
keywords: Experience Platform ; informations ; attribution de l’accès ; rubriques populaires ; attribution des informations
solution: Intelligent Services, Experience Platform
title: Découvrez les statistiques d'Attribution AI
topic-legacy: Attribution AI insights
description: Ce document sert de guide pour interagir avec les insights des instances de service dans l’interface utilisateur Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 49%

---

# Découvrir les informations d&#39;Attribution AI

Les instances de service Attribution AI fournissent des insights qui peuvent être utilisés pour prendre et mesurer des décisions marketing liées aux performances marketing et au retour sur investissement. La sélection d’une instance de service fournit des visualisations et des filtres pour vous aider à comprendre l’impact de chaque interaction client au cours de chacune des phases du parcours client.

Ce document sert de guide pour interagir avec les insights des instances de service dans l’interface utilisateur Adobe Intelligent Services.

## Prise en main

Pour utiliser les insights relatifs à Attribution AI, vous devez avoir à disposition une instance de service dont l’état d’exécution est réussi. Pour créer une nouvelle instance de service, consultez le [guide de l’interface utilisateur d’Attribution AI](./user-guide.md). Si vous avez récemment créé une instance de service et qu’elle est toujours en cours de formation et de notation, comptez 24 heures pour qu’elle se termine.

## Aperçu des insights des instances de service

Dans l&#39;interface utilisateur [!DNL Adobe Experience Platform], sélectionnez **[!UICONTROL Services]** dans le volet de navigation de gauche. Le navigateur **[!UICONTROL Services]** apparaît et affiche les services intelligents Adobe disponibles. Dans le conteneur pour Attribution AI, sélectionnez **[!UICONTROL Ouvrir]**.

![Accès à votre instance](./images/insights/open_Attribution_ai.png)

La page de service d’Attribution AI s’affiche. Cette page répertorie les instances de service d’Attribution AI et affiche les informations les concernant, notamment le nom de l’instance, les événements de conversion, la fréquence à laquelle l’instance est exécutée et l’état de la dernière mise à jour. Sélectionnez un nom d’instance de service à commencer.

>[!NOTE]
>
>Vous ne pouvez sélectionner que les instances de service ayant réussi les exécutions de notation.

![Création d’une instance](./images/insights/select-service-instance.png)

Ensuite, la page d’insights pour cette instance de service apparaît sur laquelle vous trouverez des visualisations et différents filtres pouvant interagir avec vos données. Les visualisations et les filtres sont expliqués de manière plus détaillée dans ce guide.

![page de configuration](./images/insights/landing-page.png)

### Détails des instances de service

Pour vue des détails supplémentaires pour une instance de service, sélectionnez **[!UICONTROL Afficher plus]** en haut à droite.

![afficher plus](./images/insights/show-more.png)

Une liste détaillée s’affiche. Pour plus d’informations sur l’une des propriétés répertoriées, veuillez consulter le [guide d’utilisation d’Attribution AI](./user-guide.md).

![afficher les détails](./images/insights/advanced-details.png)

### Modification d’une instance

Pour modifier une instance, sélectionnez **[!UICONTROL Modifier]** dans le volet de navigation supérieur droit.
![cliquez sur le bouton Modifier](./images/insights/edit-button.png)

La boîte de dialogue Modifier s’affiche, vous permettant de modifier le nom, la description et la fréquence d’évaluation de l’instance. Si l’état de l’instance est désactivé, la fréquence de notation ne peut pas être modifiée. Pour confirmer vos modifications et fermer la boîte de dialogue, sélectionnez **[!UICONTROL Enregistrer]** dans le coin inférieur droit.

![modifier la fenêtre contextuelle](./images/insights/edit-popover.png)

### Actions supplémentaires {#more-actions}

Le bouton **[!UICONTROL Actions supplémentaires]** se trouve dans la navigation en haut à droite en regard de **[!UICONTROL Modifier]**. La sélection de **[!UICONTROL Autres actions]** ouvre une liste déroulante qui vous permet de sélectionner l&#39;une des opérations suivantes :

- **[!UICONTROL Cloner]** : Clones l’instance.
- **[!UICONTROL Supprimer]** : supprime l’instance.
- **[!UICONTROL Télécharger des données récapitulatives]** : télécharge un fichier CSV contenant les données récapitulatives.
- **[!UICONTROL Scores]** d&#39;accès : La sélection des  **[!UICONTROL scores]** Access vous redirige vers les scores d’ [accès pour le didacticiel](./download-scores.md) Attribution AI.
- **[!UICONTROL Afficher l’historique d’exécution]** : une fenêtre contextuelle contenant une liste des exécutions de notation associée à l’instance de service apparaît.

![actions supplémentaires](./images/insights/more-actions.png)

## Filtrage de vos données

Les insights d’Attribution AI vous permettent de filtrer vos données et de mettre à jour automatiquement les visuels de l’interface utilisateur en fonction des filtres sélectionnés.

### Événement de conversion

Lorsque vous créez une nouvelle instance dans Attribution AI, le champ « Événements de conversion » fait partie des champs obligatoires. Les événements de conversion sont des objectifs professionnels qui identifient l’impact des activités marketing comme les commandes e-commerce, les achats en magasin et les visites sur le site web.

À partir de l’instance, le menu déroulant **[!UICONTROL Événements de conversion]** vous permet de sélectionner l’un des événements définis pour votre instance afin de filtrer vos données. Sélectionner des événements spécifiques modifie les visualisations de l’interface utilisateur pour ne gérer que les conversions appartenant à ces événements.

![événement de conversion](./images/insights/conversion-event.png)

### Modèle d’attribution

La sélection de **[!UICONTROL Modèle d’attribution]** ouvre une liste déroulante avec tous les différents modèles d’attribution disponibles. Vous pouvez sélectionner plusieurs modèles pour en comparer les résultats. Pour plus d’informations sur les différents modèles d’attribution et la manière dont ils fonctionnent, rendez-vous sur l’aperçu [Attribution AI](./overview.md) sur lequel vous trouverez un tableau contenant des informations sur chaque modèle.

![modèle d’attribution](./images/insights/attribution-model.png)

### Région

>[!NOTE]
>
>Ce filtre n’est présent que si vous avez réalisé l’étape facultative de [modélisation régionale](./user-guide.md#region-based-modeling-optional) dans le guide de l’interface utilisateur Attribution AI lors de la création de votre instance de service.

Ce filtre vous permet de sélectionner les régions que vous avez configurées au cours du processus de création d’instances.

### Filtres d&#39;Ajoute

Vous pouvez ajouter d’autres filtres en sélectionnant l’icône **filter** pour ouvrir la fenêtre contextuelle **[!UICONTROL Ajouter les filtres]**. La fenêtre contextuelle **[!UICONTROL Ajouter les filtres]** vous permet de filtrer par Canal, zone géographique, type de média et produit. Seuls les filtres applicables pour une instance de service sont renseignés par la fenêtre contextuelle. Par exemple, si vous n’avez pas fourni de données géographiques ou de type de média, ces attributs de filtre ne seront pas disponibles pour votre instance.

![filtres supplémentaires](./images/insights/additional-filters.png)

![fenêtre contextuelle de filtre](./images/insights/filter-popover.png)

- **[!UICONTROL Canal] : la** sélection de l’attribut canal vous permet de filtrer n’importe quel canal marketing disponible. Vous pouvez sélectionner plusieurs canaux pour les comparer.
- **[!UICONTROL Géographie] : la** sélection de l’attribut de géographie vous permet de filtrer les codes de pays en fonction de modèles régionaux. Selon vos données, ce filtre peut être présent ou non. Les codes pays se composent de deux caractères. Voir la liste complète du code de pays [ici](https://datahub.io/core/country-list).
- **[!UICONTROL Type] de média :** la sélection de l&#39;attribut de type de média vous permet de filtrer n&#39;importe quel type de média défini.
- **[!UICONTROL Produit] :** La sélection de l’attribut de produit vous permet de filtrer les produits qui ont été initialement ingérés dans la création de votre instance.

### Période

Sélectionnez l&#39;icône de calendrier pour ouvrir la fenêtre contextuelle de la période. Les dates de début et de fin de l’événement de conversion déterminent la quantité de données générées dans l’interface utilisateur. Vous pouvez choisir de limiter ou d’élargir la période pour vous concentrer sur une quantité de données générée ou l’élargir.

![période](./images/insights/display-date-range.png)

## Aperçu de vos données

La fiche **[!UICONTROL Aperçu]** affiche vos conversions totales par modèle d’attribution. Le nombre total change en fonction de la manière dont votre recherche est spécifique à l’aide des filtres soulignés précédemment dans ce document. Sélectionner plus de modèles ajoute des cercles supplémentaires à l’Aperçu, dont chacun se voit définir une couleur correspondant à la légende.

![aperçu](./images/insights/Overview.png)

## Tendances hebdomadaires

La fiche **[!UICONTROL Tendances hebdomadaires]** décompose vos conversions totales selon la période que vous avez définie au cours du processus de filtrage.

La sélection des points de suspension dans le coin supérieur droit de la carte **Tendances hebdomadaires** affiche une liste déroulante qui vous permet de sélectionner les tendances quotidiennes, hebdomadaires ou mensuelles.

Survoler la ligne des données avec votre souris d’un modèle d’attribution spécifique crée une fenêtre contextuelle qui affiche le nombre total de conversions pour cette date.

![tendances](./images/insights/weekly-trends.png)

## Répartition par canal

La fiche **[!UICONTROL Répartition par canal]** est utilisée pour déterminer le nombre total de conversions associé à chaque canal. Vous pouvez utiliser cette fiche pour vous aider à prendre des décisions sur l’efficacité de chaque canal et le retour sur investissement.

La sélection des points de suspension dans le coin supérieur droit de la carte **[!UICONTROL Ventilation par canal]** ouvre une liste déroulante qui vous permet de renseigner les données en fonction des points de contact.

![canal de répartition](./images/insights/channel-breakdown.png)

## Campagnes principales

La fiche **[!UICONTROL Campagnes principales]** affiche un aperçu de vos campagnes et des performances de vos campagnes dans chaque canal. Cette carte peut aider à informer votre équipe de l&#39;efficacité d&#39;une campagne spécifique pour un canal donné et fournir des informations sur les campagnes dans lesquelles vous devez investir davantage.

![campagnes principales](./images/insights/top-campaigns.png)

## Ventilation par position de point de contact

La sélection de l&#39;onglet **[!UICONTROL Analyse de chemin]** charge les graphiques **[!UICONTROL Ventilation par position de point de contact]** et **[!UICONTROL Principaux chemins de conversion]**.

Le graphique **[!UICONTROL Ventilation par position de point de contact]** est une ventilation des conversions attribuées par position du point de contact par comparaison entre tous les chemins de conversion. Ce graphique vous aide à comprendre quels points de contact sont les plus efficaces à différents stades du chemin de conversion. Les étapes sont débutant, joueur et plus proches.

- **Démarrage :** indique que le point de contact a été la première touche d’un chemin de conversion.
- **Lecteur :** indique que le point de contact n’était pas la première ou la dernière touche menant à une conversion.
- **Plus proche :** indique que le point de contact était la dernière touche avant une conversion.

>!![NOTE]
La somme de la contribution en pourcentage pour un modèle d’attribution sur tous les points de contact et postes doit être égale à 100.

![point de contact de ventilation user-path](./images/insights/user-paths.png)

## Principaux chemins de conversion

Le graphique **[!UICONTROL Principaux chemins de conversion]** montre les scores algorithmiques et influencés sur les principaux chemins de conversion dans les régions sélectionnées. Ce graphique vous permet de visualiser quels points de contact contribuent aux conversions et quel est le score d’attribution pour chaque point de contact. Vous pouvez utiliser ces informations pour vue les chemins les plus fréquents dans une certaine région et voir si des schémas se dégagent entre les différents ensembles de points de contact.

![Chemins d’utilisateur les plus courants](./images/insights/Touchpoint-paths.png)

## Efficacité des points de contact

La sélection de l&#39;onglet **[!UICONTROL Efficacité du point de contact]** charge la carte **[!UICONTROL Efficacité du point de contact]**. Cette carte utilise la distribution des données par Attribution AI pour afficher les informations pour chaque point de contact. Les données de ce tableau ne sont générées que pour des périodes spécifiques, comme indiqué par la date **[!UICONTROL A partir de]** dans l&#39;angle supérieur droit de la carte.

![sélection de l’efficacité du point de contact](./images/insights/Touchpoint-effectiveness.png)

Vous pouvez utiliser les informations de carte **[!UICONTROL Efficacité du point de contact]** pour comprendre comment un point de contact contribue à une conversion. Vous pouvez également déterminer l’efficacité de chaque point de contact avec les mesures de performances suivantes :

**Chemins touchés** : Cette mesure affiche un pourcentage des chemins qui atteignent ou non la conversion pour le point de contact. Vous verrez des conversions attribuées plus élevées si le ratio des chemins (en pourcentage) atteignant la conversion aux chemins n’atteignant pas la conversion est élevé.

![Mesure Chemins touchés](./images/insights/Touchpoint-metrics.png)

**Mesure** d&#39;efficacité : Cette mesure affiche les étoiles sur une échelle de un à cinq. L’échelle indique l’importance relative d’un point de contact pour effectuer une conversion.

>[!NOTE]
Un volume de point de contact plus élevé ne garantit pas une mesure d&#39;efficacité plus élevée.

**Volume** total : Nombre de fois où un utilisateur a touché un point de contact par l’agrégat. Il s’agit de la prise en compte des points de contact qui s’affichent sur un chemin menant à la conversion, ainsi que des chemins n’entraînant pas de conversion.

## Étapes suivantes

Lorsque vous avez terminé de filtrer les données et que vous pouvez afficher les informations appropriées, vous avez la possibilité d’accéder aux scores. Pour obtenir un guide détaillé sur la manière dont vous pouvez accéder à vos scores, consultez le tutoriel [Accéder aux scores dans Attribution AI](./download-scores.md). De plus, vous pouvez également télécharger les données récapitulatives comme indiqué dans [Actions supplémentaires](#more-actions). Sélectionner « Télécharger les données récapitulatives » télécharge les données récapitulatives agrégées par dates.

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre comment utiliser la page d’informations Attribution AI pour comprendre le retour sur investissement des canaux et campagnes marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
