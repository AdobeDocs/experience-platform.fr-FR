---
title: Connexion Demandbase
description: Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation d’Account-Based Marketing (ABM). Faites de la publicité auprès des personas et des rôles pertinents dans vos comptes cibles via Demand Side Platform (DSP) B2B de DemandBase. Les comptes cibles peuvent également être enrichis avec des données tierces DemandBase pour d’autres cas d’utilisation en aval dans le marketing et les ventes.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 08c2c7f5080f0e6afb7be53aad9f88ba0fccf923
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 40%

---

# Connexion Demandbase {#demandbase}

>[!AVAILABILITY]
>
>>La fonctionnalité d’activation des audiences de compte vers la destination Demandbase est disponible pour les sociétés qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Activez les profils de vos campagnes Demandbase pour le ciblage, la personnalisation et la suppression des audiences, en fonction des [audiences de compte](/help/segmentation/types/account-audiences.md) .

## Cas d’utilisation {#use-case}

Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation d’Account-Based Marketing (ABM). Faites de la publicité auprès des personas et des rôles pertinents dans vos comptes cibles via Demand Side Platform (DSP) B2B de DemandBase. Les comptes cibles peuvent également être enrichis avec des données tierces DemandBase pour d’autres cas d’utilisation en aval dans le marketing et les ventes.

Par exemple, utilisez le DSP ad-tech de Demandbase pour cibler des personnages ou des rôles spécifiques dans des comptes clés pour la génération de pistes au sommet de l’entonnoir, ou créez et développez des groupes d’achats. Utilisez la destination Demandbase pour explorer d&#39;autres cas d&#39;utilisation afin de cibler efficacement vos comptes.

Grâce à cette intégration, vous pouvez également personnaliser l’expérience du site web à l’aide de la recherche d’informations de compte en temps réel pour optimiser l’engagement.

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|--------------|-----------|---------------------------|
| Type d’exportation | Exportation d’audience | Tous les membres de l’audience seront exportés avec des identifiants clés tels que le nom, le numéro de téléphone, etc. |
| Fréquence | Diffusion en continu | Connexions basées sur l’API « Toujours actives ». Les mises à jour sont envoyées en aval immédiatement après les modifications de profil. |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour exporter les audiences de compte vers Demandbase, vous avez besoin des éléments suivants :

1. Un compte Demandbase.
2. Jeton API Demandbase. Vous pouvez générer un jeton API avec votre utilisateur dans Demandbase. Pour générer un jeton, accédez à [Mon profil > Jeton API](https://web.demandbase.com/o/ad/at) après vous être connecté à votre compte Demandbase.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Ajouter un jeton porteur](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Jeton porteur]** : renseignez le jeton porteur pour vous authentifier sur la destination. Consultez [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir le jeton.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Ajouter des informations sur la connexion de destination](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’entité]** : sélectionnez **[!UICONTROL Compte]** comme type d’entité.

Vous êtes maintenant prêt à activer vos audiences dans Demandbase.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des instructions sur l’activation des audiences de compte vers cette destination.

## Notes supplémentaires et légendes importantes {#additional-notes}

* Si une audience de compte portant le même nom a été activée précédemment sur Demandbase, vous ne pouvez pas la réactiver via un autre flux de données vers la destination Demandbase.
* Si vous avez exporté des audiences vers Demandbase et que les exportations ont réussi dans Experience Platform, mais que toutes les données n&#39;atteignent pas Demandbase, vous avez peut-être rencontré un ralentissement de l&#39;API du côté Demandbase. Contactez-les pour obtenir des éclaircissements.
