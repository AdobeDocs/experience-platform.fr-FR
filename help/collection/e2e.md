---
title: Présentation de la collecte de données Adobe Experience Platform de bout en bout
description: Présentation générale de l’envoi de données d’événement aux solutions Adobe Experience Cloud à l’aide de la collecte de données Adobe Experience Platform.
source-git-commit: b14d592c8beb5fc545ae0682000e4e05b6dac3a0
workflow-type: tm+mt
source-wordcount: '2569'
ht-degree: 1%

---

# Collecte de données Adobe Experience Platform - Aperçu de bout en bout

La collecte de données Adobe Experience Platform fournit plusieurs technologies qui fonctionnent ensemble pour collecter vos données vers d’autres produits Adobe ou destinations tierces. Pour envoyer des données d’événement de votre application au réseau Adobe Experience Platform Edge, il est important de comprendre ces technologies de base et de les configurer afin de fournir vos données aux destinations dont vous avez besoin, lorsque vous en avez besoin.

Ce guide fournit un tutoriel général sur la manière d’envoyer un événement par le biais du réseau Edge à l’aide des technologies de collecte de données. Plus précisément, le tutoriel décrit les étapes à suivre pour installer et configurer l’extension de balise SDK Web Adobe Experience Platform dans l’interface utilisateur de la collecte de données.

>[!NOTE]
>
>Vous pouvez également choisir d’installer et de configurer le SDK manuellement si vous ne souhaitez pas utiliser de balises, mais les étapes environnantes doivent toujours être effectuées comme indiqué ci-dessous.

## Conditions préalables

Ce tutoriel utilise l’interface utilisateur de la collecte de données pour créer un schéma, configurer un flux de données et installer le SDK Web. Pour effectuer ces actions dans l’interface utilisateur, vous devez avoir accès à au moins une propriété web avec les [droits de propriété](../tags/ui/administration/user-permissions.md#property-rights) suivants :

* Développer
* Gérer les extensions

Consultez le guide sur la [gestion des autorisations pour les balises](../tags/ui/administration/manage-permissions.md) pour savoir comment accorder l’accès aux propriétés et aux droits de propriété.

Pour utiliser les différents produits de collecte de données mentionnés dans ce guide, vous devez également avoir accès aux flux de données et la possibilité de créer et de gérer des schémas. Si vous avez besoin d’accéder à l’une de ces fonctionnalités, contactez votre CSM pour vous aider à obtenir l’accès nécessaire. Si vous n’avez pas acheté Adobe Experience Platform, Adobe vous donnera l’accès nécessaire pour utiliser le SDK sans frais supplémentaires.

Si vous avez déjà accès à Platform, vous devez vous assurer que toutes les [autorisations](../access-control/home.md#permissions) sous les catégories suivantes sont activées :

* Modélisation des données
* Identités

Voir la [présentation de l’interface utilisateur du contrôle d’accès](../access-control/ui/overview.md) pour savoir comment accorder des autorisations pour les fonctionnalités de Platform aux utilisateurs.

## Résumé du processus

Le processus de configuration du réseau Edge pour votre site web peut être résumé comme suit :

1. [Créez un ](#schema) schéma afin de déterminer la structure de vos données lors de leur envoi au réseau Edge.
1. [Créez un schéma de ](#datastream) données pour configurer les destinations vers lesquelles vos données doivent être envoyées.
1. [Installez et configurez le ](#sdk) SDK Web pour envoyer des données à la banque de données lorsque certains événements se produisent sur votre site Web.

Une fois que vous avez la possibilité d’envoyer des données au réseau Edge, vous pouvez également [configurer le transfert d’événement](#event-forwarding) si votre organisation dispose d’une licence pour ce transfert.

## Création d’un schéma {#schema}

[Le modèle de données d’expérience (XDM)](../xdm/home.md)  est une spécification open source qui fournit des structures et des définitions communes pour les données sous la forme de schémas. En d’autres termes, XDM est un moyen de structurer et de mettre en forme vos données d’une manière exploitable par le réseau Edge et d’autres applications Adobe Experience Cloud.

La première étape de la configuration de vos opérations de collecte de données consiste à créer un schéma XDM pour représenter vos données. À une étape ultérieure de ce tutoriel, vous allez mapper les données que vous souhaitez envoyer à la structure de ce schéma.

>[!NOTE]
>
>Les schémas XDM sont très personnalisables. Plutôt que d’être trop prescriptif, les étapes décrites ci-dessous portent spécifiquement sur les exigences de schéma pour le SDK Web. En dehors de ces paramètres, vous êtes libre de définir la structure restante de vos données comme vous le souhaitez.

Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. À partir de là, vous pouvez voir une liste des schémas créés précédemment et appartenant à votre organisation. Pour continuer, sélectionnez **[!UICONTROL Créer un schéma]**, puis **[!UICONTROL XDM ExperienceEvent]** dans le menu déroulant.

![Espace de travail des schémas](./images/e2e/schemas.png)

Une boîte de dialogue s’affiche pour vous inviter à commencer à ajouter des groupes de champs au schéma. Pour envoyer des événements à l’aide du SDK Web, vous devez ajouter le groupe de champs **[!UICONTROL Mixin ExperienceEvent du SDK Web AEP]**. Ce groupe de champs contient des définitions pour les attributs de données automatiquement collectés par la bibliothèque SDK Web.

Utilisez la barre de recherche pour réduire la liste afin de faciliter la recherche de ce groupe de champs. Une fois que vous l’avez trouvé, sélectionnez-le dans la liste avant de sélectionner **[!UICONTROL Ajouter des groupes de champs]**.

![Espace de travail des schémas](./images/e2e/add-field-group.png)

Le canevas de schéma s’affiche, présentant une arborescence de votre schéma XDM comprenant les champs fournis par le groupe de champs SDK Web.

![Structure d&#39;un schéma](./images/e2e/schema-structure.png)

Sélectionnez le champ racine dans l’arborescence pour ouvrir les **[!UICONTROL propriétés du schéma]** dans le rail de droite, où vous pouvez fournir un nom et une description facultative du schéma.

![Nommer le schéma](./images/e2e/name-schema.png)

Si vous souhaitez ajouter d’autres champs au schéma, vous pouvez le faire en sélectionnant **[!UICONTROL Ajouter]** sous la section **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![Ajouter des groupes de champs](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>Pour obtenir des instructions détaillées sur la recherche de différents groupes de champs en fonction de vos cas d’utilisation, consultez le guide sur l’ [ajout de groupes de champs](../xdm/ui/resources/schemas.md#add-field-groups) dans la documentation XDM .
>
>La bonne pratique consiste à ajouter uniquement des champs pour les données que vous prévoyez d’envoyer par le biais du réseau Edge. Une fois que vous avez ajouté des champs à un schéma et que vous l’avez enregistré, seules des modifications supplémentaires peuvent être apportées au schéma par la suite. Pour plus d’informations, reportez-vous à la section [règles d’évolution des schémas](../xdm/schema/composition.md#evolution) .

Une fois que vous avez ajouté les champs dont vous avez besoin, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma.

![Enregistrement du schéma](./images/e2e/save-schema.png)

## Création dʼun flux de données {#datastream}

Un flux de données est une configuration qui indique au réseau Edge où vous souhaitez que vos données soient envoyées. Plus précisément, un flux de données indique à quels produits Experience Cloud vous souhaitez envoyer les données et comment vous souhaitez que les données soient traitées et stockées dans chaque produit.

>[!NOTE]
>
>Si vous souhaitez utiliser le [transfert d’événement](../tags/ui/event-forwarding/overview.md) (en supposant que votre organisation dispose d’une licence pour la fonctionnalité), vous devez l’activer pour un flux de données de la même manière que vous activez les produits Adobe. Les détails de ce processus sont traités dans une [section ultérieure](#event-forwarding).

Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Flux de données]**. À partir de là, vous pouvez sélectionner une zone de données existante dans la liste à modifier ou créer une configuration en sélectionnant **[!UICONTROL Nouvelle zone de données]**.

![Flux de données](./images/e2e/datastreams.png)

Les exigences de configuration d’un flux de données dépendent des produits et fonctionnalités auxquels vous envoyez des données. Pour plus d’informations sur les options de configuration de chaque produit, consultez la [présentation des flux de données](../edge/fundamentals/datastreams.md).

## Installation et configuration du SDK Web

Une fois que vous avez créé un schéma et un flux de données, l’étape suivante consiste à installer et à configurer le SDK Web Platform pour commencer à envoyer des données au réseau Edge.

>[!NOTE]
>
>Cette section utilise l’interface utilisateur de la collecte de données pour configurer l’extension de balise du SDK Web, mais vous pouvez également l’installer et la configurer à l’aide du code brut à la place. Pour plus d’informations, consultez les guides suivants :
>
>* [Installation du SDK](../edge/fundamentals/installing-the-sdk.md)
>* [Configuration du SDK](../edge/fundamentals/configuring-the-sdk.md)

>
>Notez également que même si vous souhaitez uniquement utiliser le transfert d’événement, vous devez tout de même installer et configurer le SDK comme décrit avant de configurer le transfert d’événement à une [étape ultérieure](#event-forwarding).

Le processus peut être résumé comme suit :

1. [Installez le SDK Web de Adobe Experience Platform sur une ](#install-sdk) propriété de balise pour accéder à ses fonctionnalités.
1. [Créez un ](#data-element) élément de données d’objet XDM pour mapper les variables de votre site web à la structure du schéma XDM que vous avez créé précédemment.
1. [Créez une ](#rule) règle pour indiquer au SDK quand il doit envoyer des données au réseau Edge.
1. [Créez et installez une ](#library) bibliothèque pour mettre en oeuvre la règle sur votre site web.

### Installation du SDK sur une propriété de balise {#install-sdk}

Sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche pour afficher une liste des propriétés de balise. Si vous le souhaitez, vous pouvez choisir une propriété existante à modifier ou sélectionner **[!UICONTROL Nouvelle propriété]** à la place.

![Propriétés](./images/e2e/properties.png)

Si vous créez une propriété, nommez-la de manière descriptive et définissez [!UICONTROL Plateforme] sur **[!UICONTROL Web]**. Indiquez le domaine complet de la propriété web, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Créer une propriété](./images/e2e/create-property.png)

La page d’aperçu de la propriété s’affiche. À partir de là, sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Catalogue]**. Recherchez la liste du SDK Web Platform (éventuellement à l’aide de la barre de recherche pour limiter les résultats) et sélectionnez **[!UICONTROL Installer]**.

![Installation du SDK Web](./images/e2e/install-sdk.png)

La page de configuration du SDK s’affiche. La plupart des valeurs requises sont automatiquement renseignées avec des valeurs par défaut que vous pouvez modifier si vous le souhaitez.

![Configuration du SDK Web](./images/e2e/configure-sdk.png)

Toutefois, avant de pouvoir installer le SDK, vous devez sélectionner un flux de données pour savoir où envoyer vos données. Sous **[!UICONTROL Flux de données]**, utilisez le menu déroulant pour sélectionner le flux de données que vous avez configuré à une [étape précédente](#datastream). Une fois que vous avez défini le flux de données, sélectionnez **[!UICONTROL Enregistrer]** pour terminer l’installation du SDK sur la propriété.

![Définition d’un flux de données et enregistrement](./images/e2e/set-datastream.png)

### Création d’un élément de données XDM {#data-element}

Pour que le SDK envoie des données au réseau Edge, ces données doivent être mappées au schéma XDM que vous avez créé lors d’une [étape précédente](#schema). Ce mappage est effectué par l’utilisation d’un élément de données.

Dans l’interface utilisateur, sélectionnez **[!UICONTROL Éléments de données]**, puis sélectionnez **[!UICONTROL Créer un élément de données]**.

![Création d’un élément de données](./images/e2e/data-elements.png)

Sur l’écran suivant, sélectionnez **[!UICONTROL SDK Web Adobe Experience Platform]** dans la liste déroulante [!UICONTROL Extension], puis sélectionnez **[!UICONTROL Objet XDM]** pour le type d’élément de données.

![Type d’objet XDM](./images/e2e/xdm-object.png)

La boîte de dialogue de configuration s’affiche pour le type d’objet XDM. La boîte de dialogue sélectionne automatiquement votre environnement de test Platform. Vous pouvez y voir tous les schémas qui ont été créés dans cet environnement de test. Sélectionnez le schéma XDM que vous avez créé précédemment dans la liste.

![Type d’objet XDM](./images/e2e/select-schema.png)

La structure du schéma apparaît. Tous les champs avec un astérisque (**\***) indiquent les champs qui seront automatiquement renseignés lorsque les événements se déclenchent. Pour tous les autres champs, vous pouvez explorer la structure du schéma et renseigner le reste des données.

![Mappage des données aux champs XDM](./images/e2e/map-schema.png)

>[!NOTE]
>
>La capture d’écran ci-dessus montre comment mapper une variable accessible globalement du côté client de votre site web (`cartAbandonsTotal`) à un champ XDM en référençant son nom dans le champ [!UICONTROL Valeur], entouré de signes de pourcentage (`%`).
>
>Vous pouvez également utiliser d’autres éléments de données créés précédemment pour remplir ces champs. Pour plus d’informations, voir la référence sur les [éléments de données](../tags/ui/managing-resources/data-elements.md) dans la documentation sur les balises.

Une fois que vous avez terminé de mapper vos données au schéma, attribuez un nom à l’élément de données avant de sélectionner **[!UICONTROL Enregistrer]**.

![Nommer et enregistrer l’élément de données](./images/e2e/name-and-save.png)

### Créez une règle

Après avoir enregistré l’élément de données, l’étape suivante consiste à créer une règle qui l’enverra au réseau Edge chaque fois qu’un certain événement se produit sur votre site web (par exemple, lorsqu’un client ajoute un produit à un panier).

Par exemple, cette section explique comment créer une règle qui se déclenche lorsqu’un client ajoute un article à un panier. Cependant, vous pouvez configurer des règles pour pratiquement tous les événements qui peuvent se produire sur votre site web.

Sélectionnez **[!UICONTROL Règles]** dans le volet de navigation de gauche, puis **[!UICONTROL Créer une règle]**.

![Règles](./images/e2e/rules.png)

Dans l’écran suivant, donnez un nom à la règle. À partir de là, l’étape suivante consiste à déterminer l’événement pour la règle (en d’autres termes, le moment où la règle se déclenchera). Sélectionnez **[!UICONTROL Ajouter]** sous [!UICONTROL Événements].

![Règle de nom](./images/e2e/name-rule.png)

La page de configuration des événements s’affiche. Pour configurer un événement, vous devez d’abord sélectionner le type d’événement. Les types d’événement sont fournis par les extensions. Pour configurer un événement &quot;form submit&quot;, par exemple, sélectionnez l’extension **[!UICONTROL Core]**, puis sélectionnez le type d’événement **[!UICONTROL Submit]** sous la catégorie **[!UICONTROL Form]**. Dans la boîte de dialogue de configuration qui s’affiche, vous pouvez fournir le sélecteur CSS du formulaire spécifique sur lequel vous souhaitez que cette règle se déclenche.

>[!NOTE]
>
>Pour plus d’informations sur les différents types d’événements fournis par les extensions web d’Adobe, y compris sur la manière de les configurer, consultez la [référence des extensions d’Adobe](../tags/extensions/web/overview.md) dans la documentation des balises.

Sélectionnez **[!UICONTROL Conserver les modifications]** pour ajouter l’événement à la règle.

![Configuration des événements](./images/e2e/event-config.png)

La page de configuration des règles réapparaît, indiquant que l’événement a été ajouté. Vous pouvez réduire la valeur &quot;[!UICONTROL If]&quot; en ajoutant d’autres conditions à la règle.

Dans le cas contraire, l’étape suivante consiste à ajouter une action que la règle doit exécuter lors de son déclenchement. Sélectionnez **[!UICONTROL Ajouter]** sous **[!UICONTROL Actions]** pour continuer.

![Ajouter une action](./images/e2e/add-action.png)

La page de configuration des actions s’affiche. Pour obtenir la règle permettant d’envoyer des données au réseau Edge, sélectionnez **[!UICONTROL SDK Web Adobe Experience Platform]** pour l’extension et **[!UICONTROL Envoyer l’événement]** pour le type d’action.

![Type d’action](./images/e2e/action-type.png)

L’écran se met à jour afin d’afficher des options supplémentaires pour configurer l’action d’envoi d’événement. Sous **[!UICONTROL Type]**, vous pouvez fournir une valeur de type personnalisé pour renseigner le champ XDM `eventType`. Sous **[!UICONTROL Données XDM]**, indiquez le nom du type de données XDM que vous avez créé précédemment (entouré de signes de pourcentage) ou sélectionnez l’icône de base de données (![Icône de base](./images/e2e/database-symbol.png)) pour le sélectionner dans une liste. Il s’agit des données qui seront finalement envoyées au réseau Edge.

Sélectionnez **[!UICONTROL Conserver les modifications]** lorsque vous avez terminé.

![Configuration de l’action](./images/e2e/action-config.png)

Une fois la configuration de la règle terminée, sélectionnez **[!UICONTROL Enregistrer]** pour terminer le processus.

![Enregistrer la règle](./images/e2e/save-rule.png)

### Création et installation d’une bibliothèque {#library}

Une fois la règle configurée, vous êtes prêt à l’ajouter à une bibliothèque de balises, à la créer dans un environnement et à l’installer sur votre site web.

>[!NOTE]
>
>Si vous n’avez pas encore configuré d’environnement dans l’interface utilisateur de collecte de données, vous devez le faire avant de pouvoir créer une version. Pour plus d’informations, reportez-vous à la section [Configuration d’un environnement pour une propriété web](../tags/ui/publishing/environments.md#web-configuration) dans la documentation sur les balises.

Pour savoir comment créer une bibliothèque, ajouter des extensions et des règles à la bibliothèque et la créer dans un environnement, consultez le guide sur la [gestion des bibliothèques](../tags/ui/publishing/libraries.md) dans la documentation sur les balises. Lorsque vous créez la bibliothèque, veillez à inclure l’extension SDK Web Platform et les règles de collecte de données que vous avez créées précédemment.

Une fois que vous avez créé la bibliothèque et que sa version a été affectée à un environnement, vous pouvez installer cet environnement du côté client de votre site web. Voir la section [installation des environnements](../tags/ui/publishing/environments.md#installation) pour plus d’informations.

Une fois l’environnement installé sur votre site web, vous pouvez [tester votre mise en oeuvre](../tags/ui/publishing/embed-code-testing.md) à l’aide du débogueur Adobe Experience Platform.

## Configuration du transfert d’événement (facultatif) {#event-forwarding}

>[!NOTE]
>
>Le transfert d’événement n’est disponible que pour les organisations qui ont reçu une licence.

Une fois que vous avez configuré le SDK pour envoyer des données au réseau Edge, vous pouvez configurer le transfert d’événement pour indiquer au réseau Edge où vous souhaitez que ces données soient diffusées.

Pour utiliser le transfert d’événement, vous devez d’abord créer une propriété de transfert d’événement. Sélectionnez **[!UICONTROL Transfert d’événement]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Nouvelle propriété]**. Attribuez un nom à la propriété avant de sélectionner **[!UICONTROL Enregistrer]**.

Une fois que vous avez créé une propriété de transfert d’événement, l’étape suivante consiste à créer une règle qui détermine où les données doivent être envoyées. Les règles pour les propriétés de transfert d’événement sont créées de la même manière que les propriétés de balise, à l’exception qu’aucun événement ne peut être spécifié (puisque le transfert d’événement traite uniquement des événements qu’il reçoit directement de la banque de données). Pour l’action de la règle, vous pouvez utiliser l’une des extensions de transfert d’événement disponibles ou utiliser du code personnalisé pour diffuser l’événement à la place.

![Règle de transfert d’événement](./images/e2e/event-forwarding-rule.png)

Comme auparavant, une fois la règle configurée, vous devez l’ajouter à une bibliothèque et la créer dans un environnement.

Une fois la génération terminée, l’étape finale consiste à mettre à jour la structure de données que vous avez [précédemment configurée](#datastream) et à activer le transfert d’événement. Pour commencer, accédez à **[!UICONTROL Ensembles de données]** et sélectionnez le flux de données en question dans la liste. À partir de là, activez la bascule pour le transfert d’événement et indiquez les noms de la propriété et de l’environnement que vous venez de configurer.

![Flux de données de transfert d’événement](./images/e2e/event-forwarding-datastream.png)

## Étapes suivantes

Ce guide fournit un aperçu général de bout en bout de la manière d’envoyer des données au réseau Edge à l’aide du SDK Web Platform. Pour plus d’informations sur les différents composants et services impliqués, reportez-vous à la documentation associée à ce guide.
