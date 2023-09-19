---
keywords: extension de transfert d’événement;mixpanel;extension de transfert d’événement mixpanel
title: Extension de transfert d’événement d’API de suivi des événements Mixpanel
description: Cette extension de transfert d’événement Adobe Experience Platform envoie les événements Edge Network à Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] Extension de transfert d’événement d’API

[[!DNL Mixpanel]](https://www.mixpanel.com) est un outil d’analyse de produit qui vous permet de capturer des données sur la manière dont les utilisateurs interagissent avec un produit numérique. Vous pouvez analyser les données de produit à l’aide de rapports interactifs simples qui vous permettent d’interroger et de visualiser les données en quelques clics seulement. [!DNL Mixpanel] conçu pour rendre les équipes plus efficaces en permettant à chacun d’analyser les données utilisateur en temps réel afin d’identifier les tendances, de comprendre le comportement des utilisateurs et de prendre des décisions concernant votre produit.

[!DNL Mixpanel] applique un modèle basé sur les événements et centré sur l’utilisateur qui connecte chaque interaction à un seul utilisateur. La variable [!DNL Mixpanel] Le modèle de données repose sur les concepts d’utilisateurs, d’événements et de propriétés.

>[!NOTE]
>
>Voir [!DNL Mixpanel] documentation sur [gestion de l&#39;identité](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) pour comprendre comment [!DNL Mixpanel] fusionne les événements pour créer des clusters d’identités. Il est également recommandé de consulter le document sur [ID distincts](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) pour comprendre comment elles sont utilisées pour identifier les utilisateurs dans les données d’événement.

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données du réseau Edge dans [!DNL Mixpanel] pour tirer parti de ses fonctionnalités d’analyse de produit.

Prenons l’exemple d’une entreprise de vente au détail présente sur plusieurs canaux (site web et mobile). L’organisation capture des entrées transactionnelles ou conversationnelles en tant que données d’événement de ses plateformes et les charge dans [!DNL Mixpanel] à l’aide de l’extension de transfert d’événement.

Les équipes d’analyse peuvent alors tirer parti des [!DNL Mixpanel's] fonctionnalités permettant de traiter les jeux de données et d’obtenir des informations sur l’entreprise, qui peuvent être utilisées pour générer des graphiques, des tableaux de bord ou d’autres visualisations afin d’informer les parties prenantes de l’entreprise.

Pour plus d’informations sur les cas d’utilisation spécifiques à [!DNL Mixpanel], reportez-vous à la documentation suivante :

* [Nouveau pour [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [En quoi consiste  [!DNL Mixpanel] ?](https://developer.mixpanel.com/docs)
* [12 à essayer [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Conditions préalables de [!DNL Mixpanel] {#prerequisites-mixpanel}

Vous devez disposer d’un [!DNL Mixpanel] afin d’utiliser cette extension. Accédez au [[!DNL Mixpanel] page d’enregistrement](https://mixpanel.com/register/) pour enregistrer et créer un compte si vous n’en avez pas déjà un.

Assurez-vous que la variable [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) est activé pour votre projet. Accédez à **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** et activez le paramètre .

### Présentation des clusters d’identités dans [!DNL Mixpanel]

Dans [!DNL Mixpanel], un cluster d’identités contient une collection de `distinct_id` qui se connectent à un utilisateur individuel. [!DNL Mixpanel] gère la grappe d’identités de chaque utilisateur, en résolvant un seul canonique. `distinct_id` de chaque grappe à utiliser dans les rapports. Vous pouvez également inclure votre propre identifiant (appelé local `distinct_id`) pour les événements anonymes qui se produisent avant un événement d’identification d’utilisateur.

[!DNL Mixpanel] résout les clusters d’identités par deux méthodes :

* **Identifier** : [!DNL Mixpanel] relie l&#39;identifiant de votre choix à un anonyme `distinct_id`. Si votre site web comporte la variable [!DNL Mixpanel] SDK activé, Platform utilisera la variable `distinct_id` affectée à l’utilisateur actuellement connecté.
* **Alias**: [!DNL Mixpanel] combine deux éléments non anonymes `distinct id`s ensemble si d’autres critères de fusion sont satisfaits.

>[!NOTE]
>
>Voir [!DNL Mixpanel] document on [gestion de l&#39;identité](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) pour plus d’informations sur ces méthodes.
>
>Confirmez que vous avez activé la variable [[!DNL Mixpanel] fonctionnalité de fusion d’identités](#prerequisites-mixpanel) afin de s’assurer que les clusters d’identités sont résolus de manière appropriée.

### Collecte des détails de configuration requis {#configuration-details}

Pour vous connecter à Experience Platform [!DNL Mixpanel] vous devez disposer des entrées suivantes :

| Type de clé | Description | Exemple |
| --- | --- | --- |
| Jeton de projet | Jeton de projet associé à votre [!DNL Mixpanel] compte . Voir [!DNL Mixpanel] documentation sur [recherche du jeton de projet](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) pour obtenir des conseils. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installez et configurez le [!DNL Mixpanel] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** onglet, sélectionnez **[!UICONTROL Installer]** sur la carte de la variable [!DNL Mixpanel] extension .

![Installation de la variable [!DNL Mixpanel] extension .](../../../images/extensions/server/mixpanel/install-extension.png)

## Créez un [!DNL Send Event] règle

Commencez à créer une règle dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Mixpanel]**. Définissez ensuite le type d’action sur **[!UICONTROL Suivi de l’événement]** pour envoyer des événements Edge Network à [!DNL Mixpanel].

| Entrée | Description | Obligatoire |
| --- | --- | --- |
| [!UICONTROL Jeton de projet] | Ce champ doit être mappé au jeton de projet associé à votre [!DNL Mixpanel] compte . | Oui |
| [!UICONTROL Event Type] (Type d’événement) | Nom de l’événement. | Oui |
| [!UICONTROL Heure de l’événement] | L’heure de l’événement. | |
| [!UICONTROL Identifiant distinct du panneau mixte] | Identifiant unique de l’utilisateur qui a exécuté l’événement. | |
| [!UICONTROL Insérer un ID] | Identifiant unique de l’événement, utilisé pour le dédoublonnage. | |
| [!UICONTROL Propriétés de l’événement] | Objet JSON contenant des propriétés personnalisées de l’événement. Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. | |

>[!NOTE]
>
>Pour plus d’informations sur les champs standard d’un [!DNL Mixpanel] , voir [documentation officielle](https://developer.mixpanel.com/reference/import-events#event).

![Ajoutez une configuration d’action de règle de transfert d’événement.](../../../images/extensions/server/mixpanel/track-event-action.png)

Une fois que la variable [!UICONTROL Suivi de l’événement] est ajoutée à la règle, vous pouvez configurer les conditions de la règle de sorte qu’elle ne se déclenche que pour certains événements ou vous pouvez laisser la section conditions vide pour que la règle se déclenche pour tous les événements.

>[!IMPORTANT]
>
>Si votre site web utilise la variable [!DNL Mixpanel] SDK, vous pouvez passer à l’étape suivante de [validation de vos données dans [!DNL Mixpanel]](#validate). Si vous n’utilisez pas la variable [!DNL Mixpanel] SDK, vous devez [créer une règle de suivi d’identité distincte](#create-an-identity-tracking-rule) pour garantir les événements appropriés et `distinct_id` sont envoyées à [!DNL Mixpanel] lorsqu’un événement d’identification utilisateur se produit.

## Validation des données dans [!DNL Mixpanel] {#validate}

Si votre mise en oeuvre est réussie et que des événements sont collectés, des événements s’affichent dans la variable [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Vérifier si [!DNL Mixpanel] a fusionné les événements de post-connexion renseignés avec les valeurs d’email et les événements créés lors de l’utilisation de **[!UICONTROL Envoyer un événement]**. Si implémenté correctement, [!DNL Mixpanel] les associera à une seule [profil utilisateur](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Mixpanel] à l’aide du transfert d’événement. Cette extension de transfert d’événement tire parti de la variable [!DNL Mixpanel] SDK et API JavaScript. Pour plus d&#39;informations sur ces technologies sous-jacentes, consultez la documentation officielle :

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
