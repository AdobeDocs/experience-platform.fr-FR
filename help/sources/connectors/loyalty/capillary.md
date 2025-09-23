---
title: Présentation Des Événements De Diffusion En Continu Capillaires
description: Découvrez comment diffuser des données de Capillary vers Experience Platform.
last-substantial-update: 2025-09-23T00:00:00Z
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 8%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>La source [!DNL Capillary Streaming Events] est en version Beta. Lisez les [termes et conditions](../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL Capillary Technologies] est une plateforme de fidélité et d’engagement de premier plan, approuvée par plus de 300 marques à travers le monde. Utilisez la source [!DNL Capillary Streaming Events] pour permettre à votre entreprise de diffuser en toute transparence les profils clients, les données de fidélité et les événements transactionnels de [!DNL Capillary] vers Adobe Experience Platform. Connectez votre source [!DNL Capillary] pour activer la personnalisation en temps réel, la segmentation avancée des audiences et l’orchestration de campagnes omnicanal.

En intégrant [!DNL Capillary] à Experience Platform, vous pouvez :

* Synchronisez **points de fidélité, niveaux et récompenses** en temps réel.
* Envoyez les **données transactionnelles** à Experience Platform à des fins d’analyse et d’activation.
* Tirez parti de Real-Time CDP, Experience Platform et Adobe Journey Optimizer pour la segmentation, l’orchestration des parcours et la personnalisation.

## Conditions préalables

Avant de connecter [!DNL Capillary] à Adobe Experience Platform, vérifiez que vous disposez des éléments suivants :

* Un **ID d’organisation Adobe valide** et l’accès à un sandbox Experience Platform activé.
* **[!DNL Capillary]les informations d’identification de la source** (ID client et secret client).
* Les autorisations nécessaires dans le Adobe Admin Console pour créer des sources et des flux de données.

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Capillary] à Experience Platform :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | Identifiant client de la source de [!DNL Capillary]. | `321c8a8fee0d4a06838d46f9d3109e8a` |
| Secret client | Secret client émis avec l’ID client | `xxxxxxxxxxxxxxxxxx` |
| ID d’organisation | Votre identifiant d’organisation Adobe | `0A7D42FC5DB9D3360A495FD3@AdobeOrg` |

Pour plus d’informations sur la génération de jetons d’accès, consultez le [guide d’authentification d’Adobe](https://developer.adobe.com/developer-console/docs/guides/authentication/).

### Générer un jeton d’accès

Ensuite, utilisez votre identifiant client et votre secret client pour générer un jeton d’accès à partir d’Adobe.

**Requête**

```shell
curl -X POST 'https://ims-na1.adobelogin.com/ims/token' \
  -d 'client_id={CLIENT_ID}' \
  -d 'client_secret={CLIENT_SECRET}' \
  -d 'grant_type=client_credentials' \
  -d 'scope=openid AdobeID read_organizations additional_info.projectedProductContext session'
```

**Réponse**

```json
{
  "access_token": "eyJhbGciOi...",
  "token_type": "bearer",
  "expires_in": 86399994
}
```

## Étapes suivantes

Une fois la configuration requise pour [!DNL Capillary] terminée, lisez la documentation suivante pour savoir comment connecter votre compte et commencer à diffuser des données de [!DNL Capillary] vers Experience Platform.

* [Connexion  [!DNL Capillary Streaming Events]  Experience Platform à l’aide de l’API](../../tutorials/api/create/loyalty/capillary.md)
* [Connexion  [!DNL Capillary Streaming Events]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/loyalty/capillary.md)
