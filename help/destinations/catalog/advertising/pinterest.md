---
title: Connexion Liste des Clients Pinterest
description: Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 5cef3bbc7f2246a91ecca807825d830f240c8d45
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 45%

---

# Connexion [!DNL Pinterest Customer List]

>[!IMPORTANT]
>
>* Depuis le 16 novembre 2023, deux cartes Pinterest s’affichent côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau de l’API de l’annonceur Pinterest utilisée pour exporter des données vers Pinterest. Le connecteur de destination Pinterest existant a été renommé en **[!UICONTROL pinterest (obsolète)]** et une nouvelle carte **[!UICONTROL (Nouveau) Pinterest]** est désormais disponible.
>* Utilisez la variable **[!UICONTROL (Nouveau) Pinterest]** connexion dans le catalogue pour toutes les campagnes vers Pinterest. Si vous avez des flux de données actifs vers la variable **[!UICONTROL pinterest (obsolète)]** destination, lisez la [documentation de mise à niveau](/help/destinations/catalog/advertising/pinterest-upgrade.md) pour comprendre vos éléments d’action afin de ne pas perturber vos campagnes.

## Vue d’ensemble {#overview}

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

>[!IMPORTANT]
>
>Cette destination a été créée par l’équipe Pinterest. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse https://help.pinterest.com/en/contact.

## Conditions préalables {#prerequisites}

* L’utilisateur doit s’authentifier auprès d’un compte Pinterest ayant accès au compte publicitaire auquel il souhaite ajouter une audience. Vous trouverez des informations détaillées sur le partage de comptes publicitaires [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Plus précisément, l’utilisateur a besoin des niveaux d’accès &quot;audience&quot;.
* Vous trouverez des détails sur les formats d’identité de la liste de clients [here](https://help.pinterest.com/en/business/article/audience-targeting).

## Identités prises en charge {#supported-identities}

La variable [!DNL Pinterest Customer List] destination prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

Dans le [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, faites correspondre les identités de votre choix au champ cible. *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Faites correspondre la variable *GAID* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Faites correspondre la variable *IDFA* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| EMAIL | Adresses électroniques (texte en clair ou haché avec l’algorithme SHA256) | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. <br> Faites correspondre la variable *Email* ou *Email_LC_SHA256* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de liste de clients Pinterest. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

Pour découvrir les avantages de la destination [!DNL Pinterest Customer List] et son utilisation, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation 1

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte publicitaire]**: votre identifiant publicitaire Pinterest.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Reportez-vous à [Page Centre d’aide pinterest](https://help.pinterest.com/en/business/article/audience-targeting) pour plus d’informations.

+++ Afficher le journal des modifications


| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Novembre 2023 | Nouvelles fonctionnalités et mise à jour de la documentation | La destination Pinterest dans Real-Time CDP utilise désormais l’API v5 Advertiser. |

{style="table-layout:auto"}


+++
