---
title: Connexion à TikTok
description: Créez des audiences personnalisées sur TikTok avec vos données pour le ciblage de vos campagnes publicitaires. Il peut s’agir de personnes qui ont visité votre site web ou interagi avec votre contenu. Poussez rapidement et en toute sécurité l’audience souhaitée de Adobe Experience Platform vers TikTok à l’aide de l’intégration en temps réel d’Adobe à TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 39%

---

# Connexion à TikTok

## Vue d’ensemble {#overview}

Créez des audiences personnalisées sur TikTok avec vos données pour le ciblage de vos campagnes publicitaires. Il peut s’agir de personnes qui ont visité votre site web ou interagi avec votre contenu. Poussez rapidement et en toute sécurité l’audience souhaitée de Adobe Experience Platform vers TikTok à l’aide de l’intégration en temps réel d’Adobe à TikTok Ads Manager. Pour plus d’informations, consultez le [centre d’aide aux entreprises TikTok](https://ads.tiktok.com/help/article/audiences) .

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe TikTok. Pour toute question ou demande de mise à jour, contactez-les directement à l&#39;adresse [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination TikTok, voici un exemple de cas d’utilisation pour les clients Adobe Experience Platform.

### Cas d’utilisation {#use-case-1}

Une marque de vêtements d’athlétisme veut atteindre ses clients existants par le biais de leurs comptes de médias sociaux. La marque de vêtements peut ingérer des adresses électroniques de son propre CRM vers Adobe Experience Platform, créer des audiences à partir de ses propres données hors ligne et envoyer ces audiences à TikTok pour afficher des publicités dans les flux de médias sociaux de ses clients.

## Conditions préalables {#prerequisites}

Vous devez avoir [!DNL Admin] ou [!DNL Operator] accès au compte TikTok Ads Manager auquel vous souhaitez envoyer des audiences. Vous trouverez plus d’instructions sur le [centre d’aide de TikTok](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Avant d’envoyer des données à votre compte TikTok Ads Manager, vous devez autoriser Adobe Experience Platform à accéder à votre compte publicitaire pour `Audience Management`. Cette autorisation peut être fournie en [saisissant votre ID de gestionnaire de publicités](#authenticate) dans l’interface utilisateur de l’Experience Platform et en accordant l’autorisation après avoir été redirigé vers votre compte de gestionnaire de publicités TikTok.

## Identités prises en charge {#supported-identities}

TikTok prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| Numéro de téléphone | Numéros de téléphone hachés avec l’algorithme SHA256 | Les numéros de téléphone hachés SHA-256 et en texte brut sont pris en charge par Adobe Experience Platform et doivent être au format E.164. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| E-mail | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination TikTok. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, vous serez redirigé afin de vous connecter à votre compte [!DNL TikTok Ads Manager] et d’autoriser l’Adobe à gérer les audiences en votre nom.

![Sélection d’autorisations TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Image de l’interface utilisateur de TikTok pour la sélection des autorisations")

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Détails de la connexion de destination](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Image de l’interface utilisateur de Platform, indiquant les détails de la connexion de destination à remplir dans")

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL TikTok Ads Manager ID]** : votre [!DNL TikTok Ads Manager ID]. Vous pouvez le trouver dans votre compte [!DNL TikTok Ads manager].

![Identifiant TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Image de l’interface utilisateur de TikTok Ads Manager, indiquant comment obtenir l’identifiant TikTok Ads Manager")

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapping d’identités {#map}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’exportation d’audiences vers TikTok Ads Manager.

Sélection des champs sources :

* Sélectionnez un identifiant (par exemple :` Email_LC_SHA256`) comme identité source qui identifie de manière unique un profil dans Adobe Experience Platform et [!DNL TikTok Ads Manager].

Sélection des champs cibles :

* Sélectionnez l’espace de noms de l’email comme identité cible.

![Mappage des identités](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Image de l’interface utilisateur de Platform, mappage des identités")

## Données exportées {#exported-data}

Vérifiez votre compte [!DNL TikTok Ads Manager] (sous **Assets > Audiences**) pour vérifier si l’exportation de votre audience Experience Platform a réussi. L’audience sera renseignée sous la forme d’un type d’audience : `Partner Audience`.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, reportez-vous à la [page du Centre d’aide de TikTok](https://ads.tiktok.com/help/article/audiences) .
