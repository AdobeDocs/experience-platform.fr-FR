---
description: Cette page explique comment utiliser le point d’entrée de l’API /sample-profiles depuis Destination SDK pour générer des profils types en fonction d’un schéma source. Vous pouvez utiliser ces profils types pour tester votre configuration de destination basée sur des fichiers.
title: Génération de profils types en fonction d’un schéma source
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 93%

---


# Génération de profils types en fonction d’un schéma source

La première étape du test de la destination basée sur les fichiers consiste à utiliser le point d’entrée `/sample-profiles` pour générer un profil type en fonction de votre schéma source existant.

Les profils types peuvent vous aider à comprendre la structure JSON d’un profil. En outre, ils vous donnent une valeur par défaut que vous pouvez personnaliser avec vos propres données de profil pour d’autres tests de destination.

## Prise en main {#getting-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Conditions préalables {#prerequisites}

Avant d’utiliser le point d’entrée `/sample-profiles`, veillez à respecter les conditions suivantes :

* Une destination existante basée sur des fichiers a été créée avec Destination SDK et vous pouvez la voir dans votre [catalogue de destination](../../../ui/destinations-workspace.md).
* Au moins un flux d’activation pour la destination dans l’interface utilisateur d’Experience Platform a été créé. Le point d’entrée `/sample-profiles` crée les profils en fonction du schéma source que vous avez défini dans votre flux d’activation. Pour découvrir comment créer un flux d’activation, regardez le [tutoriel sur l’activation](../../../ui/activate-batch-profile-destinations.md).
* Pour réussir la requête API, vous avez besoin de l’identifiant d’instance de destination correspondant à l’instance de destination que vous allez tester. Obtenez l’identifiant d’instance de destination que vous devez utiliser dans l’appel API, à partir de l’URL, lorsque vous parcourez une connexion avec la destination dans l’interface utilisateur d’Experience Platform.

  ![Image de l’interface utilisateur montrant comment obtenir l’identifiant d’instance de destination à partir de l’URL.](../../assets/testing-api/get-destination-instance-id.png)

## Génération de profils types pour les tests de destination {#generate-sample-profiles}

Vous pouvez générer des profils types en fonction de votre schéma source en adressant une requête GET au point d’entrée `/sample-profiles` avec l’identifiant de l’instance de destination de la destination que vous souhaitez tester.

**Format d’API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Paramètres de requête | Description |
| -------- | ----------- |
| `destinationInstanceId` | L’identifiant de l’instance de destination pour laquelle vous générez des profils types. Pour en savoir plus sur la manière d’obtenir cet identifiant, consultez la section [Conditions préalables](#prerequisites). |
| `count` | *Facultatif*. Nombre de profils types que vous souhaitez générer. Le paramètre peut prendre des valeurs entre `1 - 1000`. Si cette propriété n’est pas définie, l’API génère un seul profil type. |

**Requête**

La requête suivante génère un profil type en fonction du schéma source défini dans l’instance de destination avec l’identifiant `destinationInstanceId` correspondant.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec le nombre spécifié d’échantillons de profils, les appartenances à l’audience, les identités et les attributs de profil qui correspondent au schéma XDM source.

>[!NOTE]
>
> La réponse ne renvoie que les appartenances à l’audience, les identités et les attributs de profil utilisés dans l’instance de destination. Même si votre schéma source comporte d’autres champs, ceux-ci sont ignorés.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![Image montrant le mappage de l’interface utilisateur aux champs à partir de la réponse de l’API.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Propriété | Description |
| -------- | ----------- |
| `segmentMembership` | Objet de mappage décrivant les appartenances à des audiences d’un individu. Pour plus d’informations sur `segmentMembership`, consultez [Détails de l’appartenance à une audience](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Date et heure de la dernière qualification de ce profil pour le segment. |
| `status` | Champ de type chaîne indiquant si l’appartenance à l’audience a été établie dans le cadre de la requête actuelle. Les valeurs suivantes sont acceptées : <ul><li>`realized` : le profil fait partie du segment.</li><li>`exited` : le profil quitte l’audience dans le cadre de la requête actuelle.</li></ul> |
| `identityMap` | Champ de type map qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de noms qui lui sont associés. Pour plus d’informations sur `identityMap`, consultez la [base de la composition des schémas](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment générer des profils types en fonction du schéma source que vous avez configuré dans votre [flux d’activation](../../../ui/activate-batch-profile-destinations.md) de destination.

Vous pouvez désormais personnaliser ces profils ou les utiliser tels qu’ils sont renvoyés par l’API pour [tester votre configuration de destination basée sur des fichiers](file-based-destination-testing-api.md).
