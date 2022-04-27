---
title: Connexion à des audiences personnalisées twitter
description: Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 21%

---

# Connexion [!DNL Twitter Custom Audiences]

## Présentation {#overview}

Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Avant de configurer votre [!DNL Twitter Custom Audiences] destination, veillez à passer en revue les conditions préalables Twitter suivantes que vous devez remplir.

1. Votre [!DNL Twitter Ads] doit être éligible à la publicité. Nouveau [!DNL Twitter Ads] les comptes ne sont pas éligibles à la publicité dans les 2 premières semaines suivant leur création.
2. Votre compte utilisateur Twitter pour lequel vous avez autorisé l’accès dans [!DNL Twitter Audience Manager] doit avoir la variable *[!DNL Partner Audience Manager]* autorisation activée.

## Identités prises en charge {#supported-identities}

[!DNL Twitter Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) et Apple ID for Advertisers (IDFA) sont pris en charge dans Adobe Experience Platform. Faites correspondre ces espaces de noms et/ou attributs de votre schéma source en conséquence dans la variable [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination. |
| adresse e-mail | Adresse(s) de courriel de l’utilisateur | Faites correspondre vos adresses électroniques en texte brut et vos adresses électroniques hachées SHA256 à ce champ. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable **[!UICONTROL Appliquer la transformation]** option, pour avoir [!DNL Platform] hachage automatique des données lors de l’activation. Si vous hachez les adresses électroniques de vos clients avant de les transférer vers Adobe Experience Platform, notez que ces identités doivent être hachées à l’aide de SHA256, sans sel. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants utilisés dans la destination Audiences personnalisées de Twitter. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL Twitter Custom Audiences] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation 1

Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform as [!DNL List Custom Audiences] dans Twitter.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Pendant la [configuration](../../ui/connect-destination.md) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant de compte]**: Votre [!DNL Twitter Ads] ID de compte. Vous pouvez le trouver dans votre [!DNL Twitter Ads] paramètres.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Lors du mappage des segments d’audience sur Twitter, assurez-vous de respecter les exigences d’attribution de noms de segment suivantes :

1. Fournir des noms de mappage de segments lisibles par l’utilisateur. Nous vous recommandons d’utiliser le même nom que celui utilisé pour les segments Experience Platform.
2. N’utilisez pas de caractères spéciaux (+ &amp; , % : ; @ / = ? $) dans les noms de mappage de segments et de segments. Si le nom du segment Experience Platform contient ces caractères, supprimez-les avant de mapper le segment à une destination Twitter.

Plus d’informations sur [!DNL List Custom Audiences] dans Twitter se trouve dans la variable [Documentation twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
