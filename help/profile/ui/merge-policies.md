---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide d’utilisation des stratégies de fusion
topic: guide
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 84%

---


# Guide d’utilisation des stratégies de fusion

Adobe Experience Platform permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view.

À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Ce guide fournit des instructions détaillées sur l’utilisation des stratégies de fusion à l’aide de l’interface utilisateur d’Adobe Experience Platform.

If you would prefer to work with merge policies using the [!DNL Real-time Customer Profile] API, please follow the instructions outlined in the [merge policies API tutorial](../api/merge-policies.md).

## Prise en main

This guide requires a working understanding of the various [!DNL Experience Platform] services involved with merge policies. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

* [!DNL Real-time Customer Profile](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [!DNL Identity Service](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et qui sont incorporées [!DNL Platform]dans.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.

## Affichage des stratégies de fusion

Within the [!DNL Experience Platform] user interface, you can begin to work with merge policies and see a list of your organization&#39;s existing merge policies by clicking **[!UICONTROL Profile]** in the left-rail and then selecting the **[!UICONTROL Merge policies]** tab.

![Page d’entrée des stratégies de fusion](../images/merge-policies/landing.png)

Les détails de chaque stratégie de fusion disponibles pour votre organisation sont visibles sur la page d’entrée, notamment le *[!UICONTROL nom de la stratégie]*, la *[!UICONTROL stratégie de fusion par défaut]*, et le *[!UICONTROL schéma]*.

Pour sélectionner les détails visibles ou ajouter des colonnes supplémentaires à l’affichage, sélectionnez l’icône de sélection des colonnes sur la droite et cliquez sur le nom d’une colonne pour l’ajouter ou la supprimer de l’affichage.

![](../images/merge-policies/adjust-view.png)

## Création d’une stratégie de fusion

Pour créer une nouvelle stratégie de fusion, cliquez sur **[!UICONTROL Créer une stratégie de fusion]** près du coin supérieur droit de l’onglet **[!UICONTROL Stratégies de fusion]**.

![Page d’entrée des stratégies de fusion](../images/merge-policies/create-new.png)

L’écran **[!UICONTROL Créer une stratégie de fusion]** apparaît et vous permet de fournir des informations importantes pour votre nouvelle stratégie de fusion.

![](../images/merge-policies/create.png)

* **[!UICONTROL Nom]** : le nom de votre stratégie de fusion devrait être descriptif, mais concis.
* **[!UICONTROL Schéma]** : le schéma associé à la stratégie de fusion. Ceci spécifie le schéma XDM pour lequel cette stratégie de fusion est créée. Les organisations peuvent créer plusieurs stratégies de fusion par schéma.
* **[!UICONTROL Combinaison d’identités]** : ce champ définit la manière de déterminer les identités liées d’un client. Deux valeurs sont possibles :
   * **[!UICONTROL Aucun]** : ne réalise pas de combinaison d’identités.
   * **[!UICONTROL Graphique privé]** : réalise des combinaisons d’identités basées sur votre graphique d’identités privé.
* **[!UICONTROL Fusion d’attributs]** : un fragment de profil correspond aux informations de profil d’une seule identité de la liste d’identités qui existe pour un client individuel. Lorsque le type de graphique d’identités utilisé génère plusieurs identités, il existe un risque de conflit des valeurs de propriété du profil et un ordre de priorité doit être établi. L’utilisation de la *fusion d’attributs* vous permet de préciser les valeurs de profil du jeu de données à prioriser en cas de conflit de fusion. Deux valeurs sont possibles :
   * **[!UICONTROL Classé par date et heure]** : en cas de conflit, vous donnez la priorité au profil mis à jour le plus récemment.
   * **[!UICONTROL Priorité du jeu de données]** : donne la priorité aux fragments de profil en fonction de leur jeu de données d’origine. Lorsque vous sélectionnez cette option, vous devez sélectionner les jeux de données associés et leur ordre de priorité. Consultez les détails de la [priorité du jeu de données](#dataset-precedence) ci-dessous pour plus d’informations.
* **[!UICONTROL Stratégie de fusion par défaut]** : un bouton de basculement qui vous permet de sélectionner cette stratégie de fusion ou non comme stratégie par défaut pour votre organisation. Si le sélecteur est activé et que la nouvelle stratégie est enregistrée, votre stratégie précédente par défaut est mise à jour automatiquement et n’est plus la stratégie par défaut.

### Priorité du jeu de données {#dataset-precedence}

Lors de la sélection d’une valeur de *[!UICONTROL fusion d’attributs]*, vous pouvez sélectionner la *[!UICONTROL priorité du jeu de données]*, ce qui vous permettra de prioriser des fragments de profil en fonction du jeu de données dont ils proviennent.

Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Lorsque vous sélectionnez une *[!UICONTROL priorité de jeu de données]*, un panneau séparé s’ouvre vous demandant de sélectionner parmi les *[!UICONTROL jeux de données disponibles]* (vous pouvez également utiliser la case à cocher pour tous les sélectionner) les jeux de données qui seront inclus. Vous pouvez ensuite faire glisser et déposer ces jeux de données dans le panneau *[!UICONTROL Jeux de données sélectionnés]* et les faire glisser dans l’ordre de priorité correct. Le jeu de données supérieur se verra accorder la priorité la plus élevée, puis le deuxième jeu de données sera placé en deuxième position et ainsi de suite.

![](../images/merge-policies/dataset-precedence.png)

Lorsque vous avez terminé de créer la stratégie de fusion, cliquez sur **[!UICONTROL Enregistrer]** pour revenir à l’onglet *[!UICONTROL Stratégies de fusion]* où votre nouvelle stratégie de fusion apparaît désormais dans la liste de stratégies.

## Modification d’une stratégie de fusion

Vous pouvez modifier une stratégie de fusion existante depuis l’onglet *[!UICONTROL Stratégies de fusion]* en cliquant sur le *[!UICONTROL Nom de la stratégie]* de la stratégie de fusion que vous souhaitez modifier.

![Page d’entrée des stratégies de fusion](../images/merge-policies/select-edit.png)

Lorsque l’écran *[!UICONTROL Modifier la stratégie de fusion]* apparaît, vous pouvez apporter des modifications au *[!UICONTROL nom]*, au *[!UICONTROL schéma]*, au type de *[!UICONTROL combinaison d’identités]* et au type de *[!UICONTROL fusion d’attributs]* ainsi que sélectionner cette stratégie ou non comme *[!UICONTROL Stratégie de fusion par défaut]* pour votre organisation.

>[!NOTE]
>
>Vous ne pouvez pas modifier l’identifiant de stratégie de fusion qui apparaît en haut de l’écran de modification. Il s’agit d’un identifiant en lecture seule généré par le système qui ne peut pas être modifié.

![](../images/merge-policies/edit-screen.png)

Lorsque vous avez apporté les modifications nécessaires, cliquez sur **[!UICONTROL Enregistrer]** pour revenir à l’onglet *[!UICONTROL Stratégies de fusion]* dans lequel les informations de la stratégie de fusion mise à jour seront désormais disponibles.

![](../images/merge-policies/edited.png)

## Violations de la politique de gouvernance des données

Lors de la création ou de la mise à jour d’une stratégie de fusion, une vérification est effectuée pour déterminer si la politique de fusion enfreint l’une des stratégies en matière d’utilisation des données définies par votre organisation. Data usage policies are part of Adobe Experience Platform [!DNL Data Governance] and are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on specific [!DNL Platform] data. Par exemple, si vous avez utilisé une stratégie de fusion pour créer un segment activé dans une destination tierce et que votre organisation dispose d’une stratégie d’utilisation des données empêchant l’exportation de données spécifiques à des tiers, vous recevrez une notification « Violations de la politique de gouvernance des données détectée » lorsque vous tenterez d’enregistrer votre stratégie de fusion.

Cette notification inclut une liste des stratégies d’utilisation des données ayant été enfreintes et vous permet de consulter les détails de la violation en sélectionnant une stratégie depuis la liste. Si vous avez sélectionné une stratégie ayant fait l’objet d’une infraction, l’onglet *Liaison des données* fournit un *motif de violation* et les *activations concernées*, chacun fournissant plus de détails sur la manière dont la stratégie d’utilisation des données a été enfreinte.

Pour en savoir plus sur la manière dont la gouvernance des données est réalisée au sein d’Adobe Experience Platform, veuillez commencer par lire la [présentation de la gouvernance des données](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Étapes suivantes

Maintenant que vous avez créé et configuré les stratégies de fusion pour votre organisation IMS, vous pouvez les utiliser pour créer des segments d’audience à partir des données de votre profil. See the [Segmentation overview](../../segmentation/home.md) for more information on how to create and work with segments using [!DNL Experience Platform].