---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2023
description: Les notes de mise à jour de février 2023 pour Adobe Experience Platform.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
TQID: https://experienceleague.adobe.com/AU3yZmvLBZ7VS68Y-kOiJzRMYKhmpTreVuURZi28udI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
subfeature_v2:
  - id: a230274e-7e6e-49eb-b817-514495a710ac
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: c1f1ac67-ccab-4be9-a93a-b7faba1192c4
  - id: d1a87129-ba05-4f15-98b1-233618f1774a
  - id: de9975b2-c43a-4287-9698-4f4cad92b83f
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1332
ht-degree: 85%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 22 février 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service de requête](#query-service)
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
| [Amélioration de la politique de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) pour les intégrations avec les [destinations basées sur des fichiers (par lots)](/help/destinations/destination-types.md#file-based) | <p> Lorsque les profils ne sont plus qualifiés pour une politique de consentement, Experience Platform communique désormais de manière proactive sa sortie de politique aux destinations basées sur des fichiers. Cela suit la [version de février 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la même fonctionnalité pour les destinations de diffusion en continu. </p> <p> <b>Remarque </b> : cette fonctionnalité est disponible uniquement pour les clients et clientes de **[!UICONTROL Privacy and Security Shield]** et celles et ceux de **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**Documentation nouvelle ou mise à jour** {#destinations-new-updated-documentation}

| Documentation | Description |
| ----------- | ----------- |
| Documentation sur le fonctionnement des destinations | <p>Nous avons publié trois nouveaux articles explicatifs sur le fonctionnement des destinations, basés sur les questions courantes des utilisateurs et utilisatrices :</p> <p><ul><li>[Paramètres d’exportation configurables et communs des destinations](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportement d’exportation de profils selon les types de destinations](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestion des identités dans le workflow d’activation des destinations](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Obsolescence de champ via l’IU | Vous pouvez désormais [rendre obsolète les champs de vos schémas une fois les données ingérées](../../xdm/tutorials/field-deprecation-ui.md). L’obsolescence des champs XDM vous permet de supprimer des champs de la vue de l’IU tout en les conservant pour les utiliser. Si nécessaire, vous pouvez afficher à nouveau les champs obsolètes. Les segments, requêtes ou solutions en aval qui font référence à ces champs s’exécuteront normalement. |

{style="table-layout:auto"}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL Profil de prospect individuel XDM]](https://github.com/adobe/xdm/pull/1669/files) | La classe XDM Individual Prospect Profile inclut des identifiants fournis par les partenaires. |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [!UICONTROL Contraintes de limitation de la fréquence] | Le groupe de champs [!UICONTROL &#x200B; Contraintes de limitation de la fréquence &#x200B;] a été [mis à jour pour prendre en charge les événements personnalisés et de répétition](https://github.com/adobe/xdm/pull/1641/files). |
| Type de données | [!UICONTROL Référent web] | Les propriétés du référent web ont été [mises à jour pour inclure `xdm:linkName` et `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivement, il s’agit du nom et de la région de l’élément HTML sélectionné sur la page précédente. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - Détails de l’interaction du message] | [Le champ [!UICONTROL URL du dispositif de suivi] a été ajouté](https://github.com/adobe/xdm/pull/1665/files) à [!UICONTROL Adobe CJM ExperienceEvent]. Ce dispositif de suivi fournit l’URL sélectionnée par l’utilisateur ou l’utilisatrice. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - Informations sur l’interaction des messages] | [La propriété `meta:enum` vide a été supprimée](https://github.com/adobe/xdm/pull/1668/files) du champ URL [!UICONTROL Type de tracking]. |
| Type de données | [!UICONTROL Informations sur les médias] | [Le modèle RegEx de la propriété `videoSegment` dans le type de données [!UICONTROL Informations sur les médias] a été supprimé](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [présentation du système XDM](../../xdm/home.md). &#x200B;

## Service de requête {#query-service}

Le service de requête vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données à partir du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans l’espace de travail de science des données ou à ingérer dans le profil client en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activer les jeux de données pour les profils avec SQL | [Utilisez des libellés dans les requêtes CTAS afin qu’un jeu de données soit « activé pour le profil »](../../query-service/sql/syntax.md#create-table-as-select), ou utilisez Modifier pour mettre à jour les jeux de données existants à activer pour le profil. Vous pouvez utiliser cette structure SQL étendue pour fournir une prise en charge transparente des jeux de données dérivés pour vos cas d’utilisation professionnels de profil client en temps réel. Consultez le document [Flux SQL transparent pour les jeux de données dérivés](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md) pour plus d’informations. |
| Surveiller les requêtes planifiées | Utilisez l’[onglet Requêtes planifiées](../../query-service/ui/monitor-queries.md) pour trouver des informations importantes sur les exécutions de vos requêtes et vous abonner aux alertes. Surveillez les requêtes pour connaître les détails du planning, le statut et les messages ou codes d’erreur en cas d’échec. |
| Activer/désactiver la fonction de saisie automatique | Éliminez certaines commandes de métadonnées et améliorez les temps de traitement en [activant la fonction de saisie automatique du requêteur](../../query-service/ui/user-guide.md#auto-complete). Cette fonctionnalité suggère automatiquement des mots-clés SQL potentiels ainsi que des détails de table pour la requête au fur et à mesure que vous l’écrivez. |
| Échantillons de jeux de données | Spécifiez un taux d’échantillonnage dans votre requête et [utilisez des échantillons de jeux de données pour créer un exemple aléatoire uniforme](../../query-service/key-concepts/dataset-samples.md), ou créez des échantillons conditionnels en fonction de critères spécifiques. |

{style="table-layout:auto"}

Pour plus d’informations sur le service de requête, consultez la section [Présentation du service de requête](../../query-service/home.md).


## Édition B2B de Real-Time Customer Data Platform {#b2b}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activer le service de comptes associés | La nouvelle fonction de basculement vous permet d’activer le service de comptes associés sur votre compte. Pour plus d’informations, consultez le guide sur l’[activation du service de comptes associés](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Pour en savoir plus sur Real-time CDP B2B Edition, consultez la [présentation de Real-time CDP B2B Edition](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Désigner l’accès au niveau de l’abonnement avec [!DNL Google PubSub] | Vous pouvez désormais définir l’accès à un abonnement à une rubrique spécifique lors de l’utilisation de la source [!DNL Google PubSub] en fournissant l’ID d’abonnement lors de l’authentification. Pour plus d’informations, consultez le tutoriel sur l’authentification [!DNL Google PubSub] [à l’aide de l’API Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [l’interface utilisateur d’Experience Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingérer des données d’activité personnalisées à partir de [!DNL Marketo] | Vous pouvez désormais importer des données d’activité personnalisées depuis votre instance [!DNL Marketo] vers Experience Platform. Pour ingérer des données d’activité personnalisées, vous devez configurer des groupes de champs d’activités personnalisées dans le schéma Activités B2B et créer un flux de données à l’aide du jeu de données des activités. Une fois le flux de données terminé, le jeu de données ingéré contiendra les activités standard et personnalisées de votre instance [!DNL Marketo]. Vous pouvez ensuite utiliser [Query Service](../../query-service/home.md) pour accéder aux enregistrements d’activités personnalisées sur Experience Platform. Pour plus d’informations, consultez le guide sur la [création d’un flux de données pour les données d’activités personnalisées](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exclure les comptes non réclamés de [!DNL Marketo] | Vous pouvez maintenant configurer si vous souhaitez exclure ou inclure les comptes non réclamés de l’ingestion lors de la création d’un flux de données pour les données d’entreprise. Pour plus d’informations, consultez le guide sur la [création d’une connexion source et d’un flux de données pour [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
