---
title: Connexion à la liste des clients pinterest
description: Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: 90aa0d16851443255dd4828e9f28330a89a12692
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# [!DNL Pinterest Customer List] connection

## Présentation {#overview}

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

>[!IMPORTANT]
>
>Cette destination a été créée par l’équipe Pinterest. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse https://help.pinterest.com/en/contact.

## Conditions préalables {#prerequisites}

* L’utilisateur doit s’authentifier auprès d’un compte Pinterest ayant accès au compte publicitaire auquel il souhaite ajouter une audience. Vous trouverez des informations détaillées sur le partage de comptes publicitaires [here](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). Plus précisément, l’utilisateur a besoin des niveaux d’accès &quot;audience&quot;.
* Vous trouverez des détails sur les formats d’identité de la liste de clients [here](https://help.pinterest.com/en/business/article/audience-targeting).


## Identités prises en charge {#supported-identities}

Le [!DNL Pinterest Customer List] destination prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

Dans le [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, faites correspondre les identités de votre choix au champ cible. *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Faites correspondre la variable *GAID* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| IDFA | [!DNL Apple ID for Advertisers] | Faites correspondre la variable *IDFA* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. Les identités sont distinguées et résolues lors de l’ingestion de données dans Pinterest. |
| EMAIL | Adresses électroniques (texte en clair ou haché avec l’algorithme SHA256) | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. <br> Faites correspondre la variable *Email* ou *Email_LC_SHA256* espace de noms d’identité source vers le champ d’identité cible *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## Type d&#39;export {#export-type}

**Exportation de segments** : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de liste de clients Pinterest.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la variable [!DNL Pinterest Customer List] destination, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.


### Cas d’utilisation #1

Créez des audiences à partir des listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest.

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).


### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant publicitaire]**: Votre identifiant publicitaire Pinterest.

## Activation des segments vers cette destination {#activate}

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Utilisation et gouvernance des données {#data-usage-governance}

Tous [!DNL Adobe Experience Platform] Les destinations sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Ressources supplémentaires {#additional-resources}

Reportez-vous au [Page Centre d’aide pinterest](https://help.pinterest.com/en/business/article/audience-targeting) pour plus d’informations.
