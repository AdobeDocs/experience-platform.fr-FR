---
title: Publication d’une extension
description: Découvrez comment effectuer une publication publique ou privée d’une extension de balise dans Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 67%

---

# Publication d’une extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une fois les tests terminés et la documentation prête, lʼextension est apte à être publiée. Il existe actuellement deux types de publications que vous pouvez exécuter :

- **Publication privée** : l’extension terminée est disponible pour toutes les propriétés de votre société, mais n’est disponible pour aucune autre société d’Adobe Experience Platform.
- **Publication publique** : l’extension terminée est disponible sur le marketplace public pour tous les utilisateurs d’Adobe Experience Platform.

>[!NOTE]
>
>Après avoir publié votre extension, vous ne pouvez plus y apporter de modifications ni annuler sa publication.  Une fois qu’elle est publiée, les correctifs de bug et les ajouts de fonctionnalités sont effectués en `POST`ant une nouvelle version de votre package d’extension et en suivant les étapes de test et de publication ci-dessus sur cette nouvelle version.

Vous devez d’abord publier votre extension en tant qu’extension privée avant qu’elle ne puisse être publiée publiquement.

## Publication privée

Le moyen le plus simple de publier votre extension avec une disponibilité privée est d’utiliser le [lanceur de publication d’extension de balise](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` vous permet de télécharger et d’exécuter un package npm sans véritablement l’installer sur votre machine. Il s’agit de la manière la plus simple d’exécuter l’outil de libération.

>[!NOTE]
> Par défaut, le créateur attend des informations d’identification d’Adobe I/O pour un flux Oauth serveur à serveur. Informations d’identification `jwt-auth` héritées
> peut être utilisé en exécutant `npx @adobe/reactor-releaser@v3.1.3` jusqu’à son abandon le 1er janvier 2025. Paramètres requis
> pour exécuter la version `jwt-auth`, vous trouverez [ici](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

L’outil de publication vous demande de ne saisir que quelques informations. Les `clientId` et `clientSecret` peuvent être récupérés à partir de la console Adobe I/O. Accédez à la [page Intégrations](https://console.adobe.io/integrations) dans la console I/O. Sélectionnez lʼorganisation adéquate dans la liste déroulante puis recherchez lʼintégration appropriée et cliquez sur **[!UICONTROL Afficher]**.

- Qu’est-ce que votre `clientId` ? Copiez et collez-le à partir de la console I/O.
- Qu’est-ce que votre `clientSecret` ? Copiez et collez-le à partir de la console I/O.

L’auteur lira les champs `name` et `platform` de votre manifeste d’extension et interrogera l’API pour obtenir un package d’extension correspondant dans la disponibilité du développement.
L’auteur de la version vous demande ensuite de confirmer qu’il a trouvé le package d’extension correct que vous souhaitez publier pour une disponibilité privée.

Si vous souhaitez publier directement votre extension pour une disponibilité privée à lʼaide de lʼAPI, reportez-vous à lʼexemple dʼappel de [publication privée dʼun package dʼextension](../../api/endpoints/extension-packages.md/#private-release) dans la documentation API pour plus de détails.

## Publication publique

Une fois la publication privée terminée, vous pouvez demander à Adobe de la publier publiquement. Votre extension sera ainsi disponible dans le catalogue public. Tout utilisateur de la Collecte de données peut installer votre extension sur nʼimporte quelle propriété.

Veuillez remplir le [formulaire de demande de publication publique](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) pour commencer le processus de publication.
