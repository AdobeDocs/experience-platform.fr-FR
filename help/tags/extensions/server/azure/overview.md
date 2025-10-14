---
title: Présentation de l’extension Microsoft Azure
description: Découvrez l’extension Microsoft Azure pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 7%

---

# Présentation de l’extension [!DNL Microsoft Azure]

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) est un service d’entrée de données en temps réel hautement évolutif qui vous permet de traiter et d’analyser les quantités massives de données produites par vos appareils et applications connectés. Une fois que les données sont collectées dans un centre d’événements, elles peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou de n’importe quel adapteur de traitement par lot/stockage.

L’extension [!DNL Microsoft Azure] [de transfert d’événement](../../../ui/event-forwarding/overview.md) exploite [!DNL Event Hubs] pour envoyer des événements de l’Edge Network Adobe Experience Platform vers [!DNL Azure] en vue d’un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Azure] valide ayant accès à [!DNL Event Hubs]. Vous devez également [&#x200B; créer un hub d’événements à l’aide du  [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) avant de suivre les étapes ci-dessous.

## Installation l’extension

Pour installer l’extension Microsoft [!DNL Azure], accédez à l’interface utilisateur de collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** . Recherchez la carte [!UICONTROL Microsoft Azure] , puis sélectionnez **[!UICONTROL Installer]**.

![Bouton [!UICONTROL Installer] sélectionné pour l’extension [!UICONTROL Microsoft Azure] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/azure/install.png)

L’extension n’ayant aucune propriété de configuration, elle est immédiatement ajoutée à la liste des extensions installées. Vous pouvez maintenant commencer à utiliser les types d’action [!DNL Event Hub] lors de la configuration des règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Microsoft Azure]** pour l’extension, puis **[!UICONTROL Envoyer les données aux centres d’événements]** pour le type d’action.

![Le type d’action [!UICONTROL Envoyer des données aux centres d’événements] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/azure/select-action-type.png)

Le panneau de droite se met à jour afin d’afficher les options de configuration permettant d’envoyer les données. Plus précisément, vous devez affecter des [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre configuration [!DNL Event Hub].

![&#x200B; Les options de configuration pour le type d’action [!UICONTROL Send Data to Event Hubs] affiché dans l’interface utilisateur.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Détails du hub d’événements]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Espace de noms] | Nom de l’espace de noms [!DNL Event Hubs] que vous avez créé lors de la [configuration du hub d’événements](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nom] | Nom du centre d’événements. |
| [!UICONTROL Nom de la règle d’autorisation SAS] | Nom de la règle d’autorisation d’accès partagée pour l’ensemble de votre espace de noms [!DNL Event Hubs] ou l’instance spécifique du hub d’événements à laquelle vous souhaitez envoyer des données. Pour plus d’informations, reportez-vous à la section de l’annexe sur l’ [obtention des valeurs d’autorisation SAS](#sas) . |
| [!UICONTROL Clé d’accès SAS] | La clé primaire de la règle d’autorisation d’accès partagée pour l’ensemble de votre espace de noms [!DNL Event Hubs] ou l’instance spécifique du hub d’événements à laquelle vous souhaitez envoyer des données. Pour plus d’informations, reportez-vous à la section de l’annexe sur l’ [obtention des valeurs d’autorisation SAS](#sas) . |
| [!UICONTROL ID de partition] | [!DNL Event Hubs] vous permet d&#39; [envoyer des événements directement à des partitions spécifiques](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Pour tirer parti de cette fonctionnalité, fournissez l’identifiant de la partition que vous souhaitez recevoir les événements. |

{style="table-layout:auto"}

**Data** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Charge utile] | Ce champ contient les données qui seront transférées vers le [!DNL Event Hubs]. Les données peuvent être un objet JSON, une chaîne ou un élément de données. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Event Hubs] à l’aide de l’extension de transfert d’événement [!DNL Microsoft Azure]. Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).

## Annexe : Obtention des valeurs d’autorisation SAS {#sas}

Les applications externes se voient accorder l’accès à [!DNL Event Hubs] par le biais de [signatures d’accès partagé (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Chaque instance [!DNL Event Hubs] d’espace de noms et de hub d’événements comporte une règle d’autorisation SAS par défaut automatiquement attribuée lors de la création, mais vous pouvez également créer des stratégies supplémentaires pour chaque ressource, si vous le souhaitez.

Lors de la [configuration d&#39;une règle de transfert d&#39;événement](#rule) à l&#39;aide de l&#39;extension [!DNL Azure], vous devez fournir le nom et la clé primaire de la règle d&#39;autorisation régissant l&#39;espace de noms ou le centre d&#39;événements spécifique auquel vous souhaitez envoyer des données. Pour plus d’informations sur la manière d’obtenir ces valeurs à partir du portail [!DNL Azure], reportez-vous aux sections suivantes de la documentation [!DNL Azure] :

* [Obtenir des valeurs SAS pour un  [!DNL Event Hubs] espace de noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtenir des valeurs SAS pour un hub d’événement spécifique dans un espace de noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Une fois que vous disposez des valeurs requises, le nom de la règle d’autorisation peut être fourni directement sous la forme d’une chaîne dans l’entrée de configuration ou vous pouvez créer un élément de données de type chaîne pour le référencer à la place. Toutefois, la clé primaire doit d’abord être contenue dans un secret de transfert d’événement avant de pouvoir être fournie dans la configuration de la règle afin de protéger votre sécurité des données.

Dans l’interface utilisateur du transfert d’événement, [créez un nouveau secret](../../../ui/event-forwarding/secrets.md) et sélectionnez **[!UICONTROL Jeton]** comme type de secret. Pour la valeur de jeton elle-même, fournissez la clé primaire que vous avez copiée précédemment. Après avoir créé le secret, créez un élément de données de type **[!UICONTROL Secret]** et sélectionnez le secret [!DNL Event Hubs] dans la liste. Une fois l’élément de données secret configuré, vous pouvez référencer cet élément de données dans le champ **[!UICONTROL Clé d’accès SAS]** .
