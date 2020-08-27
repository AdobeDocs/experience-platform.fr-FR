---
keywords: Experience Platform;home;popular topics;streaming
solution: Experience Platform
title: Dépannage de l’ingestion par flux
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c8e53a25c5b22e8d840658fe26ff47875947a6d0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 69%

---


# Guide de dépannage de l’ingestion par flux

Ce document répond aux questions les plus fréquentes sur l’ingestion par flux sur Adobe Experience Platform. For questions and troubleshooting related to other [!DNL Platform] services, including those that are encountered across all [!DNL Platform] APIs, please refer to the [Experience Platform troubleshooting guide](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] provides RESTful APIs that you can use to ingest data into [!DNL Experience Platform]. Les données ingérées sont utilisées pour mettre à jour les profils clients individuels quasiment en temps réel, ce qui vous permet de proposer des expériences personnalisées et pertinentes sur plusieurs canaux. Pour en savoir plus sur le service et les différentes méthodes d’ingestion, consultez la [présentation de Data Ingestion](../home.md). Pour savoir comment utiliser les API d’ingestion par flux, consultez la [présentation de l’ingestion par flux](../streaming-ingestion/overview.md).

## FAQ

Voici une liste de réponses aux questions fréquentes sur l’ingestion par flux.

### Comment savoir que le payload que j’envoie est correctement formaté ?

[!DNL Data Ingestion] utilise [!DNL Experience Data Model] (XDM) des schémas pour valider le format des données entrantes. L’envoi de données non conformes à la structure d’un schéma XDM prédéfini entraîne l’échec de l’ingestion. For more information on XDM and its use in [!DNL Experience Platform], see the [XDM System overview](../../xdm/home.md).

L’ingestion par flux prend en charge deux modes de validation : synchrone et asynchrone. Chaque méthode de validation gère les données ayant échoué différemment.

La **validation synchrone** doit être utilisée pendant votre processus de développement. Les enregistrements dont la validation a échoué sont ignorés et renvoient un message d’erreur expliquant pourquoi ils ont échoué (par exemple : « Format de message XDM non valide »).

La **validation asynchrone** doit être utilisée en production. Any malformed data that does not pass validation is sent to the [!DNL Data Lake] as a failed batch file, where it can be retrieved later for further analysis.

Pour plus d’informations sur la validation synchrone et asynchrone, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md). Pour savoir comment afficher des lots dont la validation a échoué, reportez-vous au guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

### Puis-je valider un payload de requête avant de l’envoyer à [!DNL Platform]?

Les payloads de requête ne peuvent être évalués qu’après avoir été envoyés à [!DNL Platform]. Lors d’une validation synchrone, les payloads valides renvoient des objets JSON renseignés, tandis que les payloads non valides renvoient des messages d’erreur. During asynchronous validation, the service detects and sends any malformed data to the [!DNL Data Lake] where it can later be retrieved for analysis. Pour plus d’informations, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md).

### Que se passe-t-il lorsque la validation synchrone est demandée sur une périphérie qui ne la prend pas en charge ?

Lorsque la validation synchrone n’est pas prise en charge pour l’emplacement demandé, une réponse d’erreur 501 est renvoyée. Pour plus d’informations sur la validation synchrone, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md).

### Comment puis-je m&#39;assurer que les données ne sont collectées qu&#39;à partir de sources fiables ?

[!DNL Experience Platform] prend en charge la collecte de données sécurisées. Lorsque la collecte de données authentifiées est activée, les clients doivent envoyer un jeton JSON Web Token (JWT) et leur ID d’organisation IMS en tant qu’en-têtes de requête. For more information on how to send authenticated data to [!DNL Platform], please see the guide on [authenticated data collection](../tutorials/create-authenticated-streaming-connection.md).

### What is the latency for streaming data to [!DNL Real-time Customer Profile]?

Streamed events are generally reflected in [!DNL Real-time Customer Profile] in under 60 seconds. Les latences réelles peuvent varier en raison du volume de données, de la taille du message et des limitations de bande passante.

### Puis-je inclure plusieurs messages dans la même requête d’API ?

Vous pouvez regrouper plusieurs messages dans un payload de requête unique et les diffuser sur [!DNL Platform]. Lorsque cette fonctionnalité est utilisée correctement, regrouper plusieurs messages au sein d’une requête unique est une excellente manière d’optimiser vos opérations de données. Pour plus d’informations, lisez le tutoriel sur l’[envoi de plusieurs messages dans une requête](../tutorials/streaming-multiple-messages.md).

### Comment savoir si les données que j’envoie sont reçues ?

All data that is sent to [!DNL Platform] (successfully or otherwise) is stored as batch files before being persisted in datasets. L’état du traitement des lots s’affiche dans le jeu de données dans lequel ils ont été envoyés.

Vous pouvez vérifier si les données ont bien été ingérées en vérifiant l’activité du jeu de données à l’aide de l’[interface utilisateur d’Experience Platform](https://platform.adobe.com). Cliquez sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour afficher une liste de jeux de données. Sélectionnez le jeu de données vers lequel vous effectuez une diffusion par flux à partir de la liste affichée pour ouvrir la page d’*[!UICONTROL activité du jeu de données]*, qui montre tous les lots envoyés au cours d’une période sélectionnée. For more information about using [!DNL Experience Platform] to monitor data streams, see the guide on [monitoring streaming data flows](../quality/monitor-data-flows.md).

If your data failed to ingest and you want to recover it from [!DNL Platform], you can retrieve the failed batches by sending their IDs to the [!DNL Data Access API]. Pour plus d’informations, consultez le guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

### Pourquoi mes données en diffusion continue ne sont-elles pas disponibles dans le lac de données ?

There are a variety of reasons why batch ingestion may fail to reach the [!DNL Data Lake], such as invalid formatting, missing data, or system errors. To determine why your batch failed, you must retrieve the batch using the [!DNL Data Ingestion Service API] and view its details. Pour obtenir des instructions détaillées sur la récupération d’un lot en échec, consultez le guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

### Comment analyser la réponse renvoyée pour la requête d’API ?

Vous pouvez analyser une réponse en vérifiant d’abord le code de réponse du serveur afin de déterminer si votre requête a été acceptée. Si un code de réponse réussie est renvoyé, vous pouvez alors examiner l’objet de tableau `responses` pour déterminer l’état de la tâche d’assimilation.

Une requête d’API à message unique réussie renvoie le code d’état 200. Une requête d’API de message par lot réussie (ou partiellement réussie) renvoie le code d’état 207.

Le fichier JSON suivant est un exemple d’objet de réponse pour une requête d’API avec deux messages : une a réussi et une a échoué. Les messages dont la diffusion continue réussit renvoient une propriété `xactionId`. Les messages dont la diffusion continue échoue renvoient une propriété `statusCode` et une réponse `message` avec plus d’informations.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Why are my sent messages not being received by [!DNL Real-time Customer Profile]?

If [!DNL Real-time Customer Profile] rejects a message, it is most likely due to incorrect identity information. Cela peut être le résultat d’une valeur ou d’un espace de noms d’identité non valide.

Il existe deux types d’espace de noms d’identité : par défaut et personnalisé. Lors de l’utilisation d’espaces de noms personnalisés, assurez-vous que l’espace de noms a été enregistré dans [!DNL Identity Service]. Pour plus d’informations sur l’utilisation des espaces de noms par défaut et personnalisés, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md).

You can use the [[!DNL Experience Platform UI]](https://platform.adobe.com) to see more information on why a message failed ingestion. Cliquez sur **[!UICONTROL Surveillance]** dans le volet de navigation de gauche, puis consultez l’onglet _[!UICONTROL Diffusion en continu de bout en bout]_ pour voir les lots de messages diffusés au cours d’une période sélectionnée.
