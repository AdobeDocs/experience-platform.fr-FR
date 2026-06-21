---
title: Extension de transfert d’événement Google Cloud Platform
description: Cette extension de transfert d’événement Adobe Experience Platform envoie des événements Edge Network à Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00.000Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
TQID: https://experienceleague.adobe.com/Tm68ab1d8YeSkWwB2a6-pKVDXfDPilQ3Gy-fubQ-qAM
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 578
ht-degree: 3%

---

# Extension de transfert d’événement [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) est une plateforme de cloud computing qui offre une grande variété de services tels que l&#39;informatique distribuée, le stockage de base de données, la diffusion de contenu et les services d&#39;intégration de logiciel en tant que service (SaaS) pour la gestion de la relation client (CRM) et la planification des ressources d&#39;entreprise (ERP).

L’extension [!DNL Google Cloud Platform] [transfert d’événement](../../../ui/event-forwarding/overview.md) tire parti de [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) pour envoyer des événements de l’Edge Network Adobe Experience Platform au [!DNL Google Cloud Platform] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Google Cloud Platform] avec une rubrique de [!DNL Cloud Pub/Sub] existante. Si vous ne disposez pas d’une rubrique préexistante, consultez la documentation [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) sur la création et la gestion des rubriques.

### Créer un secret et un élément de données

Tout d’abord, créez un `Google OAuth 2` [secret de transfert d’événement](../../../ui/event-forwarding/secrets.md) qui sera utilisé pour authentifier la connexion à votre compte tout en conservant la sécurité de la valeur.

Ensuite, [créez un élément de données](../../../ui/managing-resources/data-elements.md#create-a-data-element) à l’aide de l’extension **[!UICONTROL Core]** et d’un type d’élément de données **[!UICONTROL Secret]** pour référencer le secret de `Google OAuth 2` que vous venez de créer.

## Installation et configuration de l’extension [!DNL Google Cloud Platform] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez plutôt une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]**, sélectionnez **[!UICONTROL Installer]** sur la carte de l’extension [!DNL Google Cloud Platform].

![Extension de [!DNL Google Cloud Platform] de catalogue mettant en surbrillance install.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Dans l’écran de configuration, saisissez le secret de l’élément de données que vous avez créé précédemment dans le champ **[!UICONTROL Jeton d’accès]**. Le secret de l’élément de données contiendra votre jeton OAuth 2 [!DNL Google Cloud Platform]. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![Page de configuration de l’extension [!DNL Google Cloud Platform].](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Créer une règle de [!DNL Send Data to Cloud Pub/Sub] {#tracking-rule}

Une fois l’extension installée, créez une nouvelle [règle](../../../ui/managing-resources/rules.md) de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la configuration des actions pour la règle, sélectionnez l’extension **[!UICONTROL Google Cloud Platform]**, puis sélectionnez **[!UICONTROL Envoyer les données à Cloud Pub/Sub]** pour le type d’action.

![Vue de configuration de l’action pour [!UICONTROL Google Cloud Platform], avec l’action mise en surbrillance et [!UICONTROL Envoyer les données à Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Sujet] | Rubrique qui recevra les événements du transfert d’événement. Le format de la valeur doit être `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Data] (Données) | Ce champ contient les données à transférer à la rubrique [!DNL Cloud Pub/Sub] au format JSON.<br><br>Sous l’option **[!UICONTROL Raw]**, vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![icône de jeu de données](/help/images/icons/database.png)) à sélectionner dans une liste d’éléments de données existants pour représenter les données.<br><br>Vous pouvez également utiliser l’option **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur par le biais d’un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |
| [!UICONTROL &#x200B; Attributs &#x200B;] | Ce champ contient l’objet JSON avec des attributs supplémentaires à envoyer avec le message.<br><br>Sous l’option **[!UICONTROL Raw]**, vous pouvez coller l’objet JSON directement dans le champ de texte fourni ou sélectionner l’icône d’élément de données (![icône de jeu de données](/help/images/icons/database.png)) à sélectionner dans une liste d’éléments de données existants pour représenter les données.<br><br>Vous pouvez également utiliser l’option **[!UICONTROL Éditeur de paires clé-valeur JSON]** pour ajouter manuellement chaque paire clé-valeur par le biais d’un éditeur d’interface utilisateur. Chaque valeur peut être représentée par une entrée brute ou un élément de données peut être sélectionné à la place. |

{style="table-layout:auto"}

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Cloud Pub/Sub] à l’aide de l’extension de transfert d’événement [!DNL Google Cloud Platform]. Pour plus d’informations sur les fonctionnalités de transfert d’événement d’Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
