---
keywords: extension de transfert d’événement;mixpanel;extension de transfert d’événement mixpanel
title: Extension de transfert d’événement d’API de suivi des événements Mixpanel
description: Cette extension de transfert d’événement Adobe Experience Platform envoie les événements Adobe Experience Edge Network à Mixpanel.
source-git-commit: 54aa55fbafb5e9603b109dbf015e009efd8f5e1d
workflow-type: tm+mt
source-wordcount: '2343'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] Extension de transfert d’événement d’API

[[!DNL Mixpanel]](https://www.mixpanel.com) est un outil d’analyse de produit qui vous permet de capturer des données sur la manière dont les utilisateurs interagissent avec un produit numérique. Vous pouvez analyser les données de produit à l’aide de rapports interactifs simples qui vous permettent d’interroger et de visualiser les données en quelques clics seulement. [!DNL Mixpanel] conçu pour rendre les équipes plus efficaces en permettant à chacun d’analyser les données utilisateur en temps réel afin d’identifier les tendances, de comprendre le comportement des utilisateurs et de prendre des décisions concernant votre produit.

[!DNL Mixpanel] applique un modèle basé sur les événements et centré sur l’utilisateur qui connecte chaque interaction à un seul utilisateur. Le [!DNL Mixpanel] Le modèle de données repose sur les concepts d’utilisateurs, d’événements et de propriétés.

>[!NOTE]
>
>Reportez-vous à la section [!DNL Mixpanel] documentation sur [gestion de l&#39;identité](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) pour comprendre comment [!DNL Mixpanel] fusionne les événements pour créer des clusters d’identités. Il est également recommandé de consulter le document sur [ID distincts](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) pour comprendre comment elles sont utilisées pour identifier les utilisateurs dans les données d’événement.

Le [!DNL Mixpanel Track Events] L’extension d’API vous permet d’exploiter les deux [transfert d’événement](../../../ui/event-forwarding/overview.md) et [tags](../../../home.md) pour capturer les informations d’événement dans Adobe Experience Platform Edge Network et les envoyer à [!DNL Mixpanel] en utilisant la variable [[!DNL Track Events] API](https://developer.mixpanel.com/reference/track-event). Ce document couvre les cas d’utilisation de l’extension, comment l’installer et comment intégrer ses fonctionnalités à votre transfert d’événement. [rules](../../../ui/managing-resources/rules.md).

## Cas d’utilisation

Cette extension doit être utilisée si vous souhaitez utiliser les données du réseau Edge dans [!DNL Mixpanel] pour tirer parti de ses fonctionnalités d’analyse de produit.

Prenons l’exemple d’une entreprise de vente au détail présente sur plusieurs canaux (site web et mobile). L’organisation capture des entrées transactionnelles ou conversationnelles en tant que données d’événement de ses plateformes et les charge dans [!DNL Mixpanel] à l’aide de l’extension de transfert d’événement.

Les équipes d’analyse peuvent alors tirer parti des [!DNL Mixpanel's] fonctionnalités permettant de traiter les jeux de données et d’obtenir des informations sur l’entreprise, qui peuvent être utilisées pour générer des graphiques, des tableaux de bord ou d’autres visualisations afin d’informer les parties prenantes de l’entreprise.

Pour plus d’informations sur les cas d’utilisation spécifiques à [!DNL Mixpanel], reportez-vous à la documentation suivante :

* [Nouveau pour [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [En quoi consiste  [!DNL Mixpanel] ?](https://developer.mixpanel.com/docs)
* [12 à essayer [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Conditions préalables de [!DNL Mixpanel] {#prerequisites-mixpanel}

Vous devez disposer d’un [!DNL Mixpanel] afin d’utiliser cette extension. Accédez au [[!DNL Mixpanel] page d’enregistrement](https://mixpanel.com/register/) pour enregistrer et créer un compte si vous n’en avez pas déjà un.

Assurez-vous que la variable [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) est activé pour votre projet. Accédez à **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** et activez le paramètre .

<!-- (If these don't apply, do we need to include here at all?)
### API guardrails {#guardrails}

Refer to the [[!DNL Mixpanel] documentation](https://developer.mixpanel.com/reference/import-events#rate-limits) for limits and response codes. As [!DNL Mixpanel] only sends live events these limits should not apply.
-->

### Collecte des détails de configuration requis {#configuration-details}

Pour vous connecter à Experience Platform [!DNL Mixpanel] vous devez disposer des entrées suivantes :

| Type de clé | Description | Exemple |
| --- | --- | --- |
| Jeton de projet | Jeton de projet associé à votre [!DNL Mixpanel] compte . Reportez-vous à la section [!DNL Mixpanel] documentation sur [recherche du jeton de projet](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) pour obtenir des conseils. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Conditions préalables des Experience Cloud

Cette section décrit les étapes préalables requises dans Experience Cloud pour toutes les implémentations. En fonction de vos besoins de mise en oeuvre, il peut s’avérer utile de configurer les éléments suivants avant de configurer l’extension :

1. A [schema](../../../../xdm/schema/composition.md) pour décrire la structure des données que vous ingérez dans Experience Cloud
1. A [datastream](https://experienceleague.adobe.com/docs/platform-learn/data-collection/event-forwarding/set-up-a-datastream.html) pour acheminer les données entrantes vers les applications Adobe Experience Cloud appropriées
1. A [dataset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=fr) pour stocker les données collectées

Pour toutes les implémentations, les éléments suivants sont requis côté Experience Cloud :

1. [Créer un secret](#create-a-secret)
1. [Configuration des propriétés de balise](#set-up-tag-properties)
1. [Ajout d’éléments de données dans les propriétés de balise](#add-data-elements-within-tag-properties)
1. [Ajout de règles aux propriétés de balise](#add-rules-within-tag-properties)

### Créer un secret

Créer [secret de transfert d’événement](../../../ui/event-forwarding/secrets.md) et définissez la valeur sur votre [[!DNL Mixpanel] jeton de projet](#configuration-details). Elle sera utilisée pour authentifier la connexion à votre compte tout en conservant la valeur en sécurité.

### Configuration des propriétés de balise

[Création d’une propriété de balise](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=en) ou choisissez une propriété existante à modifier. Cette propriété sera configurée pour collecter les structures de données nécessaires pour [!DNL Mixpanel] car elles sont introduites dans le réseau Edge avant d’être envoyées à l’aide du transfert d’événement.

### Ajout d’éléments de données dans les propriétés de balise

Si votre site web utilise la variable [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs), vous devez [créer un élément de données ;](../../../ui/managing-resources/data-elements.md) qui utilise la variable **[!UICONTROL Cookie]** type (fourni par [[!UICONTROL Core] extension de balise](../../client/core/overview.md)). [!DNL Mixpanel] `distinct_id` peut être lu à partir du cookie .

Le **[!UICONTROL Nom du cookie]** doit correspondre à la valeur [!DNL Mixpanel] nom du cookie du site web. Le nom doit avoir un format similaire à `mp_{MIXPANEL_PROJECT_TOKEN_FOR_WEBSITE}_mixpanel`. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Enregistrer]**.

![Élément de données ID distinct dans les propriétés de balise.](../../../images/extensions/server/mixpanel/distinctId-data-element.png)

>[!IMPORTANT]
>
>Nom de l’élément de données ci-dessus (`distinctId` dans cet exemple) doit correspondre au nom utilisé pour le même champ de votre schéma. Cela s’applique également à l’élément de données de transfert d’événement que vous allez créer ultérieurement.

Pour le deuxième élément de données, définissez le type sur **[!UICONTROL Objet XDM]** (de la fonction [Extension SDK Web Adobe Experience Platform](../../client/sdk/overview.md)) et le mapper au schéma créé précédemment. Lorsque vous mappez les données, assurez-vous que la valeur de la variable `distinct_id` élément de données (qui contient le [!DNL Mixpanel] `distinct_id` du cookie) est référencée en tant que valeur dans l’un de vos champs de schéma.

![Élément de données de l’objet XDM liant le distinct_id du cookie au schéma dans les propriétés de balise.](../../../images/extensions/server/mixpanel/xdm-data-element.png)

>[!NOTE]
>
>Si votre site web n’exécute pas la variable [!DNL Mixpanel] SDK, un Adobe Experience Cloud ID (ECID) sera utilisé comme solution de secours. `distinct_id` valeur à transmettre avec l’événement envoyé à [!DNL Mixpanel].

Selon votre scénario, vous devrez peut-être créer un autre élément de données qui pourra être utilisé pour mapper le nom de l’événement dans le schéma. Pour ce faire, utilisez la méthode **[!UICONTROL Attribut DOM]** type fourni par [!UICONTROL Core] extension .

![Événements d’élément de données dans les propriétés de balise.](../../../images/extensions/server/mixpanel/eventname-signin-data-element.png)

### Ajout de règles aux propriétés de balise

Une fois vos éléments de données configurés, vous pouvez commencer à créer des règles qui déterminent les événements qui entraîneront l’envoi de données à [!DNL Mixpanel].

Commencez par créer une règle qui est déclenchée pour l’événement d’identification de l’utilisateur. Il peut s’agir de connexions, d’abonnements, d’inscriptions ou de tout autre événement que vous souhaitez utiliser pour l’identification des utilisateurs.

![Une règle de connexion dans les propriétés de balise.](../../../images/extensions/server/mixpanel/tag-rule-complete.png)

Sous **[!UICONTROL Événements]**, ajoutez une condition (spécifique à votre site web) qui déclenchera l’événement d’identification. Vous trouverez ci-dessous un exemple de déclenchement de la règle de connexion lors d’un clic de l’utilisateur :

![Configuration d’événement pour une règle de connexion dans les propriétés de balise.](../../../images/extensions/server/mixpanel/tag-rule-event-config.png)

Sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’événement à la règle.

Ensuite, sous **[!UICONTROL Actions]**, ajoutez les actions résultantes que la règle doit exécuter lors de son déclenchement. Parmi ces actions, **[!UICONTROL Envoyer un événement]** fourni par l’extension SDK Web Platform, qui envoie l’événement au réseau Edge, où il peut être récupéré par des extensions de transfert d’événement telles que [!DNL Mixpanel].

Lors de la configuration de l’action, sous **[!UICONTROL Données XDM]** sélectionnez la variable [élément de données que vous avez créé précédemment](#add-data-elements-within-tag-properties) qui contient le paramètre `distinct_id` .

![Configuration des actions pour une règle de connexion dans les propriétés de balise.](../../../images/extensions/server/mixpanel/tag-rule-action-config.png)

Sélectionner **[!UICONTROL Conserver les modifications]** pour ajouter l’événement à la règle, sélectionnez **[!UICONTROL Enregistrer]** pour ajouter la règle à la bibliothèque de balises. À partir de là, vous pouvez [créer un nouveau build et le déployer sur votre site web ;](../../../ui/publishing/overview.md).

## Installez et configurez le [!DNL Mixpanel] extension {#install}

Pour installer l’extension, [création d’une propriété de transfert d’événement](../../../ui/event-forwarding/overview.md#properties) ou choisissez une propriété existante à modifier.

Sélectionner **[!UICONTROL Extensions]** dans le volet de navigation de gauche. Dans le **[!UICONTROL Catalogue]** onglet, sélectionnez **[!UICONTROL Installer]** sur la carte de la variable [!DNL Mixpanel] extension .

![Installation de la variable [!DNL Mixpanel] extension .](../../../images/extensions/server/mixpanel/install-extension.png)

## Configuration des éléments de données de transfert d’événement

Après l’installation de l’extension, l’étape suivante consiste à créer des éléments de données de transfert d’événement qui captureront les éléments de données nécessaires qui seront envoyés à [!DNL Mixpanel].

### Créez un `distinctId` élément de données

Ajoutez des éléments de données sous le transfert d’événement. Si le site est configuré avec la variable [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs) la valeur [élément de données de propriété de balise](#setup-tag-properties-data-element) aurait été défini. Pour l’élément de données de transfert d’événement, vous allez maintenant fournir un **[!UICONTROL Chemin]** au lieu de .

![Ajoutez un élément de données dans le transfert d’événement.](../../../images/extensions/server/mixpanel/distinctId-ef-data-element.png)

### Créez un `event_type` élément de données

Vous trouverez ci-dessous un exemple d’élément de données défini pour un type d’événement :

![Type d’événement de transfert d’événement.](../../../images/extensions/server/mixpanel/eventname-ef-data-element.png)

### Création de mappages d’éléments de données supplémentaires

Le `distinctId` et `event_type` Les éléments de données doivent tous deux envoyer des données à [!DNL Mixpanel], mais il est également recommandé d’inclure un identifiant utilisateur connu et un objet de données personnalisé avec chaque événement, le cas échéant. Consultez le guide sur la [[!DNL Mixpanel Track Events] API REST](https://developer.mixpanel.com/reference/track-event) pour plus d’informations.

Les mappages d’éléments de données recommandés sont décrits ci-dessous.

>[!IMPORTANT]
>
>Tous les éléments de données répertoriés ci-dessous doivent utiliser la variable **[!UICONTROL Chemin]** type afin qu’ils puissent mapper sur des champs spécifiques de votre schéma, comme indiqué dans la section **Chemin du schéma** colonne .
>
>Pour les chemins d’accès au schéma, vous devez remplacer la propriété `{TENANT_ID}` espace réservé avec votre [identifiant du client](../../../../xdm/api/getting-started.md#know-your-tenant_id), qui agit comme un espace de noms pour les champs personnalisés définis par votre organisation.

| [!DNL Mixpanel] triggers | Chemin du schéma | Description | Obligatoire |
| --- | --- | --- | --- |
| [!DNL Mixpanel Distinct ID] | `arc.event.xdm._{TENANT_ID}.distinct_id` | `distinct_id` identifie l’utilisateur qui a exécuté l’événement. `distinct_id` doit être spécifié sur chaque événement, car il est essentiel pour [!DNL Mixpanel] pour exécuter correctement et efficacement l’analyse comportementale, notamment les utilisateurs uniques, les entonnoirs, la rétention, les cohortes, etc. | Oui |
| [!DNL Event Type] | `arc.event.xdm._{TENANT_ID}.event_type` | Il s’agit du nom de l’événement. [!DNL Mixpanel] recommande de limiter le nombre de noms d’événement uniques et d’utiliser les propriétés pour tout contexte de variable associé à l’événement.<br><br>Par exemple, au lieu de suivre les événements avec des noms tels que &quot;Inscription payante&quot; et &quot;Enregistrement gratuit&quot;, il est recommandé de suivre un événement appelé &quot;Enregistrement&quot; et d’avoir une propriété appelée &quot;Type de compte&quot; avec des valeurs potentielles &quot;payante&quot; et &quot;gratuit&quot;. | Oui |
| [!DNL Known User ID] | `arc.event.xdm._{TENANT_ID}.LoginID` | Adresse électronique ou identifiant de connexion de l’utilisateur, le cas échéant. | Non |
| [!DNL Data] | `arc.event.xdm._{TENANT_ID}.properties` | Objet JSON représentant toutes les propriétés de l’événement. Les données sont tronquées à 255 caractères. | Non |

{style="table-layout:auto"}

## Configuration des règles de transfert d’événement

Une fois tous vos éléments de données configurés, vous pouvez commencer à créer des règles de transfert d’événement qui déterminent quand et comment vos événements seront envoyés à [!DNL Mixpanel]. Toutefois, avant de configurer vos règles, il est important de comprendre le fonctionnement des clusters d’identités dans [!DNL Mixpanel] afin que les événements que vous envoyez soient correctement attribués à des utilisateurs individuels.

### Présentation des clusters d’identités dans [!DNL Mixpanel]

Dans [!DNL Mixpanel], un cluster d’identités contient une collection de `distinct_id` qui se connectent à un utilisateur individuel. [!DNL Mixpanel] gère la mise en grappe des identités pour chaque utilisateur, en résolvant un seul canonique. `distinct_id` de chaque grappe à utiliser dans les rapports. Vous pouvez également inclure votre propre identifiant (appelé local `distinct_id`) pour les événements anonymes qui se produisent avant un événement d’identification d’utilisateur.

[!DNL Mixpanel] résout les clusters d’identités par deux méthodes :

* **Identifier** : [!DNL Mixpanel] relie l&#39;identifiant de votre choix à un anonyme `distinct_id`. Si la variable [!DNL Mixpanel] Le SDK est configuré sur votre site web. Platform utilisera la variable `distinct_id` affectée à l’utilisateur actuellement connecté.
* **Alias**: [!DNL Mixpanel] fusionne deux éléments non anonymes ; `distinct_id`s ensemble si d’autres critères de fusion sont transmis.

>[!NOTE]
>
>Reportez-vous à la section [!DNL Mixpanel] document on [gestion de l&#39;identité](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) pour plus d’informations sur ces méthodes.
>
>Confirmez que vous avez activé la variable [[!DNL Mixpanel] fonctionnalité de fusion d’identités](#prerequisites-mixpanel) afin de s’assurer que les clusters d’identités sont résolus de manière appropriée.

Par conséquent, la [!DNL Mixpanel] l’extension de transfert d’événement prend en charge **[!UICONTROL Suivi de l’événement]** type d’action pour votre configuration de règle.

>[!IMPORTANT]
>
>Pour chaque règle, quelle que soit la méthode de résolution de cluster d’identités utilisée, l’une des actions doit utiliser la variable **[!UICONTROL Suivi de l’événement]** type. Sans ce type d’action, la règle n’enverra pas d’événements Adobe Experience Edge Network à [!DNL Mixpanel].

### Création d’une règle de suivi d’événement

Commencez à créer une règle dans votre propriété de transfert d’événement. Sous **[!UICONTROL Actions]**, ajoutez une nouvelle action et définissez l’extension sur **[!UICONTROL Mixpanel]**. Définissez ensuite le type d’action sur **[!UICONTROL Suivi de l’événement]** pour envoyer des événements Adobe Experience Edge Network à [!DNL Mixpanel].

| Entrée | Description |
| --- | --- |
| [!UICONTROL Jeton de projet] | Ce champ doit être mappé au jeton de projet associé à votre [!DNL Mixpanel] compte . |
| [!UICONTROL Event Type] (Type d’événement) | Nom de l’événement. |
| [!UICONTROL Heure de l’événement] | L’heure de l’événement. |
| [!UICONTROL Identifiant distinct du panneau mixte] | Ce champ doit être mappé à la propriété `distinctId` élément de données que vous avez créé précédemment. |
| [!UICONTROL Insérer un ID] | Ce champ doit être mappé à la propriété `insertId` élément de données. |
| [!UICONTROL Propriétés de l’événement] | Choisissez entre fournir un fichier JSON brut ou utiliser un jeu simplifié d’entrées clé-valeur. |

>[!NOTE]
>
>Pour plus d’informations sur les champs standard d’un [!DNL Mixpanel] , voir [documentation officielle](https://developer.mixpanel.com/reference/import-events#event).

![Ajoutez une configuration d’action de règle de transfert d’événement.](../../../images/extensions/server/mixpanel/track-event-action.png)

Une fois que la variable [!UICONTROL Suivi de l’événement] est ajoutée à la règle, vous pouvez configurer les conditions de la règle de sorte qu’elle ne se déclenche que pour certains événements ou vous pouvez laisser la section conditions vide pour que la règle se déclenche pour tous les événements.

>[!IMPORTANT]
>
>Si votre site web utilise la variable [!DNL Mixpanel] SDK, vous pouvez passer à l’étape suivante de [validation de vos données dans [!DNL Mixpanel]](#validate). Si vous n’utilisez pas la variable [!DNL Mixpanel] SDK, vous devez [créer une règle de suivi d’identité distincte](#create-an-identity-tracking-rule) pour s’assurer que les événements appropriés et `distinct_id` sont envoyées à [!DNL Mixpanel] lorsqu’un événement d’identification utilisateur se produit.

### Création d’une règle de suivi des identités

Si vous n’utilisez pas la variable [!DNL Mixpanel SDK], l’étape suivante consiste à créer une autre règle. Cette règle garantit que, chaque fois qu’un événement d’identification d’utilisateur se produit sur le site web (comme une connexion, une inscription, un enregistrement, etc.), les événements appropriés et `distinct_id` sont envoyées à [!DNL Mixpanel].

Démarrez le processus de création d’une règle. Pour le [!UICONTROL Conditions] ajoutez une condition qui vérifie si l’événement est un événement d’identification de l’utilisateur. Dans l’exemple ci-dessous, la condition utilise une [!UICONTROL Value Comparison] (de la fonction [!UICONTROL Core] pour vérifier si le nom de l’événement entrant est égal à `signin`, indiquant un événement de connexion de l’utilisateur.

![Afficher la configuration de l’action pour [!DNL Mixpanel] types d’actions Alias et Identifier.](../../../images/extensions/server/mixpanel/ef-rule-condition.png)

Une fois que vous avez ajouté les conditions appropriées à la règle, vous devez créer une [!UICONTROL Envoyer un événement] pour envoyer des événements Adobe Experience Edge Network à [!DNL Mixpanel].

![Ajoutez une configuration d’action de règle de transfert d’événement.](../../../images/extensions/server/mixpanel/track-event-action.png)

>[!NOTE]
>
>Pour plus d’informations sur les identités dans [!DNL Mixpanel], reportez-vous à la section [documentation officielle](https://developer.mixpanel.com/reference/create-identity).

Une fois l’action ajoutée à la règle, sélectionnez **[!UICONTROL Enregistrer]** pour ajouter la règle à votre bibliothèque de transfert d’événement. À partir de là, vous pouvez [créer un nouveau build et activer vos modifications ;](../../../ui/publishing/overview.md).

![Ajouter une règle de transfert d’événement pour [!DNL Mixpanel] types d’actions Alias et Identifier.](../../../images/extensions/server/mixpanel/ef-rule-complete.png)

## Validation des données dans [!DNL Mixpanel] {#validate}

Si votre mise en oeuvre est réussie et que des événements sont collectés, des événements s’affichent dans la variable [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Vérifier si [!DNL Mixpanel] a fusionné les événements de post-connexion renseignés avec les valeurs d’email et les événements créés lors de l’utilisation de **[!UICONTROL Envoyer un événement]**. Si implémenté correctement, [!DNL Mixpanel] les associera à une seule [profil utilisateur](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Étapes suivantes

Ce guide explique comment envoyer des événements de conversion à [!DNL Mixpanel] à l’aide du transfert d’événement. Cette extension de transfert d’événement tire parti de la variable [!DNL Mixpanel] SDK et API JavaScript. Pour plus d&#39;informations sur ces technologies sous-jacentes, consultez la documentation officielle :

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Pour plus d’informations sur les fonctionnalités de transfert d’événement dans Experience Platform, reportez-vous à la section [transfert d’événement - Aperçu](../../../ui/event-forwarding/overview.md).
