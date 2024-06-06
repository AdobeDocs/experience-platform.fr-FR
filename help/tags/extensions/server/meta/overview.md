---
title: Présentation de l’extension de l’API Meta Conversions
description: Découvrez l’extension de l’API Meta Conversions pour le transfert d’événement dans Adobe Experience Platform.
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 3cd937f49f27006e3cab60df1692d33138944ce2
workflow-type: tm+mt
source-wordcount: '2583'
ht-degree: 0%

---

# [!DNL Meta Conversions API] présentation de l’extension

La variable [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) vous permet de connecter vos données marketing côté serveur à [!DNL Meta] des technologies permettant d’optimiser le ciblage de vos publicités, de réduire le coût par action et de mesurer les résultats. Les événements sont liés à un [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) Les identifiants et sont traités de la même manière que les événements côté client.

En utilisant la variable [!DNL Meta Conversions API] , vous pouvez tirer parti des fonctionnalités de l’API dans votre [transfert d’événement](../../../ui/event-forwarding/overview.md) règles d’envoi de données à [!DNL Meta] de l’Edge Network Adobe Experience Platform. Ce document explique comment installer l’extension et utiliser ses fonctionnalités dans un transfert d’événement. [règle](../../../ui/managing-resources/rules.md).

## Démonstration

La vidéo suivante est destinée à vous aider à comprendre les [!DNL Meta Conversions API].

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## Conditions préalables

Il est vivement recommandé d’utiliser [!DNL Meta Pixel] et la variable [!DNL Conversions API] partager et envoyer les mêmes événements du côté client et du côté serveur, respectivement, car cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par [!DNL Meta Pixel]. Avant d’installer le [!DNL Conversions API] , consultez le guide sur la [[!DNL Meta Pixel] extension](../../client/meta/overview.md) pour savoir comment l’intégrer dans vos implémentations de balises côté client.

>[!NOTE]
>
>La section sur [déduplication des événements](#deduplication) plus loin, ce document décrit les étapes à suivre pour s’assurer que le même événement n’est pas utilisé deux fois, car il peut être reçu à la fois du navigateur et du serveur.

Pour utiliser la variable [!DNL Conversions API] , vous devez avoir accès au transfert d’événement et disposer d’un [!DNL Meta] compte avec accès à [!DNL Ad Manager] et [!DNL Event Manager]. Plus précisément, vous devez copier l’identifiant d’un [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (ou [créer [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) ) afin que l’extension puisse être configurée sur votre compte.

>[!INFO]
>
>Si vous prévoyez d’utiliser cette extension avec des données d’application mobile ou si vous utilisez également des données d’événement hors ligne dans votre [!DNL Meta] campagnes, vous devrez créer votre jeu de données par le biais d’une application existante et sélectionner **Créer à partir d’un ID de pixel** lorsque vous y êtes invité. Voir l’article [Déterminez quelle option de création de jeux de données convient à votre entreprise.](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) pour plus d’informations. Voir [API de conversion pour les événements d’application](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) document pour tous les paramètres de suivi d’application requis et facultatifs.

## Installation l’extension

Pour installer le [!DNL Meta Conversions API] , accédez à l’interface utilisateur de la collecte de données ou à l’interface utilisateur Experience Platform et sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche. À partir de là, sélectionnez une propriété à laquelle ajouter l’extension ou créez une propriété à la place.

Une fois que vous avez sélectionné ou créé la propriété souhaitée, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez l’option **[!UICONTROL Catalogue]** . Recherchez le [!UICONTROL API des conversions de métadonnées] carte, puis sélectionnez **[!UICONTROL Installer]**.

![La variable [!UICONTROL Installer] sélectionnée pour l’option [!UICONTROL API des conversions de métadonnées] dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/meta/install.png)

Dans la vue de configuration qui s’affiche, vous devez fournir la variable [!DNL Pixel] ID que vous avez copié précédemment pour lier l’extension à votre compte. Vous pouvez coller l’identifiant directement dans l’entrée ou vous pouvez utiliser un élément de données à la place.

Vous devez également fournir un jeton d’accès pour utiliser la variable [!DNL Conversions API] spécifiquement. Voir [!DNL Conversions API] documentation sur [générer un jeton d’accès](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) pour savoir comment obtenir cette valeur.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**

![La variable [!DNL Pixel] ID fourni en tant qu’élément de données dans la vue de configuration de l’extension.](../../../images/extensions/server/meta/configure.png)

L’extension est installée et vous pouvez désormais utiliser ses fonctionnalités dans vos règles de transfert d’événement.

## Intégration à l’extension Facebook et Instagram {#facebook}

L’intégration à l’aide de l’extension Facebook et Instagram vous permet de vous authentifier rapidement dans votre compte Meta Business. Cela renseigne ensuite automatiquement la variable [!UICONTROL ID de pixel] et l’API de métadonnées de conversion [!UICONTROL Jeton d’accès], ce qui facilite l’installation et la configuration de l’API de métadonnées de conversion.

Une invite de dialogue permettant de s’authentifier dans Facebook et Instagram s’affiche lors de l’installation du [!UICONTROL API des conversions de métadonnées] extension .

![La variable [!UICONTROL Extension de l’API Meta Conversions] mise en surbrillance de la page d’installation [!UICONTROL Connexion aux métadonnées].](../../../images/extensions/server/meta/mbe-extension-install.png)

Une invite de dialogue permettant de s’authentifier dans Facebook et Instagram s’affiche également dans l’interface utilisateur du processus de démarrage rapide dans le transfert d’événement.

![Mise en surbrillance de l’interface utilisateur de processus de démarrage rapide [!UICONTROL Connexion aux métadonnées].](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## Intégration à Event Quality Match Score (EMQ) {#emq}

L’intégration à Event Quality Match Score (EMQ) vous permet d’afficher facilement l’efficacité de votre mise en oeuvre en affichant les scores EMQ. Cette intégration minimise le changement de contexte et vous aide à améliorer le succès de vos mises en oeuvre d’API de métadonnées de conversion. Ces scores d’événement apparaissent dans la variable [!UICONTROL Extension de l’API Meta Conversions] écran de configuration.

![La variable [!UICONTROL Extension de l’API Meta Conversions] mise en surbrillance de page de configuration [!UICONTROL Afficher le score EMQ].](../../../images/extensions/server/meta/emq-score.png)

## Intégration à LiveRamp (Alpha) {#alpha}

[!DNL LiveRamp] des clients qui [!DNL LiveRamp]La solution de trafic authentifié (ATS) de’ peut choisir de partager les RampID en tant que paramètre d’informations client. Veuillez travailler avec votre [!DNL Meta] l’équipe du compte pour rejoindre le programme d’Alpha de cette fonctionnalité.

![Transfert d’événement Meta [!UICONTROL Règle] mise en surbrillance de page de configuration [!UICONTROL Nom du partenaire (alpha)] et [!UICONTROL Identifiant du partenaire (alpha)].](../../../images/extensions/server/meta/live-ramp.png)

## Configurer une règle de transfert d’événement {#rule}

Cette section explique comment utiliser la variable [!DNL Conversions API] dans une règle générique de transfert d’événement. En pratique, vous devez configurer plusieurs règles afin d&#39;envoyer toutes les règles acceptées [événements standard](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] et [!DNL Conversions API]. Pour les données d’application mobile, veuillez consulter les champs requis, les champs de données d’application, les paramètres d’informations client et les détails de données personnalisées. [here](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events).

>[!NOTE]
>
>Les événements doivent être [envoyé en temps réel](https://www.facebook.com/business/help/379226453470947?id=818859032317965) ou aussi près que possible du temps réel pour une meilleure optimisation des campagnes publicitaires.

Commencez à créer une règle de transfert d’événement et configurez ses conditions selon vos besoins. Lors de la sélection des actions de la règle, sélectionnez **[!UICONTROL Extension de l’API Meta Conversions]** pour l’extension, puis sélectionnez **[!UICONTROL Envoi de l’événement d’API de conversion]** pour le type d’action.

![La variable [!UICONTROL Envoyer la page vue] type d’action sélectionné pour une règle dans l’interface utilisateur de la collecte de données.](../../../images/extensions/server/meta/select-action.png)

Les commandes qui s’affichent vous permettent de configurer les données d’événement qui seront envoyées à [!DNL Meta] via le [!DNL Conversions API]. Ces options peuvent être saisies directement dans les entrées fournies. Vous pouvez également sélectionner des éléments de données existants pour représenter les valeurs à la place. Les options de configuration sont divisées en quatre sections principales, comme indiqué ci-dessous.

| Section de configuration | Description |
| --- | --- |
| [!UICONTROL Paramètres d’événement du serveur] | Informations générales sur l’événement, notamment l’heure à laquelle il s’est produit et l’action source qui l’a déclenché. Voir [!DNL Meta] documentation destinée aux développeurs pour plus d’informations sur le [paramètres d’événement standard](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) accepté par le [!DNL Conversions API].<br><br>Si vous utilisez les deux [!DNL Meta Pixel] et la variable [!DNL Conversions API] pour envoyer des événements, veillez à inclure une **[!UICONTROL Nom de l’événement]** (`event_name`) et **[!UICONTROL Identifiant d’événement]** (`event_id`) avec chaque événement, car ces valeurs sont utilisées pour [déduplication des événements](#deduplication).<br><br>Vous avez également la possibilité de **[!UICONTROL Activer l’utilisation limitée de données]** pour vous aider à vous conformer aux désinscriptions des clients. Voir [!DNL Conversions API] documentation sur [options de traitement des données](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) pour plus d’informations sur cette fonctionnalité. |
| [!UICONTROL Paramètres d’informations client] | Données d’identité utilisateur utilisées pour attribuer l’événement à un client. Certaines de ces valeurs doivent être hachées avant d’être envoyées à l’API.<br><br>Pour garantir une bonne connexion API commune et une qualité d’événement élevée (EMQ), il est recommandé d’envoyer tous les [paramètres d’informations client acceptés](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) à côté des événements de serveur. Ces paramètres doivent également être [Priorisés en fonction de leur importance et de leur impact sur l&#39;QE](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL Données personnalisées] | Données supplémentaires à utiliser pour l’optimisation de la diffusion publicitaire, fournies sous la forme d’un objet JSON. Voir [[!DNL Conversions API] documentation](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) pour plus d’informations sur les propriétés acceptées pour cet objet.<br><br>Si vous envoyez un événement d’achat, vous devez utiliser cette section pour fournir les attributs requis `currency` et `value`. |
| [!UICONTROL Événement test] | Cette option permet de vérifier si votre configuration entraîne la réception d’événements de serveur par [!DNL Meta] comme prévu. Pour utiliser cette fonctionnalité, sélectionnez la variable **[!UICONTROL Envoyer comme événement de test]** , puis fournissez un code d’événement de test de votre choix dans l’entrée ci-dessous. Une fois la règle de transfert d’événement déployée, si vous avez configuré correctement l’extension et l’action, les activités apparaissant dans la variable **[!DNL Test Events]** afficher dans [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’action à la configuration de la règle.

![[!UICONTROL Conserver les modifications] sélectionné pour la configuration de l’action.](../../../images/extensions/server/meta/keep-changes.png)

Lorsque la règle vous satisfait, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**. Enfin, publiez un nouveau transfert d’événement. [build](../../../ui/publishing/builds.md) pour activer les modifications apportées à la bibliothèque.

## Déduplication des événements {#deduplication}

Comme indiqué dans la section [section conditions préalables](#prerequisites), il est recommandé d’utiliser les [!DNL Meta Pixel] l’extension de balise et la variable [!DNL Conversions API] extension de transfert d’événement pour envoyer les mêmes événements du client et du serveur dans une configuration redondante. Cela peut aider à récupérer les événements qui n’ont pas été sélectionnés par une extension ou une autre.

Si vous envoyez différents types d’événements du client et du serveur sans chevauchement entre les deux, la déduplication n’est pas nécessaire. Cependant, si un événement unique est partagé par les deux [!DNL Meta Pixel] et la variable [!DNL Conversions API], vous devez vous assurer que ces événements redondants sont dédupliqués afin que vos rapports ne soient pas affectés négativement.

Lors de l’envoi d’événements partagés, veillez à inclure un identifiant et un nom d’événement avec chaque événement que vous envoyez à partir du client et du serveur. Lorsque plusieurs événements portant le même ID et le même nom sont reçus, [!DNL Meta] utilise automatiquement plusieurs stratégies pour les dédupliquer et conserver les données les plus pertinentes. Voir [!DNL Meta] documentation sur [déduplication pour [!DNL Meta Pixel] et [!DNL Conversions API] events](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) pour plus d’informations sur ce processus.

## Workflow de démarrage rapide : extension de l’API des métadonnées (version bêta) {#quick-start}

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

Pour installer la fonctionnalité, sélectionnez **[!UICONTROL Prise en main]** pour **[!DNL Send Conversions Data to Meta]** sur la collecte de données Adobe Experience Platform **[!UICONTROL Accueil]** page.

![Page d’accueil de la collecte de données présentant les données de conversion en métadonnées](../../../images/extensions/server/meta/conversion-data-to-meta.png)

Saisissez votre **[!UICONTROL Domaine]**, puis sélectionnez **[!UICONTROL Suivant]**. Ce domaine sera utilisé comme convention d’affectation des noms pour vos propriétés, règles, éléments de données, flux de données et propriétés de transfert d’événement générés automatiquement, etc.

![Écran de bienvenue demandant le nom de domaine](../../../images/extensions/server/meta/welcome.png)

Dans le **[!UICONTROL Configuration initiale]** Entrez votre **[!UICONTROL ID de pixel de méta]**, **[!UICONTROL Jeton d’accès à l’API de conversion de métadonnées]**, et **[!UICONTROL Chemin de la couche de données]**, puis sélectionnez **[!UICONTROL Suivant]**.

![Boîte de dialogue Configuration initiale](../../../images/extensions/server/meta/initial-setup.png)

Patientez quelques minutes avant que le processus de configuration initial ne soit terminé, puis sélectionnez **[!UICONTROL Suivant]**.

![Écran de confirmation de la configuration initiale](../../../images/extensions/server/meta/setup-complete.png)

Dans la **[!UICONTROL Ajout de code sur votre site]** Copiez le code fourni à l’aide de la copie ![Copier](../../../images/extensions/server/meta/copy-icon.png) et collez-les dans la fonction `<head>` de votre site web source. Une fois l’implémentation effectuée, sélectionnez **[!UICONTROL Commencer la validation]**

![Ajout de code dans la boîte de dialogue de votre site](../../../images/extensions/server/meta/add-code-on-your-site.png)

La variable [!UICONTROL Résultats de la validation] affiche les résultats de la mise en oeuvre de l’extension Meta. Sélectionner **[!UICONTROL Suivant]**. Vous pouvez également afficher des résultats de validation supplémentaires en sélectionnant **[!UICONTROL Assurance]** lien.

![Boîte de dialogue des résultats de test affichant les résultats de mise en oeuvre](../../../images/extensions/server/meta/test-results.png)

La variable **[!UICONTROL Étapes suivantes]** l’affichage de l’écran confirme la fin de la configuration. À partir de là, vous avez la possibilité d’optimiser votre mise en oeuvre en ajoutant de nouveaux événements, qui s’affichent dans la section suivante.

Si vous ne souhaitez pas ajouter d’événements supplémentaires, sélectionnez **[!UICONTROL Fermer]**.

![Boîte de dialogue Étapes suivantes](../../../images/extensions/server/meta/next-steps.png)

#### Ajout d’événements supplémentaires

Pour ajouter de nouveaux événements, sélectionnez **[!UICONTROL Modification de la propriété web des balises]**.

![Boîte de dialogue des étapes suivantes présentant la modification de la propriété web de vos balises](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

Sélectionnez la règle correspondant au méta-événement que vous souhaitez modifier. Par exemple : **MetaConversion_AddToCart**.

>[!NOTE]
>
>En l’absence d’événement, cette règle ne s’exécute pas. Cela est vrai pour toutes les règles, avec la variable **MetaConversion_PageView** étant l’exception.

Pour ajouter une sélection d’événement **[!UICONTROL Ajouter]** sous le [!UICONTROL Événements] en-tête.

![Page de propriétés de balise sans événement](../../../images/extensions/server/meta/edit-rule.png)

Sélectionnez la variable [!UICONTROL Type d’événement]. Dans cet exemple, nous avons sélectionné la variable [!UICONTROL Cliquez sur] et l’ont configuré pour se déclencher lorsque la variable **Bouton Ajouter au panier** est sélectionnée. Sélectionnez **[!UICONTROL Conserver les modifications]**.

![Écran de configuration d’événement affichant un événement de clic](../../../images/extensions/server/meta/event-configuration.png)

Le nouvel événement a été enregistré. Sélectionner **[!UICONTROL Sélectionner une bibliothèque de travail]** et sélectionnez la bibliothèque à créer.

![Sélectionner une liste déroulante de bibliothèque de travail](../../../images/extensions/server/meta/working-library.png)

Sélectionnez ensuite la liste déroulante en regard de . **[!UICONTROL Enregistrer dans la bibliothèque]** et sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]**. La modification sera alors publiée dans la bibliothèque.

![Sélectionnez Enregistrer dans la bibliothèque et créer](../../../images/extensions/server/meta/save-and-build.png)

Répétez ces étapes pour tout autre événement de conversion de métadonnées que vous souhaitez configurer.

#### Configuration de la couche de données {#configuration}

>[!IMPORTANT]
>
>La manière dont vous mettez à jour cette couche de données globale dépend de l’architecture de votre site web. Une application d’une seule page sera différente d’une application de rendu côté serveur. Il est également possible que vous soyez entièrement responsable de la création et de la mise à jour de ces données dans le produit Balises. Dans toutes les instances, la couche de données doit être mise à jour entre l’exécution de chacune des `MetaConversion_* rules`. Si vous ne mettez pas à jour les données entre les règles, vous risquez également de rencontrer un cas où vous envoyez des données obsolètes du dernier `MetaConversion_* rule` dans la `MetaConversion_* rule`.

Pendant la configuration, on vous a demandé où se trouve votre couche de données. Par défaut, cette variable serait `window.dataLayer.meta`, et à l’intérieur du `meta` , vos données seront attendues comme illustré ci-dessous.

![Métadonnées de couche de données](../../../images/extensions/server/meta/data-layer-meta.png)

Il est important de comprendre la variable `MetaConversion_*` La règle utilise cette structure de données pour transmettre les éléments de données appropriés à la variable [!DNL Meta Pixel] et au [!DNL Meta Conversions API]. Reportez-vous à la documentation relative à [événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) pour plus d’informations sur les données requises pour différents événements de métadonnées.

Par exemple, si vous souhaitez utiliser la variable `MetaConversion_Subscribe` règle, vous devez mettre à jour `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv`, et `window.dataLayer.meta.value` conformément aux propriétés de l’objet décrites dans la documentation sur [événements standard](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

Vous trouverez ci-dessous un exemple de ce qui doit être exécuté sur un site web pour mettre à jour la couche de données avant l’exécution de la règle.

![Mise à jour des métadonnées de couche de données](../../../images/extensions/server/meta/update-data-layer-meta.png)

Par défaut, la variable `<datalayerpath>.conversionData.eventId` est généré de manière aléatoire par l’action &quot;Générer un nouvel ID d’événement&quot; sur l’un des `MetaConversion_* rules`.

Pour obtenir une référence locale sur l’aspect de la couche de données, vous pouvez ouvrir l’éditeur de code personnalisé sur la page `MetaConversion_DataLayer` élément de données sur votre propriété.

## Étapes suivantes

Ce guide explique comment envoyer des données d’événement côté serveur à [!DNL Meta] en utilisant la variable [!DNL Meta Conversions API] extension . À partir de là, il est recommandé d’étendre votre intégration en connectant plus [!DNL Pixels] et partager d’autres événements, le cas échéant. L’une des actions suivantes peut vous aider à améliorer davantage les performances de votre publicité :

* Connectez-vous à un autre [!DNL Pixels] qui ne sont pas encore connectés à un [!DNL Conversions API] intégration.
* Si vous envoyez certains événements exclusivement par [!DNL Meta Pixel] côté client, envoyez ces mêmes événements au [!DNL Conversions API] du côté serveur également.

Voir [!DNL Meta] documentation sur [bonnes pratiques pour la [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) pour plus d’informations sur la mise en oeuvre efficace de votre intégration. Pour plus d’informations sur les balises et le transfert d’événement dans Adobe Experience Cloud, reportez-vous à la section [présentation des balises](../../../home.md).
