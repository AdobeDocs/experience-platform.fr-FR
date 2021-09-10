---
title: Connexion à des audiences personnalisées twitter
description: Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 5%

---


# [!DNL Twitter Custom Audiences] connection

## Présentation {#overview}

Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Avant de configurer votre destination [!DNL Twitter Custom Audiences], vérifiez les conditions préalables Twitter suivantes que vous devez remplir.

1. Votre compte [!DNL Twitter Ads] doit être éligible à la publicité. Les nouveaux comptes [!DNL Twitter Ads] ne sont pas éligibles à la publicité dans les 2 premières semaines suivant leur création.
2. L’autorisation *[!DNL Partner Audience Manager]* doit être activée pour votre compte utilisateur Twitter pour lequel vous avez autorisé l’accès dans [!DNL Twitter Audience Manager].


## Identités prises en charge {#supported-identities}

[!DNL Twitter Custom Audiences] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
|---|---|---|
| device_id | IDFA/AdID/Android ID | L’identifiant Google Advertising (GAID) et l’identifiant Apple pour les annonceurs (IDFA) sont pris en charge dans Adobe Experience Platform. Faites correspondre ces espaces de noms et/ou attributs de votre schéma source en conséquence à l’[étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination. |
| e-mail | Adresse(s) de courriel de l’utilisateur | Faites correspondre vos adresses électroniques en texte brut et vos adresses électroniques hachées SHA256 à ce champ. Lorsque votre champ source contient des attributs non hachés, cochez l&#39;option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l&#39;activation. Si vous hachez les adresses électroniques de vos clients avant de les transférer vers Adobe Experience Platform, notez que ces identités doivent être hachées à l’aide de SHA256, sans sel. |

{style=&quot;table-layout:auto&quot;}

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants utilisés dans la destination Audiences personnalisées de Twitter.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Twitter Custom Audiences], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform sous la forme [!DNL List Custom Audiences] dans Twitter.

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** du compte : Identifiant de  [!DNL Twitter Ads] compte. Vous pouvez le trouver dans vos paramètres [!DNL Twitter Ads].

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers les destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ressources supplémentaires {#additional-resources}

Lors du mappage des segments d’audience sur Twitter, assurez-vous de respecter les exigences d’attribution de noms de segment suivantes :

1. Fournir des noms de mappage de segments lisibles par l’utilisateur. Nous vous recommandons d’utiliser le même nom que celui utilisé pour les segments Experience Platform.
2. N’utilisez pas de caractères spéciaux (+ &amp; , % : ; @ / = ? $) dans les noms de mappage de segments et de segments. Si le nom du segment Experience Platform contient ces caractères, supprimez-les avant de mapper le segment à une destination Twitter.

Vous trouverez plus d’informations sur [!DNL List Custom Audiences] dans Twitter dans la [documentation Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).