---
keywords: Experience Platform;accueil;rubriques les plus consultées;streaming;ingestion en flux continu;validation de l’ingestion en flux continu;validation;validation de l’ingestion en flux continu;validation;Validation synchrone;validation synchrone;validation asynchrone;validation asynchrone;
solution: Experience Platform
title: Validation de l’ingestion en flux continu
type: Tutorial
description: 'L’ingestion par flux vous permet de charger vos données dans Adobe Experience Platform à l’aide de points d’entrée en flux continu en temps réel. Les API d’ingestion en flux continu prennent en charge deux modes de validation : synchrone et asynchrone.'
exl-id: 6e9ac943-6d73-44de-a13b-bef6041d3834
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 82%

---

# Validation de l’ingestion en flux continu

L’ingestion par flux vous permet de charger vos données dans Adobe Experience Platform à l’aide de points d’entrée en flux continu en temps réel. Les API d’ingestion en flux continu prennent en charge deux modes de validation : synchrone et asynchrone.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
- [[!DNL Streaming Ingestion]](../streaming-ingestion/overview.md) : l’une des méthodes par lesquelles les données peuvent être envoyées à [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Toutes les ressources d’[!DNL Experience Platform], y compris celles appartenant à l’[!DNL Schema Registry], sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: `application/json`

### Couverture de validation

[!DNL Streaming Validation Service] couvre la validation dans les domaines suivants :

- Plage
- Présence
- Enum
- Modèle
- Type
- Format

## Validation synchrone

La validation synchrone est une méthode de validation qui fournit des commentaires immédiats sur les raisons de l’échec d’une ingestion. Toutefois, en cas d’échec, les enregistrements dont la validation échoue sont ignorés et le système empêche leur envoi en aval. Par conséquent, la validation synchrone ne doit être utilisée que pendant le processus de développement. Lors d’une validation synchrone, les appelants sont informés du résultat de la validation et en cas d’échec, des raisons de cet échec.

La validation synchrone n’est pas activée par défaut. Pour l’activer, vous devez transmettre le paramètre de requête facultatif `syncValidation=true` lorsque vous effectuez des appels API. De plus, la validation synchrone est actuellement disponible uniquement si le point d’entrée de votre flux se trouve sur le centre de données VA7.

>[!NOTE]
>
>Le paramètre de requête `syncValidation` n’est disponible que pour le point d’entrée de message unique et ne peut pas être utilisé pour le point d’entrée par lots.

Si un message échoue au cours de la validation synchrone, le message ne sera pas écrit vers la file d’attente de sortie, qui fournit des commentaires immédiats pour les utilisateurs.

>[!NOTE]
>
>Les modifications de schéma peuvent ne pas être disponibles immédiatement, car elles sont mises en cache. Patientez jusqu’à quinze minutes pour que le cache s’actualise.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?syncValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion en continu que vous avez créée précédemment. |

**Requête**

Envoyez la requête suivante pour ingérer des données vers votre inlet de données grâce à la validation synchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?syncValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Le corps JSON des données que vous souhaitez ingérer. |

**Réponse**

Lorsque la validation synchrone est activée, une réponse réussie inclut toutes les erreurs de validation survenues dans le payload :

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [6aca7aa2d87ebd6b2780ca5724d94324a14475f140a2b69373dd5c714430dfd4] imsOrgId: [7BF122A65C5B3FE40A494026@AdobeOrg] Message is invalid",
        "cause": {
            "_streamingValidation": [
                {
                    "schemaLocation": "#",
                    "pointerToViolation": "#",
                    "causingExceptions": [
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [workEmail] is not permitted"
                        },
                        {
                            "schemaLocation": "#",
                            "pointerToViolation": "#",
                            "causingExceptions": [],
                            "keyword": "additionalProperties",
                            "message": "extraneous key [person] is not permitted"
                        },
                        {
                            "schemaLocation": "#/properties/_id",
                            "pointerToViolation": "#/_id",
                            "causingExceptions": [],
                            "keyword": "type",
                            "message": "expected type: String, found: Long"
                        }
                    ],
                    "message": "3 schema violations found"
                }
            ]
        }
    }
}
```

La réponse ci-dessus répertorie le nombre de violations de schéma et en quoi elles consistaient. Par exemple, cette réponse indique que les clés `workEmail` et `person` n’étaient pas définies dans le schéma et donc non autorisées. Elle marque également la valeur `_id` comme incorrecte, puisque le schéma attendait un `string`, mais qu’un `long` a été inséré à la place. Notez qu’une fois que cinq erreurs sont rencontrées, le service de validation **arrêtera** le traitement de ce message. Les autres messages continueront toutefois à être analysés.

## Validation asynchrone

La validation asynchrone est une méthode de validation qui ne fournit aucun feedback immédiat. Au lieu de cela, les données sont envoyées à un lot en échec [!DNL Data Lake] d’éviter la perte de données. Ces données en échec peuvent être récupérées par la suite pour une analyse et une relecture plus approfondies. Cette méthode est celle qui doit être utilisée en production. Sauf demande contraire, l’ingestion en flux continu fonctionne avec le mode de validation asynchrone.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | La valeur `id` de la connexion en continu que vous avez créée précédemment. |

**Requête**

Envoyez la requête suivante pour ingérer des données vers votre inlet de données grâce à la validation asynchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Le corps JSON des données que vous souhaitez ingérer. |

>[!NOTE]
>
>Aucun paramètre de requête supplémentaire n’est requis, car la validation asynchrone est activée par défaut.

**Réponse**

Lorsque la validation asynchrone est activée, une réponse réussie renvoie les éléments suivants :

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "syncValidation": {
        "skipped": true
    }
}
```

Veuillez noter que la réponse indique que la validation synchrone a été ignorée, car elle n’a pas été explicitement demandée.

## Annexe

Cette section contient des informations relatives à la signification des différents codes d’état pour les réponses d’ingestion de données.

### Codes d’état

| Code d’état | Signification |
| ----------- | ------------- |
| 200 | Réussite. Dans le cas d’une validation synchrone, cela signifie que la réponse a passé les contrôles de validation. Dans le cas d’une validation asynchrone, cela signifie que la réponse a simplement bien reçu le message. Les utilisateurs peuvent identifier l’état du message final en observant le jeu de données. |
| 400 | Erreur. Une erreur s’est produite avec votre demande. Un message d’erreur contenant plus de détails est reçu des services de validation par flux. |
| 401 | Erreur. Votre requête n’est pas autorisée, il vous faudra effectuer la requête avec un jeton porteur. Pour plus d’informations sur la manière de demander l’accès, consultez ce [tutoriel](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) ou cet [article de blog](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f). |
| 500 | Erreur. Une erreur système interne s’est produite. |
| 501 | Erreur. Cela signifie que la validation synchrone n’est **pas** prise en charge pour cet emplacement. |
| 503 | Erreur. Le service est actuellement indisponible. Nous conseillons aux clients de réessayer au moins trois fois en utilisant une stratégie de backoff exponentiel. |
