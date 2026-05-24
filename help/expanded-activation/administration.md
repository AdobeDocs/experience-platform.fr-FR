---
title: Administration du compte d’activation développée
description: Découvrez comment effectuer des tâches administratives sur votre compte d’activation étendue, comme surveiller l’utilisation des licences et attribuer les autorisations appropriées.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
TQID: https://experienceleague.adobe.com/UdI5T0riJi695ZM3d3ymVEDTSFFmPgx46q6Dgjy4PJQ
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: adf04a6a-050f-44bc-a52c-db79ccb22ebf
subfeature_v2: id: a9b953c0-98db-499b-97f5-a0dc3290bda3id: a9eb38d5-9d89-492f-af4e-b968a07f2d91id: d175cb4c-5781-454e-a826-bf6dff786265
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 379
ht-degree: 4%

---

# Administration des comptes

Pour ingérer des audiences d’Audience Manager et les activer vers des destinations publicitaires et sociales, vous devez d’abord créer un compte utilisateur d’activation étendu et affecter le compte au rôle d’autorisation approprié.

Cette page explique comment créer un compte utilisateur dans Admin Console et transmettre les autorisations appropriées pour l’activation étendue.

## Création de comptes utilisateur {#create-users}

Avant de pouvoir utiliser [!DNL Audience Manager Expanded Activation], vous devez créer un compte utilisateur.

Pour créer un compte d’utilisateur pour [!DNL Expanded Activation], suivez les instructions de la section Gestion des utilisateurs de la documentation de [Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/manage-users-individually.html).

## Ajouter des utilisateurs au rôle d’autorisation {#permissions}

Après avoir créé un compte utilisateur, vous devez l’ajouter au rôle d’autorisation [!DNL Expanded Activation], dans l’interface utilisateur [!DNL Expanded Activation].

Accédez à **[!UICONTROL Administration]** -> **[!UICONTROL Permissions]** -> **[!UICONTROL Roles]**, puis sélectionnez le **[!UICONTROL Expanded Activation Default Role]**.

![Image développée de l’interface utilisateur d’activation montrant la page Rôles.](assets/expanded-activation-role.png)

Accédez à l’onglet **[!UICONTROL Users]** et sélectionnez **[!UICONTROL Add Users]**.

![Image développée de l’interface utilisateur d’activation montrant la page Utilisateurs.](assets/add-users.png)

Sélectionnez l’utilisateur nouvellement créé dans la liste disponible, puis sélectionnez **[!UICONTROL Save]**.

![Image développée de l’interface utilisateur d’activation montrant la page Ajouter des utilisateurs.](assets/add-user.png)

Le compte utilisateur est maintenant créé et affecté au rôle approprié. Il est maintenant prêt à accéder à l’interface utilisateur **[!UICONTROL Expanded Activation]**.

## Surveillance de l’utilisation des licences {#license-usage}

Votre contrat [!DNL Audience Manager Expanded Activation] spécifie le nombre maximal d’e-mails hachés que vous pouvez ingérer sur votre compte.

Vous trouverez ces informations en accédant à la page **[!UICONTROL Administration]** -> **[!UICONTROL License Usage]** .

![Image développée de l’interface utilisateur d’activation affichant l’écran d’utilisation de la licence.](assets/license-usage.png)

Sur cette page, vous trouverez les informations suivantes :

* **[!UICONTROL Product]** : produit Adobe pour lequel vous possédez une licence. Il s’agit toujours de **[!UICONTROL Audience Manager Expanded Activation]**.
* **[!UICONTROL Primary metric]** : nom de la mesure faisant l’objet d’un suivi pour utilisation. Il s’agit toujours de **[!UICONTROL Addressable audience]**.
* **[!UICONTROL License amount]** : nombre maximal d’e-mails hachés que vous êtes autorisé à ingérer.

  >[!TIP]
  >
  >Vous ingérez des e-mails hachés via le connecteur source [](../sources/connectors/adobe-applications/audience-manager.md). Pour plus d’informations, consultez la documentation sur [comment activer des audiences](activate-audiences.md).

* **[!UICONTROL Usage]** : nombre d’e-mails hachés que vous avez ingérés.
* **[!UICONTROL Usage %]** : pourcentage du montant de votre licence que vous avez utilisé.

Pour en savoir plus sur l’utilisation des licences dans Experience Platform, consultez la [documentation sur l’utilisation des licences](../dashboards/guides/license-usage.md).

## Étapes suivantes {#next-steps}

Maintenant que vous avez configuré au moins un compte utilisateur avec l’accès approprié à l’activation étendue, vous pouvez commencer à utiliser le compte pour [activer des audiences](activate-audiences.md).
