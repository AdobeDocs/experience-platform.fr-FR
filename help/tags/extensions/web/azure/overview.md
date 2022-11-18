---
title: Présentation de l’extension Microsoft Azure
description: Découvrez l’extension Microsoft Azure pour le transfert d’événement dans Adobe Experience Platform.
source-git-commit: 64ab9c0fb4d6fa5e3204ad9a6bb0961b7d475ab7
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 7%

---

# [!DNL Microsoft Azure] présentation de l’extension

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) est un service d’entrée de données en temps réel hautement évolutif qui vous permet de traiter et d’analyser les quantités massives de données produites par vos appareils et applications connectés. Une fois que les données sont collectées dans un centre d’événements, elles peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou de n’importe quel adapteur de traitement/stockage par lot.

Le [!DNL Microsoft Azure] [transfert d’événement](../../../ui/event-forwarding/overview.md) les leviers d’extension [!DNL Event Hubs] pour envoyer des événements depuis Adobe Experience Platform Edge Network vers [!DNL Azure] pour un traitement ultérieur. Ce guide explique comment installer l’extension et utiliser ses fonctionnalités dans une règle de transfert d’événement.

## Conditions préalables

Pour utiliser cette extension, vous devez disposer d’un [!DNL Azure] compte avec accès à [!DNL Event Hubs]. Vous devez également [créez un hub d’événements à l’aide de la fonction [!DNL Azure] Portail](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) avant de suivre les étapes ci-dessous.

## Installer l’extension

Pour installer Microsoft [!DNL Azure] , accédez à l’interface utilisateur de la collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Catalogue]** . Recherchez le [!UICONTROL Microsoft Azure] carte, puis sélectionnez **[!UICONTROL Installer]**.

![Le [!UICONTROL Installer] sélectionné pour l’option [!UICONTROL Microsoft Azure] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/azure/install.png)

L’extension n’ayant aucune propriété de configuration, elle est immédiatement ajoutée à la liste des extensions installées. Vous pouvez maintenant commencer à utiliser [!DNL Event Hub] types d’action lors de la configuration des règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Microsoft Azure]** pour l’extension, puis sélectionnez **[!UICONTROL Envoi de données aux centres d’événements]** pour le type d’action .

![Le [!UICONTROL Envoi de données aux centres d’événements] type d’action sélectionné pour une règle dans l’interface utilisateur de la collecte de données.](../../../images/extensions/azure/select-action-type.png)

Le panneau de droite se met à jour afin d’afficher les options de configuration permettant d’envoyer les données. Plus précisément, vous devez affecter [éléments de données](../../../ui/managing-resources/data-elements.md) aux différentes propriétés qui représentent votre [!DNL Event Hub] configuration.

![Les options de configuration de la variable [!UICONTROL Envoi de données aux centres d’événements] type d’action affiché dans l’interface utilisateur.](../../../images/extensions/azure/event-hub-details.png)

**[!UICONTROL Détails de la plateforme d’événements]**

| Entrée | Description |
| --- | --- |
| [!UICONTROL Espace de noms] | Nom de la variable [!DNL Event Hubs] espace de noms que vous avez créé lors de la [configuration du centre d’événements](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nom] | Nom du centre d’événements. |
| [!UICONTROL Nom de la règle d’autorisation SAS] | Nom de la règle d’autorisation d’accès partagé pour l’ensemble de votre [!DNL Event Hubs] ou l’instance de hub d’événements spécifique à laquelle vous souhaitez envoyer des données. Voir la section de l’annexe sur [Obtention des valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL Clé d’accès SAS] | La clé Principale de la règle d’autorisation d’accès partagé pour l’ensemble de votre [!DNL Event Hubs] ou l’instance de hub d’événements spécifique à laquelle vous souhaitez envoyer des données. Voir la section de l’annexe sur [Obtention des valeurs d’autorisation SAS](#sas) pour plus d’informations. |
| [!UICONTROL ID de partition] | [!DNL Event Hubs] vous permet de [envoyer des événements directement à des partitions spécifiques ;](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Pour tirer parti de cette fonctionnalité, fournissez l’identifiant de la partition que vous souhaitez recevoir les événements. |

{style=&quot;table-layout:auto&quot;}

**Data** (Données)

| Entrée | Description |
| --- | --- |
| [!UICONTROL Payload] | Ce champ contient les données qui seront transférées à la variable [!DNL Event Hubs]. Les données peuvent être un objet JSON, une chaîne ou un élément de données. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle. Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Étapes suivantes

Ce guide explique comment envoyer des données à [!DNL Event Hubs] en utilisant la variable [!DNL Microsoft Azure] extension de transfert d’événement. Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).

## Annexe : Obtention des valeurs d’autorisation SAS {#sas}

Les applications externes ont accès à [!DNL Event Hubs] through [signatures d’accès partagé (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Chaque [!DNL Event Hubs] une règle d’autorisation SAS par défaut est automatiquement affectée à la création de l’instance d’espace de noms et de hub d’événements, mais vous pouvez également créer des stratégies supplémentaires pour chaque ressource, si vous le souhaitez.

When [configuration d’une règle de transfert d’événement](#rule) en utilisant la variable [!DNL Azure] , vous devez indiquer le nom et la clé Principale de la règle d’autorisation qui régit l’espace de noms ou le centre d’événements spécifique auquel vous souhaitez envoyer des données. Pour plus d’informations sur la manière d’obtenir ces valeurs auprès de la variable [!DNL Azure] Portal, reportez-vous aux sections suivantes du [!DNL Azure] documentation :

* [Obtention de valeurs SAS pour une [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obtention de valeurs SAS pour un centre d’événements spécifique dans un espace de noms](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Une fois que vous disposez des valeurs requises, le nom de la règle d’autorisation peut être fourni directement sous la forme d’une chaîne dans l’entrée de configuration ou vous pouvez créer un élément de données de type chaîne pour le référencer à la place. Toutefois, la clé Principale doit d’abord être contenue dans un secret de transfert d’événement avant de pouvoir être fournie dans la configuration de la règle afin de protéger votre sécurité des données.

Dans l’interface utilisateur du transfert d’événement, [créer un nouveau secret](../../../ui/event-forwarding/secrets.md) et sélectionnez **[!UICONTROL Jeton]** comme type secret. Pour la valeur de jeton elle-même, fournissez la clé Principale que vous avez copiée précédemment. Après avoir créé le secret, créez un élément de données avec le type **[!UICONTROL Secret]** et sélectionnez la variable [!DNL Event Hubs] secret de la liste. Une fois l’élément de données secret configuré, vous pouvez le référencer dans la variable **[!UICONTROL Clé d’accès SAS]** champ .
