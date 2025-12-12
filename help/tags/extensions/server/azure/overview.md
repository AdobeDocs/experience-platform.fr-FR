---
title: Présentation de l’extension Microsoft Azure
description: Découvrez l’extension Microsoft Azure pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 2%

---

# Présentation de l’extension [!DNL Microsoft Azure]

En [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) est un service d’entrée de données en temps réel et hautement évolutif qui vous permet de traiter et d’analyser les quantités massives de données produites par vos appareils et applications connectés. Une fois les données collectées dans un centre d’événements, elles peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou adaptateurs de traitement par lots/stockage.

L’extension [!DNL Microsoft Azure] [transfert d’événement](../../../ui/event-forwarding/overview.md) tire parti de [!DNL Event Hubs] pour envoyer des événements de l’Edge Network Adobe Experience Platform à [!DNL Azure] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Azure] valide avec un accès à [!DNL Event Hubs]. Vous devez également [créer un hub d’événements à l’aide du portail [!DNL Azure] ](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) avant de suivre les étapes ci-dessous.

## Installation l’extension

Pour installer l’extension Microsoft [!DNL Azure], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Event Forwarding]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalog]** . Recherchez la carte [!UICONTROL Microsoft Azure], puis sélectionnez **[!UICONTROL Install]**.

![Le bouton [!UICONTROL Install] sélectionné pour l’extension [!UICONTROL Microsoft Azure] dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/azure/install.png)

Comme l’extension ne possède aucune propriété de configuration, elle est immédiatement ajoutée à la liste des extensions installées. Vous pouvez maintenant commencer à utiliser des types d’action [!DNL Event Hub] lors de la configuration des règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Microsoft Azure]** pour l’extension, puis sélectionnez **[!UICONTROL Send Data to Event Hubs]** pour le type d’action.

![Type d’action [!UICONTROL Send Data to Event Hubs] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/azure/select-action-type.png)

Le panneau de droite se met à jour pour afficher les options de configuration relatives à la manière dont les données doivent être envoyées. Plus précisément, vous devez attribuer des [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre configuration [!DNL Event Hub].

![les options de configuration du type d’action [!UICONTROL Send Data to Event Hubs] affiché dans l’interface utilisateur.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Namespace] | Nom de l’espace de noms [!DNL Event Hubs] que vous avez créé lors de la [configuration du hub d’événements](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | Nom du hub d’événements. |
| [!UICONTROL SAS Authorization Rule Name] | Nom de la règle d’autorisation d’accès partagé pour l’ensemble de l’espace de noms [!DNL Event Hubs] ou pour l’instance Event Hub spécifique à laquelle vous souhaitez envoyer des données. Voir la section annexe sur l’[obtention de valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL SAS Access Key] | Clé primaire de la règle d’autorisation d’accès partagé pour l’ensemble de votre espace de noms [!DNL Event Hubs] ou l’instance Event Hub spécifique à laquelle vous souhaitez envoyer des données. Voir la section annexe sur l’[obtention de valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] vous permet d’[envoyer directement des événements à des partitions spécifiques](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Pour tirer parti de cette fonctionnalité, indiquez l’identifiant de la partition qui doit recevoir les événements. |

{style="table-layout:auto"}

**Data** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Payload] | Ce champ contient les données qui seront transférées au [!DNL Event Hubs]. Les données peuvent être un objet JSON, une chaîne ou un élément de données. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Keep Changes]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous convient, sélectionnez **[!UICONTROL Save to Library]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données aux [!DNL Event Hubs] à l’aide de l’extension de transfert d’événement [!DNL Microsoft Azure]. Pour plus d’informations sur les fonctionnalités de transfert d’événement d’Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).

## Annexe : obtention des valeurs d’autorisation SAS {#sas}

Les applications externes se voient accorder l’accès à [!DNL Event Hubs] par le biais de [signatures d’accès partagé (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Chaque espace de noms d’[!DNL Event Hubs] et instance Event Hub dispose d’une règle d’autorisation SAS par défaut automatiquement attribuée lors de sa création, mais vous pouvez également créer des politiques supplémentaires pour chaque ressource si vous le souhaitez.

Lors de la [configuration d’une règle de transfert d’événement](#rule) à l’aide de l’extension [!DNL Azure], vous devez indiquer le nom et la clé primaire de la règle d’autorisation régissant l’espace de noms ou le hub d’événements spécifique auquel vous souhaitez envoyer des données. Pour plus d’informations sur la manière d’obtenir ces valeurs à partir du portail [!DNL Azure], reportez-vous aux sections suivantes de la documentation [!DNL Azure] :

* [Obtention des valeurs SAS pour un espace  [!DNL Event Hubs]  noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtenir des valeurs SAS pour un hub d’événements spécifique dans un espace de noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Une fois que vous disposez des valeurs requises, le nom de la règle d’autorisation peut être fourni directement sous la forme d’une chaîne dans l’entrée de configuration ou vous pouvez créer un élément de données de type chaîne pour le référencer à la place. Toutefois, la clé primaire doit d’abord être contenue dans un secret de transfert d’événement avant de pouvoir être fournie dans la configuration de règle afin de protéger la sécurité de vos données.

Dans l’interface utilisateur de transfert d’événement, [créez un secret](../../../ui/event-forwarding/secrets.md) et sélectionnez **[!UICONTROL Token]** comme type de secret. Pour la valeur de jeton elle-même, fournissez la clé primaire que vous avez copiée précédemment. Après avoir créé le secret, créez un élément de données avec le type **[!UICONTROL Secret]** et sélectionnez le secret [!DNL Event Hubs] dans la liste. Une fois l’élément de données secret configuré, vous pouvez référencer cet élément de données dans le champ **[!UICONTROL SAS Access Key]** .
