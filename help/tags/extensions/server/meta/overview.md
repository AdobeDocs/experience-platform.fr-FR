---
title: Présentation de l’extension de l’API Meta Conversions
description: Découvrez l’extension de l’API Meta Conversions pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2583'
ht-degree: 0%

---

# Présentation de l’extension [!DNL Meta Conversions API]

Le [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) vous permet de connecter vos données marketing côté serveur aux technologies [!DNL Meta] afin d’optimiser le ciblage de vos publicités, de réduire le coût par action et de mesurer les résultats. Les événements sont liés à un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID et sont traités de la même manière que les événements côté client.

À l’aide de l’extension [!DNL Meta Conversions API], vous pouvez exploiter les fonctionnalités de l’API dans vos règles de [transfert d’événement](../../../ui/event-forwarding/overview.md) pour envoyer des données à [!DNL Meta] à partir de l’Edge Network Adobe Experience Platform. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans un transfert d’événement [rule](../../../ui/managing-resources/rules.md).

## Démonstration

La vidéo suivante est destinée à vous aider à comprendre le [!DNL Meta Conversions API].

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Conditions préalables

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] et [!DNL Conversions API] pour partager et envoyer les mêmes événements du côté client et du côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par [!DNL Meta Pixel]. Avant d’installer l’extension [!DNL Conversions API], consultez le guide sur l’ [[!DNL Meta Pixel] extension](../../client/meta/overview.md) pour connaître les étapes de son intégration dans vos implémentations de balises côté client.

>[!NOTE]
>
>La section sur la [déduplication d&#39;événements](#deduplication) ultérieure de ce document décrit les étapes permettant de s&#39;assurer qu&#39;un même événement n&#39;est pas utilisé deux fois, car il peut être reçu à la fois du navigateur et du serveur.

Pour utiliser l’extension [!DNL Conversions API], vous devez avoir accès au transfert d’événement et disposer d’un compte [!DNL Meta] valide ayant accès à [!DNL Ad Manager] et [!DNL Event Manager]. Plus précisément, vous devez copier l’identifiant d’un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) existant (ou [créer un nouvel [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) à la place) afin que l’extension puisse être configurée sur votre compte.

>[!INFO]
>
>Si vous prévoyez d’utiliser cette extension avec des données d’application mobile ou si vous utilisez également des données d’événement hors ligne dans vos campagnes [!DNL Meta], vous devrez créer votre jeu de données par le biais d’une application existante et sélectionner **Créer à partir d’un ID de pixel** lorsque vous y serez invité. Pour plus d’informations, consultez l’article [Choix de l’option de création de jeux de données adaptée à votre entreprise](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) . Reportez-vous au document [API de conversion pour les événements d’application](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) pour tous les paramètres de suivi d’application obligatoires et facultatifs.

## Installation l’extension

Pour installer l’extension [!DNL Meta Conversions API], accédez à l’interface utilisateur de collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** . Recherchez la carte [!UICONTROL &#x200B; Meta Conversions API] , puis sélectionnez **[!UICONTROL Install]**.

![L’option [!UICONTROL Install] sélectionnée pour l’extension [!UICONTROL Meta Conversions API] dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir l’ID [!DNL Pixel] que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou vous pouvez utiliser un élément de données à la place.

Vous devez également fournir un jeton d’accès pour utiliser spécifiquement [!DNL Conversions API]. Reportez-vous à la documentation [!DNL Conversions API] sur la [génération d&#39;un jeton d&#39;accès](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) pour connaître les étapes d&#39;obtention de cette valeur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![ ID [!DNL Pixel] fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/server/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Intégration à l’extension Facebook et Instagram {#facebook}

L’intégration à l’aide de l’extension Facebook et Instagram vous permet de vous authentifier rapidement dans votre compte Meta Business. Cela renseigne ensuite automatiquement votre [!UICONTROL Pixel ID] et l’API Meta Conversions [!UICONTROL Access Token], ce qui facilite l’installation et la configuration de l’API Meta Conversions.

Une invite de dialogue pour l’authentification dans Facebook et Instagram s’affiche lors de l’installation de l’extension [!UICONTROL Meta Conversions API].

![ La page d’installation de l’ [!UICONTROL extension de l’API de conversion de métadonnées] surlignant [!UICONTROL Connectez-vous à un méta].](../../../images/extensions/server/meta/mbe-extension-install.png)

Une invite de dialogue permettant de s’authentifier dans Facebook et Instagram s’affiche également dans l’interface utilisateur du processus de démarrage rapide dans le transfert d’événement.

![ L’interface utilisateur de démarrage rapide surlignant [!UICONTROL Connectez-vous à un méta].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Intégration à Event Quality Match Score (EMQ) {#emq}

L’intégration à Event Quality Match Score (EMQ) vous permet d’afficher facilement l’efficacité de votre mise en oeuvre en affichant les scores EMQ. Cette intégration minimise le changement de contexte et vous aide à améliorer le succès de vos mises en oeuvre d’API de métadonnées de conversion. Ces scores d’événement apparaissent dans l’écran de configuration de l’ [!UICONTROL extension de l’API de métadonnées].

![ La page de configuration [!UICONTROL l’extension de l’API de métadonnées] qui surligne [!UICONTROL Afficher le score EMQ].](../../../images/extensions/server/meta/emq-score.png)

## Intégration à LiveRamp (Alpha) {#alpha}

Les clients [!DNL LiveRamp] qui ont déployé la solution de trafic authentifié (ATS) de [!DNL LiveRamp] sur leurs sites peuvent choisir de partager les RampID en tant que paramètre d’informations client. Veuillez travailler avec votre équipe de compte [!DNL Meta] pour participer au programme d’Alpha de cette fonctionnalité.

![La page de configuration [!UICONTROL Rule] du transfert d’événement Meta met en surbrillance [!UICONTROL Partner Name (alpha)] et [!UICONTROL Partner ID (alpha)].](../../../images/extensions/server/meta/live-ramp.png)

## Configurer une règle de transfert d’événement {#rule}

Cette section explique comment utiliser l’extension [!DNL Conversions API] dans une règle de transfert d’événement générique. Dans la pratique, vous devez configurer plusieurs règles afin d’envoyer tous les [événements standard](https://developers.facebook.com/docs/meta-pixel/reference) acceptés via [!DNL Meta Pixel] et [!DNL Conversions API]. Pour les données d’application mobile, veuillez consulter les champs requis, les champs de données d’application, les paramètres d’informations client et les détails de données personnalisés [ici](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Les événements doivent être [envoyés en temps réel](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou aussi proches que possible du temps réel pour une meilleure optimisation des campagnes publicitaires.

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Extension de l’API de métadonnées]** pour l’extension, puis **[!UICONTROL Envoyer l’événement de l’API de conversion]** pour le type d’action.

![Le type d’action [!UICONTROL Envoyer la page vue] sélectionné pour une règle dans l’interface utilisateur de collecte de données.](../../../images/extensions/server/meta/select-action.png)

Des contrôles s’affichent pour vous permettre de configurer les données d’événement qui seront envoyées à [!DNL Meta] via l’élément [!DNL Conversions API]. Ces options peuvent être saisies directement dans les entrées fournies. Vous pouvez également sélectionner des éléments de données existants pour représenter les valeurs à la place. Les options de configuration sont divisées en quatre sections principales, comme indiqué ci-dessous.

| Section de configuration | Description |
| --- | --- |
| [!UICONTROL &#x200B; Paramètres d’événement de serveur &#x200B;] | Informations générales sur l’événement, notamment l’heure à laquelle il s’est produit et l’action source qui l’a déclenché. Pour plus d&#39;informations sur les [paramètres d&#39;événement standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) acceptés par [!DNL Conversions API], consultez la documentation destinée aux développeurs [!DNL Meta] .<br><br>Si vous utilisez à la fois [!DNL Meta Pixel] et [!DNL Conversions API] pour envoyer des événements, veillez à inclure un **[!UICONTROL Nom de l&#39;événement]** (`event_name`) et un **[!UICONTROL ID d&#39;événement]** (`event_id`) avec chaque événement, car ces valeurs sont utilisées pour la [déduplication d&#39;événements](#deduplication).<br><br>Vous avez également la possibilité de **[!UICONTROL Activer l’utilisation limitée de données]** pour vous aider à vous conformer aux désinscriptions des clients. Pour plus d’informations sur cette fonctionnalité, voir la documentation [!DNL Conversions API] sur les [ options de traitement des données](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) . |
| [!UICONTROL &#x200B; Paramètres d’informations sur le client] | Données d’identité utilisateur utilisées pour attribuer l’événement à un client. Certaines de ces valeurs doivent être hachées avant d’être envoyées à l’API.<br><br>Pour garantir une bonne connexion API commune et une qualité d’événement élevée (EMQ), il est recommandé d’envoyer tous les [ paramètres d’informations client acceptés](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) avec les événements de serveur. Ces paramètres doivent également être [classés par priorité en fonction de leur importance et de leur impact sur EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Données personnalisées] | Données supplémentaires à utiliser pour l’optimisation de la diffusion publicitaire, fournies sous la forme d’un objet JSON. Pour plus d’informations sur les propriétés acceptées pour cet objet, reportez-vous à la [[!DNL Conversions API] documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) .<br><br>Si vous envoyez un événement d’achat, vous devez utiliser cette section pour fournir les attributs requis `currency` et `value`. |
| [!UICONTROL Événement de test] | Cette option est utilisée pour vérifier si votre configuration provoque la réception des événements de serveur par [!DNL Meta] comme prévu. Pour utiliser cette fonctionnalité, cochez la case **[!UICONTROL Envoyer comme événement de test]** , puis fournissez le code d’événement de test de votre choix dans l’entrée ci-dessous. Une fois la règle de transfert d’événement déployée, si vous avez configuré correctement l’extension et l’action, les activités apparaissant dans la vue **[!DNL Test Events]** de [!DNL Meta Events Manager] doivent s’afficher. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle.

![[!UICONTROL Conserver les modifications] sélectionnées pour la configuration de l’action.](../../../images/extensions/server/meta/keep-changes.png)

Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Déduplication des événements {#deduplication}

Comme mentionné dans la [section des conditions préalables](#prerequisites), il est recommandé d’utiliser à la fois l’extension de balise [!DNL Meta Pixel] et l’extension de transfert d’événement [!DNL Conversions API] pour envoyer les mêmes événements du client et du serveur dans une configuration redondante. Cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par une extension ou une autre.

Si vous envoyez différents types d’événements du client et du serveur sans chevauchement entre les deux, la déduplication n’est pas nécessaire. Cependant, si un événement unique est partagé par [!DNL Meta Pixel] et [!DNL Conversions API], vous devez vous assurer que ces événements redondants sont dédupliqués afin que votre rapport ne soit pas affecté négativement.

Lors de l’envoi d’événements partagés, veillez à inclure un identifiant et un nom d’événement avec chaque événement que vous envoyez à partir du client et du serveur. Lorsque plusieurs événements portant le même ID et le même nom sont reçus, [!DNL Meta] utilise automatiquement plusieurs stratégies pour les dédupliquer et conserver les données les plus pertinentes. Pour plus d’informations sur ce processus, consultez la documentation [!DNL Meta] sur la [déduplication pour [!DNL Meta Pixel] et  [!DNL Conversions API] événements](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) .

## Workflow de démarrage rapide : extension de l’API de métadonnées (Beta) {#quick-start}

>[!IMPORTANT]
>
>* La fonction de démarrage rapide est disponible pour les clients qui ont acheté le package Real-Time CDP Prime et Ultimate. Pour plus dʼinformations, contactez votre représentant commercial Adobe.
>* Cette fonctionnalité est destinée aux nouvelles mises en oeuvre et ne prend actuellement pas en charge l’installation automatique d’extensions et de configurations sur les balises existantes et les propriétés de transfert d’événement.

>[!NOTE]
>
>Tout client existant peut utiliser les workflows de démarrage rapide pour créer une implémentation de référence qui peut être utilisée pour les éléments suivants :
>* Utilisez-le comme début d’une toute nouvelle mise en oeuvre.
>* Profitez-en comme implémentation de référence que vous pouvez examiner pour voir comment il a été configuré, puis répliqué dans vos implémentations de production actuelles.

La fonction de démarrage rapide vous permet de configurer facilement et efficacement l’API des conversions de métadonnées et les extensions de pixel de métadonnées. Cet outil automatise plusieurs étapes effectuées dans les balises Adobe et le transfert d’événement, réduisant considérablement le temps de configuration.

Cette fonctionnalité installe et configure automatiquement l’API des conversions de métadonnées et les extensions de pixel de métadonnées sur une nouvelle propriété de transfert d’événement et de balises générées automatiquement avec les règles et les éléments de données nécessaires. De plus, il installe et configure automatiquement le SDK Web et la banque de données Experience Platform. Enfin, la fonction de démarrage rapide publie automatiquement la bibliothèque à l’URL désignée dans un environnement de développement, ce qui permet la collecte de données côté client et le transfert d’événements côté serveur en temps réel via le transfert d’événements et l’Edge Network Experience Platform.

La vidéo suivante présente la fonction de démarrage rapide.

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### Installation de la fonction de démarrage rapide

>[!NOTE]
>
>Cette fonctionnalité est conçue pour vous aider à prendre en main une mise en oeuvre du transfert d’événement. Il ne délivrera pas de mise en oeuvre complète et complète de bout en bout qui prenne en charge tous les cas d’utilisation.

Cette configuration installe automatiquement l’API des conversions de métadonnées et les extensions des pixels de métadonnées. Cette mise en oeuvre hybride est recommandée par les métadonnées pour collecter et transférer les conversions d’événements côté serveur.
La fonction de configuration rapide est conçue pour aider les clients à prendre en main une mise en oeuvre de transfert d’événement et n’est pas destinée à fournir une mise en oeuvre complète et complète de bout en bout qui prend en charge tous les cas d’utilisation.

Pour installer la fonctionnalité, sélectionnez **[!UICONTROL Commencer]** pour **[!DNL Send Conversions Data to Meta]** sur la page **[!UICONTROL Accueil]** de la collecte de données Adobe Experience Platform.

![ Page d’accueil de la collecte de données montrant les données de conversion en méta](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Saisissez votre **[!UICONTROL Domaine]**, puis sélectionnez **[!UICONTROL Suivant]**. Ce domaine sera utilisé comme convention d’affectation des noms pour vos propriétés, règles, éléments de données, flux de données et propriétés de transfert d’événement générés automatiquement, etc.

![Écran de bienvenue demandant le nom de domaine](../../../images/extensions/server/meta/welcome.png)

Dans la boîte de dialogue **[!UICONTROL Configuration initiale]**, entrez votre **[!UICONTROL ID de méta-pixel]**, le **[!UICONTROL jeton d’accès à l’API de conversion de métadonnées]** et le **[!UICONTROL chemin d’accès à la couche de données]**, puis sélectionnez **[!UICONTROL Suivant]**.

![Boîte de dialogue de configuration initiale](../../../images/extensions/server/meta/initial-setup.png)

Patientez quelques minutes avant que le processus de configuration initial ne soit terminé, puis sélectionnez **[!UICONTROL Suivant]**.

![ Écran de confirmation de la configuration initiale terminée](../../../images/extensions/server/meta/setup-complete.png)

Dans la boîte de dialogue **[!UICONTROL Ajouter le code sur votre site]** , copiez le code fourni à l’aide de la fonction ![Copier](/help/images/icons/copy.png) et collez-le dans le `<head>` de votre site web source. Une fois la mise en oeuvre terminée, sélectionnez **[!UICONTROL Start Validation]**

![Ajouter du code dans la boîte de dialogue de votre site](../../../images/extensions/server/meta/add-code-on-your-site.png)

La boîte de dialogue [!UICONTROL Résultats de la validation] affiche les résultats de la mise en oeuvre de l’extension Meta. Sélectionnez **[!UICONTROL Suivant]**. Vous pouvez également voir d’autres résultats de validation en sélectionnant le lien **[!UICONTROL Assurance]**.

![Boîte de dialogue de résultats de test affichant les résultats de mise en oeuvre](../../../images/extensions/server/meta/test-results.png)

L’écran **[!UICONTROL Étapes suivantes]** confirme la fin de la configuration. À partir de là, vous avez la possibilité d’optimiser votre mise en oeuvre en ajoutant de nouveaux événements, qui s’affichent dans la section suivante.

Si vous ne souhaitez pas ajouter d’événements supplémentaires, sélectionnez **[!UICONTROL Fermer]**.

![Boîte de dialogue des étapes suivantes](../../../images/extensions/server/meta/next-steps.png)

#### Ajout d’événements supplémentaires

Pour ajouter de nouveaux événements, sélectionnez **[!UICONTROL Modifier la propriété web de vos balises]**.

![Boîte de dialogue Étapes suivantes présentant la modification de la propriété web de vos balises](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Sélectionnez la règle correspondant au méta-événement que vous souhaitez modifier. Par exemple, **MetaConversion_AddToCart**.

>[!NOTE]
>
>En l’absence d’événement, cette règle ne s’exécute pas. C’est vrai pour toutes les règles, avec la règle **MetaConversion_PageView** comme exception.

Pour ajouter un événement, sélectionnez **[!UICONTROL Ajouter]** sous l’en-tête [!UICONTROL Événements] .

![Page de propriétés de balise sans événement](../../../images/extensions/server/meta/edit-rule.png)

Sélectionnez le [!UICONTROL Type d’événement]. Dans cet exemple, nous avons sélectionné l’événement [!UICONTROL Click] et l’avons configuré pour se déclencher lorsque le bouton **.add-to-cart-button** est sélectionné. Sélectionnez **[!UICONTROL Conserver les modifications]**.

![ Écran de configuration d’événement affichant un événement de clic](../../../images/extensions/server/meta/event-configuration.png)

Le nouvel événement a été enregistré. Sélectionnez **[!UICONTROL Sélectionner une bibliothèque de travail]** et sélectionnez la bibliothèque à créer.

![Sélectionner une liste déroulante de bibliothèque de travail](../../../images/extensions/server/meta/working-library.png)

Sélectionnez ensuite la liste déroulante en regard de **[!UICONTROL Enregistrer dans la bibliothèque]** et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]**. La modification sera alors publiée dans la bibliothèque.

![Sélectionnez Enregistrer dans la bibliothèque et créer](../../../images/extensions/server/meta/save-and-build.png)

Répétez ces étapes pour tout autre événement de conversion de métadonnées que vous souhaitez configurer.

#### Configuration de la couche de données {#configuration}

>[!IMPORTANT]
>
>La manière dont vous mettez à jour cette couche de données globale dépend de l’architecture de votre site web. Une application d’une seule page sera différente d’une application de rendu côté serveur. Il est également possible que vous soyez entièrement responsable de la création et de la mise à jour de ces données dans le produit Balises. Dans toutes les instances, la couche de données devra être mise à jour entre l’exécution de chacune des `MetaConversion_* rules`. Si vous ne mettez pas à jour les données entre les règles, vous pouvez également rencontrer un cas où vous envoyez des données obsolètes du dernier `MetaConversion_* rule` dans le `MetaConversion_* rule` actif.

Pendant la configuration, on vous a demandé où se trouve votre couche de données. Par défaut, il s’agira de `window.dataLayer.meta` et, à l’intérieur de l’objet `meta`, vos données seront attendues, comme illustré ci-dessous.

![Métadonnées de couche de données](../../../images/extensions/server/meta/data-layer-meta.png)

Il est important de le comprendre, car chaque règle `MetaConversion_*` utilise cette structure de données pour transmettre les éléments de données pertinents à l’extension [!DNL Meta Pixel] et à l’extension [!DNL Meta Conversions API]. Reportez-vous à la documentation sur les [événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) pour plus d’informations sur les données requises par les différents événements de métadonnées.

Par exemple, si vous souhaitez utiliser la règle `MetaConversion_Subscribe`, vous devez mettre à jour `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv` et `window.dataLayer.meta.value` en fonction des propriétés d’objet décrites dans la documentation sur les [événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Vous trouverez ci-dessous un exemple de ce qui doit être exécuté sur un site web pour mettre à jour la couche de données avant l’exécution de la règle.

![ Mettre à jour les métadonnées de couche de données ](../../../images/extensions/server/meta/update-data-layer-meta.png)

Par défaut, le `<datalayerpath>.conversionData.eventId` sera généré de manière aléatoire par l’action &quot;Generate New Event Id&quot; sur l’un des `MetaConversion_* rules`.

Pour obtenir une référence locale sur l’aspect de la couche de données, vous pouvez ouvrir l’éditeur de code personnalisé sur l’élément de données `MetaConversion_DataLayer` de votre propriété.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL Meta] à l’aide de l’extension [!DNL Meta Conversions API]. À partir de là, il est recommandé d’étendre votre intégration en connectant plus de [!DNL Pixels] et en partageant plus d’événements, le cas échéant. L’une des actions suivantes peut vous aider à améliorer davantage les performances de votre publicité :

* Connectez tout autre [!DNL Pixels] qui n&#39;est pas encore connecté à une intégration [!DNL Conversions API].
* Si vous envoyez certains événements exclusivement par l’intermédiaire de [!DNL Meta Pixel] côté client, envoyez également ces mêmes événements au [!DNL Conversions API] du côté serveur.

Pour plus d&#39;informations sur la mise en oeuvre efficace de votre intégration, consultez la documentation [!DNL Meta] sur les [ bonnes pratiques pour l&#39;intégration  [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) . Pour plus d’informations sur les balises et le transfert d’événement dans Adobe Experience Cloud, reportez-vous à la [présentation des balises](../../../home.md).
