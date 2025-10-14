---
title: Réessayer les exécutions de flux de données ayant échoué
description: Découvrez comment réessayer les exécutions de flux de données ayant échoué à l’aide de l’API Flow Service.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 11%

---

# Réessayer les exécutions de flux de données ayant échoué

>[!IMPORTANT]
>
>La prise en charge de nouvelles tentatives d’exécutions de flux de données ayant échoué est disponible pour les sources par lots. Vous pouvez uniquement réessayer les exécutions de flux de données ayant échoué.

Ce tutoriel décrit les étapes à suivre pour réessayer les exécutions de flux de données ayant échoué à l’aide de l’API [[!DNL Flow Service] &#x200B;](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform].
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance de [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utilisation des API Experience Platform

Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).

## Réessayer une exécution de flux de données ayant échoué

Pour réessayer une exécution de flux de données ayant échoué, envoyez une requête POST au point d’entrée `/runs` et indiquez l’identifiant d’exécution de votre flux de données et l’opération `re-trigger` dans les paramètres de votre requête.

**Format d’API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Paramètre | Description |
| --- | --- |
| `{RUN_ID}` | Identifiant d’exécution correspondant à l’exécution du flux de données que vous souhaitez réessayer. |
| `op` | Opération qui détermine l’action à effectuer. Pour réessayer une exécution de flux de données ayant échoué, vous devez spécifier `re-trigger` comme opération. |

**Requête**

>[!NOTE]
>
>Vous pouvez également utiliser l’opération `re-trigger` pour réessayer les exécutions de flux de données réussies, étant donné que l’exécution réussie du flux de données ne comporte aucun enregistrement ingéré.

La requête suivante tente à nouveau l’exécution du flux de données pour l’ID d’exécution `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs/4fb0418e-1804-45d6-8d56-dd51f05c0baf/action?op=re-trigger' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
```

**Réponse**

Une réponse réussie renvoie un identifiant d’exécution de flux nouvellement créé et sa version d’etag correspondante.

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "etag": "\"1100c53e-0000-0200-0000-627138980000\""
}
```
