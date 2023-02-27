---
title: Notes de mise à jour de Adobe Experience Platform - Février 2023
description: Notes de mise à jour de février 2023 pour Adobe Experience Platform.
source-git-commit: 72ae96f72bfffe376fec5c0e1dcf79406cb86a26
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 37%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 22 février 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Query Service](#query-service)
- [Édition B2B de Real-Time Customer Data Platform](#b2b)
- [Sources](#sources)

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-features}

| Fonctionnalité | Description |
| ----------- | ----------- |
| [Amélioration de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) pour les intégrations avec [destinations basées sur des fichiers (par lots)](/help/destinations/destination-types.md#file-based) | <p> Lorsque les profils ne sont plus qualifiés pour une stratégie de consentement, l’Experience Platform communique désormais de manière proactive sa sortie de stratégie vers des destinations basées sur des fichiers. Cela suit le [version de février 2023](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) de la même fonctionnalité pour les destinations de diffusion en continu. </p> <p> <b>Remarque</b>: Cette fonctionnalité est disponible uniquement pour les clients de **[!UICONTROL Protection de la vie privée et protection]** et ceux de **[!UICONTROL Bouclier de santé]**. </p> |

{style=&quot;table-layout:auto&quot;}

**Documentation nouvelle ou mise à jour** {#destinations-new-updated-documentation}

| Documentation | Description |
| ----------- | ----------- |
| Fonctionnement de la documentation sur les destinations | <p>Nous avons publié trois nouveaux articles explicatifs sur le fonctionnement des destinations, sur la base des questions courantes des utilisateurs :</p> <p><ul><li>[Paramètres d’exportation configurables et communs des destinations](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[Comportement d’exportation de profils pour différents types de destinations](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[Gestion des identités dans le workflow d’activation des destinations](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Dépréciation des champs via l’interface utilisateur | Vous pouvez désormais [abandonner les champs de vos schémas une fois les données ingérées](../../xdm/tutorials/field-deprecation-ui.md). L’obsolescence des champs XDM vous permet de supprimer des champs de l’interface utilisateur tout en les conservant pour les utiliser. Si nécessaire, vous pouvez afficher à nouveau les champs obsolètes. Les segments, requêtes ou solutions en aval qui référencent ces champs s’exécuteront normalement. |

{style=&quot;table-layout:auto&quot;}

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL Profil XDM Individual Prospect]](https://github.com/adobe/xdm/pull/1669/files) | La classe XDM Individual Prospect Profile inclut des identifiants fournis par les partenaires. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [!UICONTROL Contraintes de limitation de fréquence] | Le [!UICONTROL Contraintes de limitation de fréquence] le groupe de champs a été [mise à jour afin de prendre en charge les événements de répétition et personnalisés](https://github.com/adobe/xdm/pull/1641/files). |
| Type de données | [!UICONTROL Référent web] | Les propriétés du référent web ont été [mis à jour pour inclure `xdm:linkName` et `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). Respectivement, il s’agit du nom et de la région de l’élément de HTML sélectionné sur la page précédente. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - informations sur l’interaction du message] | [Le [!UICONTROL URL du dispositif de suivi] champ ajouté](https://github.com/adobe/xdm/pull/1665/files) au [!UICONTROL Adobe de CJM ExperienceEvent]. Ce dispositif de suivi fournit l’URL sélectionnée par l’utilisateur. |
| Groupe de champs | [!UICONTROL Adobe CJM ExperienceEvent - Détails de l’interaction du message] | [Le champ vide `meta:enum` La propriété a été supprimée.](https://github.com/adobe/xdm/pull/1668/files) de l’URL [!UICONTROL Type de suivi] champ . |
| Type de données | [!UICONTROL Informations sur les médias] | [Le modèle regex de `videoSegment` dans [!UICONTROL Informations sur les médias] datatype a été supprimé.](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, lisez le [Présentation du système XDM](../../xdm/home.md)&#x200B;

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger les données dans le [!DNL Data Lake] d’Adobe Experience Platform. Vous pouvez joindre n’importe quel jeu de données du lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, Data Science Workspace ou pour ingestion dans Real-Time Customer Profile.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activation des jeux de données pour les profils avec SQL | [Utiliser des LIBELLÉS dans les requêtes CTAS pour rendre un jeu de données &quot;profile enabled&quot;](../../query-service/sql/syntax.md#create-table-as-select)ou utilisez ALTER pour mettre à jour les jeux de données existants à activer pour le profil. Vous pouvez utiliser cette structure SQL étendue pour offrir une prise en charge transparente des attributs dérivés pour vos cas d’utilisation professionnels de profil client en temps réel. Voir [Flux SQL transparent pour le document d’attributs dérivés](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) pour plus d’informations. |
| Surveillance des requêtes planifiées | Utilisez la variable [Onglet Requêtes planifiées](../../query-service/ui/monitor-queries.md) pour trouver des informations importantes sur les exécutions de vos requêtes et vous abonner aux alertes. Surveillez les requêtes pour connaître les détails du planning, l’état et les messages/codes d’erreur en cas d’échec. |
| Activation/désactivation de la fonction de saisie automatique | Élimination de certaines commandes de métadonnées et amélioration des temps de traitement par [activation/désactivation de la fonction de saisie semi-automatique de Query Editor](../../query-service/ui/user-guide.md#auto-complete). Cette fonctionnalité suggère automatiquement les mots-clés SQL potentiels et les détails du tableau pour la requête au fur et à mesure que vous l’écrivez. |
| Exemples de jeux de données | Spécifiez un taux d’échantillonnage dans votre requête et [utiliser des exemples de jeux de données pour créer un exemple aléatoire uniforme ;](../../query-service/essential-concepts/dataset-samples.md)ou créer des exemples conditionnels en fonction de critères spécifiques. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur Query Service, consultez la section [présentation de Query Service](../../query-service/home.md).


## Édition B2B de Real-Time Customer Data Platform {#b2b}

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux professionnels du marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Activation du service de comptes associés | La nouvelle fonction de basculement vous permet d’activer le service de comptes associé sur votre compte. Pour plus d’informations, consultez le guide sur [activation du service de comptes associé](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur l’édition B2B de Real-Time CDP, lisez le [Présentation de Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Désigner l’accès au niveau de l’abonnement avec [!DNL Google PubSub] | Vous pouvez désormais définir l’accès à un abonnement à une rubrique spécifique lors de l’utilisation de la propriété [!DNL Google PubSub] source en fournissant l’ID d’abonnement lors de l’authentification. Pour plus d’informations, reportez-vous à la section [!DNL Google PubSub] tutoriel sur l’authentification [utilisation de l’API Flow Service](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) ou [Interface utilisateur de Platform](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| Ingestion de données d’activité personnalisées à partir de [!DNL Marketo] | Vous pouvez désormais importer des données d’activité personnalisées depuis votre [!DNL Marketo] à l’Experience Platform. Pour ingérer des données d’activité personnalisées, vous devez configurer des groupes de champs d’activités personnalisés dans le schéma Activités B2B et créer un flux de données à l’aide du jeu de données des activités. Une fois le flux de données terminé, le jeu de données ingéré contiendra les activités standard et personnalisées de votre [!DNL Marketo] instance. Vous pouvez ensuite utiliser [Query Service](../../query-service/home.md) pour accéder aux enregistrements d’activité personnalisés sur Platform. Pour plus d’informations, consultez le guide sur [création d’un flux de données pour les données d’activité personnalisées](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| Exclure les comptes non réclamés de [!DNL Marketo] | Vous pouvez maintenant configurer si vous souhaitez exclure ou inclure des comptes non réclamés de l’ingestion lors de la création d’un flux de données pour les données d’entreprise. Pour plus d’informations, consultez le guide sur [création d’une connexion source et d’un flux de données pour [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
