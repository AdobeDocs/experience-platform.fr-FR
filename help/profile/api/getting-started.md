---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Prise en main de l’API Real-Time Customer Profile
type: Documentation
description: Le guide de prise en main de l’API Profile décrit les concepts clés et les fonctionnalités de base que vous devez connaître pour utiliser les points d’entrée de l’API Real-Time Customer Profile afin d’effectuer des opérations CRUD de base sur les données Profile.
role: Developer
exl-id: 7e30610a-a7e7-43ab-a45d-fd84ef6e36ef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 53%

---

# Prise en main de l’API [!DNL Real-Time Customer Profile] {#getting-started}

À l’aide des points d’entrée de l’API Real-Time Customer Profile, vous pouvez effectuer des opérations CRUD de base sur les données Profile, comme configurer des attributs calculés, accéder à des entités, exporter des données Profile et supprimer des jeux de données ou des lots inutiles.

L’utilisation du guide du développeur nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans l’utilisation des données [!DNL Profile]. Avant de commencer à utiliser l’API [!DNL Real-Time Customer Profile], consultez la documentation relative aux services suivants :

* [[!DNL Real-Time Customer Profile]](../home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md) : obtenez une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
* [[!DNL Adobe Experience Platform Segmentation Service]](../../segmentation/home.md) : permet de créer des audiences à partir des données du profil client en temps réel.
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuels qui divisent une instance [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de passer avec succès des appels vers des points d’entrée d’API [!DNL Profile].

## Lecture d’exemples d’appels API

La documentation de l’API [!DNL Real-Time Customer Profile] fournit des exemples d’appels d’API pour démontrer comment formater correctement les requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

## En-têtes requis

La documentation de l’API exige aussi que vous ayez suivi le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour lancer des appels vers des points d’entrée [!DNL Experience Platform] Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API [!DNL Experience Platform], comme illustré ci-dessous :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes [!DNL Experience Platform] API nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes ayant un payload dans le corps de la requête (notamment les appels POST, PUT et PATCH) doivent comporter un en-tête `Content-Type`. Les valeurs acceptées propres à chaque appel sont fournies dans les paramètres d’appel.

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Real-Time Customer Profile], sélectionnez l’un des guides de point d’entrée disponibles.
