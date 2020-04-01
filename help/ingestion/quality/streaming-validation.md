---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Validation de l’assimilation en flux continu
topic: overview
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Validation de l’assimilation en flux continu

L’assimilation en flux continu vous permet de télécharger vos données vers Adobe Experience Platform à l’aide de points de fin de flux continu en temps réel. Les API d’assimilation en flux continu prennent en charge deux modes de validation : synchrone et asynchrone.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

- [Système](../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
- [Ingestion](../streaming-ingestion/overview.md)en flux continu : L’une des méthodes par lesquelles les données peuvent être envoyées à la plateforme d’expérience.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience, y compris celles appartenant au Registre des  d’, sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../sandboxes/home.md)sandbox.

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

La validation synchrone est une méthode de validation qui fournit des commentaires immédiats sur les raisons de l’échec de l’assimilation. Toutefois, en cas d’échec, les enregistrements dont la validation échoue sont ignorés et empêchés d’être envoyés en aval. Par conséquent, la validation synchrone ne doit être utilisée que pendant le processus de développement. Lors d’une validation synchrone, les appelants sont informés du résultat de la validation XDM et, en cas d’échec, de la raison de l’échec.

Par défaut, la validation synchrone n’est pas activée. Pour l’activer, vous devez transmettre le paramètre facultatif  `synchronousValidation=true` lors des appels d’API. En outre, la validation synchrone n’est actuellement disponible que si votre point de fin de flux se trouve dans le centre de données VA7.

Si un message échoue lors de la validation synchrone, il n’est pas écrit dans la file d’attente de sortie, ce qui fournit des commentaires immédiats aux utilisateurs.

**Format API**

```http
POST /collection/{CONNECTION_ID}?synchronousValidation=true
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |

**Requête**

Envoyez la requête suivante pour assimiler des données à votre entrée de données avec une validation synchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID}?synchronousValidation=true \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Corps JSON des données que vous souhaitez importer. |

**Réponse**

Lorsque la validation synchrone est activée, une réponse réussie inclut toutes les erreurs de validation survenues dans sa charge utile :

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

La réponse ci-dessus  combien de  violations ont été découvertes et quelles étaient les violations. Par exemple, cette réponse indique que les clés `workEmail` et `person` n’étaient pas définies dans le  de et ne sont donc pas autorisées. Il indique également la valeur de `_id` comme étant incorrecte, car le attendait un `string`, mais un `long` a été inséré à la place. Notez qu’une fois cinq erreurs rencontrées, le service de validation **arrête** le traitement de ce message. D&#39;autres messages continueront toutefois d&#39;être analysés.

## Validation asynchrone

La validation asynchrone est une méthode de validation qui ne fournit aucun retour immédiat. En revanche, les données sont envoyées à un lot en échec dans Data Lake afin d’éviter toute perte de données. Ces données ayant échoué peuvent être récupérées ultérieurement pour   et relecture supplémentaires. Cette méthode doit être utilisée en production. Sauf demande contraire, l’assimilation en flux continu fonctionne dans un asynchrone.

**Format API**

```http
POST /collection/{CONNECTION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | Valeur `id` de la connexion de flux continu précédemment créée. |

**Requête**

Envoyez la requête suivante pour assimiler des données à votre entrée de données avec une validation asynchrone :

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H "Content-Type: application/json" \
  -d '{JSON_PAYLOAD}'
```

| Paramètre | Description |
| --------- | ----------- |
| `{JSON_PAYLOAD}` | Corps JSON des données que vous souhaitez importer. |

>[!NOTE] Aucun paramètre  supplémentaire n’est requis, car la validation asynchrone est activée par défaut.

**Réponse**

Lorsque la validation asynchrone est activée, une réponse réussie renvoie les éléments suivants :

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

Veuillez noter que la réponse indique que la validation synchrone a été ignorée, car elle n&#39;a pas été explicitement demandée.

## Annexe

Cette section contient des informations sur la signification des différents codes d’état pour les réponses à l’assimilation de données.

### Codes d’état

| Code d’état | Ce que ça veut dire |
| ----------- | ------------- |
| 200 | Succès. Pour la validation synchrone, cela signifie qu’il a réussi les contrôles de validation. Pour une validation asynchrone, cela signifie qu’il a reçu le message uniquement avec succès. Les utilisateurs peuvent connaître l’état final du message en observant le jeu de données. |
| 400 | Erreur. Il y a quelque chose qui cloche dans ta demande. Un message d’erreur contenant des détails supplémentaires est reçu des services de validation en flux continu. |
| 401 | Erreur. Votre demande est non autorisée - vous devrez demander avec un jeton de porteur. Pour plus d&#39;informations sur la demande d&#39;accès, consultez ce [didacticiel](../../tutorials/authentication.md) ou ce billet [de](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)blog. |
| 500 | Erreur. Erreur système interne. |
| 501 | Erreur. Cela signifie que la validation synchrone **n’est pas** prise en charge pour cet emplacement. |
| 503 | Erreur. Le service est actuellement indisponible. Les clients doivent réessayer au moins trois fois en utilisant une stratégie de sauvegarde exponentielle. |