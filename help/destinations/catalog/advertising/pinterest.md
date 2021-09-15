---
title: Connexion à la liste des clients pinterest
description: Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.
source-git-commit: a071aaaf5e9b8ef9223ef4f9ea204460f18bf95e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 5%

---

# [!DNL Pinterest Customer List] connection

## Présentation {#overview}

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

>[!IMPORTANT]
>
>Cette destination a été créée par l’équipe Pinterest. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse https://help.pinterest.com/en/contact.

## Conditions préalables {#prerequisites}

* L’utilisateur doit s’authentifier auprès d’un compte Pinterest ayant accès au compte publicitaire auquel il souhaite ajouter une audience. Vous trouverez des détails sur le partage de comptes publicitaires [ici](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Plus précisément, l’utilisateur a besoin des niveaux d’accès &quot;audience&quot;.
* Vous trouverez des détails sur les formats d’identité de la liste de clients [ici](https://help.pinterest.com/en/business/article/audience-targeting).


## Identités prises en charge {#supported-identities}

La destination [!DNL Pinterest Customer List] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

Dans l’ [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, mappez les identités souhaitées au champ cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Faites correspondre l’espace de noms de l’identité source *GAID* au champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Faites correspondre l’espace de noms de l’identité source *IDFA* au champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| EMAIL | Adresses électroniques (texte en clair ou haché avec l’algorithme SHA256) | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. <br> Mappez l’espace de noms de l’identité source  ** Email_LC_SHA256 *de l’* email au champ d’identité cible  *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de liste de clients de Pinterest.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Pinterest Customer List], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.


### Cas d’utilisation #1

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).



### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL ID]** du compte : Identifiant de votre compte publicitaire Pinterest.

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers les destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, reportez-vous à la [page du Centre d’aide de Pinterest](https://help.pinterest.com/en/business/article/audience-targeting).
