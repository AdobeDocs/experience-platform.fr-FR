---
title: Connexion Demandbase
description: Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation de Account-Based Marketing (ABM). Annoncez les rôles et les personnalités appropriés dans vos comptes cibles via le Demand Side Platform B2B de DemandBase (DSP). Les comptes Target peuvent également être enrichis avec des données tierces Demandbase, pour d’autres cas d’utilisation en aval dans le marketing et les ventes.
badgeB2B: label="Édition B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: 5c694dfab7e53cf8a78500e3ecd086a3986b9b91
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 26%

---


# Connexion Demandbase {#demandbase}

>[!AVAILABILITY]
>
>>La fonctionnalité d’activation des audiences de compte vers la destination Demandbase est disponible pour les entreprises qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Activez les profils de vos campagnes Demandbase pour le ciblage, la personnalisation et la suppression des audiences, en fonction des [audiences de compte](/help/segmentation/ui/account-audiences.md) .

## Cas d’utilisation {#use-case}

Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation de Account-Based Marketing (ABM). Annoncez les rôles et les personnalités appropriés dans vos comptes cibles via le Demand Side Platform B2B de DemandBase (DSP). Les comptes Target peuvent également être enrichis avec des données tierces Demandbase, pour d’autres cas d’utilisation en aval dans le marketing et les ventes.

Par exemple, utilisez les DSP ad-tech de Demandbase pour cibler des rôles ou des personnalités spécifiques au sein de comptes clés pour la génération de pistes principale, ou créez et développez des groupes d’achats. Utilisez la destination Demandbase pour explorer d’autres cas d’utilisation afin de cibler efficacement vos comptes.

Grâce à cette intégration, vous pouvez également personnaliser l’expérience du site web à l’aide de la recherche d’informations de compte en temps réel afin d’optimiser l’engagement.

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|--------------|-----------|---------------------------|
| Type d’exportation | Exportation de l’audience | Tous les membres de l’audience seront exportés avec des identifiants clés tels que le nom, le numéro de téléphone, etc. |
| Fréquence | Diffusion en continu | Connexions basées sur des API toujours actives. Les mises à jour sont envoyées immédiatement en aval après les modifications de profil. |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour exporter des audiences de compte vers Demandbase, vous avez besoin des éléments suivants :

1. Un compte Demandbase.
2. Jeton d’API Demandbase. Vous pouvez générer un jeton API avec votre utilisateur dans Demandbase. Pour générer un jeton, accédez à [Mon profil > Jeton API](https://web.demandbase.com/o/ad/at) après vous être connecté à votre compte Demandbase.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de **[!UICONTROL Affichage des destinations]** et de **[!UICONTROL Gestion des destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Ajouter un jeton porteur](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Jeton de porteur]** : renseignez le jeton de porteur pour vous authentifier sur la destination. Affichez les [conditions préalables](#prerequisites) pour plus d’informations sur la manière d’obtenir le jeton.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Ajout d’informations sur la connexion de destination](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’entité]** : sélectionnez **[!UICONTROL Compte]** comme type d’entité.

Vous êtes maintenant prêt à activer vos audiences dans Demandbase.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des instructions sur l’activation des audiences de compte vers cette destination.

## Remarques supplémentaires et légendes importantes {#additional-notes}

* Si une audience de compte portant le même nom a été activée antérieurement sur Demandbase, vous ne pouvez pas la réactiver par le biais d’un autre flux de données vers la destination Demandbase.
* Si vous avez exporté des audiences vers Demandbase et que les exportations sont réussies en Experience Platform, mais que toutes les données n’atteignent pas Demandbase, vous avez peut-être rencontré un ralentissement de l’API côté Demandbase. Contactez-les pour obtenir des éclaircissements.
