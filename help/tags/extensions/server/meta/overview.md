---
title: Présentation de l’extension de l’API de conversions Meta
description: Découvrez l’extension de l’API Meta Conversions pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
TQID: https://experienceleague.adobe.com/GrTuIOPkhlhBNYFBjXEyyhmjqJ3eUR64QXJ57jUc3c8
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1id: dfc56824-e8b9-499e-85d4-21aedb507314id: e43347a8-f2c5-4aa4-8623-6f13875d7e3aid: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: f002a92a-b99f-47a4-90c8-65e0e415bc7aid: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616aid: b12f6872-9271-4369-85e5-86969a0b99a2id: ba929a52-9339-4154-9487-317dc875a3c7id: bef6f891-2e8a-425e-8f99-7ddf22070daaid: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: c93393a4-e558-47e1-992e-c91ed4d480ceid: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: a94ced60-8199-4549-b453-ede2acb4101eid: ae2cba0e-54f2-464b-a3b3-ad371e8a886aid: b572b7ff-a413-4173-b2b4-d7d3874f1b9bid: b64298cc-90cc-46b7-8917-ee391f1c7516id: c1f1ac67-ccab-4be9-a93a-b7faba1192c4id: ca3d6bf4-a4af-4944-936b-8de1eb09f149id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1cid: e0c8953a-a203-4291-bef3-3560160d3041id: ee602049-8a18-43df-9299-a689a025a371id: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 2478
ht-degree: 0%

---

# Présentation de l’extension [!DNL Meta Conversions API]

Le [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) vous permet de connecter vos données marketing côté serveur aux technologies [!DNL Meta] afin d’optimiser le ciblage de vos annonces, de réduire le coût par action et de mesurer les résultats. Les événements sont liés à un ID de [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) et sont traités de la même manière que les événements côté client.

À l’aide de l’extension [!DNL Meta Conversions API], vous pouvez tirer parti des fonctionnalités de l’API dans vos règles [transfert d’événement](../../../ui/event-forwarding/overview.md) pour envoyer des données aux [!DNL Meta] à partir de l’Edge Network Adobe Experience Platform. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans une [règle](../../../ui/managing-resources/rules.md) de transfert d’événement.

## Démonstration

La vidéo suivante est destinée à vous aider à comprendre le [!DNL Meta Conversions API].

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Conditions préalables

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] et le [!DNL Conversions API] pour partager et envoyer les mêmes événements côté client et côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été récupérés par [!DNL Meta Pixel]. Avant d’installer l’extension [!DNL Conversions API], consultez le guide sur l’extension [[!DNL Meta Pixel]  pour savoir comment l’intégrer dans vos implémentations de balises côté client](../../client/meta/overview.md)

>[!NOTE]
>
>La section sur la [déduplication des événements](#deduplication) plus loin dans ce document décrit les étapes à suivre pour s’assurer qu’un même événement n’est pas utilisé deux fois, car il peut être reçu du navigateur et du serveur.

Pour utiliser l’extension [!DNL Conversions API], vous devez avoir accès au transfert d’événement et disposer d’un compte [!DNL Meta] valide avec un accès à [!DNL Ad Manager] et [!DNL Event Manager]. Plus précisément, vous devez copier l’identifiant d’un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) existant (ou [créer un nouveau [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) à la place) afin que l’extension puisse être configurée sur votre compte.

>[!INFO]
>
>Si vous envisagez d’utiliser cette extension avec des données d’application mobile ou si vous utilisez également des données d’événement hors ligne dans vos campagnes [!DNL Meta], vous devez créer votre jeu de données par le biais d’une application existante et sélectionner **Créer à partir d’un identifiant de pixel** lorsque vous y êtes invité. Pour plus d’informations, consultez l’article [Choix de l’option de création de jeu de données adaptée à votre entreprise](https://www.facebook.com/business/help/5270377362999582?id=490360542427371). Reportez-vous au document [API de conversion pour les événements d’application](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) pour tous les paramètres de suivi d’application obligatoires et facultatifs.

## Installation l’extension

Pour installer l’extension [!DNL Meta Conversions API], accédez à l’interface utilisateur de la collecte de données ou d’Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez-en une nouvelle.

Une fois la propriété sélectionnée ou créée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Recherchez la vignette [!UICONTROL API de conversions ] puis sélectionnez **[!UICONTROL Installer]**.

![L’option [!UICONTROL Installer] sélectionnée pour l’extension [!UICONTROL API de conversions Meta] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’identifiant [!DNL Pixel] que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou utiliser un élément de données à la place.

Vous devez également fournir un jeton d’accès pour utiliser le [!DNL Conversions API] spécifiquement. Reportez-vous à la documentation [!DNL Conversions API] sur la [génération d’un jeton d’accès](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) pour savoir comment obtenir cette valeur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![Identifiant [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/server/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Intégration avec l’extension Facebook et Instagram {#facebook}

L’intégration à l’aide de l’extension Facebook et Instagram vous permet de vous authentifier rapidement dans votre compte professionnel Meta. Cela renseigne ensuite automatiquement votre [!UICONTROL Pixel ID] et l’API de conversions Meta [!UICONTROL Jeton d’accès], ce qui facilite l’installation et la configuration de l’API de conversions Meta.

Une boîte de dialogue vous invitant à vous authentifier dans Facebook et Instagram s’affiche lors de l’installation de l’extension [!UICONTROL API de conversions ].

![La page d’installation de l’extension [!UICONTROL API de conversions Meta] mettant en surbrillance [!UICONTROL Connexion à Meta].](../../../images/extensions/server/meta/mbe-extension-install.png)

Une invite de boîte de dialogue pour l’authentification sur Facebook et Instagram apparaît également dans l’interface utilisateur du workflow de démarrage rapide dans le transfert d’événement.

![Mise en surbrillance de l’interface utilisateur du workflow de démarrage rapide [!UICONTROL Connexion à Meta].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Intégration au score de correspondance de qualité de l’événement (EMQ) {#emq}

L’intégration au score de correspondance de qualité de l’événement (EMQ) vous permet d’afficher facilement l’efficacité de votre implémentation en affichant les scores EMQ. Cette intégration réduit le changement de contexte et vous permet d’améliorer le succès de vos implémentations d’API de conversions Meta. Ces scores d’événement apparaissent dans l’écran de configuration de l’extension [!UICONTROL API Conversions Meta ].

![L’extension [!UICONTROL API de conversions Meta] page de configuration mettant en surbrillance [!UICONTROL Afficher le score EMQ].](../../../images/extensions/server/meta/emq-score.png)

## Intégration à LiveRamp (Alpha) {#alpha}

Les clients [!DNL LiveRamp] qui ont déployé la solution ATS (Authenticated Traffic Solution) d’[!DNL LiveRamp] sur leurs sites peuvent choisir de partager des RampID en tant que paramètre d’informations client. Veuillez travailler avec l’équipe de votre compte [!DNL Meta] pour rejoindre le programme Alpha relatif à cette fonctionnalité.

![La page de configuration du transfert d’événement Meta [!UICONTROL Règle] mettant en surbrillance [!UICONTROL Nom du partenaire (alpha)] et [!UICONTROL Identifiant du partenaire (alpha)].](../../../images/extensions/server/meta/live-ramp.png)

## Configurer une règle de transfert d’événement {#rule}

Cette section explique comment utiliser l’extension [!DNL Conversions API] dans une règle de transfert d’événement générique. En pratique, vous devez configurer plusieurs règles afin d’envoyer tous les [événements standard](https://developers.facebook.com/docs/meta-pixel/reference) acceptés via [!DNL Meta Pixel] et [!DNL Conversions API]. Pour les données des applications mobiles, reportez-vous aux champs obligatoires, aux champs de données d’application, aux paramètres d’informations client et aux détails des données personnalisées [ici](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Les événements doivent être [envoyés en temps réel](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou aussi proches que possible du temps réel pour une meilleure optimisation des campagnes publicitaires.

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Extension de l’API de conversions]** pour l’extension, puis sélectionnez **[!UICONTROL Envoyer l’événement d’API de conversions]** pour le type d’action.

![Type d’action [!UICONTROL  Envoyer la page vue ] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/meta/select-action.png)

Des commandes s’affichent pour vous permettre de configurer les données d’événement qui seront envoyées à [!DNL Meta] via le [!DNL Conversions API]. Ces options peuvent être saisies directement dans les entrées fournies ou vous pouvez sélectionner des éléments de données existants pour représenter les valeurs à la place. Les options de configuration sont divisées en quatre sections principales, comme indiqué ci-dessous.

| Section de configuration | Description |
| --- | --- |
| [!UICONTROL Paramètres d’événement du serveur] | Informations générales sur l’événement, y compris l’heure à laquelle il s’est produit et l’action source qui l’a déclenché. Reportez-vous à la documentation du développeur [!DNL Meta] pour plus d’informations sur les [paramètres d’événement standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) acceptés par le [!DNL Conversions API].<br><br>Si vous utilisez à la fois [!DNL Meta Pixel] et [!DNL Conversions API] pour envoyer des événements, veillez à inclure un **[!UICONTROL nom de l’événement]** (`event_name`) et un **[!UICONTROL identifiant de l’événement (]**) avec chaque événement, car ces valeurs sont utilisées pour `event_id`déduplication des événements[ ](#deduplication).<br><br>Vous avez également la possibilité d’**[!UICONTROL Activer l’utilisation limitée des données]** pour vous conformer aux désinscriptions des clients. Consultez la documentation [!DNL Conversions API] sur les [options de traitement des données](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) pour plus d’informations sur cette fonctionnalité. |
| [!UICONTROL Paramètres des informations client] | Données d’identité utilisateur utilisées pour attribuer l’événement à un client. Certaines de ces valeurs doivent être hachées avant de pouvoir être envoyées à l’API. <br><br>Pour garantir une bonne connexion d’API commune et une qualité de correspondance d’événement (EMQ) élevée, il est recommandé d’envoyer tous les [ paramètres d’informations client acceptés](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) ainsi que les événements de serveur. Ces paramètres doivent également être [classés par ordre de priorité en fonction de leur importance et de leur impact sur l’EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Données personnalisées] | Données supplémentaires à utiliser pour l’optimisation de la diffusion des publicités, fournies sous la forme d’un objet JSON. Reportez-vous à la [[!DNL Conversions API] documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) pour plus d’informations sur les propriétés acceptées pour cet objet.<br><br>Si vous envoyez un événement d’achat, vous devez utiliser cette section pour fournir les attributs requis `currency` et `value`. |
| [!UICONTROL Événement de test] | Cette option est utilisée pour vérifier si votre configuration entraîne la réception des événements du serveur par [!DNL Meta] comme prévu. Pour utiliser cette fonctionnalité, cochez la case **[!UICONTROL Envoyer en tant qu’événement de test]**, puis fournissez un code d’événement de test de votre choix dans l’entrée ci-dessous. Une fois la règle de transfert d’événement déployée, si vous avez correctement configuré l’extension et l’action, vous devriez voir les activités apparaître dans la vue **[!DNL Test Events]** dans [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle.

![[!UICONTROL Conserver les modifications] en cours de sélection pour la configuration de l’action.](../../../images/extensions/server/meta/keep-changes.png)

Lorsque la règle vous convient, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Déduplication des événements {#deduplication}

Comme indiqué dans la [section Conditions préalables](#prerequisites), il est recommandé d’utiliser à la fois l’extension de balise [!DNL Meta Pixel] et l’extension de transfert d’événement [!DNL Conversions API] pour envoyer les mêmes événements du client et du serveur dans une configuration redondante. Cela peut aider à récupérer les événements qui n’ont pas été récupérés par une extension ou par l’autre.

Si vous envoyez différents types d’événements à partir du client et du serveur sans chevauchement entre les deux, la déduplication n’est pas nécessaire. Cependant, si un seul événement est partagé par [!DNL Meta Pixel] et le [!DNL Conversions API], vous devez vous assurer que ces événements redondants sont dédupliqués afin que vos rapports ne soient pas affectés négativement.

Lors de l’envoi d’événements partagés, veillez à inclure un identifiant et un nom d’événement à chaque événement envoyé à partir du client et du serveur. Lorsque plusieurs événements avec le même ID et le même nom sont reçus, [!DNL Meta] utilise automatiquement plusieurs stratégies pour les dédupliquer et conserver les données les plus pertinentes. Pour plus d’informations sur ce processus [!DNL Meta Pixel]  consultez la documentation [!DNL Meta] sur [la déduplication des et  [!DNL Conversions API]  événements](https://www.facebook.com/business/help/823677331451951?id=1205376682832142).

## Workflow de démarrage rapide : extension de l’API de conversions Meta (Beta) {#quick-start}

>[!IMPORTANT]
>
>* La fonctionnalité de démarrage rapide est disponible pour les clients qui ont acheté le package Real-Time CDP Prime et Ultimate. Pour plus dʼinformations, contactez votre représentant commercial Adobe.
>* Cette fonctionnalité est destinée aux nouvelles implémentations et ne prend actuellement pas en charge l’installation automatique d’extensions et de configurations sur des balises existantes et des propriétés de transfert d’événement.

>[!NOTE]
>
>Tout client existant peut utiliser les workflows de démarrage rapide pour créer une implémentation de référence qui peut être utilisée pour les éléments suivants :
>
>* Utilisez-le comme point de départ d’une toute nouvelle implémentation.
>* Utilisez-la comme une implémentation de référence que vous pouvez examiner pour voir comment elle a été configurée, puis répliquez-la dans vos implémentations de production actuelles.

La fonctionnalité de démarrage rapide vous permet de configurer facilement et efficacement l’API Meta Conversions et les extensions de pixel Meta. Cet outil automatise plusieurs étapes effectuées dans les balises Adobe et le transfert d’événement, ce qui réduit considérablement le temps de configuration.

Cette fonctionnalité installe et configure automatiquement l’API Meta Conversions et les extensions de pixel Meta sur une nouvelle propriété de transfert d’événement et de balises générées automatiquement avec les règles et éléments de données nécessaires. En outre, il installe et configure automatiquement le SDK web Experience Platform et le flux de données. Enfin, la fonction de démarrage rapide publie automatiquement la bibliothèque vers l’URL désignée dans un environnement de développement, ce qui permet la collecte de données côté client et le transfert d’événement côté serveur en temps réel via le transfert d’événement et Experience Platform Edge Network.

La vidéo suivante présente la fonctionnalité de démarrage rapide.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Installer la fonctionnalité de démarrage rapide

>[!NOTE]
>
>La fonction de configuration guidée vous permet de configurer facilement et efficacement. Cet outil automatise plusieurs étapes effectuées dans les balises Adobe et le transfert d’événement. Il ne fournit pas une implémentation complète et fonctionnelle de bout en bout, capable de s’adapter à tous les cas d’utilisation.

Pour commencer la configuration guidée, suivez les instructions de la section [Configuration guidée du transfert d’événement](../../../ui/event-forwarding/guided-setup.md).

#### Ajouter des événements supplémentaires

Pour ajouter de nouveaux événements, sélectionnez **[!UICONTROL Modifier la propriété Web des balises]**.

![Boîte de dialogue Étapes suivantes affichant la modification de la propriété web des balises](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Sélectionnez la règle qui correspond au méta-événement que vous souhaitez modifier. Par exemple, **MetaConversion_AddToCart**.

>[!NOTE]
>
>S’il n’existe aucun événement, cette règle ne s’exécute pas. C’est le cas pour toutes les règles, la règle **MetaConversion_PageView** étant l’exception.

Pour ajouter un événement, sélectionnez **[!UICONTROL Ajouter]** sous l’en-tête [!UICONTROL Événements].

![Page des propriétés de balise n’affichant aucun événement](../../../images/extensions/server/meta/edit-rule.png)

Sélectionnez le [!UICONTROL type d’événement]. Dans cet exemple, nous avons sélectionné l’événement [!UICONTROL Click] et l’avons configuré pour se déclencher lorsque le bouton **.add-to-cart** est sélectionné. Sélectionnez **[!UICONTROL Conserver les modifications]**.

![Écran de configuration des événements affichant l’événement de clic](../../../images/extensions/server/meta/event-configuration.png)

Le nouvel événement a été enregistré. Sélectionnez **[!UICONTROL Sélectionner une bibliothèque de travail]** puis sélectionnez la bibliothèque dans laquelle vous souhaitez créer la bibliothèque.

![Sélectionnez une liste déroulante de bibliothèque de travail](../../../images/extensions/server/meta/working-library.png)

Sélectionnez ensuite la liste déroulante en regard de **[!UICONTROL Enregistrer dans la bibliothèque]** et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]**. La modification sera publiée dans la bibliothèque.

![Sélectionnez Enregistrer dans la bibliothèque et créer](../../../images/extensions/server/meta/save-and-build.png)

Répétez ces étapes pour tout autre événement de méta-conversion que vous souhaitez configurer.

#### Configuration de la couche de données {#configuration}

>[!IMPORTANT]
>
>La façon dont vous mettez à jour cette couche de données globale dépend de l’architecture de votre site web. Une application sur une seule page est différente d’une application de rendu côté serveur. Il est également possible que vous soyez entièrement responsable de la création et de la mise à jour de ces données dans le produit Balises. Dans toutes les instances, la couche de données devra être mise à jour entre l’exécution de chacune des `MetaConversion_* rules`. Si vous ne mettez pas à jour les données entre les règles, vous pouvez également rencontrer un cas où vous envoyez des données obsolètes de la dernière `MetaConversion_* rule` de la `MetaConversion_* rule` actuelle.

Lors de la configuration, il vous a été demandé où se trouve votre couche de données. Par défaut, il s’agit d’une `window.dataLayer.meta`, et à l’intérieur de l’objet `meta`, vos données sont attendues comme illustré ci-dessous.

![Métadonnées de la couche de données](../../../images/extensions/server/meta/data-layer-meta.png)

Il est important de comprendre cela, car chaque règle de `MetaConversion_*` utilise cette structure de données pour transmettre les éléments de données pertinents à l’extension [!DNL Meta Pixel] et au [!DNL Meta Conversions API]. Reportez-vous à la documentation sur [les événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) pour plus d’informations sur les données requises par les différents méta-événements.

Par exemple, si vous souhaitez utiliser la règle `MetaConversion_Subscribe`, vous devez mettre à jour `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv` et `window.dataLayer.meta.value` conformément aux propriétés d’objet décrites dans la documentation sur les [événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Vous trouverez ci-dessous un exemple de ce qui doit être exécuté sur un site web pour mettre à jour la couche de données avant l’exécution de la règle.

![Mettre à jour les métadonnées de la couche de données](../../../images/extensions/server/meta/update-data-layer-meta.png)

Par défaut, la `<datalayerpath>.conversionData.eventId` est générée de manière aléatoire par l’action « Générer un nouvel identifiant d’événement » sur l’un des `MetaConversion_* rules`.

Pour obtenir une référence locale de l’aspect de la couche de données, vous pouvez ouvrir l’éditeur de code personnalisé sur l’élément de données `MetaConversion_DataLayer` de votre propriété .

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL Meta] à l’aide de l’extension [!DNL Meta Conversions API]. À partir de là, il est recommandé d’étendre votre intégration en connectant plus de [!DNL Pixels] et en partageant davantage d’événements, le cas échéant. Effectuer l’une des opérations suivantes peut vous aider à améliorer davantage les performances de votre publicité :

* Connectez tout autre [!DNL Pixels] qui n’est pas encore connecté à une intégration [!DNL Conversions API].
* Si vous envoyez certains événements exclusivement par le biais de [!DNL Meta Pixel] côté client, envoyez également ces mêmes événements au [!DNL Conversions API] côté serveur.

Pour plus d’informations sur la mise en œuvre efficace de votre intégration [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) consultez la documentation [!DNL Meta] sur [les bonnes pratiques relatives à . Pour des informations plus générales sur les balises et le transfert d’événement dans Adobe Experience Cloud, reportez-vous à la [présentation des balises](../../../home.md).
