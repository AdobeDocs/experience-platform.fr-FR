---
title: Présentation de Meta Ads Source
description: Découvrez comment connecter Meta Ads à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badge: Beta
source-git-commit: fc795d46e7515724553edb1bdfd0f5f6b4c88914
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%

---

# [!DNL Meta Ads]

La source [!DNL Meta Ads] est un connecteur de médias achetés Adobe Experience Platform qui ingère les données de performances publicitaires des propriétés Meta ([!DNL Facebook], [!DNL Instagram]) dans le lac de données Experience Platform dans un format normalisé compatible avec le modèle de données d’expérience (XDM).

En utilisant la source de [!DNL Meta Ads], vous pouvez :

- Centralisez les données de performances des médias achetés dans Experience Platform ainsi que les données sur site, CRM et commerciales.
- Intégrez des informations sur les comptes, les campagnes, les ensembles d’annonces et les annonces au niveau des annonces via les API [!DNL Meta Marketing] (Insights).
- Utilisez une source unique et régie pour [!DNL Meta] les données entre les applications telles qu’Adobe Mix Modeler, Customer Journey Analytics et GenStudio for Performance Marketing.

La source de [!DNL Meta Ads] d’Experience Platform fournit un point d’entrée régi et réutilisable pour les données publicitaires [!DNL Meta]. Après avoir configuré l’authentification avec votre compte professionnel [!DNL Meta] et sélectionné les comptes publicitaires à ingérer, Experience Platform planifie et transforme automatiquement les données [!DNL Meta Insights] en jeux de données compatibles XDM.

Cela permet de nombreux cas d’utilisation, notamment la modélisation du mix média, l’analyse de parcours cross-canal et l’analyse des performances créatives, le tout optimisé par des données de média payant normalisées dans Experience Platform.

## Exemples de cas d’utilisation

| Cas d’utilisation | Objectif | Aide de la source de [!DNL Meta Ads] |
| --- | --- | --- |
| Modélisation du mix média et optimisation du budget | Évaluez l’impact de [!DNL Meta] dépenses aux côtés d’autres canaux (recherche, programmation, e-mail) et optimisez l’allocation des médias. | <ul><li>Ingère [!DNL Meta] performances de la campagne, de la visionneuse d’annonces et au niveau des annonces (impressions, dépenses, conversions) dans Experience Platform.</li><li>Fournit des jeux de données publicitaires normalisés à Adobe Mix Modeler via Snowflake pour entraîner des modèles de mix média sur plusieurs canaux et simuler des changements de budget.</li><li>Fournit des données cohérentes et gouvernées qui peuvent être versionnées et retraitées lors des mises à jour [!DNL Meta] des mesures historiques.</li></ul> |
| Parcours analytics : comprendre [!DNL Meta Ads] comportement sur site | Découvrez comment [!DNL Meta] expositions publicitaires sont liées aux parcours clients sur le web, l’application et d’autres points de contact. | <ul><li>Apporte [!DNL Meta] mesures de diffusion et de conversion dans Experience Platform, alignées sur des identifiants tels que : les identifiants Campaign/Ad ID ou les paramètres UTM ou les pages de destination (lorsqu’ils sont configurés).</li><li>Associé aux données Adobe Analytics ou Web SDK dans Experience Platform, vous pouvez utiliser Customer Journey Analytics pour analyser les parcours qui commencent par des impressions ou des clics [!DNL Meta], attribuer des événements en aval (inscriptions, achats) pour [!DNL Meta] des campagnes et comparer les performances de [!DNL Meta] par rapport à d’autres canaux d’acquisition.</li></ul> |
| Creative et analyse des performances du contenu | Identifiez les contenus publicitaires et les ressources des campagnes [!DNL Meta] qui ont les meilleures performances et connectez-les au contenu des systèmes Adobe. | <ul><li>Ingère des informations au niveau des annonces, y compris les mappages aux contenus publicitaires et (éventuellement) aux métadonnées des ressources.</li><li>Envoie ces données à GenStudio/Content Analytics pour : évaluer les performances des différents contenus publicitaires, formats ou messages dans [!DNL Meta] et corréler [!DNL Meta] performances avec les variantes de contenu créées ou gérées dans Adobe Experience Manager ou GenStudio.</li><li> Prend en charge les comparaisons entre réseaux une fois que [!DNL Google Ads] et d’autres réseaux publicitaires sont connectés, en utilisant le même schéma.</li></ul> |
| Rapports de performances cross-canal et cross-éditeur | Fournissez une vue unique et normalisée des performances publicitaires sur les canaux [!DNL Meta] et autres canaux payants. | <ul><li>Utilise un schéma publicitaire commun à [!DNL Meta], [!DNL Google Ads], [!DNL DV360], Trade Desk, etc.</li><li>Activation : tableaux de bord unifiés pour les équipes multimédias (dépenses, portée, conversions par canal, campagne ou audience).</li><li>KPI normalisés calculés de manière cohérente sur tous les réseaux</li><li>Réduit la dépendance aux outils ETL ad hoc ou aux pipelines par équipe et améliore l’auditabilité.</li></ul> |

{style="table-layout:auto"}

## Conditions préalables

### Configuration des autorisations sur Experience Platform

Les autorisations **[!UICONTROL View Sources]** et **[!UICONTROL Manage Sources]** doivent être activées pour votre compte afin de connecter votre compte [!DNL Meta Ads] à Experience Platform. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### Conditions préalables relatives au compte [!DNL Meta]

Avant de pouvoir connecter correctement la source de [!DNL Meta Ads] dans Experience Platform, la configuration de [!DNL Meta] du client doit remplir quelques conditions de base. Cela permet de s’assurer que le connecteur peut authentifier et récupérer les données de l’API [!DNL Meta Marketing].

Pour préparer le côté [!DNL Meta] :

**Configuration de comptes [!DNL Meta Business Manager] et publicitaires**
Vous devez avoir [!DNL Meta Business Manager] configuré et au moins un compte [!DNL Meta Ads] qui sera utilisé comme source de données. Les campagnes, les ensembles d’annonces, les annonces, les ressources et les informations doivent déjà exister dans ces comptes d’annonces ; la source d’[!DNL Meta Ads] lit à partir de ces données publicitaires existantes.

**Garantir l’accès à l’API [!DNL Meta Marketing]**
Vous devez disposer d’une application [!DNL Meta] autorisée à utiliser l’API [!DNL Meta Marketing]/l’API Graph. Cette application est ce qu’Experience Platform utilisera concrètement lorsqu’il se connectera à [!DNL Meta]. L’application doit être correctement configurée dans Developer Console d’[!DNL Meta] et liée au Business Manager approprié.

**Octroyer les autorisations d’API appropriées (portées)**
L’application [!DNL Meta] utilisée pour le connecteur doit avoir au moins les portées OAuth suivantes approuvées et disponibles :

- `ads_read` : requis pour lire les annonces, les campagnes, les ensembles d’annonces et les mesures de performances.
- `ads_management` : requis pour un accès au compte publicitaire plus large et pour certains points d’entrée de rapports.

Ces autorisations sont explicitement référencées dans la configuration OAuth de média payant [!DNL Meta] utilisée par le connecteur [!DNL Meta Ads] d’Experience Platform et doivent être accordées du côté [!DNL Meta] avant que vous ne tentiez d’autoriser la source.

**Utilisez un utilisateur [!DNL Meta] disposant d’autorisations de compte publicitaire suffisantes**

La personne qui effectue la connexion OAuth dans l’interface utilisateur des sources Experience Platform doit être un utilisateur [!DNL Meta] disposant des autorisations appropriées sur le ou les comptes publicitaires qui seront connectés. En pratique, cela signifie généralement :

- L’utilisateur fait partie du même Business Manager que les comptes publicitaires.
- L’utilisateur dispose au moins d’un accès de niveau annonceur (souvent supérieur, tel qu’administrateur) à ces comptes publicitaires.

Si l’utilisateur dispose d’autorisations limitées, [!DNL Meta] pouvez autoriser la connexion mais restreindre l’accès à certains comptes publicitaires ou points d’entrée de rapports, ce qui entraîne des données incomplètes ou vides lors de l’exécution des flux de données.

**Vérifiez que l’application [!DNL Meta] et l’utilisateur peuvent voir les comptes publicitaires prévus**

Avant de tenter de créer la connexion source sur Experience Platform, il est recommandé de :

- Vérifiez [!DNL Meta Business Manager] l&#39;application est associée à l&#39;entreprise et peut accéder aux comptes publicitaires.
- Vérifiez que l’utilisateur autorisé à partir d’Experience Platform peut voir ces comptes publicitaires dans l’interface utilisateur d’[!DNL Meta] et via l’API Graph.

Cela réduit le risque de problèmes « aucune donnée renvoyée » causés par des incohérences d’autorisations entre l’application, l’utilisateur et les comptes publicitaires.

## Configuration du schéma

La source [!DNL Meta Ads] est fournie avec un ensemble normalisé de schémas de médias achetés XDM qui fournissent une modélisation cohérente des données publicitaires [!DNL Meta] (Facebook/Instagram) dans Experience Platform et les applications. Ces schémas sont conçus pour être cross-canal, joignables et extensibles.

| Schéma/Jeu de données | Rôle | Groupes de champs / Attributs clés | Niveaux d&#39;entité standard |
| --- | --- | --- | --- |
| Recherche de compte média payant | Métadonnées de recherche/compte | Identifiant, nom, devise, fuseau horaire, statut, date de création du compte | Compte |
| Recherche de campagne multimédia payante | Métadonnées de campagne | Identifiant, nom, statut, objectif, budget, type, date de début/fin de la campagne | Campaign |
| Recherche de groupe publicitaire de médias payants | Métadonnées des groupes publicitaires/ressources | ID de groupe publicitaire, lien de campagne, statut, budget, objectifs d’optimisation | Groupe publicitaire/ensemble publicitaire |
| Recherche de publicité multimédia payante | Métadonnées au niveau des annonces | ID d’annonce publicitaire, nom, détails de la création, lien vers le groupe d’annonces et la campagne | Annonce publicitaire |
| Recherche de ressources multimédias payantes | Métadonnées de ressource publicitaire (image/vidéo) | ID de ressource, type, URL source, dimensions, utilisation | Ressource |
| Recherche d’expérience de média payante | Métadonnées au niveau de l’expérience (expérience créative) | Experience ID, ressources impliquées, titre, description, call-to-action | Expérience |
| Mesures récapitulatives du média payant | Résumé des performances/rapports agrégés | Impressions, clics, conversions, dépenses, portée, mesures vidéo, etc. | Publicité, Expérience, Ressource, Campagne |

### Exemples de champs de schéma principaux par entité

| Entité | Champs XDM clés | Mappage des champs Logique/Meta |
| --- | --- | --- |
| Compte | payMedia.accountID, payMedia.accountGUID, nom, statut, createdTime, fuseau horaire, devise | Meta account_id, GUID calculé, statut, méta-informations de compte |
| Campaign | payMedia.campaignID, campaignGUID, nom, statut, objectif, budgetType, dailyBudget, date de début/fin | Meta campaign_id, GUID, tous mappés directement à partir de l’API |
| AdGroup | payMedia.adGroupID, adGroupGUID, nom, statut, optimizationGoal | Meta adset_id, GUID calculé, méta-informations sur la visionneuse d’annonces |
| Annonce publicitaire | payMedia.adID, adGUID, adType, creative, deliveryStatus, reviewStatus | Meta ad_id, creative*, UDF du classificateur, énumérations de statut |
| Ressource | payMedia.assetID, assetGUID, assetType, sourceURL, height, width | Meta image_hash/video_id, URL, taille |
| Expérience | experienceID, experienceGUID, experienceAssetIDs, titre, description, cta | Dérivé, unique par creative+copy |
| Mesures | impressions, clics, conversions, valeurs de conversion, dépenses, portée, mesures vidéo (débit, rétention, lectures, etc.) | Champs d’informations Meta, mappés à une mesure XDM ou à une valeur/un tableau |

**Structure des mesures récapitulatives**

Toutes les données de performances utilisent `paid-media-summary-metrics.schema.json` comme base. Pour chaque ligne de date et de niveau d’entité, vous obtenez :

- account_id, campaign_id, ad_id, asset_id, asset_id, experience_id (en fonction de la répartition)
- impressions, clics, conversions, dépenses, portée, unique_clicks, toutes les mesures de visionnage vidéo
- répartitions : appareil, plateforme, emplacement, âge, sexe (facultatif dans la demande)
- champs de mesure : normalisé en tant qu’{ « valeur »: 1234 } objets

+++Afficher des exemples de champs d’agrégat

```json
{
  "account_id": "...",
  "campaign_id": "...",
  "ad_id": "...",
  "date": "YYYY-MM-DD",
  "impressions": { "value": 155023 },
  "clicks": { "value": 225 },
  "conversions": { "value": 42 },
  "spend": { "value": 459.96 },
  "video_thruplay_watched_actions": { "value": 88 }
}
```

+++

## Étapes suivantes

Cette page résume le connecteur média payant [!DNL Meta Ads] : ce qu’il ingère à partir de [!DNL Meta] dans Experience Platform, des exemples de cas d’utilisation (tels que la modélisation de mix média, l’analyse de parcours et le reporting cross-canal), ainsi que les autorisations Experience Platform et [!DNL Meta] et la configuration de compte dont vous avez besoin avant de vous connecter.

Lorsque vous êtes prêt à créer la connexion source, suivez le tutoriel sur l’[ingestion  [!DNL Meta Ads]  données vers Experience Platform dans l’interface utilisateur](../../tutorials/ui/create/advertising/meta-ads.md).


