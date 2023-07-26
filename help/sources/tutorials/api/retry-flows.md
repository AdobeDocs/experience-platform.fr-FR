---
title: Réessayer les exécutions de flux de données ayant échoué
description: Découvrez comment réessayer les exécutions de flux de données ayant échoué à l’aide de l’API Flow Service.
exl-id: b9abc737-9a57-47e6-98ab-6d6c44f38d17
source-git-commit: d4dba26a151619a555a69287e182ff8398cca7b4
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 38%

---

# Réessayer les exécutions de flux de données ayant échoué

>[!IMPORTANT]
>
>La prise en charge de la nouvelle tentative d’exécutions de flux de données ayant échoué est disponible pour les sources par lots. Vous pouvez uniquement réessayer les exécutions de flux de données qui ont échoué.

Ce tutoriel décrit les étapes à suivre pour tenter de relancer des exécutions de flux de données ayant échoué à l’aide de la méthode [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../home.md)[!DNL Platform] : Experience  permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../sandboxes/home.md)[!DNL Platform] : Experience  fournit des sandbox virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Utiliser les API Platform

Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).

## Reprise d’une exécution de flux de données ayant échoué

Pour réessayer une exécution de flux de données ayant échoué, envoyez une requête de POST à la fonction `/runs` point d’entrée lors de la fourniture de l’identifiant d’exécution de votre flux de données et de la variable `re-trigger` dans le cadre de vos paramètres de requête.

**Format d’API**

```http
POST /runs/{RUN_ID}/action?op=re-trigger
```

| Paramètre | Description |
| --- | --- |
| `{RUN_ID}` | L’identifiant d’exécution qui correspond à l’exécution de flux de données que vous souhaitez réessayer. |
| `op` | Opération qui détermine l’action à effectuer. Pour réessayer une exécution de flux de données ayant échoué, vous devez indiquer `re-trigger` comme votre opération. |

**Requête**

>[!NOTE]
>
>Vous pouvez utiliser la variable `re-trigger` pour essayer de relancer les exécutions de flux de données réussies, étant donné que l’exécution de flux de données réussie ne comporte aucun enregistrement ingéré.

La requête suivante tente de relancer l’exécution du flux de données pour l’ID d’exécution. `4fb0418e-1804-45d6-8d56-dd51f05c0baf`.

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
