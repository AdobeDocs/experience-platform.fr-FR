---
title: Configuration d’extension
description: Découvrez comment configurer une extension de balise pour rassembler les paramètres globaux d’un utilisateur dans l’interface utilisateur de Adobe Experience Platform ou l’interface utilisateur de la collecte de données.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 89%

---

# Configurations d’extension

La configuration d’extension est la manière dont une extension rassemble les paramètres globaux d’un utilisateur. Prenons l’exemple d’une extension qui permet à l’utilisateur d’envoyer une balise à l’aide d’une action Envoyer la balise, la balise devant toujours contenir un identifiant de compte. Nous ne voulons pas troubler les utilisateurs en leur demandant l’identifiant de compte chaque fois qu’ils configurent une action Envoyer la balise. Au lieu de cela, l’extension doit demander une fois l’identifiant de compte à partir de la vue de configuration de l’extension. Chaque fois qu’une balise doit être envoyée, le module Bibliothèque d’action Envoyer la balise peut extraire l’identifiant de compte de la configuration de l’extension et l’ajouter à la balise.

Lorsque les utilisateurs installent une propriété de balise dans Adobe Experience Platform, ils reçoivent la vue de configuration d’extension que votre extension fournira. Ils ne peuvent pas terminer l’installation de l’extension sans avoir terminé sa configuration. Consultez le document sur les [vues](./web/views.md) pour savoir comment créer une vue pour la configuration de l’extension.

Une fois les paramètres enregistrés à partir dʼune vue de configuration dʼextension, ils seront émis dans la bibliothèque dʼexécution des balises. Vous pouvez ensuite accéder à ces paramètres à partir des modules Bibliothèque d’extension en appelant [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configuration d’extension est une fonction facultative que vous pouvez choisir de ne pas utiliser.
