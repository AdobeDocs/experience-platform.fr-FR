---
title: Publication d’une extension
description: Découvrez comment effectuer une publication publique ou privée d’une extension de balise dans Adobe Experience Platform.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 99%

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

Vous devez publier votre extension en tant qu’extension privée avant de pouvoir la publier publiquement.

## Publication privée

Le moyen le plus simple de publier votre extension en disponibilité privée consiste à utiliser lʼoutil [Tag Extension Releaser](https://www.npmjs.com/package/@adobe/reactor-releaser). Vous trouverez davantage d’instructions dans sa documentation.

Si vous souhaitez publier directement votre extension pour une disponibilité privée à lʼaide de lʼAPI, reportez-vous à lʼexemple dʼappel de [publication privée dʼun package dʼextension](../../api/endpoints/extension-packages.md/#private-release) dans la documentation API pour plus de détails.

## Publication publique

Une fois la publication privée terminée, vous pouvez demander à Adobe de la publier publiquement. Votre extension sera ainsi disponible dans le catalogue public. Tout utilisateur de la Collecte de données peut installer votre extension sur nʼimporte quelle propriété.

Veuillez remplir le [formulaire de demande de publication publique](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest) pour commencer le processus de publication.
