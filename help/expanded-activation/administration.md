---
title: Administration étendue des comptes d’activation
description: Découvrez comment effectuer des tâches administratives sur votre compte d’activation étendue, comme surveiller l’utilisation des licences et attribuer les autorisations appropriées.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Administration de comptes

Pour ingérer des audiences à partir de l’Audience Manager et les activer vers des destinations sociales et publicitaires, vous devez d’abord créer un compte utilisateur d’activation étendue et affecter le compte au rôle d’autorisation approprié.

Cette page explique comment créer un compte utilisateur dans le Admin Console et attribuer les autorisations appropriées pour l’activation étendue.

## Création de comptes d’utilisateur {#create-users}

Avant d’utiliser [!DNL Audience Manager Expanded Activation], vous devez créer un compte utilisateur.

Pour créer un compte utilisateur pour [!DNL Expanded Activation], suivez les instructions de gestion des utilisateurs à partir de la fonction [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-users-individually.html) la documentation.

## Ajout d’utilisateurs au rôle d’autorisation {#permissions}

Après avoir créé un compte utilisateur, vous devez l’ajouter à la variable [!DNL Expanded Activation] rôle d’autorisation, dans [!DNL Expanded Activation] de l’interface utilisateur.

Accédez à **[!UICONTROL Administration]** -> **[!UICONTROL Autorisations]** -> **[!UICONTROL Rôles]**, puis sélectionnez la variable **[!UICONTROL Rôle par défaut de l’activation étendue]**.

![Image développée de l’interface utilisateur Activation affichant la page Rôles.](assets/expanded-activation-role.png)

Accédez au **[!UICONTROL Utilisateurs]** et sélectionnez **[!UICONTROL Ajout d’utilisateurs]**.

![Image développée de l’interface utilisateur Activation affichant la page Utilisateurs.](assets/add-users.png)

Sélectionnez l’utilisateur nouvellement créé dans la liste disponible, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Image développée de l’interface utilisateur Activation affichant la page Ajouter des utilisateurs .](assets/add-user.png)

Le compte utilisateur est maintenant créé et affecté au rôle approprié. Il est maintenant prêt à accéder au **[!UICONTROL Activation étendue]** de l’interface utilisateur.

## Surveiller l’utilisation des licences {#license-usage}

Votre [!DNL Audience Manager Expanded Activation] Contrat indique le nombre maximal de courriers électroniques hachés que vous pouvez ingérer dans votre compte.

Vous pouvez trouver ces informations en vous rendant dans le **[!UICONTROL Administration]** -> **[!UICONTROL Utilisation de la licence]** page.

![Image développée de l’interface utilisateur Activation affichant l’écran d’utilisation des licences.](assets/license-usage.png)

Sur cette page, vous trouverez les informations suivantes :

* **[!UICONTROL Produit]**: le produit Adobe pour lequel vous disposez d’une licence. Cette variable sera toujours **[!UICONTROL Audience Manager d’activation étendue]**.
* **[!UICONTROL Mesure Principal]**: nom de la mesure suivie pour utilisation. Cette variable sera toujours **[!UICONTROL Audience adressable]**.
* **[!UICONTROL Montant de la licence]**: nombre maximal de courriers électroniques hachés que vous êtes autorisé à ingérer.

  >[!TIP]
  >
  >Vous ingérez des courriers électroniques hachés via [Connecteur source d’Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Consultez la documentation relative à [activation d’audiences](activate-audiences.md) pour plus d’informations.

* **[!UICONTROL Utilisation]**: nombre de courriers électroniques hachés que vous avez ingérés.
* **[!UICONTROL Utilisation %]**: pourcentage du montant de votre licence que vous avez utilisé.

Pour en savoir plus sur l’utilisation des licences dans Experience Platform, voir [documentation sur l’utilisation des licences](../dashboards/guides/license-usage.md).

## Étapes suivantes {#next-steps}

Maintenant que vous avez configuré au moins un compte utilisateur avec l’accès correct à l’activation étendue, vous pouvez commencer à utiliser le compte pour [activation des audiences](activate-audiences.md).
