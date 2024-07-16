---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2023
description: Les notes de mise à jour de février 2023 pour Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 96%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 22 février 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Query Service](#query-service)
- [Édition B2B de Real-Time Customer Data Platform](#b2b)
- [Sources](#sources)

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

### Assurance {#assurance}

Adobe Assurance permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont accomplies dans l’application mobile.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| API publiques | Les API d’Adobe Assurance sont désormais disponibles. Les API Assurance sont un ensemble d’API qui permettent aux utilisateurs et utilisatrices de tester et de déboguer leurs propres applications web et mobiles, lorsqu’elles sont équipées de l’extension Adobe Assurance avec le SDK mobile. Pour en savoir plus sur les API Assurance, consultez lire la [présentation de l’API Assurance](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Pour plus d’informations sur l’assurance, consultez la [documentation sur l’assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-features}

| Fonctionnalité | Description |
| ----------- | ----------- |
| [Amélioration de la politique de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) pour les intégrations avec les [destinations basées sur des fichiers (par lots)](/help/destinations/destination-types.md#file-based) | <p> Lorsque les profils ne sont plus qualifiés pour une politique de consentement, Experience Platform communique désormais de manière proactive sa sortie de politique aux destinations basées sur des fichiers. Cela suit la [version de février 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la même fonctionnalité pour les destinations de diffusion en continu. </p> <p> <b>Remarque</b> : cette fonctionnalité est disponible uniquement pour les clientes et clients de **[!UICONTROL Privacy and Security Shield]** et celles et ceux de **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour** {#destinations-new-updated-documentation}

| Documentation | Description |
| ----------- | ----------- |
| Documentation sur le fonctionnement des destinations | <p>Nous avons publié trois nouveaux articles explicatifs sur le fonctionnement des destinations, basés sur les questions courantes des utilisateurs et utilisatrices :</p> <p><ul><li>[Paramètres d’exportation configurables et communs des destinations](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportement d’exportation de profils selon les types de destinations](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestion des identités dans le workflow d’activation des destinations](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obsolescence de champ via l’IU | Vous pouvez désormais [rendre obsolète les champs de vos schémas une fois les données ingérées](../../xdm/tutorials/field-deprecation-ui.md). L’obsolescence des champs XDM vous permet de supprimer des champs de la vue de l’IU tout en les conservant pour les utiliser. Si nécessaire, vous pouvez afficher à nouveau les champs obsolètes. Les segments, requêtes ou solutions en aval qui font référence à ces champs s’exécuteront normalement. |

{style="table-layout:auto"}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1669/files) | La classe XDM Individual Prospect Profile inclut des identifiants fournis par les partenaires. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [!UICONTROL Contraintes de limitation de la fréquence] | Le groupe de champs [!UICONTROL Contraintes de limitation de la fréquence] a été [mis à jour pour prendre en charge les événements personnalisés et de répétition](https://github.com/adobe/xdm/pull/1641/files). |
| Type de données | [!UICONTROL Référent web] | Les propriétés du référent web ont été [mises à jour pour inclure `xdm:linkName` et `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivement, il s’agit du nom et de la région de l’élément HTML sélectionné sur la page précédente. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - Informations sur l’interaction des messages] | [Le champ [!UICONTROL URL du dispositif de suivi] a été ajouté](https://github.com/adobe/xdm/pull/1665/files) à [!UICONTROL Adobe CJM ExperienceEvent]. Ce dispositif de suivi fournit l’URL sélectionnée par l’utilisateur ou l’utilisatrice. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - Informations sur l’interaction des messages] | [La propriété vide `meta:enum` a été supprimée](https://github.com/adobe/xdm/pull/1668/files) du champ [!UICONTROL Type de suivi] de l’URL. |
| Type de données | [!UICONTROL Informations sur les médias] | [Le modèle RegEx de la propriété `videoSegment` dans le type de données [!UICONTROL Informations sur les médias] a été supprimé](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer en tant que profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activer les jeux de données pour les profils avec SQL | [Utilisez des libellés dans les requêtes CTAS afin qu’un jeu de données soit « activé pour le profil »](../../query-service/sql/syntax.md#create-table-as-select), ou utilisez Modifier pour mettre à jour les jeux de données existants à activer pour le profil. Vous pouvez utiliser cette structure SQL étendue pour offrir une prise en charge transparente des jeux de données dérivés pour vos cas d’utilisation professionnels de profil client en temps réel. Pour plus d’informations, voir le document [Flux SQL transparent pour les jeux de données dérivés](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) . |
| Surveiller les requêtes planifiées | Utilisez l’[onglet Requêtes planifiées](../../query-service/ui/monitor-queries.md) pour trouver des informations importantes sur les exécutions de vos requêtes et vous abonner aux alertes. Surveillez les requêtes pour connaître les détails du planning, le statut et les messages ou codes d’erreur en cas d’échec. |
| Activer la fonction de saisie automatique | Éliminez certaines commandes de métadonnées et améliorez les temps de traitement en [activant la fonction de saisie automatique de Query Editor](../../query-service/ui/user-guide.md#auto-complete). Cette fonctionnalité suggère automatiquement des mots-clés SQL potentiels ainsi que des détails de table pour la requête au fur et à mesure que vous l’écrivez. |
| Échantillons de jeux de données | Spécifiez un taux d’échantillonnage dans votre requête et [utilisez des échantillons de jeux de données pour créer un exemple aléatoire uniforme](../../query-service/key-concepts/dataset-samples.md), ou créez des échantillons conditionnels en fonction de critères spécifiques. |

{style="table-layout:auto"}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).


## Édition B2B de Real-Time Customer Data Platform {#b2b}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activer le service de comptes associés | La nouvelle fonction de basculement vous permet d’activer le service de comptes associés sur votre compte. Pour plus d’informations, consultez le guide sur l’[activation du service de comptes associés](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Pour en savoir plus sur Real-time CDP B2B Edition, consultez la [présentation de Real-time CDP B2B Edition](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Désigner l’accès au niveau de l’abonnement avec [!DNL Google PubSub] | Vous pouvez désormais définir l’accès à un abonnement à une rubrique spécifique lors de l’utilisation de la source [!DNL Google PubSub] en fournissant l’ID d’abonnement lors de l’authentification. Pour plus d’informations, reportez-vous au tutoriel sur l’authentification [!DNL Google PubSub] [à l’aide de l’API Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou de l’[IU de Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingérer des données d’activité personnalisées à partir de [!DNL Marketo] | Vous pouvez désormais importer des données d’activité personnalisées depuis votre instance [!DNL Marketo] vers Experience Platform. Pour ingérer des données d’activité personnalisées, vous devez configurer des groupes de champs d’activités personnalisées dans le schéma Activités B2B et créer un flux de données à l’aide du jeu de données des activités. Une fois le flux de données terminé, le jeu de données ingéré contiendra les activités standard et personnalisées de votre instance [!DNL Marketo]. Vous pouvez ensuite utiliser [Query Service](../../query-service/home.md) pour accéder aux enregistrements d’activités personnalisées sur Platform. Pour plus d’informations, consultez le guide sur la [création d’un flux de données pour les données d’activités personnalisées](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exclure les comptes non réclamés de [!DNL Marketo] | Vous pouvez maintenant configurer si vous souhaitez exclure ou inclure les comptes non réclamés de l’ingestion lors de la création d’un flux de données pour les données d’entreprise. Pour plus d’informations, consultez le guide sur la [création d’une connexion source et d’un flux de données pour [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
