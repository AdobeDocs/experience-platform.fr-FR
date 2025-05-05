---
keywords: destination Qualtrics en continu
title: Automatisations Qualtrics
description: Synchronisez les données d’expérience et des clients opérationnels pour déverrouiller la personnalisation à grande échelle. Utilisez l’agrégation de plusieurs sources de données opérationnelles dans Adobe Experience Platform en tant qu’entrée dans Qualtrics Experience ID pour mieux comprendre vos clients et permettre une communication ciblée pour combler le fossé en termes de compréhension des facteurs d’intention, d’émotion et d’expérience.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 29%

---

# Automatisations Qualtrics

## Vue d’ensemble {#overview}

Synchronisez les données d’expérience et des clients opérationnels pour déverrouiller la personnalisation à grande échelle.

Utilisez l’agrégation de plusieurs sources de données opérationnelles dans Adobe Experience Platform en tant qu’entrée dans Qualtrics Experience ID pour mieux comprendre vos clients et permettre une communication ciblée pour combler le fossé en termes de compréhension des facteurs d’intention, d’émotion et d’expérience.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe Qualtrics. Pour toute question ou demande de mise à jour, contactez-les directement en vous connectant au [Centre de succès client](https://support-portal.qualtrics.com/).

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination *Automations Qualtrics*, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1 {#use-case-1}

**Scénario** : une entreprise souhaite mesurer la satisfaction de ses clients sur divers points de contact numériques, tels que son site web et son application mobile. Ils utilisent Adobe Experience Platform pour déclencher des enquêtes Qualtrics en fonction des interactions des utilisateurs, comme l’exécution d’un achat ou la visite d’une page web spécifique.

**Résultat** : en collectant des commentaires en temps réel, l’entreprise peut améliorer l’expérience client grâce aux données, ce qui lui permet d’accroître la satisfaction et la fidélité.

### Cas d’utilisation #2 {#use-case-2}

**Scénario** : une entreprise vise à améliorer son processus d’intégration des employés. Ils utilisent Adobe Experience Platform pour recueillir les commentaires des nouveaux employés par le biais des enquêtes Qualtrics. Les enquêtes sont automatiquement déclenchées après une période d&#39;intégration prédéfinie.

**Résultat** : les commentaires continus permettent à l’entreprise d’adapter et d’améliorer le processus d’intégration, ce qui se traduit par un meilleur engagement et une meilleure productivité parmi les nouveaux employés.

## Conditions préalables

Avant de configurer la destination Qualtrics dans Adobe Experience Platform, assurez-vous que les conditions préalables suivantes sont remplies :

* Vous disposez d’un compte Qualtrics.
* Vous avez obtenu le jeton API nécessaire à partir de Qualtrics.

### Obtention d’un jeton API

Vous trouverez ci-dessous les étapes nécessaires pour obtenir un jeton API à partir de Qualtrics.

1. Connectez-vous à votre compte Qualtrics.
2. Accédez à **Paramètres du compte**.
3. Sélectionnez **ID Qualtrics**.
4. Sur cette page, recherchez la section **API** qui contient un champ **Token**. Il s’agit du jeton API, qui sera requis lors de la configuration de la destination.

## Identités prises en charge {#supported-identities}

*Automations Qualtrics* prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| adresse e-mail | Adresses email en texte brut | Seules les adresses électroniques en texte brut sont prises en charge par Qualtrics. |
| external_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination *des automatisations Qualtrics*. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **&#x200B;**&#x200B;et des **&#x200B;**&#x200B;[&#128279;](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Dans le cadre de l&#39;authentification, vous devrez fournir un **nom d&#39;utilisateur** et un **mot de passe**. Le nom d’utilisateur est votre nom d’utilisateur Qualtrics et le mot de passe est le jeton API de votre compte Qualtrics. Pour récupérer le jeton API, suivez les instructions de la section **Conditions préalables** ci-dessus.

![Authentification](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL URL]** : URL trouvée dans l’ [événement JSON](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) qui déclenche votre [workflow dans Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Voir la capture d’écran ci-dessous pour obtenir un exemple.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des **&#x200B;**, **[!UICONTROL Activer les destinations]**, **&#x200B;**&#x200B;et **&#x200B;**&#x200B;[  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Cette destination comporte un schéma ouvert afin que vous puissiez envoyer toutes les propriétés à Qualtrics.

#### Attributs de mappage

Pour ajouter un attribut à votre mappage, sélectionnez simplement **attributs personnalisés** lors de l’ajout d’un nouveau mappage. Vous pouvez saisir n’importe quel nom pour votre attribut. Qualtrics encourage la convention de nommage *camelCase* pour les noms d’attribut (voir la capture d’écran ci-dessous pour un exemple).

![Attribut personnalisé](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Reportez-vous à la capture d’écran ci-dessous pour obtenir un exemple de mappages d’attributs possibles.

![Exemples de mappages](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mapping d’identités

Il est obligatoire de sélectionner un espace de noms d’identité pour cette destination. Les deux champs sources possibles pour cibler les mappages de champs sont les suivants :

| Champ source | Champ cible |
|--------------------|-----------------------|
| IdentityMap : Email | Identité : email |
| IdentityMap : ECID | Identité : external_id |

Voir la capture d’écran ci-dessous pour obtenir un exemple.

![Espace de noms d’identité](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Comme mentionné précédemment, cette destination utilise un schéma ouvert. Toutes les propriétés peuvent donc être envoyées à Qualtrics. Néanmoins, les données envoyées à Qualtrics suivront la structure suivante :

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

Pour vérifier que les données ont été ingérées dans Qualtrics, passez en revue le workflow contenant votre **événement JSON**, puis accédez à l’historique d’exécution **où vous devriez voir les exécutions de votre workflow.** Chaque workflow a un état **Succès** ou **Échec**. La sélection d’une exécution spécifique permet d’en savoir plus, ce qui vous permet de résoudre les problèmes éventuels.

Si aucune exécution n’est visible dans **Run history**, cela signifie que le workflow n’a pas encore été déclenché, ce qui indique qu’il peut y avoir un problème. Assurez-vous que le workflow est activé et que l’ **URL** de la destination dans Adobe Experience Platform est correct. Les exécutions de workflows ne sont pas instantanées. Il se peut donc que vous deviez attendre longtemps avant de les terminer.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
