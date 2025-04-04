---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Envoyer votre Source
description: Le document suivant décrit les étapes à suivre pour tester et vérifier une nouvelle source à l’aide de l’API Flow Service et intégrer une nouvelle source par le biais de sources en libre-service (SDK par lots).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 10%

---

# Envoyer votre source

La dernière étape de l’intégration de votre nouvelle source à Adobe Experience Platform à l’aide de sources en libre-service (SDK par lots) consiste à tester votre source à des fins de vérification. Une fois l’opération réussie, vous pouvez envoyer votre nouvelle source en contactant votre représentant Adobe.

Le document suivant décrit les étapes à suivre pour tester et déboguer votre source à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

* Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Experience Platform, consultez le guide [Prise en main des API Experience Platform](../../../landing/api-guide.md).
* Pour plus d’informations sur la génération de vos informations d’identification pour les API Experience Platform, consultez le tutoriel sur l’[authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
* Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Experience Platform, consultez le tutoriel sur [configuration de Developer Console et  [!DNL Postman]](../../../landing/postman.md).
* Pour faciliter votre processus de test et de débogage, téléchargez ici l’environnement et la collection de vérification des sources en libre-service [](../assets/sdk-verification.zip) et suivez les étapes décrites ci-dessous.

## Tester votre source

Pour tester votre source, vous devez exécuter la [collection de vérification et l’environnement des sources en libre-service](../assets/sdk-verification.zip) sur [!DNL Postman] tout en fournissant les variables d’environnement appropriées qui se rapportent à votre source.

Pour commencer les tests, vous devez d’abord configurer la collection et l’environnement sur [!DNL Postman]. Indiquez ensuite l’identifiant de spécification de connexion à tester.

### Spécifier des `authSpecName`

Une fois que vous avez saisi votre identifiant de spécification de connexion, vous devez spécifier le `authSpecName` que vous utilisez pour votre connexion de base. Selon votre choix, il peut s’agir de `OAuth 2 Refresh Code` ou de `Basic Authentication`. Une fois que vous avez spécifié votre `authSpecName`, vous devez inclure ses informations d’identification requises dans votre environnement. Par exemple, si vous spécifiez `authSpecName` comme `OAuth 2 Refresh Code`, vous devez fournir les informations d’identification requises pour OAuth 2, à savoir `host` et `accessToken`.

### Spécifier des `sourceSpec`

Une fois vos paramètres de spécification d’authentification ajoutés, vous devez ajouter les propriétés requises à partir de votre spécification source. Les propriétés requises se trouvent dans `sourceSpec.spec.properties`. Dans le cas de l’exemple de [!DNL MailChimp Members] ci-dessous, la seule propriété requise est `listId`, ce qui signifie `listId` et sa valeur d’identifiant correspondante pour votre environnement de [!DNL Postman].

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Une fois vos paramètres d’authentification et de spécification de source fournis, vous pouvez commencer à renseigner le reste de vos variables d’environnement, voir le tableau ci-dessous pour référence :

>[!NOTE]
>
>Toutes les variables d’exemple ci-dessous sont des valeurs d’espace réservé que vous devez mettre à jour, à l’exception de `flowSpecificationId` et `targetConnectionSpecId`, qui sont des valeurs fixes.

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `x-api-key` | Identifiant unique utilisé pour authentifier les appels aux API Experience Platform. Pour plus d’informations sur la récupération de vos `x-api-key`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Entité d’entreprise pouvant posséder des produits et services ou en obtenir la licence et permettre l’accès à ses membres. Consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations de `x-gw-ims-org-id`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Jeton d’autorisation requis pour effectuer des appels vers les API Experience Platform. Pour plus d’informations sur la récupération de vos `authorizationToken`, consultez le tutoriel sur [l’authentification et l’accès aux API Experience Platform](../../../landing/api-authentication.md). | `Bearer authorizationToken` |
| `schemaId` | Pour que les données sources soient utilisées dans Experience Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Version unique correspondant à votre schéma. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Le `meta:altId` renvoyé avec le `schemaId` lors de la création d’un schéma. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Les jeux de mappages peuvent être utilisés pour définir la façon dont les données d’un schéma source sont mappées à celui d’un schéma de destination. Pour obtenir des instructions détaillées sur la création d’un mappage, consultez le tutoriel sur la [création d’un jeu de mappages à l’aide de l’API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Identifiant unique qui correspond à votre jeu de mappages. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Identifiant de spécification de connexion correspondant à votre source. Il s’agit de l’identifiant que vous avez généré après [création d’une spécification de connexion](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Identifiant de spécification de flux de `RestStorageToAEP`. **Il s’agit d’une valeur fixe**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | Identifiant de connexion cible du lac de données où se trouvent les données ingérées. **Il s’agit d’une valeur fixe**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalle de temps désigné à suivre lors de la vérification de la fin d’une exécution de flux. | `40` |
| `startTime` | Heure de début désignée pour votre flux de données. L&#39;heure de début doit être au format horaire unix. | `1597784298` |

Une fois que vous avez fourni toutes vos variables d’environnement, vous pouvez commencer à exécuter la collection à l’aide de l’interface [!DNL Postman]. Dans l’interface [!DNL Postman], sélectionnez les points de suspension (**...**) à côté de [!DNL Sources SSSs Verification Collection], puis sélectionnez **Exécuter la collection**.

![runner](../assets/runner.png)

L’interface [!DNL Runner] s’affiche, vous permettant de configurer l’ordre d’exécution de votre flux de données. Sélectionnez **Exécuter la collecte de vérification SSS** pour exécuter la collecte.

>[!NOTE]
>
>Vous pouvez désactiver le **flux de suppression** de la liste de contrôle de l’ordre d’exécution si vous préférez utiliser le tableau de bord de surveillance des sources dans l’interface utilisateur d’Experience Platform. Cependant, une fois les tests terminés, vous devez vous assurer que vos flux de test sont supprimés.

![run-collection](../assets/run-collection.png)

## Envoyer votre source

Une fois que votre source est en mesure de terminer l’ensemble du workflow, vous pouvez contacter votre représentant Adobe et envoyer votre source pour intégration.
