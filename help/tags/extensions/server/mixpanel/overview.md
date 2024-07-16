---
keywords: extension de transfert d’événement;mixpanel;extension de transfert d’événement mixpanel
title: Extension de transfert d’événement d’API de suivi des événements Mixpanel
description: Cette extension de transfert d’événement Adobe Experience Platform envoie les événements Edge Network à Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] Extension de transfert d’événement d’API

[[!DNL Mixpanel]](https://www.mixpanel.com) est un outil d’analyse de produit qui vous permet de capturer des données sur la manière dont les utilisateurs interagissent avec un produit numérique. Vous pouvez analyser les données de produit à l’aide de rapports interactifs simples qui vous permettent d’interroger et de visualiser les données en quelques clics seulement. [!DNL Mixpanel] conçu pour rendre les équipes plus efficaces en permettant à chacun d’analyser les données utilisateur en temps réel afin d’identifier les tendances, de comprendre le comportement des utilisateurs et de prendre des décisions concernant votre produit.

[!DNL Mixpanel] utilise un modèle basé sur les événements et centré sur l’utilisateur qui connecte chaque interaction à un seul utilisateur. Le modèle de données [!DNL Mixpanel] repose sur les concepts d’utilisateurs, d’événements et de propriétés.

>[!NOTE]
>
>Reportez-vous à la documentation [!DNL Mixpanel] sur la [gestion des identités](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) pour comprendre comment [!DNL Mixpanel] fusionne des événements pour créer des clusters d’identités. Il est également recommandé de consulter le document sur les [identifiants distincts](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) pour comprendre comment ils sont utilisés pour identifier les utilisateurs dans les données d’événement.

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données de l’Edge Network dans [!DNL Mixpanel] pour tirer parti de ses fonctionnalités d’analyse de produit.

Prenons l’exemple d’une entreprise de vente au détail présente sur plusieurs canaux (site web et mobile). L’organisation capture des entrées transactionnelles ou conversationnelles en tant que données d’événement de ses plateformes et les charge dans [!DNL Mixpanel] à l’aide de l’extension de transfert d’événement.

Les équipes d’analyse peuvent ensuite exploiter les fonctionnalités [!DNL Mixpanel's] pour traiter les jeux de données et obtenir des informations sur l’entreprise, qui peuvent être utilisées pour générer des graphiques, des tableaux de bord ou d’autres visualisations pour informer les parties prenantes de l’entreprise.

Pour plus d&#39;informations sur les cas d&#39;utilisation spécifiques à [!DNL Mixpanel], consultez la documentation suivante :

* [Nouveau à [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Présentation du service [!DNL Mixpanel] ](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Conditions préalables de [!DNL Mixpanel] {#prerequisites-mixpanel}

Pour utiliser cette extension, vous devez disposer d’un compte [!DNL Mixpanel] valide. Accédez à la [[!DNL Mixpanel] page d&#39;inscription](https://mixpanel.com/register/) pour vous enregistrer et créer un compte si vous n&#39;en avez pas déjà un.

Vérifiez que le paramètre [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) est activé pour votre projet. Accédez à **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** et faites basculer le paramètre.

### Présentation des clusters d’identités dans [!DNL Mixpanel]

Dans [!DNL Mixpanel], un cluster d&#39;identités contient une collection de valeurs `distinct_id` qui se connectent à un utilisateur individuel. [!DNL Mixpanel] gère la grappe d’identités de chaque utilisateur, résolvant un seul `distinct_id` canonique de chaque grappe à utiliser dans les rapports. Vous pouvez également inclure votre propre identifiant (appelé `distinct_id` local) pour les événements anonymes qui se produisent avant un événement d’identification d’utilisateur.

[!DNL Mixpanel] résout les clusters d’identités par deux méthodes :

* **Identifier** : [!DNL Mixpanel] connecte l’identifiant choisi à un `distinct_id` anonyme. Si le SDK [!DNL Mixpanel] est activé sur votre site web, Platform utilisera le `distinct_id` attribué à l’utilisateur actuellement connecté.
* **Alias** : [!DNL Mixpanel] combine ensemble deux `distinct id` non anonymes si d’autres critères de fusion sont satisfaits.

>[!NOTE]
>
>Pour plus d’informations sur ces méthodes, consultez le document [!DNL Mixpanel] sur la [ gestion des identités](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) .
>
>Confirmez que vous avez activé la [[!DNL Mixpanel] fonctionnalité de fusion d’identités](#prerequisites-mixpanel) pour vous assurer que les grappes d’identités sont résolues de manière appropriée.

### Collecte des détails de configuration requis {#configuration-details}

Pour vous connecter à Experience Platform à [!DNL Mixpanel], vous devez disposer des entrées suivantes :

| Type de clé | Description | Exemple |
| --- | --- | --- |
| Jeton de projet | Jeton de projet associé à votre compte [!DNL Mixpanel]. Pour plus d&#39;informations, reportez-vous à la documentation [!DNL Mixpanel] sur la [recherche du jeton de votre projet](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) . | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installation et configuration de l’extension [!DNL Mixpanel] {#install}

Pour installer l’extension, [créez une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier à la place.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans l’onglet **[!UICONTROL Catalogue]** , sélectionnez **[!UICONTROL Installer]** sur la carte de l’extension [!DNL Mixpanel].

![Installation de l’extension [!DNL Mixpanel].](../../../images/extensions/server/mixpanel/install-extension.png)

## Création d’une règle [!DNL Send Event]

Commencez à créer une règle dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Mixpanel]**. Ensuite, définissez le type d’action sur **[!UICONTROL Track Event]** pour envoyer les événements Edge Network à [!DNL Mixpanel].

| Entrée | Description | Obligatoire |
| --- | --- | --- |
| [!UICONTROL Jeton de projet] | Ce champ doit être mappé au jeton de projet associé à votre compte [!DNL Mixpanel]. | Oui |
| [!UICONTROL Event Type] (Type d’événement) | Nom de l’événement. | Oui |
| [!UICONTROL Heure de l’événement] | Heure de l’événement. | |
| [!UICONTROL Identifiant distinct Mixpanel] | Identifiant unique de l’utilisateur qui a exécuté l’événement. | |
| [!UICONTROL Insérer l’ID] | Identifiant unique de l’événement, utilisé pour le dédoublonnage. | |
| [!UICONTROL Propriétés de l’événement] | Objet JSON contenant des propriétés personnalisées de l’événement. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | |

>[!NOTE]
>
>Pour plus d&#39;informations sur les champs standard d&#39;un événement [!DNL Mixpanel], consultez la [documentation officielle](https://developer.mixpanel.com/reference/import-events#event).

![Ajoutez une configuration d&#39;action de règle de transfert d&#39;événement.](../../../images/extensions/server/mixpanel/track-event-action.png)

Une fois l’action [!UICONTROL Track Event] ajoutée à la règle, vous pouvez configurer les conditions de la règle de sorte qu’elle ne se déclenche que pour certains événements, ou vous pouvez laisser la section conditions vide pour que la règle se déclenche pour tous les événements.

>[!IMPORTANT]
>
>Si votre site web utilise le SDK [!DNL Mixpanel], vous pouvez passer à l’étape suivante de la [ validation de vos données dans  [!DNL Mixpanel]](#validate). Si vous n&#39;utilisez pas le SDK [!DNL Mixpanel], vous devez [ créer une règle de suivi d&#39;identité distincte ](#create-an-identity-tracking-rule) pour vous assurer que les événements appropriés et les valeurs `distinct_id` sont envoyés à [!DNL Mixpanel] lorsqu&#39;un événement d&#39;identification de l&#39;utilisateur se produit.

## Validation des données dans [!DNL Mixpanel] {#validate}

Si votre mise en oeuvre est réussie et que les événements sont collectés, des événements s’affichent dans la [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Vérifiez si [!DNL Mixpanel] a fusionné les événements de post-connexion renseignés avec les valeurs d&#39;email et les événements créés lors de l&#39;utilisation de **[!UICONTROL Send Event]**. Si implémentés correctement, [!DNL Mixpanel] les associera à un seul [profil utilisateur](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion vers [!DNL Mixpanel] à l’aide du transfert d’événement. Cette extension de transfert d’événement utilise le SDK [!DNL Mixpanel] et l’API JavaScript. Pour plus d&#39;informations sur ces technologies sous-jacentes, consultez la documentation officielle :

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Pour plus d’informations sur les fonctionnalités de transfert d’événement en Experience Platform, consultez la [présentation du transfert d’événement](../../../ui/event-forwarding/overview.md).
