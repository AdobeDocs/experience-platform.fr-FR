---
title: Publication d’une extension
description: Découvrez comment effectuer une publication publique ou privée d’une extension de balise dans Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
TQID: https://experienceleague.adobe.com/QAvAkYBmGV51WG5gvI0LoTJb0V5XYaIew4lEHF7EqS8
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
subfeature_v2:
  - id: ae2cba0e-54f2-464b-a3b3-ad371e8a886a
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 407
ht-degree: 66%

---

# Publication d’une extension

Une fois les tests terminés et la documentation prête, lʼextension est apte à être publiée. Il existe actuellement deux types de publications que vous pouvez exécuter :

- **Publication privée** : l’extension terminée est disponible pour toutes les propriétés de votre société, mais n’est disponible pour aucune autre société d’Adobe Experience Platform.
- **Publication publique** : l’extension terminée est disponible sur le marketplace public pour tous les utilisateurs d’Adobe Experience Platform.

>[!NOTE]
>
>Après avoir publié votre extension, vous ne pouvez plus y apporter de modifications ni annuler sa publication.  Une fois qu’elle est publiée, les correctifs de bug et les ajouts de fonctionnalités sont effectués en `POST`ant une nouvelle version de votre package d’extension et en suivant les étapes de test et de publication ci-dessus sur cette nouvelle version.

Vous devez d’abord publier votre extension en tant qu’extension privée avant de pouvoir la publier publiquement.

## Publication privée

Le moyen le plus simple de publier votre extension en disponibilité privée consiste à utiliser [tag extension releaser](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` vous permet de télécharger et d’exécuter un package npm sans véritablement l’installer sur votre machine. Il s&#39;agit de la méthode la plus simple pour exécuter l&#39;outil de libération.

>[!NOTE]
> Par défaut, l’outil de libération attend des informations d’identification Adobe I/O pour un flux Oauth serveur à serveur. Les informations d> identification de `jwt-auth` héritées peuvent être utilisées en exécutant `npx @adobe/reactor-releaser@v3.1.3` jusqu’à leur obsolescence le 1er janvier 2025. Les paramètres requis >  exécuter la version `jwt-auth` sont disponibles [ici](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

L&#39;outil de libération nécessite que vous ne saisissiez que quelques informations. Les `clientId` et `clientSecret` peuvent être récupérés à partir de la console Adobe I/O. Accédez à la [page Intégrations](https://console.adobe.io/integrations) dans la console I/O. Sélectionnez l’organisation appropriée dans la liste déroulante, recherchez l’intégration appropriée, puis sélectionnez **[!UICONTROL Affichage]**.

- Quel est votre `clientId` ? Copiez et collez-le à partir de la console I/O.
- Quel est votre `clientSecret` ? Copiez et collez-le à partir de la console I/O.

L’outil de libération lira les champs `name` et `platform` de votre manifeste d’extension et demandera à l’API un package d’extension correspondant dans Disponibilité du développement.
L’outil de libération vous demandera ensuite de confirmer qu’il a trouvé le package d’extension correct que vous souhaitez publier pour une disponibilité privée.

Si vous souhaitez publier directement votre extension pour une disponibilité privée à lʼaide de lʼAPI, reportez-vous à lʼexemple dʼappel de [publication privée dʼun package dʼextension](/help/tags/api/endpoints/extension-packages.md#private-release) dans la documentation API pour plus de détails.

## Publication publique

Une fois la publication privée terminée, vous pouvez demander à Adobe de la publier publiquement.  Votre extension sera ainsi disponible dans le catalogue public. Tout utilisateur de la Collecte de données peut installer votre extension sur nʼimporte quelle propriété.

Veuillez remplir le [formulaire de demande de publication publique](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) pour commencer le processus de publication.
