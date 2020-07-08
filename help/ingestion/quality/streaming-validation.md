---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Validation de l’assimilation en flux continu
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# Validation de l’assimilation en flux continu

L’assimilation en flux continu vous permet de transférer vos données vers l’Adobe Experience Platform à l’aide de points de terminaison en flux continu en temps réel. Les API d’assimilation en flux continu prennent en charge deux modes de validation : synchrone et asynchrone.

## Prise en main

Ce guide exige une compréhension pratique des éléments suivants de l&#39;Adobe Experience Platform :

- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
- [Ingestion](../streaming-ingestion/overview.md)en flux continu : L&#39;une des méthodes par lesquelles les données peuvent être envoyées à l&#39;Experience Platform.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [façon de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de l’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour passer des appels aux API Platform, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API Experience Platform, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources en Experience Platform, y compris celles appartenant au Registre des Schémas, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes aux API Platform nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : `application/json`

### Couverture de validation

Le service de validation en flux continu couvre la validation dans les domaines suivants :
- Plage
- Présence
- Enum
- Modèle
- Type
- Format

## Validation synchrone

La validation synchrone est une méthode de validation qui fournit des informations immédiates sur les raisons de l’échec de l’assimilation. Cependant, en cas d’échec, les enregistrements dont la validation a échoué sont ignorés et empêchés d’être envoyés en aval. Par conséquent, la validation synchrone ne doit être utilisée que pendant le processus de développement. Lors d’une validation synchrone, les appelants sont informés du résultat de la validation XDM et, en cas d’échec, de la raison de l’échec.

Par défaut, la validation synchrone n’est pas activée. Pour l&#39;activer, vous devez transmettre le paramètre de requête facultatif `synchronousValidation=true` lors des appels d&#39;API. En outre, la validation synchrone n’est actuellement disponible que si votre point de terminaison de flux se trouve sur le centre de données VA7.

Si un message échoue lors de la validation synchrone, il ne sera pas écrit dans la file d’attente de sortie, ce qui fournit des commentaires immédiats aux utilisateurs.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |

**Requête**

Envoyez la demande suivante pour assimiler des données à votre entrée de données avec une validation synchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Corps JSON des données que vous souhaitez importer. |

**Réponse**

Lorsque la validation synchrone est activée, une réponse réussie comprend toutes les erreurs de validation rencontrées dans sa charge utile :

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

La réponse ci-dessus liste combien de violations de schéma ont été constatées et quelles en ont été les violations. Par exemple, cette réponse indique que les clés `workEmail` et `person` n’ont pas été définies dans le schéma et que, par conséquent, elles ne sont pas autorisées. Il indique également la valeur de `_id` comme incorrecte, car le schéma attendait un `string`, mais un `long` a été inséré à la place. Notez qu’une fois cinq erreurs rencontrées, le service de validation **arrête** le traitement de ce message. D&#39;autres messages continueront cependant d&#39;être analysés.

## Validation asynchrone

La validation asynchrone est une méthode de validation qui ne fournit pas de commentaires immédiats. En revanche, les données sont envoyées à un lot en échec dans Data Lake afin d’éviter toute perte de données. Ces données ayant échoué peuvent être récupérées ultérieurement pour une analyse et une relecture ultérieures. Cette méthode doit être utilisée en production. Sauf demande contraire, l’assimilation en flux continu fonctionne en mode de validation asynchrone.

**Format d’API**

```http
POST /collection/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |

**Requête**

Envoyez la demande suivante pour assimiler des données à votre entrée de données avec une validation asynchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Corps JSON des données que vous souhaitez importer. |

>[!NOTE]
>
>Aucun paramètre de requête supplémentaire n’est requis, car la validation asynchrone est activée par défaut.

**Réponse**

Lorsque la validation asynchrone est activée, une réponse positive renvoie les éléments suivants :

```json
{
    "inletId": "f6ca9706d61de3b78be69e2673ad68ab9fb2cece0c1e1afc071718a0033e6877",
    "xactionId": "1555445493896:8600:8",
    "receivedTimeMs": 1555445493932,
    "synchronousValidation": {
        "skipped": true
    }
}
```

Veuillez noter comment la réponse indique que la validation synchrone a été ignorée, car elle n&#39;a pas été explicitement demandée.

## Annexe

Cette section contient des informations sur la signification des différents codes d’état pour les réponses à l’assimilation de données.

### Codes d’état

| Code de statut | Ce que signifie |
| ----------- | ------------- |
| 200 | Succès. Pour une validation synchrone, cela signifie qu’elle a réussi les contrôles de validation. Pour une validation asynchrone, cela signifie qu’il a reçu le message uniquement avec succès. Les utilisateurs peuvent déterminer l’état final du message en observant le jeu de données. |
| 400 | Erreur. Il y a quelque chose qui cloche dans votre demande. Un message d’erreur contenant des détails supplémentaires est reçu des Services de validation en flux continu. |
| 401 | Erreur. Votre demande n&#39;est pas autorisée ; vous devrez la demander avec un jeton de porteur. Pour plus d&#39;informations sur la façon de demander un accès, consultez ce [tutoriel](../../tutorials/authentication.md) ou cet article [de](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)blog. |
| 500 | Erreur. Une erreur système interne s&#39;est produite. |
| 501 | Erreur. Cela signifie que la validation synchrone **n’est pas** prise en charge pour cet emplacement. |
| 503 | Erreur. Le service est actuellement indisponible. Les clients doivent réessayer au moins trois fois en utilisant une stratégie de sauvegarde exponentielle. |