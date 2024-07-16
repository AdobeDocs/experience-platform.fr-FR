---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour d’août 2023 pour Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 46%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 23 août 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Real-Time Customer Data Platform](#rtcdp)
- [Contrôle d’accès basé sur les attributs](#abac)
- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Ingestion de données](#data-ingestion)
- [Préparation des données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Basé sur Experience Platform, Real-Time Customer Data Platform ([!DNL Real-Time CDP]) aide les entreprises à rassembler des données connues et inconnues pour activer les profils clients avec une prise de décision intelligente tout au long du parcours client.

[!DNL Real-Time CDP] associe plusieurs sources de données d’entreprise pour créer des profils client en temps réel. Les segments créés à partir de ces profils peuvent ensuite être envoyés vers des destinations en aval afin de fournir des expériences personnalisées et individuelles aux clients et clientes sur tous les canaux et appareils.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Guide de cas d’utilisation du réengagement intelligent | Le guide de cas d’utilisation [Réengagement intelligent](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) fournit des détails sur la manière de réengager un client qui a abandonné une conversion avant de l’exécuter de manière intelligente et responsable. Ce guide utilise les exemples de parcours suivants pour réengager les clients : <ul><li>Parcours de réengagement - Ciblage des clients qui ont abandonné la navigation sur les produits.</li><li>Parcours de panier abandonné : ciblage des clients qui ont placé des produits dans le panier mais n’ont pas encore effectué l’achat.</li><li>Parcours de confirmation de commande - Se concentrer sur les achats de produits</li></ul> Utilisez le lien d’options de retour détaillé au bas du [guide d’utilisation du réengagement intelligent](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) pour fournir des commentaires. |
| Prise en charge des données du partenaire | Exécutez le marketing entonnoir supérieur dans Real-Time CDP, avec les profils de prospect et les identifiants de partenaire d’origine pour atteindre de nouveaux clients et enrichir vos données propriétaires : <ul><li>Acquisition des clients et capacité d’adressage : tirez parti des identifiants sans cookie et des informations d’identification personnelles hachées des partenaires de données de votre choix pour atteindre les nouveaux clients nets et réduire la dépendance aux cookies tiers.</li><li>Marketing entonnoir complet dans un seul système : segmentation en libre-service, traitement de l’audience et activation native pour les clients potentiels et connus dans un seul système.</li><li>Fondement de la confiance : gérez les données et les profils des partenaires avec une utilisation des données brevetée, l’étiquetage, les contrôles d’accès, etc. afin de mieux commercialiser les données de manière responsable. Pour plus d’informations, lisez les guides de cas pratique suivants : les guides de cas pratique de prospection sont désormais disponibles. Lisez les guides de cas d’utilisation de la prospection pour découvrir comment engager et acquérir de nouveaux clients par le biais de cas d’utilisation de la prospection :<ul><li>[ ](../../rtcdp/partner-data/prospecting.md)</li><li>[La personnalisation sur site](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Compléter les profils propriétaires](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Activer les audiences de prospects](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de Real-Time CDP](../../rtcdp/overview.md).

## Contrôle d’accès basé sur les attributs {#abac}

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui offre une plus grande flexibilité dans la gestion de l’accès utilisateur. Elle est destinée aux marques veillant à garantir un haut niveau de confidentialité. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles d’utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs Platform spécifiques au sein de votre organisation.

Grâce au contrôle d’accès basé sur les attributs, les administrateurs de votre organisation peuvent contrôler l’accès des utilisateurs aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisées sur l’ensemble des workflows et ressources de Platform. Les administrateurs et administratrices peuvent définir des rôles d’utilisateur ou d’utilisatrice qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Configuration de l’environnement de test de stratégie d’autorisations | La nouvelle fonctionnalité [configuration de l’environnement de test des stratégies d’autorisation](../../access-control/abac/ui/policies.md) vous permet d’appliquer une stratégie de contrôle d’accès basée sur les attributs sur l’ensemble des environnements de test ou sur un nombre sélectionné d’environnements de test, en fonction de vos besoins et de vos exigences. |

{style="table-layout:auto"}

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). Pour consulter un guide complet sur le workflow de contrôle d’accès basé sur les attributs, reportez-vous au [guide complet du contrôle d’accès basé sur les attributs](../../access-control/abac/end-to-end-guide.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Cas d’utilisation de l’analyse du consentement et du suivi | Découvrez comment créer un tableau de bord de consentement pour divers cas d’utilisation marketing pour les données Real-Time CDP avec le [document d’analyse et de suivi de consentement](../../dashboards/insights-use-cases/consent-analysis.md). Il explique comment créer une audience avec les attributs appropriés pour vos besoins professionnels, puis utiliser les informations à l’aide de widgets préconfigurés dans l’interface utilisateur de Adobe Experience Platform. Il fournit également des instructions sur la création de votre propre widget personnalisé avec la fonction de tableaux de bord définis par l’utilisateur. Le document couvre les cas d’utilisation des tendances de consentement et de chevauchement du consentement. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Balises et transfert d’événement | [Balises Experience Platform (Chine)](/help/tags/ui/publishing/premium-cdn.md) | La nouvelle fonctionnalité Balises Experience Platform (Chine) améliore la fiabilité et la latence du site web, ce qui accélère les temps de réponse pour les clients qui déploient des balises sur des sites web en Chine. Les clients peuvent désormais utiliser le code JavaScript dans la bibliothèque de balises lors de l’implémentation de sites web en Chine. Cette fonctionnalité a également été ajoutée au protocole UPP (Unified Provisioning Protocol), ce qui permet d’automatiser le déploiement des produits après leur achat. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des collections de données](../../tags/home.md).

## Ingestion des données {#data-ingestion}

Adobe Experience Platform fournit un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Vous pouvez les ingérer à l’aide des API Batch ou Streaming, des sources intégrées Adobe, des partenaires d’intégration de données ou de l’interface utilisateur d’Adobe Experience Platform.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modifications apportées aux workflows d’ingestion de données | Les lignes de données contenant des valeurs supérieures au type de données spécifié (par exemple, les longues données transmises sous la forme d’un type de données entier) seront désormais rejetées et les messages d’erreur seront signalés. Auparavant, ces lignes étaient rejetées sans avertissement. |

Pour plus d’informations, consultez la [présentation de l’ingestion de données](../../ingestion/home.md).

## Préparation de données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge du filtrage des identités secondaires | Vous pouvez désormais utiliser la préparation de données pour filtrer les identités provenant d’Adobe Analytics, telles qu’AAID et AACUSTOMID. Si elles sont filtrées, ces identités ne sont pas ingérées dans Real-Time Customer Profile. Les données non filtrées continueront à être ingérées dans le lac de données. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

- Vous pouvez désormais [activer les audiences de prospects](../../destinations/ui/activate-prospect-audiences.md) vers les destinations de stockage dans le cloud.
- La [barrière de sécurité d’activation](../../destinations/guardrails.md#general-activation-guardrails) générale de 100 destinations maximum par environnement de test a été mise à jour pour être une _limite stricte_.

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Utilisez cette classe pour importer les profils de prospect provenant des cas d’utilisation d’acquisition client les plus récents des fournisseurs de données. Pour consulter des exemples et en savoir plus, reportez-vous à la documentation [[!UICONTROL XDM Individual Prospect Profile]](../../xdm/classes/prospect.md) . |

{style="table-layout:auto"}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Extension ([!UICONTROL Extension complète Adobe Analytics ExperienceEvent]) | [[!UICONTROL Données contextuelles]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL  Objet map ] de données contextuelles ajouté à l’ [!UICONTROL extension complète Adobe Analytics ExperienceEvent] afin de fournir des données contextuelles pour Adobe Analytics. |
| Groupe de champs | Multiple | Plusieurs champs ont été ajoutés à [[!UICONTROL Enriched Event Segment Details]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Le service d’identités d’Adobe Experience Platform vous offre la possibilité de mieux connaître vos clients et leur comportement en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Modifications des limites des graphiques d’identités | D’ici la fin du mois de septembre, le graphique d’identités passera à 50 identités par graphique, et la dernière identité sera ingérée. Par conséquent, l’identité la plus ancienne sera supprimée en fonction de l’horodatage d’ingestion et du type d’identité, les types d’identité de cookie étant d’abord supprimés. Aujourd’hui, les graphiques d’identités sont limités à 150 identités par graphique. Une fois cette limite atteinte, les graphiques ne sont plus mis à jour. Contactez le représentant de votre compte pour demander un changement de type d’identité si votre environnement de test de production contient : <ul><li>Un espace de noms personnalisé dans lequel les identifiants de personne (tels que les identifiants CRM) sont configurés en tant que type d’identité Cookie/Périphérique.</li><li>Un espace de noms personnalisé dans lequel les identifiants de cookie/périphérique sont configurés en tant que type d’identité multi-périphérique.</li></ul> L’ingénierie d’Adobe traitera manuellement ces demandes. Pour plus d’informations, consultez les [mécanismes de sécurité pour les données du Service d’identités](../../identity-service/guardrails.md). |

Pour plus d’informations, consultez la [présentation d’Identity Service](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Audiences analogue (disponibilité limitée) | Les audiences semblables fournissent des insights intelligents sur chacune de vos audiences, en exploitant les insights basés sur l’apprentissage automatique pour identifier et cibler les clients à forte valeur ajoutée dans vos campagnes marketing. Avec les audiences look-alike, vous pouvez créer des audiences étendues qui ciblent des clients similaires à vos audiences hautement performantes ou des clients ciblés similaires aux audiences converties précédemment. Pour plus d’informations sur les audiences look-alike, consultez la [présentation des audiences look-alike](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale de [!DNL SugarCRM] | [!DNL SugarCRM] sources sont désormais disponibles. Utilisez les [!DNL SugarCRM Accounts & Contacts] et les sources [!DNL SugarCRM Events] pour importer des données à partir de votre compte [!DNL SugarCRM] dans Experience Platform. Pour plus d’informations, consultez la [[!DNL SugarCRM] vue d’ensemble](../../sources/connectors/crm/sugarcrm.md). |
| Prise en charge de l’ingestion à la demande pour les flux de données de sources dans l’interface utilisateur | Vous pouvez désormais créer des exécutions de flux à la demande pour un flux de données de sources existantes dans l’interface utilisateur. Pour plus d’informations, consultez le guide sur la [création d’une exécution de flux à la demande pour les sources à l’aide de l’interface utilisateur](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Prise en charge du nouveau champ `correlationID` pour Adobe Analytics | Le champ `_experience.decisioning.propositions.scopeDetails.correlationID` est maintenant disponible dans le schéma du connecteur source Adobe Analytics. Ce champ est utilisé pour prendre en charge les classifications A4T et sera renseigné à compter de septembre 2023. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des sources](../../sources/home.md).
