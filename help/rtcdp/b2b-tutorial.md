---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;plateforme de données client en temps réel;real time cdp;b2b;cdp
solution: Experience Platform
title: Prise en main de Real-Time Customer Data Platform B2B edition
description: Utilisez cet exemple de scénario comme exemple lors de la configuration de votre implémentation d’Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions" newtab=true
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 43%

---

# Prise en main de Real-Time Customer Data Platform B2B edition

Ce document fournit un workflow de haut niveau de bout en bout pour la prise en main de Real-Time Customer Data Platform (CDP) B2B edition, à l’aide d’un exemple de cas d’utilisation pour illustrer des concepts clés.

La société de technologie Bodea souhaite combiner des données relatives aux personnes et aux comptes provenant de différentes sources de données cloisonnées afin de cibler efficacement les clients avec un e-mail et une campagne publicitaire LinkedIn pour son nouveau produit. Bodea utilise une plateforme d’automatisation du marketing et doit segmenter une audience spécifique au B2B à partir de plusieurs CRM contenant des données client.

## Prise en main

Ce workflow de tutoriel repose sur plusieurs services Adobe Experience Platform dans le cadre de la démonstration. Si vous souhaitez suivre cette procédure, il est recommandé de bien comprendre les services suivants :

- [Modèle de données d’expérience (XDM)](../xdm/home.md)
- [Sources](../sources/home.md)
- [Segmentation](../segmentation/home.md)
- [Destinations](../destinations/home.md)

## Création de schémas pour vos données

Dans le cadre de la configuration initiale, le service informatique de Bodea doit créer un schéma XDM pour s’assurer que ses données suivent un format standard lors de leur importation dans Experience Platform et qu’elles sont exploitables dans différents services Experience Platform et produits Adobe Experience Cloud (tels qu’Adobe Analytics et Adobe Target).

>[!WARNING]
>
>Vous devez suivre les modèles d’ingestion tels que décrits dans la documentation pertinente sur les sources dont vous trouverez les liens tout au long de ce tutoriel. Il n’est pas garanti que les autres méthodes de mappage de champs fonctionnent.

Adobe Experience Platform vous permet de générer automatiquement les schémas et les espaces de noms requis pour les sources de données B2B. Cet outil permet de s’assurer que les schémas créés décrivent les données d’une manière structurée et réutilisable. Suivez la [documentation de l’utilitaire de génération automatique de schémas et d’espaces de noms B2B](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) pour une référence complète au processus de configuration. 

Dans l’interface utilisateur de Adobe Experience Platform, le marketeur Bodea sélectionne **[!UICONTROL Schemas]** dans le rail de gauche, suivi de l’onglet **[!UICONTROL Browse]** . Comme ils ont utilisé l’utilitaire de génération automatique, les nouveaux schémas vides apparaissent dans la liste et comportent tous un préfixe « B2B ».

![Onglet Parcourir de l’espace de travail des schémas](./assets/b2b-tutorial/empty-b2b-schemas.png)

L’utilitaire de génération automatique a défini la structure de modèle de données pour les schémas à l’aide des classes XDM B2B standard (telles que [XDM Business Account](../xdm/classes/b2b/business-account.md) et [XDM Business Opportunity](../xdm/classes/b2b/business-opportunity.md)) qui capturent les entités de données B2B fondamentales. En outre, les schémas B2B générés automatiquement et construits sur ces classes ont des relations préétablies qui permettent des cas d’utilisation de segmentation avancés. Les groupes de champs supplémentaires requis pour la structure de données peuvent facilement être créés ici via l’interface utilisateur. Pour plus d’informations, consultez le [guide de l’interface utilisateur XDM, section Ajout de groupes de champs à un schéma](../xdm/ui/resources/schemas.md#add-field-groups). 

>[!NOTE]
> 
>Si vous n’utilisez pas l’utilitaire de génération automatique ou si une nouvelle relation doit être créée, consultez le tutoriel sur la [création de relations entre les schémas B2B](../xdm/tutorials/relationship-b2b.md).

Le profil client en temps réel fusionne des données provenant de sources disparates pour créer des profils consolidés d’entités B2B clés. Puisque les profils sont générés en fonction d’une seule classe, l’utilitaire de génération automatique configure des relations entre les schémas en fonction de cas d’utilisation métier courants. Par conséquent, l’équipe Bodea est maintenant prête à ingérer des données en fonction de leurs schémas B2B. 

>[!NOTE]
> 
>Les espaces de noms d’identité par défaut, les clés primaires et les relations créés pour les schémas par l’utilitaire de génération automatique sont facilement détectables dans l’espace de travail des schémas. 
>
>![affichage par défaut de l’identité du schéma et des relations dans l’interface utilisateur](./assets/b2b-tutorial/schema-identity-relationship.png)

## Ingestion de données dans Experience Platform

Ensuite, le marketeur Bodea utilise un [connecteur source](../sources/home.md) pour ingérer des données dans Experience Platform en vue de les utiliser dans des services en aval. Vous pouvez également ingérer des données à l’aide de l’une des sources approuvées pour Real-Time CDP B2B edition.

>[!NOTE]
> 
>Pour savoir quels connecteurs source sont disponibles pour votre organisation, vous pouvez afficher le catalogue de sources dans l’interface utilisateur d’Experience Platform. Pour accéder au catalogue, sélectionnez **Sources** dans le volet de navigation de gauche, puis sélectionnez **Catalogue**. 

Pour établir une connexion entre un compte source et Experience Platform, vous devez acquérir des informations d’authentification. Pour obtenir des instructions détaillées sur l’obtention des informations d’authentification pour chaque type de source, reportez-vous à la [présentation des sources](../sources/home.md).

Après l’acquisition des informations d’authentification, le marketeur Bodea crée une connexion entre le compte source et son organisation Experience Platform. Voir la [documentation sur les sources](../sources/home.md) pour plus d’informations sur la configuration d’une connexion source.

Le connecteur source fournit une fonctionnalité de mappage automatique pour faciliter le processus de mappage de tous vos champs de données à ceux des schémas nouvellement créés.

>[!NOTE]
> 
>Si vous avez créé des groupes de champs personnalisés dans vos schémas XDM, il se peut que vous ayez des champs non connectés à ce stade du processus. Veillez à vérifier toutes les valeurs qui renseignent vos groupes de champs personnalisés. 

Le spécialiste marketing Bodea vérifie que tous les groupes de champs sont correctement mappés et poursuit le processus de configuration des sources en initialisant un flux de données. En créant un flux de données pour importer les données sources, les données entrantes peuvent être utilisées par les services Experience Platform en aval. Au cours du processus d’ingestion initial, les données sont importées dans Experience Platform sous la forme d’un lot. Ensuite, les données ingérées suivantes sont diffusées en continu dans Profile avec des mises à jour en temps quasi réel. 

## Création d’une audience pour évaluer vos données

La tâche suivante consiste à créer une audience pour la nouvelle campagne de marketing par e-mail de Bodea en fonction d’attributs spécifiques des entités associées dans les données source. Dans l’interface utilisateur d’Experience Platform, le marketeur Bodea commence par sélectionner **[!UICONTROL Segments]** dans le volet de navigation de gauche, puis **[!UICONTROL Create segment]**.

Dans cet exemple, l’audience trouve toutes les personnes qui travaillent dans le service des ventes et qui sont liées à n’importe quel compte ayant au moins une opportunité ouverte. Ces audiences nécessitent un lien entre la classe XDM Individual Profile, la classe XDM Business Account et la classe XDM Business Opportunity.

![Segment de cas d’utilisation](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Pour plus d’informations sur la création d’audiences afin d’évaluer vos données, consultez le [guide de l’interface utilisateur du créateur de segments](../segmentation/ui/segment-builder.md). Pour des cas d’utilisation de la segmentation B2B plus spécifiques, reportez-vous à la [présentation de la segmentation pour Real-Time CDP B2B edition](./segmentation/b2b.md).

Le créateur de segments vous permet de créer une audience vendable à partir des données du profil client en temps réel et d’afficher les estimations de votre audience potentielle en fonction de la combinaison des attributs, événements et audiences existantes que vous avez définis.

## Activation de vos données évaluées vers une destination

Une fois l’audience créée, un résumé est fourni dans la section [!UICONTROL Details] de l’espace de travail. Comme aucune destination n’est actuellement activée pour la définition de segment, le marketeur Bodea doit exporter l’audience vers un jeu de données où elle peut être accessible et sur lequel il peut agir.

Dans l’espace de travail [!UICONTROL Segments] de l’interface utilisateur d’Experience Platform, le marketeur Bodea sélectionne **[!UICONTROL Activate to destination]**.

![Activer l’audience vers une destination](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Consultez le tutoriel sur [l’activation d’une audience vers une destination](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=fr) pour obtenir des instructions complètes sur la manière d’y parvenir.

Le marketeur Bodea active l’audience vers une destination, ce qui lui permet d’envoyer les données d’audience d’Experience Platform vers sa plateforme d’automatisation marketing. Lisez le [catalogue des destinations](../destinations/catalog/overview.md) pour plus d’informations sur les destinations disponibles.

## Étapes suivantes

En suivant ce tutoriel, vous avez exploité avec succès les différents services Adobe Experience Platform utilisés par Real-Time CDP B2B edition. Par conséquent, vous avez appris à ingérer, segmenter, évaluer et exporter vos données B2B en tant qu’audiences exploitables pouvant être engagées sur différents canaux. 
