---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Prise en main de l’API Real-time Customer Profile
type: Documentation
description: Le guide de prise en main de l’API Profile décrit les concepts clés et les fonctionnalités de base dont vous avez besoin pour utiliser les points de terminaison de l’API Real-Time Customer Profile afin d’effectuer des opérations CRUD de base sur les données de Profile.
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 53%

---

# Prise en main de l’API [!DNL Real-Time Customer Profile] {#getting-started}

À l’aide des points de terminaison de l’API Real-Time Customer Profile, vous pouvez effectuer des opérations CRUD de base sur les données de profil, telles que la configuration des attributs calculés, l’accès aux entités, l’exportation des données de profil et la suppression des jeux de données ou des lots inutiles.

L’utilisation du guide de développement nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation de [!DNL Profile] data. Avant de commencer à utiliser l’API [!DNL Real-Time Customer Profile], consultez la documentation relative aux services suivants :

* [[!DNL Real-Time Customer Profile]](../home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Obtenez une meilleure vue de vos clients et de leur comportement en rapprochant des identités entre les appareils et les systèmes.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md): Permet de créer des segments d’audience à partir de données Real-time Customer Profile.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Platform organise les données de l’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à [!DNL Profile] Points d’entrée API.

## Lecture d’exemples d’appels API

Le [!DNL Real-Time Customer Profile] La documentation des API fournit des exemples d’appels API pour démontrer comment formater correctement les requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour lancer des appels vers des points d’entrée [!DNL Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Demandes à [!DNL Platform] Les API requièrent un en-tête qui spécifie le nom de l’environnement de test dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Real-Time Customer Profile], sélectionnez l’un des guides de point d’entrée disponibles.
