---
title: Connexion à des audiences personnalisées par twitter
description: Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 43%

---

# Connexion [!DNL Twitter Custom Audiences]

## Présentation {#overview}

Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Avant de configurer votre [!DNL Twitter Custom Audiences] destination, veillez à passer en revue les conditions préalables Twitter suivantes que vous devez remplir.

1. Votre [!DNL Twitter Ads] doit être éligible à la publicité. Nouveau [!DNL Twitter Ads] les comptes ne sont pas éligibles à la publicité dans les 2 premières semaines suivant leur création.
2. Votre compte utilisateur de Twitter pour lequel vous avez autorisé l’accès dans [!DNL Twitter Audience Manager] doit avoir la variable *[!DNL Partner Audience Manager]* autorisation activée.

## Identités prises en charge {#supported-identities}

[!DNL Twitter Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) et Apple ID for Advertisers (IDFA) sont pris en charge dans Adobe Experience Platform. Faites correspondre ces espaces de noms et/ou attributs de votre schéma source en conséquence dans la variable [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination. |
| adresse e-mail | Adresse(s) de courriel de l’utilisateur | Faites correspondre vos adresses électroniques en texte brut et vos adresses électroniques hachées SHA256 à ce champ. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. Si vous hachez les adresses électroniques de vos clients avant de les transférer vers Adobe Experience Platform, notez que ces identités doivent être hachées à l’aide de SHA256, sans sel. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants utilisés dans la destination Audiences personnalisées du Twitter. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Cas d’utilisation {#use-cases}

Pour mieux comprendre comment et à quel moment utiliser la variable [!DNL Twitter Custom Audiences] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation 1

Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform as [!DNL List Custom Audiences] en Twitter.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez le [!DNL Twitter Custom Audiences] destination dans le catalogue des destinations et sélectionnez **[!UICONTROL Configuration]**.
2. Sélectionner **[!UICONTROL Se connecter à la destination]**.
   ![Authentification à LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Saisissez vos informations d’identification de Twitter et sélectionnez **Connexion**.

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="Identifiant de compte"
>abstract="Identifiant de votre compte Twitter Ads. Vous pouvez le trouver dans vos paramètres Twitter Ads."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]**: votre [!DNL Twitter Ads] ID de compte. Vous pouvez le trouver dans votre [!DNL Twitter Ads] paramètres.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Lors du mappage des audiences sur Twitter, assurez-vous de respecter les exigences suivantes en termes d’attribution de noms aux audiences :

1. Fournir des noms de mappage d’audience lisibles par l’utilisateur. Nous vous recommandons d’utiliser le même nom que celui utilisé pour les segments Experience Platform.
2. N’utilisez pas de caractères spéciaux (+ &amp; , % : ; @ / = ? $) dans les noms des mappages d’audience et d’audience. Si le nom de l’audience Experience Platform contient ces caractères, supprimez-les avant de mapper l’audience à une destination de Twitter.

Plus d’informations sur [!DNL List Custom Audiences] en Twitter se trouve dans la variable [Documentation du twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
