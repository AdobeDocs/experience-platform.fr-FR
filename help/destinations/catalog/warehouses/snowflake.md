---
title: Connexion en continu Snowflake
description: Créez un partage de données Snowflake en direct pour recevoir des mises à jour d’audience en flux continu directement sous forme de tables partagées dans votre compte .
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: 59df2c6a0fb5d9dbdd10b52d82fb6b94f5083c3a
workflow-type: tm+mt
source-wordcount: '1466'
ht-degree: 22%

---

# Connexion en continu Snowflake {#snowflake-destination}

>[!AVAILABILITY]
>
>Ce connecteur de destination est en disponibilité limitée et disponible uniquement pour les clients Real-Time CDP Ultimate configurés dans la région [VA7](/help/landing/multi-cloud.md#azure-regions).

## Vue d’ensemble {#overview}

Utilisez le connecteur de destination Snowflake pour exporter des données vers l’instance Adobe Snowflake, qu’Adobe partage ensuite avec votre instance par le biais de [listes privées](https://other-docs.snowflake.com/en/collaboration/collaboration-listings-about).

Lisez les sections suivantes pour comprendre comment fonctionne la destination Snowflake et comment les données sont transférées entre Adobe et Snowflake.

### Fonctionnement du partage des données de Snowflake {#data-sharing}

Cette destination utilise un partage de données [!DNL Snowflake], ce qui signifie qu’aucune donnée n’est physiquement exportée ou transférée vers votre propre instance de Snowflake. Au lieu de cela, Adobe vous accorde un accès en lecture seule à une table dynamique hébergée dans l’environnement Adobe Snowflake. Vous pouvez interroger cette table partagée directement à partir de votre compte Snowflake, mais vous n’êtes pas propriétaire de la table et ne pouvez pas la modifier ni la conserver au-delà de la période de conservation spécifiée. Adobe gère entièrement le cycle de vie et la structure de la table partagée.

La première fois que vous partagez des données de l’instance Adobe Snowflake vers la vôtre, vous êtes invité à accepter la liste privée d’Adobe.

![Capture d’écran affichant l’écran d’acceptation de la liste privée Snowflake](../../assets/catalog/cloud-storage/snowflake/snowflake-accept-listing.png)

### Conservation des données et durée de vie (TTL) {#ttl}

Toutes les données partagées par le biais de cette intégration ont une durée de vie (TTL) fixe de sept jours. Sept jours après la dernière exportation, la table partagée expire automatiquement et devient inaccessible, que le flux de données soit toujours actif ou non. Si vous devez conserver les données pendant plus de sept jours, vous devez copier le contenu dans une table que vous détenez dans votre propre instance Snowflake avant l’expiration de la TTL.

### Comportement de mise à jour de l’audience {#audience-update-behavior}

Si votre audience est évaluée en [mode batch](../../../segmentation/methods/batch-segmentation.md), les données du tableau partagé sont actualisées toutes les 24 heures. Cela signifie qu’il peut y avoir un retard de jusqu’à 24 heures entre les modifications de l’appartenance à l’audience et le moment où ces modifications sont répercutées dans le tableau partagé.

### Logique d’exportation incrémentielle {#incremental-export}

Lorsqu’un flux de données s’exécute pour une audience pour la première fois, il effectue un renvoi et partage tous les profils actuellement qualifiés. Après ce renvoi initial, seules les mises à jour incrémentielles sont répercutées dans le tableau partagé. Cela signifie les profils qui sont ajoutés ou supprimés de l’audience. Cette approche garantit des mises à jour efficaces et maintient la table partagée à jour.

## Partage de données par lots ou en flux continu {#batch-vs-streaming}

Experience Platform fournit deux types de destinations Snowflake : [Diffusion en continu Snowflake](snowflake.md) et [Lot Snowflake](snowflake-batch.md).

Le tableau ci-dessous vous aidera à choisir la destination à utiliser en décrivant les scénarios où chaque méthode de partage de données est la plus appropriée.

|  | Choisissez [Snowflake Batch](snowflake-batch.md) lorsque vous en avez besoin | Choisissez [Snowflake Streaming](snowflake.md) lorsque vous en avez besoin |
|--------|-------------------|----------------------|
| **Fréquence de mise à jour** | Instantanés périodiques | Mises à jour continues en temps réel |
| **Présentation des données** | Instantané d’audience complet qui remplace les données précédentes | Mises à jour incrémentielles en fonction des modifications de profil |
| **Cas d’utilisation ciblé** | Charges de travail analytiques/ML pour lesquelles la latence n’est pas critique | Scénarios d’action immédiate nécessitant des mises à jour en temps réel |
| **Gestion des données** | Toujours afficher le dernier instantané complet | Mises à jour incrémentielles en fonction des modifications de l’appartenance à une audience |
| **Exemples de scénarios** | Création de rapports d’entreprise, analyse de données, formation au modèle ML | Suppression des campagnes marketing, personnalisation en temps réel |

Pour plus d’informations sur le partage de données par lots, consultez la documentation sur la connexion par lots de [Snowflake](snowflake-batch.md) .

## Cas d’utilisation {#use-cases}

Le partage de données en flux continu est idéal pour les scénarios où vous avez besoin de mises à jour immédiates lorsqu’un profil modifie son appartenance ou d’autres attributs. Cela est essentiel pour les cas d’utilisation nécessitant une réactivité en temps réel, tels que :

* **Suppression des campagnes marketing** : supprimez immédiatement les campagnes marketing pour les utilisateurs et utilisatrices qui ont effectué des actions spécifiques, telles que l’inscription à un service ou l’achat
* **Personnalisation en temps réel** : mettez instantanément à jour les expériences utilisateur lorsque les attributs de profil changent, par exemple lorsqu’un utilisateur visite un site web, consulte une page produit ou ajoute des articles dans un panier
* **Scénarios d’action immédiate** : exécutez une suppression et un reciblage rapides en fonction des données en temps réel pour réduire les retards et vous assurer que les campagnes marketing sont plus pertinentes et plus rapides
* **Efficacité et nuance** : augmentez l’efficacité et la nuance des efforts marketing en permettant une réponse rapide aux changements de comportement des utilisateurs et utilisatrices
* **Optimisation du parcours client en temps réel** : mettez immédiatement à jour les expériences client lorsque l’appartenance à un segment ou les attributs de profil changent

Le partage de données en flux continu fournit des mises à jour continues en fonction des modifications de segment, des modifications de mappage d’identités ou des modifications d’attributs, ce qui le rend adapté aux scénarios où la latence est critique et où des mises à jour immédiates sont requises.

## Conditions préalables {#prerequisites}

Avant de configurer votre connexion Snowflake, veillez à respecter les conditions préalables suivantes :

* Vous avez accès à un compte [!DNL Snowflake].
* Votre compte Snowflake est abonné à des annonces privées. Vous ou un membre de votre société disposant de droits d’administrateur de compte sur Snowflake pouvez configurer cette option.

Lisez la [[!DNL Snowflake] documentation](https://docs.snowflake.com/en/collaboration/consumer-listings-access#access-a-private-listing) pour plus d’informations sur les autorisations nécessaires.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination. Les deux tableaux ci-dessous indiquent les audiences prises en charge par ce connecteur, par _origine de l’audience_ et _types de profil inclus dans l’audience_ :

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | ✓ | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Snowflake]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Connect to destination]**.

![Exemple de capture d’écran montrant comment s’authentifier à la destination](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### Renseigner les détails de la destination {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_accountID"
>title="Saisir votre identifiant de compte Snowflake"
>abstract="Si votre compte est lié à une organisation, utilisez le format suivant : `OrganizationName.AccountName`<br><br>. Si votre compte n’est pas lié à une organisation, utilisez le format suivant : `AccountName`."

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Exemple de capture d’écran montrant comment remplir les détails pour votre destination](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Snowflake Account ID]** : identifiant de votre compte Snowflake. Utilisez le format d’identifiant de compte suivant selon que votre compte est lié ou non à une organisation :
   * Si votre compte est lié à une organisation, procédez comme suit `OrganizationName.AccountName`.
   * Si votre compte n’est pas lié à une organisation, `AccountName`.
* **[!UICONTROL Account acknowledgment]** : activez/désactivez l’accusé de réception de l’ID de compte Snowflake pour confirmer que l’ID de compte est correct et qu’il vous appartient.

>[!IMPORTANT]
>
> Les caractères spéciaux utilisés dans le nom de la destination et le nom du sandbox Experience Platform sont automatiquement convertis en traits de soulignement (`_`) dans Snowflake. Pour éviter toute confusion, n’utilisez pas de caractères spéciaux dans la destination et le nom du sandbox.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de mappage {#map}

La destination Snowflake prend en charge le mappage des attributs de profil aux attributs personnalisés.

![Image de l’interface utilisateur d’Experience Platform montrant l’écran de mappage pour la destination Snowflake.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

Les attributs de la cible sont automatiquement créés dans Snowflake à l’aide du nom d’attribut que vous fournissez dans le champ **[!UICONTROL Attribute name]** .

## Données exportées / Valider l’exportation des données {#exported-data}

Vérifiez votre compte Snowflake pour vous assurer que les données ont été correctement exportées.

## Limites connues {#known-limitations}

### Restriction de la politique de fusion par défaut {#default-merge-policy-restriction}

Actuellement, seules les audiences mappées à la politique de fusion par défaut peuvent être exportées.

### Disponibilité régionale {#regional-availability}

Actuellement, la destination de diffusion en continu [!DNL Snowflake] n’est disponible que pour les clients Real-Time CDP configurés dans la région VA7 d’Experience Platform.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
