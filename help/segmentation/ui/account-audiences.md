---
title: Audiences du compte
description: Découvrez comment créer et utiliser des audiences de compte pour cibler des profils de compte dans des destinations en aval.
badgeLimitedAvailability: label="Disponibilité limitée" type="Caution"
badgeB2B: label="Édition B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 5%

---

# Audiences du compte

>[!AVAILABILITY]
>
>Les audiences de compte ne sont disponibles que dans la variable [Édition B2B de Real-time Customer Data Platform](../../rtcdp/b2b-overview.md). En outre, la fonctionnalité d’audience de compte figure actuellement dans **disponibilité limitée**. Contactez le service à la clientèle d’Adobe ou votre représentant d’Adobe pour demander l’accès à cette fonctionnalité.

Grâce à la segmentation des comptes, Adobe Experience Platform vous permet d’offrir une expérience de segmentation marketing simplifiée et conviviale, allant des audiences basées sur les personnes aux audiences basées sur les comptes.

Les audiences de compte peuvent être utilisées comme entrée pour les destinations basées sur un compte, ce qui vous permet de cibler les personnes contenues dans ces comptes dans les services en aval. Par exemple, vous pouvez utiliser des audiences basées sur un compte pour récupérer les enregistrements de tous les comptes qui le font. **not** avoir des coordonnées avec le titre de chef des opérations ou de directeur du marketing.

## Terminologie {#terminology}

Avant de commencer à utiliser les audiences de compte, veuillez examiner les différences entre les différents types d’audience :

- **Audiences du compte**: une audience de compte est une audience créée à l’aide de **account** données de profil. Les données de profil de compte peuvent être utilisées pour créer des audiences qui ciblent les personnes dans les comptes en aval. Pour plus d’informations sur les profils de compte, veuillez lire la section [présentation du profil de compte](../../rtcdp/accounts/account-profile-overview.md).
- **Audiences de personnes**: une audience de type personne est une audience créée à l’aide de **client** données de profil. Les données de profil client peuvent être utilisées pour créer des audiences qui ciblent la clientèle de votre entreprise. Pour plus d’informations sur les profils client, veuillez lire la section [Présentation de Real-Time Customer Profile](../../profile/home.md).
- **Public potentiel**: une audience de prospect est une audience créée à l’aide de **prospect** données de profil. Les données de profil de prospects peuvent être utilisées pour créer des audiences à partir d’utilisateurs non authentifiés. Pour plus d’informations sur les profils de prospect, veuillez lire la section [présentation du profil de prospect](../../profile/ui/prospect-profile.md).

## Accéder à {#access}

Pour accéder aux audiences du compte, sélectionnez **[!UICONTROL Audiences]** dans le **[!UICONTROL Comptes]** .

![Le bouton Audiences est mis en surbrillance dans la section Comptes .](../images/ui/account-audiences/select.png)

La variable [!UICONTROL Parcourir] s’affiche, avec la liste de toutes les audiences de compte pour l’organisation.

![Les audiences du compte appartenant à l’organisation s’affichent.](../images/ui/account-audiences/browse.png)

Cette vue répertorie des informations sur l’audience, notamment le nom, le nombre de profils, l’origine, l’état du cycle de vie, la date de création et la date de dernière mise à jour.

## Créer une audience {#create}

Pour créer une audience de compte, sélectionnez **[!UICONTROL Créer une audience]** sur le [!UICONTROL Parcourir] page.

![La variable [!UICONTROL Créer une audience] est mis en surbrillance sur la page de navigation de l’audience du compte.](../images/ui/account-audiences/select-create-audience.png)

Le créateur de segments s’affiche. Les attributs de compte s’affichent dans la barre de navigation de gauche.

![Le créateur de segments s’affiche. Notez que seuls les attributs sont affichés.](../images/ui/account-audiences/segment-builder.png)

Lors de la création d’audiences de compte, notez que les événements sont répertoriés sous **[!UICONTROL Personnes]**, plutôt que d’être leur propre onglet, car ces attributs sont associés à des personnes.

![L’emplacement où trouver les événements, qui se trouve dans la variable [!UICONTROL Personnes] , est mis en surbrillance.](../images/ui/account-audiences/attributes.png)

Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [Guide de l’interface utilisateur du créateur de segments](./segment-builder.md).

## Activer l’audience {#activate}

>[!NOTE]
>
>Seul un nombre limité de destinations prennent en charge les audiences du compte. Assurez-vous que la destination que vous souhaitez activer prend en charge les audiences de compte avant de poursuivre ce processus.

Après avoir créé l’audience de votre compte, vous pouvez activer l’audience vers d’autres services en aval.

Sélectionnez l’audience que vous souhaitez activer, suivie de **[!UICONTROL Activer la destination]**.

![La variable [!UICONTROL Activer la destination] est mis en surbrillance dans le menu actions rapides de l’audience sélectionnée.](../images/ui/account-audiences/activate.png)

La variable [!UICONTROL Activer la destination] s’affiche. Pour plus d’informations sur le processus d’activation, y compris les destinations prises en charge et les détails sur les mappages de champs, veuillez lire le [activation des audiences de compte](/help/destinations/ui/activate-account-audiences.md) tutoriel .

## Étapes suivantes {#next-steps}

Après avoir lu ce guide, vous comprenez mieux comment créer et utiliser les audiences de votre compte dans Adobe Experience Platform. Pour savoir comment utiliser d’autres types d’audiences dans Platform, veuillez lire le [Guide de l’interface utilisateur de Segmentation Service](./overview.md).
