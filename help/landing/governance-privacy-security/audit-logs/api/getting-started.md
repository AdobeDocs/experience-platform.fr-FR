---
title: Prise en main de l’API de requête d’audit
description: L’API de requête d’audit vous permet de récupérer des données de mesure pour différentes fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant de lancer des appels à l’API de requête d’audit.
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 40%

---

# Prise en main de l’API de requête d’audit

Adobe Experience Platform vous permet de contrôler l’activité des utilisateurs pour divers services et fonctionnalités sous la forme de journaux d’événements de contrôle. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’e-mail de l’utilisateur qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

L’API de requête d’audit vous permet de contrôler l’activité des utilisateurs pour divers services et fonctionnalités sous la forme de journaux d’événements d’audit. Ce document présente les concepts de base que vous devez connaître avant de lancer des appels à l’API de requête d’audit.

## Conditions préalables

Pour gérer les événements de contrôle, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le journal d’activité de l’utilisateur]** (disponible dans la catégorie [!UICONTROL  Gouvernance des données]). Pour savoir comment gérer les autorisations individuelles pour les fonctionnalités de Platform, reportez-vous à la [documentation sur le contrôle d’accès](../../../../access-control/home.md).

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’effectuer des appels aux API de Platform avec succès. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu. Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’API [!DNL Audit Query], reportez-vous au [guide de point de terminaison events](./events.md) et au [guide de point de terminaison export](./export.md).
