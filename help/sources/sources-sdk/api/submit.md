---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Envoyer votre source (bêta)
topic-legacy: overview
description: Le document suivant décrit les étapes à suivre pour tester et vérifier une nouvelle source à l’aide de l’API Flow Service et intégrer une nouvelle source via le SDK Sources.
hide: true
hidefromtoc: true
source-git-commit: 274784a5b82d12497f7437fdeaf665dd64224c2d
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 3%

---

# Envoyer votre source (bêta)

>[!IMPORTANT]
>
>Le SDK Sources est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Les fonctionnalités décrites dans cette documentation peuvent faire l’objet de modifications.

La dernière étape de l’intégration de votre nouvelle source à Adobe Experience Platform à l’aide de [!DNL Sources SDK] est destiné à tester votre source pour vérification. Une fois l’opération terminée, vous pouvez envoyer votre nouvelle source en contactant votre représentant Adobe.

Le document suivant décrit les étapes à suivre pour tester et déboguer votre source à l’aide du [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Prise en main

* Pour plus d’informations sur la manière d’effectuer avec succès des appels vers les API Platform, consultez le guide sur [Prise en main des API Platform](../../../landing/api-guide.md).
* Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
* Pour plus d’informations sur la configuration [!DNL Postman] pour les API Platform, consultez le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md).
* Pour faciliter le processus de test et de débogage, téléchargez la [[!DNL Sources SDK] collecte et environnement de vérification ici](../assets/sdk-verification.zip) et suivez les étapes décrites ci-dessous.

## Test de votre source

Pour tester votre source, vous devez exécuter la variable [[!DNL Sources SDK] collecte et environnement de vérification](../assets/sdk-verification.zip) on [!DNL Postman] tout en fournissant les variables d’environnement appropriées qui se rapportent à votre source.

Pour commencer le test, vous devez d’abord configurer la collection et l’environnement sur [!DNL Postman]. Indiquez ensuite l’identifiant de spécification de connexion que vous souhaitez tester. Cet identifiant doit être le même que celui généré à l’aide de la variable [!DNL Sources SDK].

### Spécifiez les `authSpecName`

Une fois que vous avez saisi votre identifiant de spécification de connexion, vous devez alors spécifier la variable `authSpecName` que vous utilisez pour votre connexion de base. Selon votre choix, il peut s’agir de `OAuth 2 Refresh Code` ou  `Basic Authentication`. Une fois que vous avez spécifié votre `authSpecName`, vous devez ensuite inclure les informations d’identification requises dans votre environnement. Par exemple, si vous spécifiez `authSpecName` as `OAuth 2 Refresh Code`, vous devez ensuite fournir les informations d’identification requises pour OAuth 2, qui sont `host` et `accessToken`.

### Spécifiez les `sourceSpec`

Une fois vos paramètres de spécification d’authentification ajoutés, vous devez ajouter les propriétés requises de votre spécification source. Vous trouverez les propriétés requises dans `sourceSpec.spec.properties`. Dans le cas de la fonction [!DNL MailChimp Members] exemple ci-dessous, la seule propriété requise est `listId`, ce qui signifie `listId` et qu’il s’agit de la valeur d’identifiant correspondante à votre [!DNL Postman] environnement.

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

Une fois les paramètres d’authentification et de spécification source fournis, vous pouvez commencer à renseigner le reste des variables d’environnement. Voir le tableau ci-dessous à titre de référence :

>[!NOTE]
>
>Toutes les variables d’exemple ci-dessous sont des valeurs d’espace réservé que vous devez mettre à jour, à l’exception de `flowSpecificationId` et `targetConnectionSpecId`, qui sont des valeurs fixes.

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `x-api-key` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Voir le tutoriel sur [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la manière de récupérer votre `x-gw-ims-org-id` informations. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Voir le tutoriel sur [authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour plus d’informations sur la manière de récupérer votre `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Pour que les données source soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données source en fonction de vos besoins. Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, consultez le tutoriel sur [création d’un schéma à l’aide de l’API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La version unique qui correspond à votre schéma. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Le `meta:altId` qui est renvoyé avec le  `schemaId` lors de la création d’un nouveau schéma. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, consultez le tutoriel sur [création d’un jeu de données à l’aide de l’API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Les jeux de mappages peuvent être utilisés pour définir la façon dont les données d’un schéma source sont mappées à celui d’un schéma de destination. Pour obtenir des instructions détaillées sur la création d’un mappage, consultez le tutoriel sur [création d’un jeu de mappages à l’aide de l’API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | L’identifiant unique qui correspond à votre jeu de mappages. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | L’identifiant de spécification de connexion qui correspond à votre source. Il s’agit de l’identifiant que vous avez généré après [création d’une nouvelle spécification de connexion](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | L’identifiant de spécification de flux de `RestStorageToAEP`. **Il s’agit d’une valeur fixe**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | L’identifiant de connexion cible du lac de données dans lequel les données ingérées se trouvent. **Il s’agit d’une valeur fixe**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalle de temps désigné à suivre lors de la vérification de la fin d’une exécution de flux. | `40` |
| `startTime` | Heure de début désignée pour votre flux de données. L’heure de début doit être formatée en heure unique. | `1597784298` |

Une fois que vous avez fourni toutes vos variables d’environnement, vous pouvez commencer à exécuter la collection à l’aide de la variable [!DNL Postman] . Dans le [!DNL Postman] , sélectionnez les ellipses (**...**) en regard de [!DNL Sources SSSs Verification Collection] puis sélectionnez **Exécution de la collection**.

![coureur](../assets/runner.png)

Le [!DNL Runner] s’affiche, ce qui vous permet de configurer l’ordre d’exécution de votre flux de données. Sélectionner **Exécution de la collection de vérification SSS** pour exécuter la collection.

>[!NOTE]
>
>Vous pouvez désactiver **Supprimer le flux** dans la liste de contrôle de l’ordre d’exécution si vous préférez utiliser le tableau de bord de surveillance des sources dans l’interface utilisateur de Platform. Cependant, une fois le test terminé, vous devez vous assurer que vos flux de test sont supprimés.

![run-collection](../assets/run-collection.png)

## Envoyer votre source

Une fois que votre source a pu terminer l’ensemble du workflow, vous pouvez contacter votre représentant d’Adobe et envoyer votre source pour l’intégration.