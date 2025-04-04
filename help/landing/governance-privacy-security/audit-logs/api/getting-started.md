---
title: Prise en main de l’API Audit Query
description: L’API Audit Query vous permet de récupérer des données de mesure pour diverses fonctionnalités de Adobe Experience Platform. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API Audit Query.
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 35%

---

# Prise en main de l’API Audit Query

Adobe Experience Platform vous permet d’auditer l’activité des utilisateurs et utilisatrices pour divers services et fonctionnalités sous la forme de journaux d’événements d’audit. Chaque action enregistrée dans un journal contient des métadonnées qui indiquent le type d’action, la date et l’heure, l’ID d’e-mail de l’utilisateur ou de l’utilisatrice qui a exécuté l’action et des attributs supplémentaires liés au type d’action.

L’API Audit Query vous permet d’auditer l’activité des utilisateurs pour divers services et fonctionnalités sous la forme de journaux d’événements d’audit. Ce document présente les concepts de base que vous devez connaître avant d’effectuer des appels à l’API Audit Query.

## Conditions préalables

Pour gérer les événements d’audit, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le journal d’activité de l’utilisateur]** accordée (dans la catégorie [!UICONTROL Gouvernance des données]). Pour savoir comment gérer les autorisations individuelles pour les fonctionnalités Experience Platform, reportez-vous à la [documentation sur le contrôle d’accès](../../../../access-control/home.md).

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées pour les exemples d’appels API dans la documentation, consultez la section sur la [lecture d’exemples d’appels API](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage d’Experience Platform.

### Collecte des valeurs des en-têtes requis

Ce guide nécessite que vous ayez suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour passer avec succès des appels aux API Experience Platform. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée. Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

Toutes les requêtes contenant un payload (POST, PUT et PATCH) requièrent un en-tête supplémentaire :

* Content-Type: application/json

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Audit Query], reportez-vous au guide de point d’entrée [events](./events.md) et au guide de point d’entrée [export](./export.md).
