---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide d’utilisation des stratégies de fusion
topic: guide
translation-type: tm+mt
source-git-commit: 98be95e0a6e0661dcddf2db1cf6993b643d4df2b
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 45%

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

Within the [!DNL Experience Platform] user interface, you can begin to work with merge policies and see a list of your organization&#39;s existing merge policies by selecting **[!UICONTROL Profiles]** in the left-rail and then selecting the **[!UICONTROL Merge policies]** tab.

![Page d’entrée des stratégies de fusion](../images/merge-policies/landing.png)

Details for each merge policy available to your organization are visible on the landing page, including the [!UICONTROL Policy Name], [!UICONTROL Default merge policy], and [!UICONTROL Schema].

Pour sélectionner les détails visibles ou ajouter d&#39;autres colonnes à l&#39;affichage, sélectionnez l&#39;icône du sélecteur de colonnes et cliquez sur le nom d&#39;une colonne pour l&#39;ajouter ou la supprimer de la vue.

![](../images/merge-policies/adjust-view.png)

## Création d’une stratégie de fusion

Pour créer une stratégie de fusion, sélectionnez **[!UICONTROL Créer une stratégie]** de fusion.

![Page d’entrée des stratégies de fusion](../images/merge-policies/create-new.png)

L’écran **[!UICONTROL Créer une stratégie de fusion]** apparaît et vous permet de fournir des informations importantes pour votre nouvelle stratégie de fusion.

![](../images/merge-policies/create.png)

* **[!UICONTROL Nom]** : le nom de votre stratégie de fusion devrait être descriptif, mais concis.
* **[!UICONTROL Schéma]** : le schéma associé à la stratégie de fusion. Ceci spécifie le schéma XDM pour lequel cette stratégie de fusion est créée. Les organisations peuvent créer plusieurs stratégies de fusion par schéma.
* **[!UICONTROL Combinaison d’identités]** : ce champ définit la manière de déterminer les identités liées d’un client. Deux valeurs sont possibles :
   * **[!UICONTROL Aucun]** : ne réalise pas de combinaison d’identités.
   * **[!UICONTROL Graphique privé]** : réalise des combinaisons d’identités basées sur votre graphique d’identités privé.
* **[!UICONTROL Fusion d’attributs]** : un fragment de profil correspond aux informations de profil d’une seule identité de la liste d’identités qui existe pour un client individuel. Lorsque le type de graphique d&#39;identité utilisé génère plusieurs identités, il existe un risque de conflit d&#39;attributs de profil et la priorité doit être spécifiée. L’utilisation de la fusion  Attribut vous permet de spécifier les valeurs de profil de jeux de données à classer par priorité en cas de conflit de fusion entre des jeux de données de type Valeur clé (données d’enregistrement). Deux valeurs sont possibles :
   * **[!UICONTROL Classé par date et heure]** : en cas de conflit, vous donnez la priorité au profil mis à jour le plus récemment. [!UICONTROL L’horodatage ordonné] prend également en charge les horodatages personnalisés qui prennent la priorité sur les horodatages système lors de la fusion de données dans le même jeu de données (identités multiples) ou entre plusieurs jeux de données. Pour en savoir plus, reportez-vous à la section [horodatage ordonné](#timestamp-ordered) qui suit.
   * **[!UICONTROL Priorité du jeu de données]** : donne la priorité aux fragments de profil en fonction de leur jeu de données d’origine. Lorsque vous sélectionnez cette option, vous devez sélectionner les jeux de données associés et leur ordre de priorité. Consultez les détails de la [priorité du jeu de données](#dataset-precedence) ci-dessous pour plus d’informations.
* **[!UICONTROL Stratégie de fusion par défaut]** : un bouton de basculement qui vous permet de sélectionner cette stratégie de fusion ou non comme stratégie par défaut pour votre organisation. Si le sélecteur est activé et que la nouvelle stratégie est enregistrée, votre stratégie précédente par défaut est mise à jour automatiquement et n’est plus la stratégie par défaut.

### Horodatage trié {#timestamp-ordered}

Comme les enregistrements de Profil sont ingérés dans l&#39;Experience Platform, un horodatage système est obtenu au moment de l&#39;assimilation et ajouté à l&#39;enregistrement. Lorsque l’ [!UICONTROL horodatage ordonné] est sélectionné comme type de fusion  Attribut pour une stratégie de fusion, les profils sont fusionnés en fonction de l’horodatage système. En d’autres termes, la fusion est effectuée en fonction de l’horodatage du moment où l’enregistrement a été ingéré dans la plate-forme.

Il peut arriver, par exemple, que des données soient renvoyées ou que l’ordre des événements soit correct si les enregistrements sont ingérés dans l’ordre, lorsqu’il est nécessaire de fournir un horodatage personnalisé et que la stratégie de fusion respecte l’horodatage personnalisé plutôt que l’horodatage système.

>[!NOTE]
>
>Cette fonctionnalité n&#39;est disponible que pour l&#39;assimilation entre des jeux de données. Si les enregistrements sont ingérés à l’aide du même jeu de données, le comportement de remplacement par défaut se produit.

### Utilisation d’horodatages personnalisés {#custom-timestamps}

Pour utiliser un horodatage personnalisé, le mélange [!UICONTROL Détails de l&#39;audit du système] externe source doit être ajouté à votre schéma de Profil. Une fois ajouté, l’horodatage personnalisé peut être renseigné à l’aide du `lastUpdatedDate` champ.

Lorsqu&#39;un enregistrement est assimilé à un champ `lastUpdatedDate` rempli, l&#39;Experience Platform utilise ce champ pour fusionner des enregistrements dans des jeux de données. Si elle `lastUpdatedDate` n’est pas présente ou n’est pas renseignée, la plate-forme continuera à utiliser l’horodatage du système.

>[!NOTE]
>
>Vous devez vous assurer que l’ `lastUpdatedDate` horodatage est renseigné lors de l’importation d’une mise à jour sur le même enregistrement.

La capture d&#39;écran suivante affiche les champs du Mélange [!UICONTROL des détails de l&#39;audit du système source]externe. Pour obtenir des instructions détaillées sur l’utilisation des schémas à l’aide de l’interface utilisateur, y compris sur la façon d’ajouter des mixins aux schémas, consultez le [didacticiel de création d’un schéma à l’aide de l’interface utilisateur](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

Pour utiliser des horodatages personnalisés à l’aide de l’API, reportez-vous à l’Annexe du guide [des points de terminaison des stratégies de](../api/merge-policies.md) fusion, puis à la section relative à l’ [utilisation d’horodatages](../api/merge-policies.md#custom-timestamps)personnalisés.

### Priorité du jeu de données {#dataset-precedence}

Lors de la sélection d’une valeur de [!UICONTROL fusion d’attributs], vous pouvez sélectionner la [!UICONTROL priorité du jeu de données], ce qui vous permettra de prioriser des fragments de profil en fonction du jeu de données dont ils proviennent.

Par exemple, un cas d’utilisation serait la présence d’informations de votre organisation dans un jeu de données que vous préférez ou dont les données sont davantage de confiance par rapport à un autre jeu de données.

Lorsque vous sélectionnez une [!UICONTROL priorité de jeu de données], un panneau séparé s’ouvre vous demandant de sélectionner parmi les [!UICONTROL jeux de données disponibles] (vous pouvez également utiliser la case à cocher pour tous les sélectionner) les jeux de données qui seront inclus. Vous pouvez ensuite faire glisser et déposer ces jeux de données dans le panneau [!UICONTROL Jeux de données sélectionnés] et les faire glisser dans l’ordre de priorité correct. Le jeu de données supérieur se verra accorder la priorité la plus élevée, puis le deuxième jeu de données sera placé en deuxième position et ainsi de suite.

![](../images/merge-policies/dataset-precedence.png)

Once you have finished creating the merge policy, select **[!UICONTROL Save]** to return to the [!UICONTROL Merge policies] tab where your new merge policy now appears in the list of policies.

## Modification d’une stratégie de fusion

You can modify an existing merge policy through the [!UICONTROL Merge policies] tab by clicking on the [!UICONTROL Policy name]* for the merge policy you wish to edit.

![Page d’entrée des stratégies de fusion](../images/merge-policies/select-edit.png)

Lorsque l’écran [!UICONTROL Modifier la stratégie de fusion] apparaît, vous pouvez apporter des modifications au [!UICONTROL nom], au [!UICONTROL schéma], au type de [!UICONTROL combinaison d’identités] et au type de [!UICONTROL fusion d’attributs] ainsi que sélectionner cette stratégie ou non comme [!UICONTROL Stratégie de fusion par défaut] pour votre organisation.

>[!NOTE]
>
>Vous ne pouvez pas modifier l’identifiant de stratégie de fusion qui apparaît en haut de l’écran de modification. Il s’agit d’un identifiant en lecture seule généré par le système qui ne peut pas être modifié.

![](../images/merge-policies/edit-screen.png)

Once you have made the necessary changes, select **[!UICONTROL Save]** to return to the [!UICONTROL Merge policies] tab where the updated merge policy information is now visible.

![](../images/merge-policies/edited.png)

## Violations de la politique de gouvernance des données

Lors de la création ou de la mise à jour d’une stratégie de fusion, une vérification est effectuée pour déterminer si la politique de fusion enfreint l’une des stratégies en matière d’utilisation des données définies par votre organisation. Data usage policies are part of Adobe Experience Platform [!DNL Data Governance] and are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on specific [!DNL Platform] data. For example, if a merge policy was used to create a segment that activated to a third-party destination, and your organization had a data usage policy preventing the export of specific data to third parties, you would receive a &quot;[!UICONTROL Data governance policy violation detected]&quot; notification when attempting to save your merge policy.

Cette notification inclut une liste des stratégies d’utilisation des données ayant été enfreintes et vous permet de consulter les détails de la violation en sélectionnant une stratégie depuis la liste. Upon selecting a violated policy, the [!UICONTROL Data lineage] tab provides the reason for the violation and the [!UICONTROL Affected activations], each providing more detail into how the data usage policy has been violated.

Pour en savoir plus sur la manière dont la gouvernance des données est réalisée au sein d’Adobe Experience Platform, veuillez commencer par lire la [présentation de la gouvernance des données](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## Étapes suivantes

Maintenant que vous avez créé et configuré les stratégies de fusion pour votre organisation IMS, vous pouvez les utiliser pour créer des segments d’audience à partir des données de votre profil. See the [Segmentation overview](../../segmentation/home.md) for more information on how to create and work with segments using [!DNL Experience Platform].