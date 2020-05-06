---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Résolution des problèmes d'assimilation en flux continu
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 0eecd802fc8d0ace3a445f3f188a7f095b97d0c8
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%

---


# Guide de dépannage de l&#39;assimilation en flux continu

Ce document fournit des réponses aux questions fréquentes sur l’assimilation en flux continu sur Adobe Experience Platform. Pour toute question ou dépannage concernant d’autres services de plate-forme, y compris ceux rencontrés sur toutes les API de plate-forme, reportez-vous au guide [de dépannage de](../../landing/troubleshooting.md)la plate-forme d’expérience.

L’administration des données de la plate-forme Adobe Experience Platform fournit des API RESTful que vous pouvez utiliser pour assimiler des données dans la plate-forme Experience. Les données saisies permettent de mettre à jour les profils individuels des clients en temps quasi réel, ce qui vous permet de fournir des expériences personnalisées et pertinentes sur plusieurs canaux. Veuillez lire l&#39;aperçu [de l&#39;](../home.md) importation de données pour plus d&#39;informations sur le service et les différentes méthodes d&#39;assimilation. Pour obtenir des instructions sur l’utilisation des API d’assimilation en flux continu, consultez la présentation [de l’assimilation en](../streaming-ingestion/overview.md)flux continu.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquemment posées sur l’assimilation en flux continu.

### Comment savoir si la charge utile que j’envoie est correctement formatée ?

L’importation de données utilise les schémas du modèle de données d’expérience (XDM) pour valider le format des données entrantes. L’envoi de données non conformes à la structure d’un schéma XDM prédéfini entraîne l’échec de l’assimilation. Pour plus d’informations sur XDM et son utilisation dans la plate-forme d’expérience, voir la présentation [du système](../../xdm/home.md)XDM.

L’assimilation en flux continu prend en charge deux modes de validation : synchrone et asynchrone. Chaque méthode de validation traite différemment les données ayant échoué.

**La validation** synchrone doit être utilisée pendant votre processus de développement. Les enregistrements dont la validation a échoué sont ignorés et renvoient un message d’erreur expliquant pourquoi ils ont échoué (par exemple : &quot;Format de message XDM non valide&quot;).

**La validation** asynchrone doit être utilisée en production. Toute donnée incorrecte non validée est envoyée à Data Lake sous la forme d’un fichier de commandes en échec, où elle peut être récupérée ultérieurement pour analyse ultérieure.

Pour plus d’informations sur la validation synchrone et asynchrone, voir l’aperçu [de la validation en](../quality/streaming-validation.md)flux continu. Pour savoir comment vue les lots dont la validation a échoué, reportez-vous au guide sur la [récupération des lots](../quality/retrieve-failed-batches.md)qui ont échoué.

### Puis-je valider une charge utile de demande avant de l’envoyer à la plate-forme ?

Les charges de demande ne peuvent être évaluées qu’après leur envoi à la plateforme. Lors d’une validation synchrone, les charges utiles valides renvoient des objets JSON renseignés tandis que les charges non valides renvoient des messages d’erreur. Lors de la validation asynchrone, le service détecte et envoie toute donnée incorrecte à Data Lake, où elle peut être récupérée ultérieurement pour analyse. See the [streaming validation overview](../quality/streaming-validation.md) for more information.

### Que se passe-t-il lorsque la validation synchrone est demandée sur un bord qui ne la prend pas en charge ?

Lorsque la validation synchrone n’est pas prise en charge pour l’emplacement demandé, une réponse d’erreur 501 est renvoyée. Pour plus d’informations sur la validation synchrone, consultez la présentation [de la validation](../quality/streaming-validation.md) en flux continu.

### Comment puis-je m&#39;assurer que les données ne sont collectées qu&#39;à partir de sources fiables ?

Experience Platform prend en charge la collecte de données sécurisée. Lorsque la collecte de données authentifiées est activée, les clients doivent envoyer un JSON Web Token (JWT) et leur ID d’organisation IMS en tant qu’en-têtes de demande. Pour plus d&#39;informations sur la manière d&#39;envoyer des données authentifiées à la plate-forme, consultez le guide sur la collecte [de données](../tutorials/create-authenticated-streaming-connection.md)authentifiées.

### Quelle est la latence de la diffusion des données sur le Profil client en temps réel ?

Les événements en flux continu sont généralement reflétés dans le Profil client en temps réel en moins de 60 secondes. Les latences réelles peuvent varier en raison du volume de données, de la taille du message et des limitations de bande passante.

### Puis-je inclure plusieurs messages dans la même demande d’API ?

Vous pouvez regrouper plusieurs messages dans une charge utile de requête unique et les diffuser sur la plateforme. Lorsqu’il est utilisé correctement, le regroupement de plusieurs messages au sein d’une même requête constitue un excellent moyen d’optimiser vos opérations de données. Veuillez lire le tutoriel sur l&#39; [envoi de plusieurs messages dans une demande](../tutorials/streaming-multiple-messages.md) pour plus d&#39;informations.

### Comment savoir si les données que j&#39;envoie sont reçues ?

Toutes les données envoyées à la plate-forme (réussies ou non) sont stockées sous forme de fichiers de commandes avant d’être conservées dans les jeux de données. L&#39;état de traitement des lots s&#39;affiche dans le jeu de données auquel ils ont été envoyés.

Vous pouvez vérifier si les données ont été correctement ingérées en vérifiant l’activité des jeux de données à l’aide de l’interface [utilisateur de la plateforme](https://platform.adobe.com)d’expérience. Cliquez sur **Datasets** dans le volet de navigation de gauche pour afficher une liste de datasets. Sélectionnez le jeu de données auquel vous diffusez en continu à partir de la liste affichée pour ouvrir sa page activité *de* dataset, en affichant tous les lots envoyés au cours d&#39;une période sélectionnée. Pour plus d’informations sur l’utilisation de la plateforme d’expérience pour surveiller les flux de données, voir le guide sur la [surveillance des flux](../quality/monitor-data-flows.md)de données en flux continu.

Si l&#39;importation de vos données a échoué et que vous souhaitez les récupérer à partir de la plate-forme, vous pouvez récupérer les lots en échec en envoyant leurs ID à l&#39;API [d&#39;accès aux][Data Access Service API]données. Pour plus d&#39;informations, consultez le guide sur la [récupération des lots](../quality/retrieve-failed-batches.md) ayant échoué.

### Pourquoi mes données en flux continu ne sont-elles pas disponibles dans Data Lake ?

Il y a plusieurs raisons pour lesquelles l&#39;assimilation par lots peut ne pas atteindre le lac Data, par exemple une mise en forme incorrecte, des données manquantes ou des erreurs système. Pour déterminer pourquoi votre lot a échoué, vous devez récupérer le lot à l&#39;aide de l&#39;API [][Data Ingestion Service] Data Ingestion Service et en vue les détails. Pour obtenir des instructions détaillées sur la récupération d&#39;un lot en échec, consultez le guide sur la [récupération des lots](../quality/retrieve-failed-batches.md)en échec.

### Comment analyser la réponse renvoyée pour la demande d’API ?

Vous pouvez analyser une réponse en commençant par vérifier le code de réponse du serveur afin de déterminer si votre demande a été acceptée. Si un code de réponse réussi est renvoyé, vous pouvez alors examiner l&#39;objet de `responses` tableau pour déterminer l&#39;état de la tâche d&#39;assimilation.

Une requête d’API à message unique réussie renvoie le code d’état 200. Une requête d’API de message par lot réussie (ou partiellement réussie) renvoie le code d’état 207.

Le fichier JSON suivant est un exemple d’objet de réponse pour une requête d’API avec deux messages : une a réussi et une a échoué. Les messages dont le flux est réussi renvoient une `xactionId` propriété. Les messages qui ne sont pas diffusés en continu renvoient une `statusCode` propriété et une réponse `message` contenant plus d’informations.

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

### Pourquoi mes messages envoyés ne sont-ils pas reçus par le Profil client en temps réel ?

Si le Profil client en temps réel rejette un message, il est probable qu’il soit dû à des informations d’identité incorrectes. Cela peut être dû à la fourniture d&#39;une valeur ou d&#39;un espace de nommage non valide pour une identité.

Il existe deux types d&#39;espaces de nommage d&#39;identité : par défaut et personnalisé. Lorsque vous utilisez des espaces de nommage personnalisés, assurez-vous que l&#39;espace de nommage a été enregistré dans Identity Service. Pour plus d&#39;informations sur l&#39;utilisation des espaces de nommage par défaut et personnalisés, consultez la présentation [de l&#39;espace de nommage](../../identity-service/namespaces.md) d&#39;identité.

Vous pouvez utiliser l’interface utilisateur [de la plateforme](https://platform.adobe.com) d’expérience pour afficher plus d’informations sur les raisons pour lesquelles un message a échoué lors de l’assimilation. Cliquez sur **Surveillance** dans le volet de navigation de gauche, puis vue l’onglet _Diffusion en flux continu de bout en bout_ pour afficher les lots de messages diffusés pendant une période sélectionnée.