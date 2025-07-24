---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 7e91181f71b84fdaf04a39e003cbbd415827e282
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 22%

---

# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 29 juillet 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Destinations](#destinations)
- [Ingestion des données](#ingestion)
- [Service de requête](#query-service)
- [Édition B2B de Real-Time CDP](#b2b)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Destinations mises à jour**

| Destination | Description |
| --- | --- |
| Consolidation des cartes de destination Marketo | Les cartes de destination Marketo V2 et Marketo Engage Person Sync ont été consolidées en une seule carte de destination unifiée. Cette consolidation simplifie le processus de sélection de destination et offre une expérience plus rationalisée pour les intégrations Marketo. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Informations améliorées sur les flux de données pour les destinations Edge | Les informations du rail droit améliorées pour les destinations Adobe Target et Personalization personnalisé affichent désormais le nom du flux de données, ce qui offre une visibilité plus claire sur les configurations de flux de données associées et réduit la confusion lors de la révision des flux de données existants. Le sélecteur **[!UICONTROL Identifiant du flux de données]** dans l’écran de configuration de destination a été mis à jour vers **[!UICONTROL Flux de données]** pour une plus grande clarté dans l’interface utilisateur. |
| Visibilité des actions marketing dans la sélection de destination | Les actions marketing sont désormais affichées dans le rail droit de l’onglet de destination **[!UICONTROL Parcourir]** et dans la page **[!UICONTROL Exécutions de flux de données]**, offrant une visibilité immédiate des modifications apportées aux actions marketing sans qu’il faille accéder à la page d’affichage. Cette amélioration améliore l’expérience utilisateur en facilitant la vérification des configurations d’action marketing lors de la configuration de la destination. |
| (Version bêta limitée) Modifier les actions marketing pour les destinations | Vous pouvez désormais modifier les actions marketing pour les destinations existantes. Cette fonctionnalité est en version bêta limitée. Pour demander l’accès, contactez votre représentant Adobe. |
| (Version bêta limitée) Modifier les destinations | Vous pouvez désormais modifier votre configuration de destination après l’avoir créée. Cette fonctionnalité est en version bêta limitée. Pour demander l’accès, contactez votre représentant Adobe. |
| Noms et descriptions des comptes pour les connexions de destination | Vous pouvez désormais ajouter des noms et des descriptions de compte lors de la connexion aux destinations, ce qui permet une meilleure gestion des destinations avec plusieurs comptes. |

**Correctifs**

| Problème | Description |
| --- | --- |
| Fonctionnalité de défilement des catégories | Correction d’un problème en raison duquel le menu latéral des catégories dans le catalogue des destinations et des sources ne défilait pas correctement lors du pointage de la souris, ce qui améliorait la convivialité de la navigation pour les utilisateurs qui parcouraient les catégories de destination. |

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../destinations/home.md).

## Ingestion des données {#ingestion}

Experience Platform fournit une structure complète d’ingestion de données qui prend en charge l’ingestion de données par lots et par flux à partir de diverses sources.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Prise en charge de la surveillance de l’ingestion de profils en flux continu | La surveillance en temps réel de l’ingestion des profils de streaming est désormais disponible, offrant ainsi une transparence sur les mesures de débit, de latence et de qualité des données. Elle prend en charge les alertes proactives et les informations exploitables pour aider les ingénieurs de données à identifier les violations de capacité et les problèmes d’ingestion. |

Pour plus d’informations, consultez la [présentation de l’ingestion des données](../ingestion/home.md).

## Service de requête {#query-service}

Adobe Experience Platform Query Service fournit une interface SQL robuste pour l’analyse et l’exploration des données sur la plateforme.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Gestion améliorée des sessions | Data Distiller offre désormais des fonctionnalités améliorées de gestion des sessions, ce qui permet de mieux contrôler les sessions des utilisateurs et d’améliorer la surveillance des performances dans les environnements de développement et de production. |
| Prise en charge des restrictions de caractères de mot de passe des informations d’identification non expirantes | Data Distiller prend désormais en charge les informations d’identification non expirantes avec des restrictions de caractères spécifiques. Bien que les mots de passe requièrent au moins un chiffre, une lettre minuscule, une lettre majuscule et un caractère spécial, le signe dollar ($) n’est pas pris en charge. Les caractères spéciaux recommandés comprennent les `!, @, #, ^, or &`. |
| Amélioration de la cohérence des performances entre les environnements | Les performances de Data Distiller sont désormais cohérentes entre les sandbox de développement et de production, avec des ressources principales similaires disponibles dans les deux environnements. Les heures de calcul consommées peuvent varier en fonction du volume de données et des ressources de calcul principales disponibles au moment du traitement. |

Pour plus d’informations, consultez la [présentation de Query Service](../query-service/home.md).

## Édition B2B de Real-Time CDP {#b2b}

Real-Time CDP B2B edition offre des fonctionnalités complètes de gestion des données client B2B, ce qui permet aux entreprises de créer des profils client unifiés, de créer des audiences B2B sophistiquées et d’activer des données sur divers canaux marketing.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à niveau de l’architecture B2B | Experience Platform effectue une mise à niveau vers une nouvelle architecture B2B qui apporte des améliorations significatives aux audiences à entités multiples avec des attributs B2B. Cette mise à niveau consolide la prise en charge des politiques de fusion, améliore la précision du nombre d’audiences et améliore les fonctionnalités de résolution des entités. |
| Consolidation de la politique de fusion pour les audiences à entités multiples | Les audiences d’entités multiples avec des attributs B2B ne prennent désormais en charge qu’une seule politique de fusion (la politique de fusion par défaut) au lieu de prendre en charge plusieurs politiques de fusion. Cette modification garantit une composition cohérente de l’audience et simplifie la gestion de la logique de fusion. |
| Mises à jour des contraintes d’audience du compte | Les audiences de compte ne présentent plus les contraintes précédentes d’un intervalle de recherche en amont de 30 jours pour les événements d’expérience, les restrictions d’entité personnalisée ou les limitations d’utilisation des événements de `inSegment`. Ces mises à jour offrent une plus grande flexibilité dans la création de définitions d’audience B2B complexes. |
| Nombre d’audiences amélioré pour les entités B2B | Les estimations de taille d’audience pour les audiences avec des entités B2B telles que Comptes et Opportunités sont désormais exactes, en fonction des résultats de segmentation en temps réel. Cette amélioration fournit des estimations plus précises et plus fiables pour les audiences impliquant des relations B2B complexes. |
| Instantanés de compte pour l’appartenance à une audience | Les détails d’appartenance à l’audience sont désormais inclus pour les entités de compte dans les exportations d’instantanés, ce qui permet d’accéder au statut d’audience au niveau du compte, aux horodatages et aux indicateurs d’appartenance. Cela apporte la parité des fonctionnalités entre les modèles de segmentation Profil (Personne) et Compte . |
| Modifications de l’outil Sandbox pour les audiences à entités multiples | L’importation d’audiences d’entités multiples avec des entités B2B et des événements d’expérience exportés avant la migration n’est plus prise en charge. La validation de l’importation de ces audiences échoue et ne peuvent pas être automatiquement converties dans la nouvelle architecture. Les audiences doivent être réexportées après la migration avant l’importation dans les sandbox cibles. |
| Obsolescence de l’API d’entité B2B | La création d’audiences via l’API pour les entités B2B (compte, opportunité, relation compte-personne, relation opportunité-personne, campagne, membre de campagne, liste marketing et membre de liste marketing) est désormais obsolète. En outre, les opérations de recherche et de suppression de l’API d’accès au profil pour ces entités B2B sont également obsolètes. |
| Mises à jour de l’espace de noms d’identité pour la résolution d’entité | Les entités Compte et Opportunité utilisent désormais la fusion basée sur la priorité temporelle avec des espaces de noms d’identité spécifiques (`b2b_account` pour Compte, `b2b_opportunity` pour Opportunité). Toutes les autres entités sont unifiées avec des chevauchements d’identités principales fusionnés à l’aide d’une fusion basée sur la priorité temporelle. |

Pour plus d’informations, consultez la présentation de Real-Time CDP B2B edition [](../rtcdp/b2b-overview.md).

## Sandbox {#sandboxes}

Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modifications des imports d’audiences à entités multiples | L’outil Sandbox a été mis à jour pour prendre en charge la nouvelle mise à niveau de l’architecture B2B. Les audiences à entités multiples contenant des entités B2B et des événements d’expérience doivent être réexportées après la mise à niveau de l’architecture avant d’être importées dans les sandbox cibles via l’outil sandbox. L’importation de versions antérieures à la mise à niveau échoue lors de la validation. |

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| API d’audience externe | Vous pouvez utiliser l’API d’audiences externes pour importer par programmation dans Adobe Experience Platform des audiences générées en externe. |

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Source | Description |
| --- | --- |
| Prise en charge de [!DNL Didomi] (Streaming SDK) | Le connecteur source [!DNL Didomi] vous permet d’ingérer des données de gestion du consentement à partir de la plateforme d’[!DNL Didomi], en respectant les réglementations de confidentialité et les stratégies marketing basées sur le consentement. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la capture de données de modification dans certaines sources | Vous pouvez désormais créer des flux de données qui permettent de modifier la capture de données pour une ingestion incrémentielle à l’aide des connecteurs source. Cette fonctionnalité permet aux clients d’apporter des modifications au type de données pour une ingestion incrémentielle, ce qui améliore la fraîcheur des données et réduit les frais de traitement. |
| Prise en charge de la suppression réversible des enregistrements dans [!DNL Salesforce] | La source [!DNL Salesforce] prend désormais en charge l’inclusion d’enregistrements supprimés de manière réversible via un paramètre de `includeDeletedObjects` facultatif. Lorsque la valeur est définie sur true, les clients peuvent inclure des enregistrements supprimés de manière réversible dans leurs requêtes [!DNL Salesforce] et importer ces enregistrements dans Experience Platform. |

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../sources/home.md).
