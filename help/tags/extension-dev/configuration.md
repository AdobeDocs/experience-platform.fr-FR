---
title: Configuration d’extension
description: Découvrez comment configurer une extension de balise pour rassembler les paramètres globaux d’un utilisateur dans l’interface utilisateur de collecte de données de Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 64%

---

# Configuration d’extension

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

La configuration d’extension est la manière dont une extension rassemble les paramètres globaux d’un utilisateur. Prenons l’exemple d’une extension qui permet à l’utilisateur d’envoyer une balise à l’aide d’une action Envoyer la balise, la balise devant toujours contenir un identifiant de compte. Nous ne voulons pas troubler les utilisateurs en leur demandant l’identifiant de compte chaque fois qu’ils configurent une action Envoyer la balise. Au lieu de cela, l’extension doit demander une fois l’identifiant de compte à partir de la vue de configuration de l’extension. Chaque fois qu’une balise doit être envoyée, le module Bibliothèque d’action Envoyer la balise peut extraire l’identifiant de compte de la configuration de l’extension et l’ajouter à la balise.

Lorsque les utilisateurs installent une extension sur une propriété de balise dans Adobe Experience Platform, la vue de configuration de l’extension fournie par votre extension s’affiche. Ils ne peuvent pas terminer l’installation de l’extension sans avoir terminé sa configuration. Consultez le document sur les [vues](./web/views.md) pour savoir comment créer une vue pour la configuration de l’extension.

Une fois les paramètres enregistrés à partir d’une vue de configuration de l’extension, ils sont émis dans la bibliothèque du runtime de balises. Vous pouvez ensuite accéder à ces paramètres à partir des modules Bibliothèque d’extension en appelant [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configuration d’extension est une fonction facultative que vous pouvez choisir de ne pas utiliser.
