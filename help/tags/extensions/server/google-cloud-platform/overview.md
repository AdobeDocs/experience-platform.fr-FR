---
title: Extension de transfert d’événements de la plateforme Google Cloud
description: Cette extension de transfert d’événement Adobe Experience Platform envoie des événements Edge Network à Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# Extension de transfert d’événement [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) est une plateforme de cloud computing qui offre un large éventail de services tels que l’informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d’intégration de logiciels en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources de l’entreprise (ERP).

L’extension [!DNL Google Cloud Platform] [ de transfert d’événement](../../../ui/event-forwarding/overview.md) exploite [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) pour envoyer des événements de l’Edge Network Adobe Experience Platform vers le [!DNL Google Cloud Platform] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Google Cloud Platform] avec une rubrique [!DNL Cloud Pub/Sub] existante. Si vous ne disposez pas d’une rubrique préexistante, consultez la documentation [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) sur la création et la gestion des rubriques.

### Créer un secret et un élément de données

Créez tout d&#39;abord un nouveau `Google OAuth 2` [secret de transfert d&#39;événement](../../../ui/event-forwarding/secrets.md), qui sera utilisé pour authentifier la connexion à votre compte tout en gardant la valeur sécurisée.

Ensuite, [créez un élément de données](../../../ui/managing-resources/data-elements.md#create-a-data-element) à l’aide de l’extension **[!UICONTROL Core]** et d’un type d’élément de données **[!UICONTROL Secret]** pour référencer le secret `Google OAuth 2` que vous venez de créer.

## Installation et configuration de l’extension [!DNL Google Cloud Platform] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier à la place.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]** , sélectionnez **[!UICONTROL Installer]** sur la carte de l’extension [!DNL Google Cloud Platform].

![L’extension [!DNL Google Cloud Platform] de catalogue mettant en surbrillance l’installation.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Dans l’écran de configuration, saisissez le secret de l’élément de données que vous avez créé précédemment dans le champ **[!UICONTROL Jeton d’accès]**. Le secret de l’élément de données contiendra votre jeton [!DNL Google Cloud Platform] OAuth 2. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![La page de configuration de l’extension [!DNL Google Cloud Platform].](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Création d’une règle [!DNL Send Data to Cloud Pub/Sub] {#tracking-rule}

Une fois l’extension installée, créez un transfert d’événement [rule](../../../ui/managing-resources/rules.md) et configurez ses conditions selon vos besoins. Lors de la configuration des actions pour la règle, sélectionnez l’extension **[!UICONTROL Google Cloud Platform]**, puis sélectionnez **[!UICONTROL Envoyer les données au Cloud Pub/Sub]** pour le type d’action.

![Vue de configuration de l’action pour [!UICONTROL Google Cloud Platform], avec l’action mise en surbrillance et [!UICONTROL Envoyer des données au Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Topic] | Rubrique qui recevra les événements du transfert d’événement. La valeur doit avoir le format `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] (Données) | Ce champ contient les données à transférer vers la rubrique [!DNL Cloud Pub/Sub] au format JSON.<br><br>Sous l’option **[!UICONTROL Brut]**, vous pouvez coller l’objet JSON directement dans le champ de texte fourni, ou vous pouvez sélectionner l’icône d’élément de données (![Icône Jeu de données](/help/images/icons/database.png)) pour effectuer une sélection dans une liste d’éléments de données existants pour représenter les données.<br><br>Vous pouvez également utiliser l’option **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur via un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |
| [!UICONTROL Attributs] | Ce champ contient l’objet JSON avec des attributs supplémentaires à envoyer avec le message.<br><br>Sous l’option **[!UICONTROL Brut]**, vous pouvez coller l’objet JSON directement dans le champ de texte fourni, ou vous pouvez sélectionner l’icône d’élément de données (![Icône Jeu de données](/help/images/icons/database.png)) pour effectuer une sélection dans une liste d’éléments de données existants pour représenter les données.<br><br>Vous pouvez également utiliser l’option **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur via un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |

{style="table-layout:auto"}

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Cloud Pub/Sub] à l’aide de l’extension de transfert d’événement [!DNL Google Cloud Platform]. Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
