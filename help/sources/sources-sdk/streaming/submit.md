---
title: Test Et Envoi De Votre Source
description: Le document suivant décrit les étapes à suivre pour tester et vérifier une nouvelle source à l’aide de l’API Flow Service et intégrer une nouvelle source par le biais de sources en libre-service (SDK de diffusion en continu).
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 22%

---

# Test et envoi de la source

>[!NOTE]
>
>Le SDK de diffusion en continu des sources en libre-service est en version bêta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Les dernières étapes pour intégrer votre nouvelle source à Adobe Experience Platform à l’aide de sources en libre-service (SDK de diffusion en continu) consistent à tester et à envoyer votre nouvelle source. Une fois que vous avez terminé la spécification de connexion et mis à jour la spécification du flux de diffusion en continu, vous pouvez commencer à tester la fonctionnalité de votre source via l’API ou l’interface utilisateur. En cas de réussite, vous pouvez envoyer votre nouvelle source en contactant votre représentant d’Adobe.

Le document suivant décrit les étapes à suivre pour tester et déboguer votre source à l’aide de l’ [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Commencer

* Pour plus d’informations sur la manière d’effectuer des appels vers les API Platform, consultez le guide [Prise en main des API Platform](../../../landing/api-guide.md).
* Pour plus d’informations sur la génération de vos informations d’identification pour les API Platform, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md).
* Pour plus d’informations sur la configuration de [!DNL Postman] pour les API Platform, consultez le tutoriel sur la [configuration de la console de développement et [!DNL Postman]](../../../landing/postman.md).
* Pour faciliter le processus de test et de débogage, téléchargez la [collecte de vérification des sources en libre-service et l’environnement ici](../assets/sdk-verification.zip) et suivez les étapes décrites ci-dessous.

## Test de votre source à l’aide de l’API

Pour tester votre source à l’aide de l’API, vous devez exécuter la [collecte et environnement de vérification des sources en libre-service](../assets/sdk-verification.zip) sur [!DNL Postman] tout en fournissant les variables d’environnement appropriées qui se rapportent à votre source.

Pour commencer les tests, vous devez d’abord configurer la collection et l’environnement sur [!DNL Postman]. Indiquez ensuite l’identifiant de spécification de connexion que vous souhaitez tester.

>[!NOTE]
>
>Toutes les variables d’exemple ci-dessous sont des valeurs d’espace réservé que vous devez mettre à jour, à l’exception de `flowSpecificationId` et `targetConnectionSpecId`, qui sont des valeurs fixes.

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `x-api-key` | Identifiant unique utilisé pour authentifier les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `x-api-key`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Personne morale pouvant posséder ou accorder une licence pour des produits et des services et permettre l’accès à ses membres. Consultez le tutoriel sur la [configuration de Developer Console et [!DNL Postman]](../../../landing/postman.md) pour obtenir des instructions sur la récupération de vos informations `x-gw-ims-org-id`. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Jeton d’autorisation requis pour terminer les appels vers les API Experience Platform. Pour plus d’informations sur la récupération de votre `authorizationToken`, consultez le tutoriel sur l’ [ authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) . | `Bearer authorizationToken` |
| `schemaId` | Pour que les données sources soient utilisées dans Platform, un schéma cible doit être créé pour structurer les données sources en fonction de vos besoins. Pour obtenir des instructions détaillées sur la création d’un schéma XDM cible, suivez le tutoriel sur la [création d’un schéma à l’aide de l’API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | La version unique qui correspond à votre schéma. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | `meta:altId` renvoyé avec le `schemaId` lors de la création d’un nouveau schéma. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Pour obtenir des instructions détaillées sur la création d’un jeu de données cible, suivez le tutoriel sur la [création d’un jeu de données à l’aide de l’API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Les jeux de mappages peuvent être utilisés pour définir la façon dont les données d’un schéma source sont mappées à celui d’un schéma de destination. Pour obtenir des instructions détaillées sur la création d’un mappage, consultez le tutoriel sur la [création d’un jeu de mappages à l’aide de l’API](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | L’identifiant unique qui correspond à votre jeu de mappages. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | L’identifiant de spécification de connexion qui correspond à votre source. Il s’agit de l’identifiant que vous avez généré après la [création d’une spécification de connexion](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | ID de spécification de flux de `GenericStreamingAEP`. **Il s’agit d’une valeur fixe**. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | L’identifiant de connexion cible du lac de données dans lequel les données ingérées se trouvent. **Il s’agit d’une valeur fixe**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Intervalle de temps désigné à suivre lors de la vérification de la fin d’une exécution de flux. | `40` |
| `startTime` | Heure de début désignée pour votre flux de données. L’heure de début doit être formatée en heure unique. | `1597784298` |

Une fois que vous avez fourni toutes vos variables d’environnement, vous pouvez commencer à exécuter la collection à l’aide de l’interface [!DNL Postman]. Dans l’interface [!DNL Postman], sélectionnez les ellipses (**...**) en regard de [!DNL Sources SSSs Verification Collection], puis sélectionnez **Exécuter la collection**.

![runner](../assets/runner.png)

L’interface [!DNL Runner] s’affiche, vous permettant de configurer l’ordre d’exécution de votre flux de données. Sélectionnez **Exécuter la collection de vérification SSS** pour exécuter la collection.

>[!NOTE]
>
>Vous pouvez désactiver la **suppression du flux** de la liste de contrôle de l’ordre d’exécution si vous préférez utiliser le tableau de bord de surveillance des sources dans l’interface utilisateur de Platform. Cependant, une fois le test terminé, vous devez vous assurer que vos flux de test sont supprimés.

![run-collection](../assets/run-collection.png)

## Test de votre source à l’aide de l’interface utilisateur

Pour tester votre source dans l’interface utilisateur, accédez au catalogue des sources de l’environnement de test de votre entreprise dans l’interface utilisateur de Platform. À partir de là, votre nouvelle source devrait apparaître sous la catégorie *Diffusion en continu*.

Maintenant que votre nouvelle source est disponible dans votre environnement de test, vous devez suivre le processus des sources pour tester les fonctionnalités. Pour commencer, sélectionnez **[!UICONTROL Configurer]**.

![Catalogue de sources affichant la nouvelle source de diffusion en continu.](../assets/testing/catalog-test.png)

L’étape [!UICONTROL Ajouter les données] apparaît. Pour vérifier que votre source peut diffuser des données en continu, utilisez le côté gauche de l’interface pour télécharger [un exemple de données JSON](../assets/testing/raw.json.zip). Une fois vos données chargées, le côté droit de l’interface se met à jour en un aperçu de la hiérarchie de fichiers de vos données. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![L’étape d’ajout de données dans le processus des sources où vous pouvez charger et prévisualiser vos données avant l’ingestion.](../assets/testing/add-data-test.png)

La page [!UICONTROL Détails du flux de données] vous permet de choisir si vous souhaitez utiliser un jeu de données existant ou un nouveau jeu de données. Au cours de ce processus, vous pouvez également configurer vos données à ingérer dans Profile, et activer des paramètres tels que [!UICONTROL Diagnostic d’erreur] et [!UICONTROL Ingestion partielle].

Pour les tests, sélectionnez **[!UICONTROL Nouveau jeu de données]** et indiquez un nom de jeu de données de sortie. Au cours de cette étape, vous pouvez également fournir une description facultative pour ajouter des informations supplémentaires à votre jeu de données. Sélectionnez ensuite un schéma à mapper à l’aide de l’option [!UICONTROL Recherche avancée] ou en faisant défiler la liste des schémas existants dans le menu déroulant. Une fois que vous avez sélectionné un schéma, saisissez un nom et une description pour votre flux de données.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données dans le flux de production des sources.](../assets/testing/dataflow-details-test.png)

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [guide de l’interface utilisateur de la préparation des données](../../../data-prep/ui/mapping.md)

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](../assets/testing/mapping-test.png)

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le nom de votre compte, le type de source et d’autres informations diverses spécifiques à la source de stockage dans le cloud en continu que vous utilisez.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données et le schéma cible que vous utilisez pour votre flux de données.

Une fois que vous avez vérifié votre flux de données, sélectionnez **[!UICONTROL Terminer]** et patientez quelques instants le temps que le flux de données soit créé.

![L’étape de révision du workflow des sources.](../assets/testing/review-test.png)

Enfin, vous devez récupérer le point de terminaison de diffusion en continu de votre flux de données. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform. Pour récupérer votre point de terminaison de diffusion en continu, accédez à la page [!UICONTROL Activité Flux de données] du flux de données que vous venez de créer et copiez le point de terminaison depuis le bas du panneau [!UICONTROL Propriétés].

![Le point d’entrée de diffusion en continu dans l’activité de flux de données.](../assets/testing/endpoint-test.png)

## Envoyer votre source

Une fois que votre source a pu terminer l’ensemble du processus, vous pouvez contacter votre représentant d’Adobe et envoyer votre source pour intégration à d’autres organisations Experience Platform.
