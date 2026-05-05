---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9b191535ba96c8791a4528361a1945ae27c6456c
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 23%

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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : avril 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service de requête](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandbox](#sandboxes)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [!BADGE Beta ]{type=Informative} [Correspondance client Microsoft Ads](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Faites correspondre les clients par adresse e-mail et reprenez contact avec eux dans l’ensemble du [!DNL Microsoft Advertising Network], y compris grâce aux annonces Search et Audience. Liez votre compte [!DNL Microsoft Advertising] à Real-Time CDP pour automatiser la création et la gestion des listes de correspondance client directement depuis Experience Platform. Pour obtenir l’accès, contactez votre gestionnaire de compte Adobe. |
| [!BADGE ]{type=Informative} [Audience Personnalisée Reddit](../destinations/catalog/advertising/reddit-custom-audience.md) | Envoyez des audiences d’Experience Platform vers [!DNL Reddit Ads]. Connectez votre compte [!DNL Reddit], mappez des identités et activez des audiences pour atteindre les personnes qui explorent activement leurs intérêts sur [!DNL Reddit]. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] est la destination actuelle de toutes les nouvelles connexions [!DNL Amazon Ads]. Si vous disposez d’une connexion [ (héritée) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) existante, elle continue à fonctionner sans aucune modification requise. [!DNL Amazon Ads v2] se connecte à [!DNL Ads Data Manager], qui prend en charge les types d’identité étendus, les champs liés aux adresses et le partage de données entre les produits [!DNL Amazon Ads], ce qui améliore le ciblage et les taux de correspondance d’audience par rapport à [ (hérité) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Utilisez [!DNL Rokt] pour connecter les audiences Experience Platform à la prise de décision en temps réel pilotée par l’IA, améliorant ainsi les performances des campagnes grâce à un ciblage, une suppression et une personnalisation plus précis. |
| Prise en charge des audiences externes pour [ Criteo ](../destinations/catalog/advertising/criteo.md) | Activez les audiences d’origines autres que Segmentation Service vers [!DNL Criteo], y compris les audiences de chargement personnalisées (importées depuis CSV), les audiences semblables, les audiences fédérées et les audiences créées dans d’autres applications Experience Platform telles que [!DNL Adobe Journey Optimizer]. Voir la section [audiences prises en charge](../destinations/catalog/advertising/criteo.md#supported-audiences) pour plus d’informations. |
| [Connexion à l’audience Acxiom](../destinations/catalog/advertising/acxiom-audience-connection.md) | La destination [!DNL Acxiom Audience Connection] est désormais disponible pour tous. Utilisez-le pour améliorer les audiences avec la technologie [!DNL Acxiom's Real ID] et les activer sur d’autres plateformes, notamment [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL LG Ads], [!DNL Spectrum] et [!DNL Viant]. |
| [Connexion à l’audience Acxiom Real ID](../destinations/catalog/advertising/acxiom-real-id-audience-connection.md) | La destination [!DNL Acxiom Real ID Audience Connection] est désormais disponible pour tous. Utilisez-la pour activer des audiences à l’aide de [!DNL Acxiom's Real ID] comme clé de correspondance sur le même ensemble de plateformes prises en charge, notamment [!DNL Altice], [!DNL Ampersand], [!DNL Comcast], [!DNL Cox], [!DNL LG Ads], [!DNL Spectrum] et [!DNL Viant]. |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Corriger | Description |
| --- | --- |
| Prise en charge de la surveillance Personalization personnalisée | Le tableau de bord de surveillance des destinations prend désormais en charge les destinations [!DNL Custom Personalization]. La note de limitation indiquant que les [!DNL Custom Personalization] exclues de la surveillance a été supprimée. |
| Nombre de profils dans la révision de l’activation | L’étape de révision de l’activation affiche désormais le nombre de profils pour les audiences déjà activées. Le nombre de profils s’affiche également pour les destinations de diffusion en streaming, et pas seulement pour les destinations par lots. |
| Visibilité de l’expiration du jeton d’[!DNL Pinterest] | La destination [!DNL Pinterest] fait désormais surface avec le délai d’expiration du jeton renvoyé directement par [!DNL Pinterest], afin que vous puissiez voir quand la réauthentification est nécessaire. |
| L’exportation du fichier est maintenant désactivée pour les plannings non valides | L’action **[!UICONTROL Export file now]** est désormais désactivée lorsque le planning d’audience est non valide ou obsolète. Une info-bulle explique pourquoi l’action n’est pas disponible. |
| Correctif de visibilité de colonne dans le workflow d’activation | Correction d’un problème en raison duquel la modification des colonnes visibles dans une table affectait incorrectement les autres tables du workflow d’activation. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification open source qui fournit des structures et des définitions communes (schémas) pour les données importées dans Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Visibilité de l’utilisation du schéma du groupe de champs | Affichez les schémas qui utilisent un groupe de champs de la page de détails et explorez-les dans une boîte de dialogue triable avec les métadonnées du schéma. Cela vous permet d’évaluer rapidement les dépendances et l’impact sans quitter . |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [ Présentation du système XDM ](../xdm/home.md).

## Service de requête {#query-service}

Utilisez Query Service pour interroger des données dans Adobe Experience Platform [!DNL Data Lake] avec le langage SQL standard. Rejoignez n’importe quel jeu de données du [!DNL Data Lake] et capturez les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans le Workspace de science des données ou lors de l’ingestion dans le profil client en temps réel.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Accélérateurs de Distiller de données | Exécutez et planifiez des modèles SQL paramétrés gérés par Adobe dans l’interface utilisateur de Query Service pour effectuer des analyses courantes sans écrire de code SQL. Cela vous permet de normaliser les workflows d’analyse et de réutiliser une logique de requête fiable dans votre organisation. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation de Query Service](../query-service/home.md).

## Real-Time CDP {#rtcdp}

[!DNL Real-Time CDP] fournit des profils clients unifiés et exploitables en ingérant, traitant et activant des données sur plusieurs canaux en temps réel. Avec Real-Time CDP, les entreprises peuvent connecter des sources de données existantes, créer et activer des audiences enrichies et assurer une activation conforme à la confidentialité entre les destinations, le tout depuis Experience Platform. Les spécialistes marketing, les analystes et les équipes informatiques peuvent ainsi proposer à leurs clients des expériences hautement personnalisées en temps voulu, grâce à des campagnes marketing cross-canal transparentes.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Real-Time CDP MCP (Beta) | Utilisez le MCP Real-Time CDP pour importer Real-Time CDP dans les agents d’IA et les clients compatibles avec MCP, ce qui vous permet d’interagir avec les outils Real-Time CDP directement via votre expérience LLM native. En connectant un client compatible MCP (tel que Claude, ChatGPT, Claude Code, Codex, Curseur ou VS Code) au point d’entrée fourni par votre représentant Adobe, vous pouvez utiliser un langage naturel pour inspecter les audiences, la configuration de destination et l’historique d’exécution de l’activation, sans écrire d’appels d’API REST Experience Platform ni parcourir plusieurs workflows d’interface utilisateur. Après vous être connecté à Adobe à l’aide d’un navigateur, vous disposez d’un accès en lecture seule aux outils suivants : <ul><li>Rechercher des audiences existantes</li><li>Prévisualiser L’Appartenance À Une Audience</li><li>Liste des types de destination</li><li>Liste des comptes configurés</li><li>Liste des destinations configurées</li><li>Liste des connexions Source</li><li>Liste des connexions cibles</li><li>Inspecter les exécutions d’activation</li></ul>. Chaque requête nécessite des paramètres `imsOrgId` et `sandboxName` pour s’assurer que les actions sont limitées à votre organisation et à votre sandbox. Notez que les opérations d’écriture ne sont pas prises en charge dans cette version de Beta. |

{style="table-layout:auto"}

Pour plus d&#39;informations, lisez la présentation de Real-Time CDP [](../rtcdp/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Copie express | Utilisez Express Copy pour copier des objets dans un sandbox cible en une seule action à partir de l’[interface utilisateur de l’outil Sandbox](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Les objets dépendants sont détectés automatiquement et sont créés dans le sandbox cible ou réutilisés lorsqu’ils existent déjà. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des sandbox](../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

Utilisez Segmentation Service pour créer des audiences à partir des données de vos clients et gérer leur cycle de vie complet dans Experience Platform.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Surveillance de la segmentation en flux continu | Surveillez la segmentation en flux continu avec une visibilité en temps réel sur le taux d’évaluation, la latence d’ingestion et les mesures de qualité des données au niveau du sandbox, du jeu de données et du segment. Affichez les mesures telles que le taux d’évaluation, la latence d’ingestion P95, les enregistrements reçus, les enregistrements évalués, les enregistrements ayant échoué et les enregistrements ignorés. Affichez également les nouveaux profils nets qualifiés et disqualifiés par segment. Utilisez ces informations pour identifier les violations de capacité et les problèmes d’ingestion avant qu’ils n’affectent vos données. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des audiences](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Désactivation automatique du flux de données | Les flux de données d’ingestion des sources qui échouent en continu pendant 30 jours sont automatiquement désactivés, ce qui permet de faire apparaître les flux de données non sains et de réduire les échecs d’exécution répétés. |
| [!DNL Delta Sharing] | Vous pouvez utiliser la source [!DNL Delta Sharing] pour importer des tables Delta dans Experience Platform par le biais d’un protocole de partage de données ouvert et sécurisé. Une fois que vous avez configuré une connexion [!DNL Delta Sharing] et sélectionné les partages et les tableaux à ingérer, Platform importe automatiquement ces données dans vos jeux de données afin que vous puissiez les utiliser pour l’analyse, la segmentation et l’activation. |
| [!DNL Meta Ads] (Beta) | Vous pouvez utiliser le connecteur source [!DNL Meta Ads] (Beta) dans l’espace de travail Sources pour vous authentifier auprès de [!DNL Meta], sélectionner vos comptes publicitaires et planifier l’ingestion des données de campagne et de performances [!DNL Meta Ads] dans les jeux de données Experience Platform. |
| [!DNL Talon.One] | Vous pouvez désormais connecter Experience Platform à [!DNL Talon.One] à l’aide des nouvelles sources de lots et de diffusion en continu [!DNL Talon.One]. Utilisez les nouvelles sources pour ingérer les données de profil de fidélité, ainsi que les événements d’activité de transaction et de fidélité dans Experience Platform. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).
