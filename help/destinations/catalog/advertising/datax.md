---
title: Connexion Verizon MediaYahoo DataX
description: DataX, une infrastructure globale appartenant à Verizon Media/Yahoo, permet dʼhéberger différents composants et dʼéchanger des données avec les partenaires externes de Verizon Media/Yahoo, de manière sécurisée, automatisée et évolutive.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 32%

---

# Connexion [!DNL Verizon Media/Yahoo DataX]

## Vue d’ensemble {#overview}

[!DNL DataX] est une infrastructure de [!DNL Verizon Media/Yahoo] agrégée qui héberge divers composants permettant à [!DNL Verizon Media/Yahoo] d’échanger des données avec ses partenaires externes de manière sécurisée, automatisée et évolutive.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe [!DNL Verizon Media/Yahoo] de [!DNL DataX]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse [dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)

## Conditions préalables {#prerequisites}

**ID MDM**

Il s’agit d’un identifiant unique dans [!DNL Yahoo DataX] et il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre gestionnaire de compte [!DNL Yahoo DataX].

**Métadonnées de taxonomie**

La ressource Taxonomie définit une extension sur la structure de métadonnées de [!DNL DataX] de base

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Pour en savoir plus sur la [Métadonnées de taxonomie](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/), consultez la documentation destinée aux développeurs et développeuses [!DNL DataX].

## Limites de taux et mécanismes de sécurisation {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Lors de l’activation de plus de 100 audiences sur [!DNL Verizon Media/Yahoo DataX], vous pouvez recevoir des erreurs de limitation de débit de la destination. Lors de l’activation des audiences vers cette destination, essayez d’activer moins de 100 audiences dans un seul flux de données d’activation. Si vous devez activer d’autres segments, créez une nouvelle destination sur le même compte.

[!DNL DataX] est limité par le taux conformément aux limites de quota pour les publications de taxonomie et d’audience décrites dans la documentation de [DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Code d’erreur | Message d’erreur | Description |
|---------|----------|---------|
| 429 Too many requests | Taux limite dépassé par heure **(Limite : 100)** | Nombre de requêtes autorisées par heure et par fournisseur. |

{style="table-layout:auto"}

## Identités prises en charge {#supported-identities}

[!DNL Verizon Media] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail, GAID, IDFA) utilisés dans la destination Verizon Media. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

Les API [!DNL DataX] sont disponibles pour les annonceurs qui souhaitent cibler un groupe d’audiences spécifique dont les adresses e-mail ont été désactivées dans [!DNL Verizon Media] (VMG). Ils peuvent rapidement créer une nouvelle audience et envoyer le groupe d’audiences souhaité à l’aide de l’API en temps quasi réel de VMG.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

![Carte de destination Yahoo DataX dans l’interface utilisateur d’Experience Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL MDM ID]** : il s’agit d’un identifiant unique dans [!DNL Yahoo DataX] et il s’agit d’un champ obligatoire pour configurer les exportations de données vers cette destination. Si vous ne connaissez pas cet identifiant, contactez votre gestionnaire de compte [!DNL Yahoo DataX].  Avec les identifiants MDM, les données peuvent être limitées pour une utilisation uniquement avec un certain ensemble d’utilisateurs exclusifs (tels que les données propriétaires pour les annonceurs).

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer des profils et des audiences vers une destination](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers les destinations.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, consultez la [!DNL Yahoo/Verizon Media] [documentation sur [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
