---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Résolution des problèmes d'assimilation en flux continu
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Guide de dépannage de l&#39;assimilation en flux continu

Ce répond aux questions les plus fréquentes sur l’assimilation en flux continu sur Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services de plateforme, y compris ceux rencontrés sur toutes les API de plateforme, reportez-vous au guide [de dépannage de la plateforme](../../landing/troubleshooting.md)d’expérience.

L’intégration des données d’Adobe Experience Platform fournit des API RESTful que vous pouvez utiliser pour assimiler des données dans Experience Platform. Les données assimilées sont utilisées pour mettre à jour les  de clients en temps quasi réel, ce qui vous permet de proposer des expériences personnalisées et pertinentes sur plusieurs . Veuillez lire l&#39;aperçu [de l&#39;Ingestion des](../home.md) données pour plus d&#39;informations sur le service et les différentes méthodes d&#39;ingestion. Pour savoir comment utiliser les API d’assimilation en flux continu, consultez la présentation [de l’assimilation en](../streaming-ingestion/overview.md)flux continu.

## FAQ

Voici un  de réponses aux questions fréquentes sur l’ingestion en flux continu.

### Comment savoir que la charge utile que j’envoie est correctement formatée ?

L’administration des données utilise le XDM (Experience Data Model) pour valider le format des données entrantes. L’envoi de données non conformes à la structure d’un XDM prédéfini entraîne l’échec de l’assimilation. Pour plus d’informations sur XDM et son utilisation dans Experience Platform, voir Présentation [du système](../../xdm/home.md)XDM.

L’assimilation en flux continu prend en charge deux modes de validation : synchrone et asynchrone. Chaque méthode de validation gère les données ayant échoué différemment.

**La validation** synchrone doit être utilisée pendant votre processus de développement. Les enregistrements dont la validation a échoué sont ignorés et renvoient un message d’erreur expliquant pourquoi ils ont échoué (par exemple : &quot;Format de message XDM non valide&quot;).

**La validation** asynchrone doit être utilisée en production. Toute donnée incorrecte qui n’est pas validée est envoyée à Data Lake sous la forme d’un fichier de commandes en échec, où elle peut être récupérée plus tard pour d’autres  .

Pour plus d’informations sur la validation synchrone et asynchrone, voir l’aperçu [de la validation en](../quality/streaming-validation.md)flux continu. Pour savoir comment des lots qui ne sont pas validés, reportez-vous au guide sur la [récupération des lots](../quality/retrieve-failed-batches.md)ayant échoué.

### Puis-je valider une charge utile de requête avant de l’envoyer à la plateforme ?

Les charges de demande ne peuvent être évaluées qu’après avoir été envoyées à la plateforme. Lors d’une validation synchrone, les charges utiles valides renvoient des objets JSON renseignés, tandis que les charges non valides renvoient des messages d’erreur. Lors d’une validation asynchrone, le service détecte et envoie toutes les données incorrectes au lac Data, où elles peuvent être récupérées ultérieurement pour  . See the [streaming validation overview](../quality/streaming-validation.md) for more information.

### Que se passe-t-il lorsque la validation synchrone est demandée sur un bord qui ne le prend pas en charge ?

Lorsque la validation synchrone n’est pas prise en charge pour l’emplacement demandé, une réponse d’erreur 501 est renvoyée. Pour plus d’informations sur la validation synchrone, consultez l’aperçu [de la validation en](../quality/streaming-validation.md) flux continu.

### Comment authentifier les données envoyées ?

Experience Platform prend en charge la collecte de données sécurisée. Lorsque la collecte de données authentifiées est activée, les clients doivent envoyer un JSON Web Token (JWT) et leur ID d’organisation IMS en tant qu’en-têtes de demande. Pour plus d’informations sur la manière d’envoyer des données authentifiées à Platform, consultez le guide sur la collecte [de données](../tutorials/create-authenticated-streaming-connection.md)authentifiées.

### Quelle est la latence de la diffusion des données en flux continu vers le client en temps réel ?

Les  en flux continu sont généralement reflétées dans le du client en temps réel en moins de 60 secondes. Les latences réelles peuvent varier en raison du volume de données, de la taille du message et des limitations de bande passante.

### Puis-je inclure plusieurs messages dans la même requête d’API ?

Vous pouvez regrouper plusieurs messages dans une charge utile de requête unique et les diffuser sur la plateforme. Lorsqu’il est utilisé correctement, le regroupement de plusieurs messages au sein d’une même requête constitue un excellent moyen d’optimiser vos opérations de données. Veuillez lire le didacticiel sur l&#39; [envoi de plusieurs messages dans une demande](../tutorials/streaming-multiple-messages.md) pour plus d&#39;informations.

### Comment savoir si les données que j&#39;envoie sont reçues ?

Toutes les données envoyées à la plate-forme (avec succès ou autrement) sont stockées sous forme de fichiers par lot avant d’être conservées dans les jeux de données. L’état de traitement des lots s’affiche dans le jeu de données auquel ils ont été envoyés.

Vous pouvez vérifier si les données ont bien été assimilées en vérifiant le jeu de données   à l’aide de l’interface [utilisateur de la plateforme](https://platform.adobe.com)d’expérience. Cliquez sur **Jeu de données** dans le volet de navigation de gauche pour afficher un de jeux de données. Sélectionnez le jeu de données vers lequel vous effectuez une diffusion en continu à partir du  affiché pour ouvrir sa page de  de jeux de *données  de* , en affichant tous les lots envoyés au cours d’une période sélectionnée. Pour plus d’informations sur l’utilisation de la plateforme d’expérience pour surveiller les flux de données, voir le guide sur la [surveillance des flux](../quality/monitor-data-flows.md)de données en flux continu.

Si vos données n’ont pas été assimilées et que vous souhaitez les récupérer à partir de la plateforme, vous pouvez récupérer les lots en échec en envoyant leurs ID à l’API [d’accès aux][Data Access Service API]données. Pour plus d’informations, consultez le guide sur la [récupération des lots](../quality/retrieve-failed-batches.md) ayant échoué.

### Pourquoi mes données en flux continu ne sont-elles pas disponibles dans Data Lake ?

Il existe diverses raisons pour lesquelles l’assimilation par lots peut ne pas atteindre le lac de données, par exemple une mise en forme incorrecte, des données manquantes ou des erreurs système. Pour déterminer pourquoi votre lot a échoué, vous devez récupérer le lot à l’aide de l’API [du service d’][Data Ingestion Service] assimilation des données et  ses détails. Pour obtenir des instructions détaillées sur la récupération d&#39;un lot en échec, consultez le guide sur la [récupération des lots](../quality/retrieve-failed-batches.md)en échec.

### Comment analyser la réponse renvoyée pour la demande d’API ?

Vous pouvez analyser une réponse en vérifiant d’abord le code de réponse du serveur afin de déterminer si votre demande a été acceptée. Si un code de réponse réussi est renvoyé, vous pouvez alors examiner l’objet `responses` du tableau pour déterminer l’état du d’assimilation.

Une requête d’API à message unique réussie renvoie le code d’état 200. Une requête d’API de message par lot réussie (ou partiellement réussie) renvoie le code d’état 207.

Le fichier JSON suivant est un exemple d’objet de réponse pour une requête d’API avec deux messages : une a réussi et une a échoué. Les messages dont le flux continu a réussi à renvoyer une `xactionId` propriété. Les messages qui ne parviennent pas à diffuser en continu renvoient une `statusCode` propriété et une réponse `message` avec plus d’informations.

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

### Pourquoi mes messages envoyés ne sont-ils pas reçus par le de clients en temps réel ?

Si le du client en temps réel rejette un message, il est probable qu’il soit dû à des informations d’identité incorrectes. Cela peut être le résultat d&#39;une valeur non valide ou d&#39;un   d&#39;identité non valide.

Il existe deux types d&#39;identité   : default et custom. Lors de l’utilisation d’ de  personnalisées, assurez-vous que le  a été enregistré dans Identity Service. Pour plus d’informations sur l’utilisation des de  par défaut et personnalisés, reportez-vous à la vue d’ensemble [de l’ d’](../../identity-service/namespaces.md) identité  du.

Vous pouvez utiliser l’interface utilisateur [de la plateforme](https://platform.adobe.com) d’expérience pour afficher plus d’informations sur les raisons pour lesquelles un message a échoué lors de l’assimilation. Cliquez sur **Surveillance** dans le volet de navigation de gauche, puis  l’onglet _Diffusion en flux continu de bout en bout_ pour voir les lots de messages diffusés pendant une période sélectionnée.