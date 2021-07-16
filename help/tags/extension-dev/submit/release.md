---
title: Publication d’une extension
description: Découvrez comment publier publiquement ou en privé une extension de balise dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 58%

---

# Publication d’une extension

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une fois les tests et la documentation terminés, l’extension est prête à être publiée. Il existe actuellement deux types de publications que vous pouvez exécuter :

- **Publication privée** : l’extension terminée est disponible pour toutes les propriétés de votre société, mais n’est disponible pour aucune autre société d’Adobe Experience Platform.
- **Publication** publique : L’extension terminée est disponible sur le marché public pour tous les utilisateurs de Adobe Experience Platform.

>[!NOTE]
>
>Une fois que vous avez publié votre extension, vous ne pouvez plus y apporter de modifications et vous ne pouvez plus la dépublier.  Une fois qu’elle est publiée, les correctifs de bug et les ajouts de fonctionnalités sont effectués en `POST`ant une nouvelle version de votre package d’extension et en suivant les étapes de test et de publication ci-dessus sur cette nouvelle version.

Vous devez publier votre extension en tant qu’extension privée avant de pouvoir la publier publiquement.

## Publication privée

Le moyen le plus simple de publier votre extension avec une disponibilité privée est d’utiliser l’[lanceur d’extension de balise](https://www.npmjs.com/package/@adobe/reactor-releaser). Vous trouverez davantage d’instructions dans sa documentation.

Si vous souhaitez publier directement votre extension avec une disponibilité privée à l’aide de l’API, reportez-vous à l’exemple d’appel de [publication privée d’un package d’extension](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) dans la documentation API pour plus de détails.

## Publication publique

Une fois la publication privée terminée, vous pouvez demander à Adobe de la publier publiquement. Votre extension sera ainsi disponible dans le catalogue public. Tout utilisateur de la collecte de données peut installer votre extension sur n’importe quelle propriété.

Veuillez remplir le [formulaire de demande de publication publique](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) pour commencer le processus de publication.
