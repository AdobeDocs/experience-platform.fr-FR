---
title: Présentation des caractéristiques
description: Découvrez comment utiliser les caractéristiques, qui sont un moyen léger et plus efficace de stocker l’activité des profils. Vous pouvez utiliser les caractéristiques pour maintenir la conformité aux droits de licence de votre profil tout en préservant l’activation enrichie des profils.
hide: true
source-git-commit: b86770c580e495fb9e2d80d4ef59f642ac15c1f2
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 3%

---


# Présentation des caractéristiques

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Dans Adobe Experience Platform, le profil client en temps réel vous permet de consolider vos données client en une vue unifiée en combinant des données issues de plusieurs canaux.

## Comprendre les caractéristiques {#understanding}

Actuellement, vous pouvez stocker l’ensemble de l’« événement brut » dans le profil via les événements d’expérience. Les événements d’expérience contiennent des données d’événement complètes et non filtrées, qui peuvent utiliser davantage d’espace de stockage dans Experience Platform.

Avec les caractéristiques, vous pouvez ajouter des données « précalculées » basées sur les règles que vous avez définies. Les caractéristiques sont basées sur la logique conditionnelle que vous spécifiez et sont plus efficaces en termes de stockage que l’événement d’expérience brut.

Les caractéristiques offrent une approche plus légère et plus efficace du stockage de l’activité des profils. Par conséquent, cela peut vous aider à maintenir la conformité avec vos droits de licence de profil tout en préservant l’activation des données de profil riches. Par exemple, vous pouvez utiliser les caractéristiques pour prendre en charge la collecte de données si le débit d’ingestion est élevé.

## Conditions préalables {#prerequisites}

Pour utiliser les caractéristiques, vous **devez** respecter les conditions préalables suivantes :

- Au moins **un** jeu de données d’événement d’expérience ingéré à l’aide de la collecte de données Adobe sur Edge Network
   - Vous devez disposer de l’autorisation **Gérer les jeux de données** pour activer un jeu de données pour les caractéristiques.
- L’autorisation **Afficher les caractéristiques**
   - Vous pouvez ainsi afficher vos caractéristiques et les utiliser dans le créateur de segments
- L’autorisation **Gérer les caractéristiques**
   - Vous pouvez ainsi créer, modifier et supprimer vos caractéristiques
   - Gérer les caractéristiques **inclut** toutes les autorisations **Afficher les caractéristiques**

## Limites de la version Beta {#beta}

Avec la version Beta des caractéristiques actuelle, gardez à l’esprit les restrictions suivantes :

- Vous pouvez créer **maximum** 1 000 caractéristiques
- La requête **maximum** par seconde (tr/s) est de 1 500 tr/s

## Création d’une caractéristique {#create}

>[!NOTE]
>
>Les contraintes suivantes s’appliquent lors de la création d’une caractéristique :
>
>- Vous pouvez uniquement créer une caractéristique à partir d’un jeu de données **activé pour les caractéristiques**
>- La caractéristique **doit** doit être créée avant l’ingestion de données, car les caractéristiques ne stockeront les données qu’une fois la caractéristique créée
>- Actuellement, les caractéristiques ne prennent en charge que la **logique booléenne**
>- Les caractéristiques sont évaluées par événement

Pour créer une caractéristique, accédez à la section **[!UICONTROL Profiles]** et sélectionnez **[!UICONTROL Traits]**.

![Le bouton Caractéristiques est mis en surbrillance.](/help/profile/images/traits/access-traits.png)

La page de navigation des caractéristiques s’affiche. Avant de pouvoir créer une caractéristique, vous devez activer les jeux de données à utiliser avec les caractéristiques en sélectionnant **[!UICONTROL Enable dataset for traits]**.

![Le bouton Activer le jeu de données pour les caractéristiques est mis en surbrillance.](/help/profile/images/traits/select-enable.png)

>[!IMPORTANT]
>
>L’activation d’un jeu de données pour les caractéristiques est un **processus irréversible**. Si vous activez un jeu de données pour les caractéristiques, il ne peut pas être activé pour le profil.
>
>Pour activer un jeu de données pour les caractéristiques, le jeu de données **doit** satisfaire aux conditions suivantes :
>
>- Le jeu de données **doit** être pour les événements d’expérience
>- Le jeu de données **ne doit** contenir aucune donnée déjà ingérée
>- Le jeu de données **doit** être activé pour Profil

La fenêtre contextuelle **[!UICONTROL Enable dataset for traits]** s’affiche. Une liste de tous vos jeux de données s’affiche. Sélectionnez les jeux de données que vous souhaitez activer pour les caractéristiques, puis **[!UICONTROL Continue]**.

>[!NOTE]
>
>Pour sélectionner Continuer, vous **devez** accepter que vous comprenez que l’activation d’un jeu de données pour les caractéristiques est irréversible.

![La fenêtre contextuelle Activer le jeu de données pour les caractéristiques s’affiche. Le bouton Continuer est mis en surbrillance.](/help/profile/images/traits/enable-traits-popover.png)

Maintenant que vous disposez d’un jeu de données compatible avec les caractéristiques, vous pouvez créer votre caractéristique. Sélectionnez **[!UICONTROL Create trait]** pour afficher le créateur de caractéristiques.

![&#x200B; La fenêtre contextuelle Jeu de données activé pour les caractéristiques s’affiche. Le bouton Créer une caractéristique est mis en surbrillance.](/help/profile/images/traits/select-create-trait.png)

Dans le créateur de caractéristiques, vous pouvez créer la caractéristique et en définir les détails. Pour créer une caractéristique, choisissez un événement dans la barre de navigation de gauche et ajoutez-le à la zone de travail.

![Le créateur de caractéristiques s’affiche.](/help/profile/images/traits/trait-builder.png)

Après avoir ajouté vos événements, vous pouvez ajouter les détails de la caractéristique.

| Champ | Description |
| ----- | ----------- |
| Nom d’affichage | Nom d’affichage de la caractéristique. |
| Nom du champ | Nom du champ pour la caractéristique. Ce nom est généré automatiquement à partir du nom d’affichage. |
| Jeu de données | Jeu de données auquel appartient la caractéristique. Cela a déjà été choisi lors de la création de la caractéristique. |
| Description | Description de la caractéristique. |
| Expiration des données | Expiration des données de la caractéristique. Cela détermine la durée pendant laquelle les données de la caractéristique sont actives. Cette valeur peut être définie sur un maximum de 120 jours. Par défaut, cette valeur est définie sur 1 jour. |

Une fois que les détails de la caractéristique sont définis, vous pouvez **[!UICONTROL Save as draft]** ou **[!UICONTROL Publish]** la caractéristique. Pour utiliser votre caractéristique dans une audience, vous **devez** la publier.

>[!NOTE]
>
>Une fois votre caractéristique publiée, le stockage et le traitement des données peuvent prendre jusqu’à 24 heures. De plus, vous **ne pourrez pas** modifier votre caractéristique une fois qu’elle sera publiée.

## Utilisation des caractéristiques {#using}

>[!IMPORTANT]
>
>Vous pouvez **uniquement** utiliser des caractéristiques dans les audiences évaluées à l’aide de la segmentation par lots ou de la segmentation Edge. La segmentation en flux continu n’est **pas** prise en charge pour le moment.

Une fois votre caractéristique créée, vous pouvez l’utiliser dans vos définitions d’audience. Pour ouvrir le créateur de segments, sélectionnez **[!UICONTROL Audiences]**, puis **[!UICONTROL Create audience]**, **[!UICONTROL Build rule]** et **[!UICONTROL Create]**.

![Le chemin d’accès au Créateur d’audience s’affiche et est mis en surbrillance.](/help/profile/images/traits/create-audience.png)

Le créateur de segments s’affiche. Dans le créateur de segments, vous pouvez voir toutes les caractéristiques publiées qui appartiennent à votre sandbox.

![L’onglet Caractéristiques s’affiche dans le Créateur d’audience, affichant toutes les caractéristiques que vous pouvez utiliser lors de la création de l’audience.](/help/profile/images/traits/traits-in-audience-builder.png)

Après avoir ajouté les caractéristiques à la zone de travail de création des règles, vous pouvez choisir de créer une audience qui **inclut** ou **exclut** la caractéristique ajoutée. Vous pouvez éventuellement sélectionner **[!UICONTROL Recency]** pour vérifier si la condition de caractéristique a été remplie dans la période spécifiée.

![Les options disponibles dans les caractéristiques dans le Créateur d’audience s’affichent.](/help/profile/images/traits/trait-attribute.png)

## Gestion des caractéristiques {#manage}

Vous pouvez surveiller et gérer vos caractéristiques par le biais de diverses interfaces.

Dans la vue Liste **[!UICONTROL Traits]**, vous pouvez voir toutes les caractéristiques créées dans le sandbox, ainsi qu’un aperçu de toutes les définitions des caractéristiques.

![La page Parcourir les caractéristiques s’affiche, affichant les caractéristiques disponibles pour le sandbox.](/help/profile/images/traits/browse-traits.png)

| Champ | Description |
| ----- | ----------- |
| Nom | Nom de la caractéristique. |
| Description | Description de la caractéristique. |
| Jeu de données | Jeu de données auquel appartient la caractéristique. |
| Créé par | Nom d’utilisateur de la personne qui a créé la caractéristique. |
| Expiration des données | Valeur d’expiration des données pour la caractéristique. Cela détermine la durée pendant laquelle les données de la caractéristique sont actives. |
| Statut du cycle de vie | Statut de la caractéristique. Les valeurs possibles sont **[!UICONTROL Invalid]**, **[!UICONTROL Pending]** et **[!UICONTROL Published]**. |
| Dernière mise à jour | Date et heure de la dernière mise à jour de la caractéristique. |
| Created | Date et heure de création de la caractéristique. |

Vous pouvez également sélectionner les points de suspension (...) à côté de la caractéristique pour d’autres options, y compris la création d’une audience à l’aide de la caractéristique sélectionnée, la désactivation de la caractéristique et la suppression de la caractéristique.

Vous pouvez afficher plus de détails en sélectionnant le nom de la caractéristique. La page de détails des caractéristiques s’affiche. Cette page affiche des informations, notamment le résumé de la caractéristique, les profils qualifiés au fil du temps et les audiences avec cette caractéristique.

![La page de détails des caractéristiques s’affiche, affichant les informations disponibles sur la caractéristique.](/help/profile/images/traits/traits-details.png)

<!-- In the **audience details** page, you can see all the traits that were used within that audience. -->

<!-- IMAGE -->

<!-- In the **dataset details** page, you can see all the traits that were created from that dataset. -->

<!-- IMAGE -->

