---
title: Administration étendue des comptes d’activation
description: Découvrez comment effectuer des tâches administratives sur votre compte d’activation étendue, comme surveiller l’utilisation des licences et attribuer les autorisations appropriées.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Administration de comptes

Pour ingérer des audiences à partir de l’Audience Manager et les activer vers des destinations sociales et publicitaires, vous devez d’abord créer un compte utilisateur d’activation étendue et affecter le compte au rôle d’autorisation approprié.

Cette page explique comment créer un compte utilisateur dans l’Admin Console et attribuer les autorisations appropriées pour l’activation étendue.

## Création de comptes d’utilisateur {#create-users}

Avant de pouvoir utiliser [!DNL Audience Manager Expanded Activation], vous devez créer un compte utilisateur.

Pour créer un compte utilisateur pour [!DNL Expanded Activation], suivez les instructions de gestion des utilisateurs de la documentation [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-users-individually.html).

## Ajout d’utilisateurs au rôle d’autorisation {#permissions}

Après avoir créé un compte utilisateur, vous devez l’ajouter au rôle d’autorisation [!DNL Expanded Activation] dans l’interface utilisateur de [!DNL Expanded Activation].

Accédez à **[!UICONTROL Administration]** -> **[!UICONTROL Autorisations]** -> **[!UICONTROL Rôles]**, puis sélectionnez le **[!UICONTROL rôle par défaut d’activation étendu]**.

![Image de l’interface utilisateur de l’activation étendue affichant la page Rôles.](assets/expanded-activation-role.png)

Accédez à l’onglet **[!UICONTROL Users]** et sélectionnez **[!UICONTROL Add Users]**.

![Image de l’interface utilisateur de l’activation étendue montrant la page Utilisateurs.](assets/add-users.png)

Sélectionnez l’utilisateur nouvellement créé dans la liste disponible et sélectionnez **[!UICONTROL Enregistrer]**.

![Image de l’interface utilisateur de l’activation étendue montrant la page Ajouter des utilisateurs.](assets/add-user.png)

Le compte utilisateur est maintenant créé et affecté au rôle approprié. Il est maintenant prêt à accéder à l’interface utilisateur **[!UICONTROL Activation étendue]**.

## Surveiller l’utilisation des licences {#license-usage}

Votre contrat [!DNL Audience Manager Expanded Activation] spécifie le nombre maximal de courriers électroniques hachés que vous pouvez ingérer pour votre compte.

Vous pouvez trouver ces informations en vous rendant sur la page **[!UICONTROL Administration]** -> **[!UICONTROL Utilisation de la licence]** .

![Image de l’interface utilisateur de l’activation étendue montrant l’écran d’utilisation de la licence.](assets/license-usage.png)

Sur cette page, vous trouverez les informations suivantes :

* **[!UICONTROL Product]** : Adobe de produit pour lequel vous disposez d’une licence. Il s’agira toujours de l’ **[!UICONTROL Audience Manager de l’activation étendue]**.
* **[!UICONTROL Mesure de Principal]** : nom de la mesure suivie pour utilisation. Il s’agira toujours de **[!UICONTROL audience adressable]**.
* **[!UICONTROL Montant de la licence]** : nombre maximal de courriers électroniques hachés que vous êtes autorisé à ingérer.

  >[!TIP]
  >
  >Vous ingérez des emails hachés via le [connecteur source d&#39;Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations, consultez la documentation sur [l’activation des audiences](activate-audiences.md) .

* **[!UICONTROL Utilisation]** : nombre de courriers électroniques hachés que vous avez ingérés.
* **[!UICONTROL Utilisation %]** : pourcentage du montant de votre licence que vous avez utilisé.

Pour en savoir plus sur l’utilisation des licences en Experience Platform, consultez la [documentation sur l’utilisation des licences](../dashboards/guides/license-usage.md).

## Étapes suivantes {#next-steps}

Maintenant que vous avez configuré au moins un compte utilisateur avec l’accès correct à l’activation étendue, vous pouvez commencer à utiliser le compte pour [activer les audiences](activate-audiences.md).
