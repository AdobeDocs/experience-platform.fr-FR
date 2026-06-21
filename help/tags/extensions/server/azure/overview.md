---
title: Présentation de l’extension Microsoft Azure
description: Découvrez l’extension Microsoft Azure pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00.000Z
TQID: https://experienceleague.adobe.com/TChdA0zKwBpe8oyauafbwWZKgZkPcz6Y4cj76NoCGjw
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: b64298cc-90cc-46b7-8917-ee391f1c7516id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1cid: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d095671a-1355-40aa-8b5f-06c33c68080bid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 940
ht-degree: 1%

---

# Présentation de l’extension [!DNL Microsoft Azure]

En [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) est un service d’entrée de données en temps réel et hautement évolutif qui vous permet de traiter et d’analyser les quantités massives de données produites par vos appareils et applications connectés. Une fois les données collectées dans un centre d’événements, elles peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou adaptateurs de traitement par lots/stockage.

L’extension [!DNL Microsoft Azure] [transfert d’événement](../../../ui/event-forwarding/overview.md) tire parti de [!DNL Event Hubs] pour envoyer des événements de l’Edge Network Adobe Experience Platform à [!DNL Azure] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Azure] valide avec un accès à [!DNL Event Hubs]. Vous devez également [créer un hub d’événements à l’aide du portail [!DNL Azure] ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) avant de suivre les étapes ci-dessous.

## Installation l’extension

Pour installer l’extension Microsoft [!DNL Azure], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Recherchez la vignette [!UICONTROL Microsoft Azure], puis sélectionnez **[!UICONTROL Installer]**.

![Le bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL Microsoft Azure] dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/azure/install.png)

Comme l’extension ne possède aucune propriété de configuration, elle est immédiatement ajoutée à la liste des extensions installées. Vous pouvez maintenant commencer à utiliser des types d’action [!DNL Event Hub] lors de la configuration des règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Microsoft Azure]** pour l’extension, puis sélectionnez **[!UICONTROL Envoyer les données vers les centres d’événements]** pour le type d’action.

Le type d’action [!UICONTROL  Envoyer les données aux concentrateurs d’événements] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/azure/select-action-type.png)![

Le panneau de droite se met à jour pour afficher les options de configuration relatives à la manière dont les données doivent être envoyées. Plus précisément, vous devez attribuer des [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre configuration [!DNL Event Hub].

![les options de configuration du type d’action [!UICONTROL Envoyer des données aux concentrateurs d’événements] affiché dans l’interface utilisateur.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Détails du hub d’événements]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Espace de noms] | Nom de l’espace de noms [!DNL Event Hubs] que vous avez créé lors de la [configuration du hub d’événements](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nom] | Nom du hub d’événements. |
| [!UICONTROL Nom de la règle d’autorisation SAS] | Nom de la règle d’autorisation d’accès partagé pour l’ensemble de l’espace de noms [!DNL Event Hubs] ou pour l’instance Event Hub spécifique à laquelle vous souhaitez envoyer des données. Voir la section annexe sur l’[obtention de valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL  Clé d’accès SAS ] | Clé primaire de la règle d’autorisation d’accès partagé pour l’ensemble de votre espace de noms [!DNL Event Hubs] ou l’instance Event Hub spécifique à laquelle vous souhaitez envoyer des données. Voir la section annexe sur l’[obtention de valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL ID de partition] | [!DNL Event Hubs] vous permet d’[envoyer directement des événements à des partitions spécifiques](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Pour tirer parti de cette fonctionnalité, indiquez l’identifiant de la partition qui doit recevoir les événements. |

{style="table-layout:auto"}

**Data** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Payload] | Ce champ contient les données qui seront transférées au [!DNL Event Hubs]. Les données peuvent être un objet JSON, une chaîne ou un élément de données. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données aux [!DNL Event Hubs] à l’aide de l’extension de transfert d’événement [!DNL Microsoft Azure]. Pour plus d’informations sur les fonctionnalités de transfert d’événement d’Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).

## Annexe : obtention des valeurs d’autorisation SAS {#sas}

Les applications externes se voient accorder l’accès à [!DNL Event Hubs] par le biais de [signatures d’accès partagé (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Chaque espace de noms d’[!DNL Event Hubs] et instance Event Hub dispose d’une règle d’autorisation SAS par défaut automatiquement attribuée lors de sa création, mais vous pouvez également créer des politiques supplémentaires pour chaque ressource si vous le souhaitez.

Lors de la [configuration d’une règle de transfert d’événement](#rule) à l’aide de l’extension [!DNL Azure], vous devez indiquer le nom et la clé primaire de la règle d’autorisation régissant l’espace de noms ou le hub d’événements spécifique auquel vous souhaitez envoyer des données. Pour plus d’informations sur la manière d’obtenir ces valeurs à partir du portail [!DNL Azure], reportez-vous aux sections suivantes de la documentation [!DNL Azure] :

* [Obtention des valeurs SAS pour un espace  [!DNL Event Hubs]  noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtention de valeurs SAS pour un hub d’événements spécifique dans un espace de noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Une fois que vous disposez des valeurs requises, le nom de la règle d’autorisation peut être fourni directement sous la forme d’une chaîne dans l’entrée de configuration ou vous pouvez créer un élément de données de type chaîne pour le référencer à la place. Toutefois, la clé primaire doit d’abord être contenue dans un secret de transfert d’événement avant de pouvoir être fournie dans la configuration de règle afin de protéger la sécurité de vos données.

Dans l’interface utilisateur de transfert d’événement, [créez un secret](../../../ui/event-forwarding/secrets.md) et sélectionnez **[!UICONTROL Jeton]** comme type de secret. Pour la valeur de jeton elle-même, fournissez la clé primaire que vous avez copiée précédemment. Après avoir créé le secret, créez un élément de données avec le type **[!UICONTROL Secret]** et sélectionnez le secret [!DNL Event Hubs] dans la liste. Une fois l’élément de données secret configuré, vous pouvez référencer cet élément de données dans le champ **[!UICONTROL Clé d’accès SAS]**.
