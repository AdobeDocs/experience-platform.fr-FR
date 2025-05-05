---
title: Présentation de Data Ingestion
description: Ce document présente les trois principales manières dont les données sont ingérées dans Experience Platform, avec des liens vers leur documentation de présentation respective pour des informations plus détaillées.
exl-id: c189dd4a-5c59-4189-a18c-a3e45a9ff01d
source-git-commit: 0e484dffa38d454561f9d67c6bea92f426d3515d
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 14%

---

# Présentation de Data Ingestion

Dans Adobe Experience Platform, l’ingestion de données est le transport de données provenant de sources variées vers un support de stockage où elles peuvent être accessibles, utilisées et analysées par une organisation. Dans Experience Platform, l’ingestion de données peut être regroupée en deux catégories principales : **ingestion par flux** et **ingestion par lots**.

Sous ingestion par lots et en flux continu , vous pouvez utiliser plusieurs méthodes différentes pour ingérer vos données dans Experience Platform. Ces méthodes incluent l’utilisation de diverses **sources** et la connexion à ces sources pour importer ensuite des données dans Experience Platform.

Lisez ce document pour obtenir un aperçu des nombreuses façons dont les données peuvent être ingérées dans Experience Platform.

<!-- Adobe Experience Platform brings data from multiple sources together in order to help marketers better understand the behavior of their customers. Adobe Experience Platform Data Ingestion represents the multiple methods by which Experience Platform ingests data from these sources, as well as how that data is persisted within the Data Lake for use by downstream Experience Platform services. -->

## Ingestion en flux continu {#streaming}

Vous pouvez utiliser l’ingestion par flux pour envoyer en temps réel des données à Experience Platform à partir d’appareils côté client et côté serveur. Experience Platform prend en charge l’utilisation des entrées de données pour diffuser des données d’expérience entrantes, qui sont conservées dans les jeux de données activés dans le flux au sein du lac de données. Les entrées de données peuvent être configurées pour authentifier automatiquement les données qu’elles collectent, en veillant à ce que celles-ci proviennent d’une source approuvée.

Pour plus d’informations, consultez la [présentation de l’ingestion en flux continu](./streaming-ingestion/overview.md).

## Ingestion par lots {#batch}

Dans Experience Platform, un lot est un ensemble de données collectées sur une période de temps et traitées ensemble comme une seule unité. Les jeux de données sont constitués de lots. Vous pouvez utiliser l’ingestion par lots pour ingérer des données dans Experience Platform sous forme de fichiers de lots. Une fois ingérés, les lots fournissent des métadonnées qui décrivent le nombre d’enregistrements correctement ingérés ainsi que les enregistrements ayant échoué et les messages d’erreur associés.

Les fichiers de données chargés manuellement, tels que les fichiers CSV plats (mappés à des schémas XDM) et les fichiers parquet, doivent être ingérés à l’aide de cette méthode.

Pour plus d’informations, consultez la [présentation de l’ingestion par lots](./batch-ingestion/overview.md).

## Sources {#sources}

Vous pouvez également ingérer des données en vous connectant aux sources Experience Platform. Experience Platform conserve un catalogue de différentes sources de données auxquelles vous pouvez vous connecter et à partir desquelles vous pouvez ingérer des données. Ces sources peuvent être des applications Adobe natives telles que la source Adobe Analytics ou la source Marketo Engage. Vous pouvez également vous connecter à des sources tierces telles que la source de [!DNL Amazon S3] et la source de [!DNL Google Cloud Storage].

Les sources sont regroupées en différentes catégories, telles que les stockages dans le cloud, les bases de données et les systèmes CRM. Une source donnée peut prendre en charge l’ingestion par lots ou par flux.

Avec les sources, vous pouvez ingérer des données provenant de plusieurs sources de données différentes et de différentes catégories de cas d’utilisation. En outre, l’ingestion de données via une source vous donne la possibilité de vous authentifier auprès de la source de données externe, de configurer un planning d’ingestion et de gérer le débit d’ingestion.

Pour plus d’informations, reportez-vous à la [présentation des sources](../sources/home.md).

### Création de schémas assistée par ML {#ml-assisted-schema-creation}

Pour intégrer rapidement de nouvelles sources de données, vous pouvez désormais utiliser des algorithmes de machine learning pour générer un schéma à partir de données d’exemple. Cette automatisation simplifie la création de schémas précis, réduit les erreurs et accélère le processus de la collecte de données à l’analyse et aux informations.

Pour plus d’informations sur ce workflow[&#128279;](../xdm/ui/ml-assisted-schema-creation.md) consultez le guide de création de schéma assistée par machine learning .

## Préparation des données {#data-prep}

Bien que la préparation des données ne soit pas une méthode d’ingestion, elle constitue une partie importante du processus d’ingestion des données. Utilisez les fonctions de préparation de données pour mapper, transformer et valider les données vers et depuis le modèle de données d’expérience (XDM) avant de créer un flux de données pour ingérer vos données dans Experience Platform. La préparation des données apparaît comme l’étape de « mappage » dans l’interface utilisateur d’Experience Platform au cours du processus d’ingestion des données.

Pour plus d’informations, consultez la [présentation de la préparation des données](../data-prep/home.md).

## Méthodes d’ingestion en flux continu {#streaming-ingestion-methods}

Le tableau suivant décrit les différentes méthodes que vous pouvez utiliser pour ingérer des données de flux vers Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1123px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:31px; vertical-align:top; width:1123px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Sources de streaming</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Méthode</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:401px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Cas d’utilisation courants</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocoles</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:20px; vertical-align:top; width:282px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Considérations</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr" style="color:#0563c1; text-decoration:underline">Adobe Web/Mobile SDK</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Collecte de données à partir de sites web et d’applications mobiles.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Méthode préférée pour la collecte côté client.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Implémentez plusieurs applications Adobe à l’aide d’un seul SDK.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/streaming/http" style="color:#0563c1; text-decoration:underline">Connecteur API HTTP</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Collecte à partir de sources en flux continu, de transactions, d’événements et de signaux clients pertinents.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, API REST, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Les données brutes ou XDM sont diffusées directement vers le hub, sans segmentation Edge en temps réel ni transfert d’événement.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/data-collection/interactive-data-collection.html?lang=en" style="color:#0563c1; text-decoration:underline">[!DNL Edge Network] API</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Collecte à partir de sources en flux continu, de transactions, d’événements clients pertinents et de signaux provenant de l’[!DNL Edge Network] distribué dans le monde.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, API REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Les données sont diffusées en continu via le [!DNL Edge Network]. Prise en charge de la segmentation en temps réel et du transfert d’événement sur Edge. </span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/analytics.html?lang=en" style="color:#0563c1; text-decoration:underline">Applications Adobe</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingestion de données à partir d’applications telles qu’Adobe Analytics, Marketo Engage, Adobe Campaign Managed Services, Adobe Target, Adobe Audience Manager</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, connecteurs Source et API</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">L’approche recommandée consiste à migrer vers le SDK Web/Mobile au lieu d’utiliser les SDK d’application traditionnels.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">Sources de streaming</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingestion d’un flux d’événement d’entreprise, généralement utilisé pour partager des données d’entreprise avec plusieurs applications en aval. </span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, API REST, JSON</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Les données sont diffusées en continu au format JSON et peuvent être mappées au schéma XDM.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:222px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/sdk/streaming-sdk/getting-started" style="color:#0563c1; text-decoration:underline">SDK des sources en flux continu</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:401px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Utilisez les fonctionnalités en libre-service de la diffusion en continu de sources en libre-service SDK pour intégrer votre propre source de données au catalogue de sources Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:218px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, API HTTP, JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:39px; vertical-align:top; width:282px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Parmi les exemples de sources de streaming intégrées par les partenaires, citons : Braze, Pendo et RainFocus.</span></span></span></li>
</ul>
</td>
</tr>
</tbody>
</table>

## Méthodes d’ingestion par lots {#batch-ingestion-methods}

Le tableau suivant décrit les différentes méthodes que vous pouvez utiliser pour ingérer des données par lots vers Experience Platform.

<table cellspacing="0" class="Table" style="border-collapse:collapse; width:1105px">
<tbody>
<tr>
<td colspan="4" style="background-color:#308fff; border-bottom:4px solid white; border-left:1px solid white; border-right:1px solid white; border-top:1px solid white; height:37px; vertical-align:top; width:1105px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><strong><span style="color:black">Sources de lot</span></strong></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Méthode</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:397px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Cas d’utilisation courants</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Protocoles</span></span></span></p>
</td>
<td style="background-color:#969696; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:34px; vertical-align:top; width:277px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Considérations</span></span></span></p>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview" style="color:#0563c1; text-decoration:underline">API Batch Ingestion</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingestion depuis une file d’attente gérée par l’entreprise. Utilisez l’ingestion par lots si vos données doivent être préparées et formatées avant l’ingestion.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Notification push, JSON ou Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ils doivent gérer les lots et les fichiers pour l’ingestion.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/en/docs/experience-platform/sources/home" style="color:#0563c1; text-decoration:underline">Sources de lot</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Approche courante pour l’ingestion de données provenant d’applications de stockage dans le cloud, de gestion de la relation client et d’automatisation marketing.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Idéal pour ingérer de grandes quantités de données historiques.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Pull, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Ingestion de Source basée sur des intervalles planifiés préconfigurés.</span></span></span></li>
</ul>
</td>
</tr>
<tr>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/data-landing-zone.html?lang=en" style="color:#0563c1; text-decoration:underline">Zone d’atterrissage des données</a></span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Stockage de fichiers dans le cloud configuré par Adobe. Vous avez accès à un conteneur Data Landing Zone par sandbox.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Envoyez vos fichiers dans la zone d’atterrissage de données pour une ingestion ultérieure dans Experience Platform.</span></span></span></li>
</ul>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Push, CSV, JSON, Parquet</span></span></span></p>
</td>
<td style="background-color:#e8eeff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Experience Platform applique un délai d’expiration strict de sept jours sur tous les fichiers et dossiers chargés dans un conteneur Data Landing Zone. Tous les fichiers et les dossiers sont supprimés au bout de sept jours.</span></span></span></li>
</ul>
</tr>
<tr>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:1px solid white; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:217px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black"><a href="https://experienceleague.adobe.com/docs/experience-platform/sources/sdk/overview.html?lang=en" style="color:#0563c1; text-decoration:underline">SDK des sources par lots</a></span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:397px">
<ul style="list-style-type:square">
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Utilisez les fonctionnalités en libre-service du SDK par lots des sources en libre-service pour intégrer votre propre source de données au catalogue des sources Experience Platform.</span></span></span></li>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Idéal pour les connecteurs partenaires ou pour une expérience de workflow personnalisée pour configurer un connecteur d’entreprise.</span></span></span></li>
</ul>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:215px">
<p><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Extraction, API REST, CSV ou JSON</span></span></span></p>
</td>
<td style="background-color:#cddbff; border-bottom:1px solid white; border-left:none; border-right:1px solid white; border-top:none; height:62px; vertical-align:top; width:277px">
<ul>
<li><span style="font-size:12pt"><span style="font-family:Calibri,sans-serif"><span style="color:black">Mailchimp, OneTrust, Zendesk sont des exemples de sources de lots intégrées par les partenaires</span></span></span></li>
</ul>

<p> </p>
</td>
</tr>
</tbody>
</table>

## Étapes suivantes et ressources supplémentaires

Ce document vous a présenté brièvement les différents aspects de [!DNL Data Ingestion] dans [!DNL Experience Platform]. Poursuivez votre lecture de la documentation de présentation de chaque méthode d’ingestion pour vous familiariser avec leurs différentes capacités, les cas d’utilisation et les bonnes pratiques. Vous pouvez également compléter votre apprentissage en regardant la vidéo de présentation de lʼingestion ci-dessous. Pour en savoir plus sur la manière dont [!DNL Experience Platform] suit les métadonnées pour les enregistrements ingérés, reportez-vous à la [présentation du service de catalogue](../catalog/home.md).

>[!WARNING]
>
>Le terme « Profil unifié » utilisé dans la vidéo suivante est obsolète. Les termes [!DNL "Profile"] ou [!DNL "Real-Time Customer Profile"] sont les termes appropriés utilisés dans la documentation dʼ[!DNL Experience Platform]. Reportez-vous à la documentation pour connaître les dernières fonctionnalités.

>[!VIDEO](https://video.tv.adobe.com/v/27106?quality=12&learn=on)
