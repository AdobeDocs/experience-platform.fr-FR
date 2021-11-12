---
keywords: RTCDP;CDP;Édition B2B;Real-time Customer Data Platform;plateforme de données client en temps réel;cdp en temps réel;b2b;cdp
solution: Experience Platform
title: Prise en main de Real-time Customer Data Platform B2B Edition
description: Utilisez cet exemple de scénario comme exemple lors de la configuration de votre mise en oeuvre de Real-time Customer Data Platform B2B Edition.
source-git-commit: e6f71954d52e0a998955c3420307417cc011c24d
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 1%

---

# Prise en main de Real-time Customer Data Platform B2B Edition

Ce document fournit un processus de haut niveau de bout en bout pour la prise en main de l’édition B2B de Real-time Customer Data Platform (CDP), à l’aide d’un exemple de cas d’utilisation pour illustrer des concepts clés.

La société de technologie Bodea souhaite combiner des données personnelles et de compte provenant de différentes sources de données isolées afin de cibler efficacement les clients avec un email et une campagne publicitaire LinkedIn pour son nouveau produit. Bodea utilise Marketo Engage comme plateforme d’automatisation marketing et doit segmenter une audience spécifique à B2B à partir de plusieurs CRM contenant des données client.

## Prise en main

Ce workflow de tutoriel repose sur plusieurs services Adobe Experience Platform dans le cadre de la démonstration. Si vous souhaitez suivre cette procédure, il est recommandé de bien comprendre les services suivants :

- [Modèle de données d’expérience (XDM)](../xdm/home.md)
- [Sources](../sources/home.md)
- [Segmentation](../segmentation/home.md)
- [Destinations](../destinations/home.md)

## Création de schémas pour vos données

Dans le cadre de la configuration initiale, le service informatique de Bodea doit créer un schéma XDM pour s’assurer que ses données suivent un format standard lors de leur importation dans Platform et qu’elles sont exploitables dans différents services Platform et produits Adobe Experience Cloud (Adobe Analytics et Adobe Target, par exemple).

Adobe Experience Platform vous permet de générer automatiquement les schémas et les espaces de noms requis pour les sources de données B2B. Cet outil permet de s’assurer que les schémas créés décrivent les données d’une manière structurée et réutilisable. Suivez la [Espaces de noms B2B et documentation de l’utilitaire de génération automatique de schéma](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) pour une référence complète au processus de configuration.

Dans l’interface utilisateur de Adobe Experience Platform, le spécialiste marketing de la boîte sélectionne **[!UICONTROL Schémas]** dans le rail de gauche, suivi de la fonction **[!UICONTROL Parcourir]** . Comme ils ont utilisé l’utilitaire de génération automatique du Marketo Engage, les nouveaux schémas vides apparaissent dans la liste et tous comportent un préfixe &quot;B2B&quot;.

![Onglet Parcourir de l’espace de travail des schémas](./assets/b2b-tutorial/empty-b2b-schemas.png)

L’utilitaire de génération automatique a défini la structure de modèle de données pour les schémas à l’aide des classes XDM B2B standard (telles que [Compte d’entreprise XDM](../xdm/classes/b2b/business-account.md) et [Opportunités commerciales XDM](../xdm/classes/b2b/business-opportunity.md)) qui capturent les entités de données B2B fondamentales. En outre, les schémas B2B générés automatiquement sur ces classes ont des relations préétablies qui permettent des cas d’utilisation de segmentation avancés. Les groupes de champs supplémentaires requis pour la structure de données peuvent facilement être créés ici via l’interface utilisateur. Voir [Guide de l’interface utilisateur XDM, ajout de groupes de champs à une section de schéma](../xdm/ui/resources/schemas.md#add-field-groups) pour plus d’informations.

>[!NOTE]
> 
>Si vous n’utilisez pas l’utilitaire de génération automatique ou si une nouvelle relation doit être créée, consultez le tutoriel sur [création de relations entre les schémas B2B](../xdm/tutorials/relationship-b2b.md).

Real-time Customer Profile fusionne des données provenant de sources disparates afin de créer des profils consolidés de principales entités B2B. Puisque les profils sont générés en fonction d’une seule classe, l’utilitaire de génération automatique configure des relations entre les schémas en fonction de cas d’utilisation métier courants. Par conséquent, l’équipe Bodea est maintenant prête à ingérer des données en fonction de leurs schémas B2B.

>[!NOTE]
> 
>Les espaces de noms d’identité par défaut, les clés Principales et les relations créés pour les schémas par l’utilitaire de génération automatique sont facilement détectables dans l’espace de travail des schémas.
>
>![affichage de l’identité et de la relation du schéma par défaut](./assets/b2b-tutorial/schema-identity-relationship.png)

## Ingestion de vos données dans Experience Platform

Ensuite, le spécialiste marketing de la boîte utilise la variable [Connecteur Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) pour ingérer des données dans Platform en vue de les utiliser dans des services en aval. Vous pouvez également ingérer des données à l’aide de l’une des sources approuvées pour l’édition B2B de la plateforme CDP en temps réel.

>[!NOTE]
> 
>Pour savoir quels connecteurs source sont disponibles pour votre entreprise, vous pouvez afficher le catalogue de sources dans l’interface utilisateur de Platform. Pour accéder au catalogue, sélectionnez **Sources** dans le volet de navigation de gauche, puis sélectionnez **Catalogue**.

Pour créer une connexion entre un compte Marketo et Platform, vous devez acquérir des informations d’authentification. Voir [guide sur l’obtention des informations d’authentification du connecteur source Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) pour obtenir des instructions détaillées.

Après l’acquisition des informations d’authentification, le spécialiste du marketing de la boîte crée une connexion entre le compte Marketo et son organisation IMS de plateforme. Consultez la documentation pour obtenir des instructions sur [Comment connecter un compte Marketo à l’aide de l’interface utilisateur de Platform](../sources/tutorials/ui/create/adobe-applications/marketo.md).

Le connecteur source du Marketo Engage fournit une fonctionnalité de mappage automatique pour faciliter le processus de mappage de tous vos champs de données à ceux des schémas nouvellement créés.

>[!NOTE]
> 
>Si vous avez créé des groupes de champs personnalisés dans vos schémas XDM, vous pouvez avoir des champs non connectés à ce stade du processus. Veillez à vérifier toutes les valeurs qui renseignent vos groupes de champs personnalisés.

Le spécialiste du marketing de boîte vérifie que tous les groupes de champs sont correctement mappés et poursuit le processus de configuration des sources en initialisant un flux de données. En créant un flux de données pour importer les données Marketo, les données entrantes peuvent être utilisées par les services Platform en aval. Au cours du processus d’ingestion initial, les données sont introduites dans Experience Platform sous la forme d’un lot. Ensuite, les données ingérées suivantes sont diffusées en continu dans Profile avec des mises à jour en temps quasi réel.

## Création d’un segment pour évaluer vos données

La tâche suivante consiste à créer une audience pour la nouvelle campagne de marketing par e-mail de Bodea en fonction d’attributs spécifiques des entités associées dans les données source. Dans l’interface utilisateur de Platform, le spécialiste marketing de la boîte commence par sélectionner **[!UICONTROL Segments]** dans le volet de navigation de gauche, puis **[!UICONTROL Créer un segment]**.

Dans cet exemple, le segment trouve toutes les personnes qui travaillent dans le service des ventes et qui sont liées à n’importe quel compte ayant au moins une opportunité ouverte. Ce segment nécessite un lien entre la classe XDM Individual Profile, la classe XDM Business Account et la classe XDM Business Opportunity.

![Segment de cas d’utilisation](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Pour plus d’informations sur la création de segments afin d’évaluer vos données, voir [Guide de l’interface utilisateur du créateur de segments](../segmentation/ui/segment-builder.md). Pour des cas d’utilisation de la segmentation B2B plus spécifiques, reportez-vous à la section [présentation de la segmentation pour l’édition B2B de la plateforme CDP en temps réel](./segmentation/b2b.md).

Le créateur de segments vous permet de créer une audience vendable à partir des données de Real-time Customer Profile et d’afficher les estimations de votre audience potentielle en fonction de la combinaison des attributs, événements et audiences existantes que vous avez définies.

## Activation des données évaluées vers une destination

Une fois le segment créé, un résumé est fourni dans la variable [!UICONTROL Détails] de l’espace de travail. Comme aucune destination n’est actuellement activée pour le segment, le spécialiste marketing de la boîte doit exporter l’audience vers un jeu de données où elle peut être accessible et sur lequel il peut agir.

Dans le [!UICONTROL Segments] espace de travail de l’interface utilisateur de Platform, le spécialiste marketing de la boîte sélectionne **[!UICONTROL Activer la destination]**.

![Activation du segment vers une destination](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Voir le tutoriel sur [activation d’un segment vers une destination](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) pour obtenir des instructions complètes sur la manière d’y parvenir.

Le spécialiste du marketing de boîte active le segment vers la destination Marketo, ce qui lui permet de transférer les données de segment de Platform vers Marketo Engage sous la forme d’une liste statique. Consultez le guide sur la [Destination Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html?lang=fr) pour plus d’informations.

## Étapes suivantes

En suivant ce tutoriel, vous avez exploité avec succès les différents services Adobe Experience Platform utilisés par l’édition B2B de la plateforme CDP en temps réel. Par conséquent, vous avez appris à ingérer, segmenter, évaluer et exporter vos données B2B en tant qu’audiences exploitables pouvant être engagées sur différents canaux.
