---
keywords: diffusion en continu, destination Qualtrics
title: Automatisations de Qualtrics
description: Synchronisez les données client opérationnelles et d’expérience pour déverrouiller la personnalisation à grande échelle. Utilisez l’agrégation de plusieurs sources de données opérationnelles dans Adobe Experience Platform comme entrée dans Qualtrics Experience ID pour mieux comprendre vos clients et permettre une sensibilisation ciblée afin de combler l’écart en matière de compréhension des moteurs d’intention, d’émotion et d’expérience.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 24%

---

# Automatisations de Qualtrics

## Vue d’ensemble {#overview}

Synchronisez les données client opérationnelles et d’expérience pour déverrouiller la personnalisation à grande échelle.

Utilisez l’agrégation de plusieurs sources de données opérationnelles dans Adobe Experience Platform comme entrée dans Qualtrics Experience ID pour mieux comprendre vos clients et permettre une sensibilisation ciblée afin de combler l’écart en matière de compréhension des moteurs d’intention, d’émotion et d’expérience.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe Qualtrics. Pour toute demande ou information, contactez directement l’équipe en vous connectant au [Hub du succès client](https://support-portal.qualtrics.com/).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination *Automatisations Qualtrics*, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1 {#use-case-1}

**Scénario** : une entreprise souhaite mesurer la satisfaction de sa clientèle à travers différents points de contact numériques, tels que son site web et son application mobile. Ils utilisent Adobe Experience Platform pour déclencher des enquêtes Qualtrics en fonction des interactions utilisateur, telles que la réalisation d’un achat ou la visite d’une page web spécifique.

**Résultat** : en recueillant des commentaires en temps réel, l’entreprise peut améliorer l’expérience de ses clients en fonction des données, ce qui lui permet d’accroître sa satisfaction et sa fidélité.

### Cas d’utilisation #2 {#use-case-2}

**Scénario** : une organisation vise à améliorer son processus d’intégration des employés. Ils utilisent Adobe Experience Platform pour recueillir les commentaires des nouvelles recrues par le biais d’enquêtes Qualtrics. Les questionnaires sont automatiquement déclenchés après une période d’intégration prédéfinie.

**Résultat** : La rétroaction continue permet à l&#39;organisation d&#39;adapter et d&#39;améliorer le processus d&#39;intégration, ce qui se traduit par une meilleure mobilisation et une meilleure productivité parmi les nouveaux employés.

## Conditions préalables

Avant de configurer la destination Qualtrics dans Adobe Experience Platform, vérifiez que les conditions préalables suivantes sont remplies :

* Vous disposez d’un compte Qualtrics.
* Vous avez obtenu le jeton API nécessaire auprès de Qualtrics.

### Obtention d’un jeton API

Vous trouverez ci-dessous les étapes nécessaires pour obtenir un jeton API auprès de Qualtrics.

1. Connectez-vous à votre compte Qualtrics.
2. Accédez à **Paramètres du compte**.
3. Sélectionnez **ID des mesures qualitatives**.
4. Sur cette page, recherchez la section **API**, elle contient un champ **Jeton**. Il s’agit du jeton API qui sera requis lors de la configuration de la destination.

## Identités prises en charge {#supported-identities}

*Automatisation des Qualtrics* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresses e-mail en clair | Seules les adresses e-mail en texte brut sont prises en charge par Qualtrics. |
| external_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

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
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Segment export]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *Automatisations Qualtrics*. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Dans le cadre de l’authentification, vous devez fournir un **Nom d’utilisateur** et **Mot de passe**. Le nom d’utilisateur est votre nom d’utilisateur Qualtrics et le mot de passe est le jeton API de votre compte Qualtrics. Pour récupérer le jeton API, suivez les instructions de la section **Conditions préalables** ci-dessus.

![Authentification](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL URL]** : URL trouvée dans l’événement [JSON](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) qui déclenche votre [workflow dans Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Consultez la capture d’écran ci-dessous pour obtenir un exemple.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Cette destination a un schéma ouvert. Vous pouvez donc envoyer n’importe quelle propriété à Qualtrics.

#### Attributs de mappage

Pour ajouter un attribut à votre mappage, sélectionnez simplement **attributs personnalisés** lors de l’ajout d’un nouveau mappage. Vous pouvez saisir n’importe quel nom pour votre attribut. Qualtrics applique la convention de dénomination *camelCase* pour les noms d’attribut (voir la capture d’écran ci-dessous pour obtenir un exemple).

![ Attribut personnalisé ](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Consultez la capture d’écran ci-dessous pour obtenir un exemple de mappages d’attributs possibles.

![Exemples de mappages](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mapping d’identités

Il est obligatoire de sélectionner un espace de noms d’identité pour cette destination. Les deux mappages possibles champ source vers champ cible sont les suivants :

| Champ source | Champ cible |
|--------------------|-----------------------|
| IdentityMap : e-mail | Identité : email |
| IdentityMap : ECID | Identité : external_id |

Consultez la capture d’écran ci-dessous pour obtenir un exemple.

![Espace de noms d’identité](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Comme mentionné précédemment, cette destination utilise un schéma ouvert. Toute propriété peut donc être envoyée à Qualtrics. Néanmoins, les données envoyées à Qualtrics suivront la structure ci-dessous :

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Pour vérifier que les données ont été ingérées dans Qualtrics, accédez au workflow contenant votre **Événement JSON**, puis accédez à **Historique d’exécution** où vous devriez voir les exécutions de votre workflow. Chaque workflow présente le statut **Réussi** ou **Échec**. La sélection d’une exécution spécifique affiche plus d’informations à son sujet, ce qui vous permet de résoudre les problèmes éventuels.

Si aucune exécution n’est visible dans l’**historique d’exécution**, cela signifie que le workflow n’a pas encore été déclenché, ce qui indique qu’il peut y avoir un problème. Assurez-vous que le workflow est activé et que l’**URL** de la destination dans Adobe Experience Platform est correcte. Les exécutions de workflows ne sont pas instantanées, vous devrez donc peut-être attendre quelques instants avant qu’elles ne se terminent.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
