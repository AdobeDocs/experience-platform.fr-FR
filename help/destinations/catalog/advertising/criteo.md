---
keywords: la publicité, les critères;
title: Connexion à un critère
description: Criteo optimise la publicité de confiance et d’impact afin d’offrir à chaque consommateur des expériences plus riches sur l’Internet libre. Grâce au jeu de données commercial le plus important du monde et à l’IA la plus performante du monde, Criteo s’assure que chaque point de contact du parcours d’achat est personnalisé pour atteindre les clients avec la bonne publicité, au bon moment.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 30%

---

# (Version bêta) Connexion Criteo

## Vue d’ensemble {#overview}

>[!IMPORTANT]
>
>Cette page de documentation et de connecteur de destination est créée et conservée par Criteo. Il s’agit actuellement d’un produit en version Beta qui peut faire l’objet de modifications. Pour toute demande de mise à jour ou de mise à jour, contactez directement Criteo. [here](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo optimise la publicité de confiance et d’impact afin d’offrir à chaque consommateur des expériences plus riches sur l’Internet libre. Grâce au jeu de données commercial le plus important du monde et à l’IA la plus performante du monde, Criteo s’assure que chaque point de contact du parcours d’achat est personnalisé pour atteindre les clients avec la bonne publicité, au bon moment.

## Conditions préalables {#prerequisites}

* Vous devez disposer d’un compte utilisateur administrateur sur [Centre de gestion des critères](https://marketing.criteo.com).
* Vous aurez besoin de votre identifiant publicitaire Criteo (demandez à votre contact Criteo si vous ne possédez pas cet identifiant).
* Vous devrez fournir [!DNL GUM caller ID], au cas où vous souhaitez utiliser [!DNL GUM ID] comme identifiant.

## Limites {#limitations}

* Acceptation des critères uniquement [!DNL SHA-256]Emails en texte brut et hachés (à transformer en [!DNL SHA-256] avant envoi). Veuillez ne pas envoyer d&#39;informations d&#39;identification personnelles, telles que le nom ou les numéros de téléphone d&#39;un individu.
* Le critère nécessite qu’au moins un identifiant soit fourni par le client. Elle établit des priorités. [!DNL GUM ID] comme identifiant sur un email haché, car il contribue à un meilleur taux de correspondance.

![Conditions préalables](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identités prises en charge {#supported-identities}

Criteo prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr#getting-started).

| Identité cible | Description | Considérations |
| --- | --- | --- |
| `email_sha256` | Adresses électroniques hachées avec l’algorithme SHA-256 | Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA-256. Lorsque votre champ source contient des attributs non hachés, vérifiez la variable [!UICONTROL Appliquer la transformation] pour que Platform hache automatiquement les données lors de l’activation. |
| `gum_id` | Criteo [!DNL GUM] identifiant de cookie | [!DNL GUM IDs] permettre aux clients de gérer une correspondance entre leur système d’identification utilisateur et l’identification utilisateur de Criteo ([!DNL UID]). Si le type d’identifiant est `gum_id`, un paramètre supplémentaire, la variable [!DNL GUM Caller ID], doit également être inclus. Contactez votre équipe de compte Criteo pour connaître les [!DNL GUM Caller ID] ou pour obtenir plus d’informations à ce sujet [!DNL GUM ID] synchronisation, si nécessaire. |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
| --- | --- | --- |
| Type d’exportation | Export d’audience | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Criteo]. |
| Fréquence des exportations | Diffusion en continu | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](../../destination-types.md#streaming-destinations). |

## Cas d’utilisation {#use-cases}

Pour mieux comprendre comment utiliser la variable [!DNL Criteo] destination, voici quelques objectifs que les clients Adobe Experience Platform peuvent atteindre. [!DNL Criteo]:

### Cas d’utilisation 1 : Obtention du trafic

Présenter à votre entreprise des offres de produits pertinentes et des créations flexibles. Avec des recommandations de produits intelligentes, vos publicités proposeront automatiquement les produits les plus susceptibles de déclencher des visites et des engagements. Le ciblage flexible vous permet de créer des audiences à partir de l’ensemble de données commerciales de Criteo ou de vos propres listes de prospects et d’Adobe de segments CDP.

### Cas d’utilisation 2 : augmentation des conversions du site web

Lorsque les visiteurs quittent votre site web, rappelez-leur ce qui leur manque avec les publicités de reciblage qui augmentent les conversions en présentant des offres spéciales et des offres hyper-pertinentes, où qu’ils se rendent. Connectez votre audience CDP d’Adobe pour réengager les clients existants ou cibler les consommateurs similaires à vos acheteurs les plus fidèles.

## Connexion à Criteo {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Authentification à un critère

Les étapes de connexion sont les suivantes :

1. Connectez-vous à Adobe Experience Platform et connectez-vous à la destination Criteo.

   ![Connexion](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Vous serez redirigé vers Criteo pour autoriser la connexion. Vous devrez peut-être d’abord vous connecter à l’aide de vos informations d’identification Criteo :

   ![Connexion aux critères](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Connexion aux critères](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Connexion aux critères](../../assets/catalog/advertising/criteo/log-in-3.png)


### Paramètres de connexion {#connection-parameters}

Après vous être authentifié à la destination, veuillez renseigner les paramètres de connexion suivants.

![Paramètres de connexion](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Champ | Description | Obligatoire |
| --- | --- | --- |
| Nom | Un nom qui vous aidera à reconnaître cette destination à l’avenir. Le nom que vous choisissez ici sera : [!DNL Audience] dans le Centre de gestion des critères et ne peut pas être modifié ultérieurement. | Oui |
| Description | Description qui vous aidera à identifier cette destination ultérieurement. | Non |
| Identifiant annonceur | Identifiant de publicitaire de critère de votre organisation. Contactez votre gestionnaire de compte Criteo pour obtenir ces informations. | Oui |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] de votre organisation. Contactez votre équipe de compte Criteo pour connaître les [!DNL GUM Caller ID] ou pour obtenir plus d’informations à ce sujet [!DNL GUM] synchronisation, si nécessaire. | Oui, chaque fois que [!DNL GUM ID] est fourni comme identifiant |

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate-segments}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

## Données exportées {#exported-data}

Vous pouvez afficher les audiences exportées dans la variable [Centre de gestion des critères](https://marketing.criteo.com/audience-manager/dashboard).

Le corps de la requête d’ajout d’un profil utilisateur reçu par le [!DNL Criteo] La connexion ressemble à ceci :

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

Le corps de requête de suppression du profil utilisateur reçu par le [!DNL Criteo] La connexion ressemble à ceci :

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Utilisation et gouvernance des données {#data-usage}

Toutes les destinations Adobe Experience Platform sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la manière dont Adobe Experience Platform applique la gouvernance des données, consultez la section [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires

* [Centre d’aide de Criteo](https://help.criteo.com/kb/en)
* [Portail de développement de critères](https://developers.criteo.com)
