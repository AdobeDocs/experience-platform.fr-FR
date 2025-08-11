---
title: Notes de mise à jour d’Adobe Experience Platform - Juillet 2025
description: Les notes de mise à jour de juillet 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: ht
source-wordcount: '1574'
ht-degree: 100%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : 29 juillet 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Capacité](#capacity)
- [Destinations](#destinations)
- [Ingestion de données](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [Sources](#sources)


## Capacité {#capacity}

>[!AVAILABILITY]
>
>Cette fonctionnalité peut être utilisée en fonction de votre région. Pour les utilisateurs et utilisatrices des Amériques, cette fonctionnalité sera disponible à partir du 11 août. Pour les utilisateurs et utilisatrices en Europe, cette fonctionnalité sera disponible à partir du 25 août. Pour les utilisateurs et utilisatrices en Asie, cette fonctionnalité sera disponible à partir du 8 septembre.

La capacité fournit une vue d’ensemble complète des [mécanismes de sécurisation](../../rtcdp/guardrails/overview.md) de votre organisation et fournit des recommandations sur la manière de résoudre les violations de capacité potentielles en allouant vos capacités à un niveau de sandbox. Avec cette version, vous pouvez afficher votre capacité pour l’ingestion en flux continu et la segmentation en flux continu.

Pour plus d’informations, consultez la [vue d’ensemble de la capacité](../../landing/license-usage-and-guardrails/capacity.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Destinations mises à jour**

| Destination | Description |
| --- | --- |
| Disponibilité limitée de la connexion [Ciblage par liste de clients de Google + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) | Après avoir été brièvement disponible pour toute la clientèle en juin, Adobe a rétabli la disponibilité limitée de cette intégration. Actuellement, l’accès à cette destination est limité à la clientèle qui en a déjà l’autorisation, tandis qu’Adobe et Google s’efforcent de résoudre les problèmes d’implémentation. Si vous souhaitez utiliser cette intégration après la reprise du déploiement général, contactez votre représentant ou représentante Adobe pour exprimer votre intention. |
| Mise à niveau interne de [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) | À compter du 31 juillet 2025, vous pourrez voir deux cartes [!DNL The Trade Desk] côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne du service de destinations. <br><br>Le connecteur de destination [!DNL The Trade Desk] existant a été renommé **[!UICONTROL (obsolète) The Trade Desk]** et une nouvelle carte portant le nom **[!UICONTROL The Trade Desk]** est désormais disponible. Utilisez la nouvelle connexion **[!UICONTROL The Trade Desk]** dans le catalogue pour obtenir de nouveaux flux de données d’activation. <br><br>Si des flux de données sont actifs vers la destination **[!UICONTROL (obsolète) The Trade Desk]**, ils seront automatiquement mis à jour. Aucune action n’est donc requise de votre part. <br><br>Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes :<ul><li>ID de spécification de flux : `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>ID de spécification de connexion : `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Noms et descriptions des comptes pour les connexions de destination | Vous pouvez désormais [ajouter des noms et des descriptions de compte](/help/destinations/ui/connect-destination.md) lors de la connexion aux destinations, ce qui permet une meilleure gestion des destinations avec plusieurs comptes. |
| Informations améliorées sur les trains de données pour les destinations Edge | Les informations du rail droit pour les destinations [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) et [Personnalisation sur mesure](/help/destinations/catalog/personalization/custom-personalization.md) ont été améliorées pour afficher le nom du flux de données, offrant ainsi une visibilité plus claire sur les configurations de trains de données associées et contribuant à réduire la confusion lors de la révision des flux de données existants. Le sélecteur **[!UICONTROL Identifiant du train de données]** dans l’écran de configuration de destination a été mis à jour vers **[!UICONTROL Train de données]** pour une plus grande clarté dans l’interface d’utilisation. |
| Visibilité des actions marketing dans la sélection de destination | Les actions marketing sont désormais affichées dans le rail droit de l’onglet **[[!UICONTROL Parcourir]](/help/destinations/ui/destinations-workspace.md#browse)** dans l’espace de travail Destinations et sur la page **[[!UICONTROL Exécutions de flux de données]](/help/dataflows/ui/monitor-destinations.md)**, offrant une visibilité immédiate sur les modifications apportées aux actions marketing sans avoir à accéder à la page d’affichage. Ceci améliore l’expérience clientèle en facilitant la vérification des configurations d’action marketing lors de la configuration de la destination. |
| [!BADGE Version bêta limitée]{type=Informative} Modifier les actions marketing pour les destinations | Vous pouvez désormais [modifier les actions marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) pour les destinations existantes. Cette fonctionnalité est actuellement en version bêta limitée. Pour obtenir l’accès, contactez votre représentant ou représentante Adobe. |
| [!BADGE Version bêta limitée]{type=Informative} Modifier les destinations | Vous pouvez désormais [modifier votre configuration de destination](/help/destinations/ui/edit-destination.md) après sa création. Cette fonctionnalité est actuellement en version bêta limitée. Pour obtenir l’accès, contactez votre représentant ou représentante Adobe. |

**Correctifs**

| Problème | Description |
| --- | --- |
| Fonctionnalité de défilement des catégories | Correction d’un problème en raison duquel le menu latéral des catégories dans le catalogue des destinations et des sources ne défilait pas correctement lors du pointage de la souris. Amélioration de la convivialité de la navigation pour les utilisateurs et utilisatrices qui parcourent les catégories de destination. |

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Ingestion de données {#ingestion}

Experience Platform fournit une structure complète d’ingestion de données qui prend en charge l’ingestion de données par lots et en flux continu à partir de diverses sources.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la surveillance de l’ingestion de profils en flux continu | La surveillance en temps réel de l’ingestion des profils en flux continu est désormais disponible, offrant ainsi une transparence sur les mesures de débit, de latence et de qualité des données. Cela participe à des alertes proactives et à des informations exploitables pour aider les ingénieures et ingénieurs de données à identifier les violations de capacité et les problèmes d’ingestion. Pour plus d’informations, consultez le guide sur la [surveillance de l’ingestion de profils en flux continu](../../dataflows/ui/monitor-streaming-profile.md). |

Pour plus d’informations, consultez la [vue d’ensemble d’ingestion de données](../../ingestion/home.md).

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition offre des fonctionnalités complètes de gestion des données client B2B. Cela permet aux entreprises de créer des profils client unifiés, de créer des audiences B2B sophistiquées et d’activer des données sur divers canaux marketing.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à niveau de l’architecture B2B | Experience Platform effectue une mise à niveau vers une nouvelle architecture B2B qui apporte des améliorations significatives aux audiences à entités multiples avec des attributs B2B. Cette mise à niveau consolide la prise en charge des politiques de fusion, améliore la précision du nombre d’audiences et améliore les fonctionnalités de résolution des entités. Consultez la [vue d’ensemble de la mise à niveau de l’architecture de Real-Time CDP B2B Edition](../../rtcdp/b2b-architecture-upgrade.md) pour une description complète des modifications. |
| Consolidation de la politique de fusion pour les audiences à entités multiples | Les audiences à entités multiples avec des attributs B2B ne prennent désormais en charge qu’une seule politique de fusion (la politique de fusion par défaut) au lieu de prendre en charge plusieurs politiques de fusion. Cette modification garantit une composition d’audiences cohérente et simplifie la gestion de la logique de fusion. Pour plus d’informations, reportez-vous à la [vue d’ensemble des politiques de fusion](../../profile/merge-policies/overview.md). |
| Nombres d’audiences améliorés pour les entités B2B | Les estimations de taille d’audience pour les audiences avec des entités B2B telles que Comptes et Opportunités sont désormais exactes, en fonction des résultats de segmentation en temps réel. Cette amélioration fournit des estimations plus précises et plus fiables pour les audiences impliquant des relations B2B complexes. |
| Instantanés de compte pour l’appartenance à une audience | Les détails d’appartenance à une audience sont désormais inclus pour les entités de compte dans les exportations d’instantanés. Cela permet d’accéder au statut d’audience au niveau du compte, aux horodatages et aux indicateurs d’appartenance. Cela apporte la parité des fonctionnalités entre les modèles de segmentation Profil (Personne) et Compte. |
| Modifications des outils sandbox pour les audiences à entités multiples | L’importation d’audiences à entités multiples avec des entités B2B et des événements d’expérience exportés avant la migration n’est plus prise en charge. La validation de l’importation de ces audiences échoue et elles ne peuvent pas être automatiquement converties dans la nouvelle architecture. Les audiences doivent être exportées à nouveau après la migration et avant l’importation dans les sandbox cibles. Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |
| Obsolescences de l’API d’entité B2B | Les opérations de recherche d’API [!DNL Profile Access] pour les entités B2B (relation compte-personne, relation opportunité-personne, campagne, membre de campagne, liste marketing et membres de liste marketing) sont désormais obsolètes. En outre, les opérations de suppression de l’API [!DNL Profile Access] pour les entités B2B (compte, relation compte-personne, opportunité, relation opportunité-personne, campagne, membre de campagne, liste marketing et membres de liste marketing) sont également obsolètes. Pour plus d’informations, consultez le [guide sur l’API de point d’entrée pour les entités](../../profile/api/entities.md). |
| Mises à jour de l’espace de noms d’identité pour la résolution des entités | Les entités Compte et Opportunité utilisent désormais la fusion basée sur la priorité temporelle avec des espaces de noms d’identité spécifiques (`b2b_account` pour Compte, `b2b_opportunity` pour Opportunité). Toutes les autres entités sont unifiées avec des chevauchements d’identités principales fusionnés à l’aide d’une fusion basée sur la priorité temporelle. Pour plus d’informations sur la résolution des entités, consultez le [guide sur l’API de point d’entrée pour les entités](../../profile/api/entities.md). |

Pour plus d’informations, consultez la [vue d’ensemble de Real-Time CDP B2B Edition](../../rtcdp/b2b-overview.md).

## Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modifications des imports d’audiences à entités multiples | Les outils sandbox ont été mis à jour pour prendre en charge la nouvelle mise à niveau de l’architecture B2B. Les audiences à entités multiples contenant des entités B2B et des événements d’expérience doivent être exportées à nouveau après la mise à niveau de l’architecture et avant d’être importées dans les sandbox cibles via les outils sandbox. L’importation de versions antérieures à la mise à niveau échoue lors de la validation. Pour plus d’informations, consultez le [guide sur les objets pris en charge pour les outils sandbox](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling). |

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| API d’audiences externes | Vous pouvez utiliser l’API d’audiences externes pour importer des audiences générées en externe par programmation dans Adobe Experience Platform. Pour plus d’informations, consultez le [guide des points d’entrée des audiences externes](../../segmentation/api/external-audiences.md). |

Pour plus d’informations sur la segmentation, consultez la [vue d’ensemble du service de segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Source | Description |
| --- | --- |
| Prise en charge de la version [!BADGE Beta]{type=Informative} [!DNL Didomi] (SDK Streaming) | Utilisez la source [!DNL Didomi] pour ingérer les données de gestion du consentement et des préférences depuis [!DNL Didomi]. Cela permet de respecter les réglementations de confidentialité et les stratégies marketing basées sur le consentement. Consultez la [[!DNL Didomi] vue d’ensemble de la source](../../sources/connectors/consent-and-preferences/didomi.md) pour plus d’informations sur la configuration. Pour découvrir comment créer une connexion source, consultez le [[!DNL Didomi] guide de connexion source](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md). |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la capture de données de modification dans certaines sources à l’aide de l’API [!DNL Flow Service] | Vous pouvez désormais créer des flux de données qui permettent la capture de données de modification pour une ingestion incrémentielle à l’aide des connecteurs source. Cette fonctionnalité permet à la clientèle d’apporter le type de données de modification pour une ingestion incrémentielle, ce qui améliore la pertinence des données et réduit les frais de traitement. Pour plus d’informations, consultez la documentation relative à l’[utilisation de la capture des données de modification pour les sources](../../sources/tutorials/api/change-data-capture.md). |
| Prise en charge de la suppression réversible des enregistrements dans [!DNL Salesforce] | La source [!DNL Salesforce] prend désormais en charge l’inclusion d’enregistrements supprimés de manière réversible via un paramètre `includeDeletedObjects` facultatif. Lorsque la valeur est définie sur true, les clientes et clients peuvent inclure des enregistrements supprimés de manière réversible dans leurs requêtes [!DNL Salesforce] et importer ces enregistrements dans Experience Platform. Pour plus dʼinformations, consultez la [[!DNL Salesforce] documentation sur les sources](../../sources/connectors/crm/salesforce.md). |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).
