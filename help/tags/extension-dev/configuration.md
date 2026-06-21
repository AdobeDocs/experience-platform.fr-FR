---
title: Configuration d’extension
description: Découvrez comment configurer une extension de balise pour rassembler les paramètres globaux d’un utilisateur dans l’interface utilisateur de Adobe Experience Platform ou l’interface utilisateur de la collecte de données.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
TQID: https://experienceleague.adobe.com/lW8Mmn8baFACD38UIgN-lmjuCZBjmapOZOudjl6xogc
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 229
ht-degree: 89%

---

# Configurations d’extension

La configuration d’extension est la manière dont une extension rassemble les paramètres globaux d’un utilisateur. Prenons l’exemple d’une extension qui permet à l’utilisateur d’envoyer une balise à l’aide d’une action Envoyer la balise, la balise devant toujours contenir un identifiant de compte. Nous ne voulons pas troubler les utilisateurs en leur demandant l’identifiant de compte chaque fois qu’ils configurent une action Envoyer la balise. Au lieu de cela, l’extension doit demander une fois l’identifiant de compte à partir de la vue de configuration de l’extension. Chaque fois qu’une balise doit être envoyée, le module Bibliothèque d’action Envoyer la balise peut extraire l’identifiant de compte de la configuration de l’extension et l’ajouter à la balise.

Lorsque les utilisateurs installent une propriété de balise dans Adobe Experience Platform, ils reçoivent la vue de configuration d’extension que votre extension fournira. Ils ne peuvent pas terminer l’installation de l’extension sans avoir terminé sa configuration. Consultez le document sur les [vues](./web/views.md) pour savoir comment créer une vue pour la configuration de l’extension.

Une fois les paramètres enregistrés à partir dʼune vue de configuration dʼextension, ils seront émis dans la bibliothèque dʼexécution des balises. Vous pouvez ensuite accéder à ces paramètres à partir des modules Bibliothèque d’extension en appelant [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configuration d’extension est une fonction facultative que vous pouvez choisir de ne pas utiliser.
