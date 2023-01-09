---
title: Présentation de l’extension de l’API Meta Conversions
description: Découvrez l’extension de l’API Meta Conversions pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 1%

---

# [!DNL Meta Conversions API] présentation de l’extension

Le [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) vous permet de connecter vos données marketing côté serveur à [!DNL Meta] des technologies permettant d’optimiser le ciblage de vos publicités, de réduire le coût par action et de mesurer les résultats. Les événements sont liés à un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) Les identifiants et sont traités de la même manière que les événements côté client.

En utilisant la variable [!DNL Meta Conversions API] , vous pouvez tirer parti des fonctionnalités de l’API dans votre [transfert d’événement](../../../ui/event-forwarding/overview.md) règles d’envoi de données à [!DNL Meta] à partir du réseau Adobe Experience Platform Edge. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans un transfert d’événement. [règle](../../../ui/managing-resources/rules.md).

## Conditions préalables

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] et le [!DNL Conversions API] partager et envoyer les mêmes événements du côté client et du côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par [!DNL Meta Pixel]. Avant d’installer le [!DNL Conversions API] , consultez le guide sur la [[!DNL Meta Pixel] extension](../../client/meta/overview.md) pour savoir comment l’intégrer dans vos implémentations de balises côté client.

>[!NOTE]
>
>La section sur [déduplication des événements](#deduplication) plus loin, ce document décrit les étapes à suivre pour s’assurer que le même événement n’est pas utilisé deux fois, car il peut être reçu à la fois du navigateur et du serveur.

Pour utiliser la variable [!DNL Conversions API] , vous devez avoir accès au transfert d’événement et disposer d’un [!DNL Meta] compte avec accès à [!DNL Ad Manager] et [!DNL Event Manager]. Plus précisément, vous devez copier l’identifiant d’un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (ou [créer [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) ) afin que l’extension puisse être configurée sur votre compte.

## Installation l’extension

Pour installer le [!DNL Meta Conversions API] , accédez à l’interface utilisateur de la collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Catalogue]** . Recherchez le [!UICONTROL API des conversions de métadonnées] carte, puis sélectionnez **[!UICONTROL Installer]**.

![Le [!UICONTROL Installer] sélectionné pour l’option [!UICONTROL API des conversions de métadonnées] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir la variable [!DNL Pixel] ID que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou vous pouvez utiliser un élément de données à la place.

Vous devez également fournir un jeton d’accès pour utiliser la variable [!DNL Conversions API] spécifiquement. Reportez-vous à la section [!DNL Conversions API] documentation sur [génération d’un jeton d’accès](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) pour savoir comment obtenir cette valeur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![Le [!DNL Pixel] ID fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/server/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Configurer une règle de transfert d’événement {#rule}

Cette section explique comment utiliser la variable [!DNL Conversions API] dans une règle générique de transfert d’événement. En pratique, vous devez configurer plusieurs règles afin d&#39;envoyer toutes les règles acceptées [événements standard](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] et [!DNL Conversions API].

>[!NOTE]
>
>Les événements doivent être [envoyé en temps réel](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou aussi près que possible du temps réel pour une meilleure optimisation des campagnes publicitaires.

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Extension de l’API Meta Conversions]** pour l’extension, puis sélectionnez **[!UICONTROL Envoi de l’événement d’API de conversion]** pour le type d’action.

![Le [!UICONTROL Envoyer la page vue] type d’action sélectionné pour une règle dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/meta/select-action.png)

Les commandes qui s’affichent vous permettent de configurer les données d’événement qui seront envoyées à [!DNL Meta] via le [!DNL Conversions API]. Ces options peuvent être saisies directement dans les entrées fournies. Vous pouvez également sélectionner des éléments de données existants pour représenter les valeurs à la place. Les options de configuration sont divisées en quatre sections principales, comme indiqué ci-dessous.

| Section de configuration | Description |
| --- | --- |
| [!UICONTROL Paramètres d’événement du serveur] | Informations générales sur l’événement, notamment l’heure à laquelle il s’est produit et l’action source qui l’a déclenché. Reportez-vous à la section [!DNL Meta] documentation destinée aux développeurs pour plus d’informations sur le [paramètres d’événement standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) accepté par le [!DNL Conversions API].<br><br>Si vous utilisez les deux [!DNL Meta Pixel] et le [!DNL Conversions API] pour envoyer des événements, veillez à inclure une **[!UICONTROL Nom de l’événement]** (`event_name`) et **[!UICONTROL Identifiant d’événement]** (`event_id`) avec chaque événement, car ces valeurs sont utilisées pour [déduplication des événements](#deduplication).<br><br>Vous avez également la possibilité de **[!UICONTROL Activer l’utilisation limitée de données]** pour vous aider à vous conformer aux désinscriptions des clients. Voir [!DNL Conversions API] documentation sur [options de traitement des données](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) pour plus d’informations sur cette fonctionnalité. |
| [!UICONTROL Paramètres des informations client] | Données d’identité utilisateur utilisées pour attribuer l’événement à un client. Certaines de ces valeurs doivent être hachées avant d’être envoyées à l’API.<br><br>Pour garantir une bonne connexion API commune et une qualité d’événement élevée, il est recommandé d’envoyer tous les [paramètres d’informations client acceptés](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) à côté des événements de serveur. Ces paramètres doivent également être [Priorisés en fonction de leur importance et de leur impact sur l&#39;QE](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Données personnalisées] | Données supplémentaires à utiliser pour l’optimisation de la diffusion publicitaire, fournies sous la forme d’un objet JSON. Reportez-vous à la section [[!DNL Conversions API] documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) pour plus d’informations sur les propriétés acceptées pour cet objet.<br><br>Si vous envoyez un événement d’achat, vous devez utiliser cette section pour fournir les attributs requis. `currency` et `value`. |
| [!UICONTROL Événement de test] | Cette option permet de vérifier si votre configuration entraîne la réception d’événements de serveur par [!DNL Meta] comme prévu. Pour utiliser cette fonctionnalité, sélectionnez la variable **[!UICONTROL Envoyer en tant qu’événement de test]** , puis fournissez un code d’événement de test de votre choix dans l’entrée ci-dessous. Une fois la règle de transfert d’événement déployée, si vous avez configuré correctement l’extension et l’action, les activités apparaissant dans la variable **[!DNL Test Events]** afficher dans [!DNL Meta Events Manager]. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle.

![[!UICONTROL Conserver les modifications] sélectionné pour la configuration de l’action.](../../../images/extensions/server/meta/keep-changes.png)

Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Déduplication des événements {#deduplication}

Comme indiqué dans la section [section conditions préalables](#prerequisites), il est recommandé d’utiliser les [!DNL Meta Pixel] l’extension de balise et la variable [!DNL Conversions API] extension de transfert d’événement pour envoyer les mêmes événements du client et du serveur dans une configuration redondante. Cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par une extension ou une autre.

Si vous envoyez différents types d’événements du client et du serveur sans chevauchement entre les deux, la déduplication n’est pas nécessaire. Cependant, si un événement unique est partagé par les deux [!DNL Meta Pixel] et le [!DNL Conversions API], vous devez vous assurer que ces événements redondants sont dédupliqués afin que vos rapports ne soient pas affectés négativement.

Lors de l’envoi d’événements partagés, veillez à inclure un identifiant et un nom d’événement avec chaque événement que vous envoyez à partir du client et du serveur. Lorsque plusieurs événements portant le même ID et le même nom sont reçus, [!DNL Meta] utilise automatiquement plusieurs stratégies pour les dédupliquer et conserver les données les plus pertinentes. Voir [!DNL Meta] documentation sur [déduplication pour [!DNL Meta Pixel] et [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) pour plus d’informations sur ce processus.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL Meta] en utilisant la variable [!DNL Meta Conversions API] extension . À partir de là, il est recommandé d’étendre votre intégration en connectant plus [!DNL Pixels] et partager d’autres événements, le cas échéant. L’une des actions suivantes peut vous aider à améliorer davantage les performances de votre publicité :

* Connecter une autre [!DNL Pixels] qui ne sont pas encore connectés à un [!DNL Conversions API] intégration.
* Si vous envoyez certains événements exclusivement par [!DNL Meta Pixel] côté client, envoyez ces mêmes événements au [!DNL Conversions API] du côté serveur également.

Voir [!DNL Meta] documentation sur [bonnes pratiques pour la [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) pour plus d’informations sur la mise en oeuvre efficace de votre intégration. Pour plus d’informations sur les balises et le transfert d’événement dans Adobe Experience Cloud, reportez-vous à la section [présentation des balises](../../../home.md).
