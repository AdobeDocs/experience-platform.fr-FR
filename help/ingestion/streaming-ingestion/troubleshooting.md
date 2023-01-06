---
keywords: Experience Platform;accueil;rubriques les plus consultées;flux;ingestion en flux continu;dépannage;dépannage de l’ingestion en flux continu;faq sur l’ingestion en flux continu;faq;
solution: Experience Platform
title: Guide de dépannage de l’ingestion en flux continu
description: Ce document répond aux questions les plus fréquentes sur l’ingestion par flux sur Adobe Experience Platform.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Guide de dépannage de l’ingestion par flux

Ce document répond aux questions les plus fréquentes sur l’ingestion par flux sur Adobe Experience Platform. Pour les questions et le dépannage liés à d’autres [!DNL Platform] les services, y compris ceux qui sont rencontrés dans tous les [!DNL Platform] API, reportez-vous à la section [Guide de dépannage des Experience Platform](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] fournit des API RESTful que vous pouvez utiliser pour ingérer des données dans [!DNL Experience Platform]. Les données ingérées sont utilisées pour mettre à jour les profils clients individuels quasiment en temps réel, ce qui vous permet de proposer des expériences personnalisées et pertinentes sur plusieurs canaux. Pour en savoir plus sur le service et les différentes méthodes d’ingestion, consultez la [présentation de Data Ingestion](../home.md). Pour savoir comment utiliser les API d’ingestion par flux, consultez la [présentation de l’ingestion par flux](../streaming-ingestion/overview.md).

## FAQ

Voici une liste de réponses aux questions fréquentes sur l’ingestion par flux.

### Comment savoir que le payload que j’envoie est correctement formaté ?

[!DNL Data Ingestion] tire [!DNL Experience Data Model] schémas (XDM) pour valider le format des données entrantes. L’envoi de données non conformes à la structure d’un schéma XDM prédéfini entraîne l’échec de l’ingestion. Pour plus d’informations sur XDM et son utilisation dans [!DNL Experience Platform], reportez-vous à la section [Présentation du système XDM](../../xdm/home.md).

L’ingestion par flux prend en charge deux modes de validation : synchrone et asynchrone. Chaque méthode de validation gère les données ayant échoué différemment.

La **validation synchrone** doit être utilisée pendant votre processus de développement. Les enregistrements dont la validation a échoué sont ignorés et renvoient un message d’erreur expliquant pourquoi ils ont échoué (par exemple : « Format de message XDM non valide »).

La **validation asynchrone** doit être utilisée en production. Toutes les données incorrectes qui ne sont pas validées sont envoyées à la variable [!DNL Data Lake] en tant que fichier de lot en échec, où il peut être récupéré ultérieurement pour une analyse plus approfondie.

Pour plus d’informations sur la validation synchrone et asynchrone, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md). Pour savoir comment afficher des lots dont la validation a échoué, reportez-vous au guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

### Puis-je valider un payload de requête avant de l’envoyer à [!DNL Platform]?

Les payloads de requête ne peuvent être évalués qu’après avoir été envoyés à [!DNL Platform]. Lors d’une validation synchrone, les payloads valides renvoient des objets JSON renseignés, tandis que les payloads non valides renvoient des messages d’erreur. Lors d’une validation asynchrone, le service détecte et envoie toutes les données incorrectes à la variable [!DNL Data Lake] où il pourra être récupéré ultérieurement pour analyse. Pour plus d’informations, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md).

### Que se passe-t-il lorsque la validation synchrone est demandée sur une périphérie qui ne la prend pas en charge ?

Lorsque la validation synchrone n’est pas prise en charge pour l’emplacement demandé, une réponse d’erreur 501 est renvoyée. Pour plus d’informations sur la validation synchrone, consultez la [présentation de la validation de l’ingestion par flux](../quality/streaming-validation.md).

### Comment puis-je m’assurer que les données sont uniquement collectées auprès de sources approuvées ?

[!DNL Experience Platform] prend en charge la collecte de données sécurisée. Lorsque la collecte de données authentifiées est activée, les clients doivent envoyer un jeton JSON Web Token (JWT) et leur ID d’organisation IMS en tant qu’en-têtes de requête. Pour plus d’informations sur la manière d’envoyer des données authentifiées à [!DNL Platform], consultez le guide sur la [collecte de données authentifiées](../tutorials/create-authenticated-streaming-connection.md).

### Quelle est la latence de diffusion des données en continu vers ? [!DNL Real-Time Customer Profile]?

Les événements diffusés en continu sont généralement reflétés dans [!DNL Real-Time Customer Profile] en moins de 60 secondes. Les latences réelles peuvent varier en raison du volume de données, de la taille du message et des limitations de bande passante.

### Puis-je inclure plusieurs messages dans la même requête d’API ?

Vous pouvez regrouper plusieurs messages dans un payload de requête unique et les diffuser sur [!DNL Platform]. Lorsque cette fonctionnalité est utilisée correctement, regrouper plusieurs messages au sein d’une requête unique est une excellente manière d’optimiser vos opérations de données. Pour plus d’informations, lisez le tutoriel sur l’[envoi de plusieurs messages dans une requête](../tutorials/streaming-multiple-messages.md).

### Comment savoir si les données que j’envoie sont reçues ?

Toutes les données envoyées à [!DNL Platform] (réussi ou non) est stocké en tant que fichiers de lot avant d’être conservé dans les jeux de données. L’état du traitement des lots s’affiche dans le jeu de données dans lequel ils ont été envoyés.

Vous pouvez vérifier si les données ont bien été ingérées en vérifiant l’activité du jeu de données à l’aide de l’[interface utilisateur d’Experience Platform](https://platform.adobe.com). Cliquez sur **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour afficher une liste de jeux de données. Sélectionnez le jeu de données vers lequel vous effectuez une diffusion par flux à partir de la liste affichée pour ouvrir la page d’**[!UICONTROL activité du jeu de données]**, qui montre tous les lots envoyés au cours d’une période sélectionnée. Pour plus d’informations sur l’utilisation de [!DNL Experience Platform] pour surveiller les flux de données, consultez le guide sur [surveillance des flux de données en flux continu](../quality/monitor-data-ingestion.md).

Si vos données n’ont pas été ingérées et que vous souhaitez les récupérer [!DNL Platform], vous pouvez récupérer les lots en échec en envoyant leurs identifiants à la variable [!DNL Data Access API]. Pour plus d’informations, consultez le guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

### Pourquoi mes données en diffusion continue ne sont-elles pas disponibles dans le lac de données ?

Plusieurs raisons peuvent expliquer l’échec de l’ingestion par lots à atteindre la variable [!DNL Data Lake], comme une mise en forme non valide, des données manquantes ou des erreurs système. Pour déterminer pourquoi votre lot a échoué, vous devez récupérer le lot à l’aide de la variable [!DNL Data Ingestion Service API] et afficher ses détails. Pour obtenir des instructions détaillées sur la récupération d’un lot en échec, consultez le guide sur la [récupération des lots en échec](../quality/retrieve-failed-batches.md).

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### Pourquoi mes messages envoyés ne sont-ils pas reçus par [!DNL Real-Time Customer Profile]?

If [!DNL Real-Time Customer Profile] rejette un message, probablement en raison d’informations d’identité incorrectes. Cela peut être le résultat d’une valeur ou d’un espace de noms d’identité non valide.

Il existe deux types d’espace de noms d’identité : par défaut et personnalisé. Lors de l’utilisation d’espaces de noms personnalisés, assurez-vous que l’espace de noms a été enregistré dans [!DNL Identity Service]. Pour plus d’informations sur l’utilisation des espaces de noms par défaut et personnalisés, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md).

Vous pouvez utiliser la variable [[!DNL Experience Platform UI]](https://platform.adobe.com) pour afficher plus d’informations sur les raisons de l’échec de l’ingestion d’un message. Cliquez sur **[!UICONTROL Surveillance]** dans le volet de navigation de gauche, puis consultez l’onglet **[!UICONTROL Diffusion en continu de bout en bout]** pour voir les lots de messages diffusés au cours d’une période sélectionnée.
