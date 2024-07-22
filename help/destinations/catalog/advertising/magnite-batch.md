---
title: Destination du lot Magnite
description: Utilisez cette destination pour diffuser par lots des audiences CDP d’Adobe vers la plateforme de diffusion en continu Magnite.
badgeBeta: label="Version bêta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: b8921e887b827fcc7b9115045a1954c41a37bce8
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 14%

---


# Magnite : connexion par lots {#magnite-streaming-batch}

## Vue d’ensemble {#overview}

Ce document décrit la destination Magnite : lot et fournit des exemples de cas d’utilisation pour vous aider à mieux comprendre comment activer et exporter des audiences vers cette destination.

Les audiences Adobe Real-Time CDP peuvent être diffusées sur la plateforme de diffusion en continu Magnite de deux manières : elles peuvent être diffusées une fois par jour ou elles peuvent être diffusées en temps réel :

1. Si vous ne souhaitez diffuser des audiences qu’une seule fois par jour et/ou si vous devez le faire, vous pouvez utiliser la destination Magnite : lot qui diffuse des audiences vers la diffusion en continu Magnite par le biais d’une diffusion quotidienne de fichiers par lots S3. Ces audiences par lots sont stockées indéfiniment dans la plateforme Magnite, à la différence des audiences en temps réel, qui ne sont stockées que pendant quelques jours.

2. Cependant, si vous souhaitez diffuser des audiences plus fréquemment, vous devrez utiliser la destination [Magnite Real-Time](/help/destinations/catalog/advertising/magnite-streaming.md). Lors de l’utilisation de la destination en temps réel, la diffusion en flux continu Magnite recevra les audiences en temps réel, mais elle ne pourra stocker que les audiences en temps réel temporairement sur sa plateforme, et celles-ci seront supprimées du système dans les quelques jours. Pour cette raison, si vous souhaitez utiliser la destination en temps réel de Magnite, vous devrez *également* utiliser la destination de lot Magnite : chaque audience que vous activez vers la destination en temps réel, vous devrez également l’activer vers la destination de lot.

Pour récapituler : si vous ne souhaitez diffuser des audiences Adobe Real-Time CDP qu’une fois par jour, vous utiliserez la destination Magnite : lot uniquement, et les audiences seront diffusées une fois par jour. Si vous souhaitez diffuser des audiences Adobe Real-Time CDP en temps réel, vous utiliserez *à la fois* la destination Magnite : lot et la destination Magnite en temps réel. Pour plus d’informations, contactez Magnite : Streaming.


Pour plus d’informations sur Magnite : destination du lot, comment s’y connecter et comment activer les audiences Adobe Real-Time CDP, reportez-vous à la section ci-dessous.
Pour plus d’informations sur la destination en temps réel, reportez-vous à [cette page de documentation](magnite-streaming.md) à la place.

>[!IMPORTANT]
>
>Ce connecteur de destination est en version bêta et disponible uniquement pour certains clients. Pour demander l’accès, contactez votre représentant Adobe.
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Magnite]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse `adobe-tech@magnite.com`.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Magnite : lot, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1 {#use-case-1}

Vous avez activé une audience sur la destination en temps réel de Magnite.

Toutes les audiences activées via la destination Temps réel de Magnite doivent également utiliser la destination Magnite : Lot , car les données de la diffusion par lot sont destinées à remplacer/conserver les données de la diffusion en temps réel dans la plateforme de diffusion en continu de Magnite.

### Cas d’utilisation #2 {#use-case-2}

Vous souhaitez activer une audience uniquement par lots/par jour vers la plateforme de diffusion en continu Magnite.

Toutes les audiences activées via Magnite : la destination du lot sera diffusée en mode batch/quotidien et seront ensuite disponibles pour le ciblage dans la plateforme de diffusion en continu Magnite.

## Conditions préalables {#prerequisites}

Pour utiliser les destinations [!DNL Magnite] dans Adobe Experience Platform, vous devez d’abord disposer d’un compte de diffusion en continu Magnite. Si vous disposez d’un compte [!DNL Magnite Streaming], contactez votre gestionnaire de compte [!DNL Magnite] pour qu’il vous fournisse les informations d’identification lui permettant d’accéder aux destinations [!DNL Magnite's]. Si vous ne disposez pas d’un compte [!DNL Magnite Streaming], contactez adobe-tech@magnite.com

## Identités prises en charge {#supported-identities}

La destination Magnite : lot peut recevoir *n’importe quelle* source d’identité de la plateforme de données clients Adobe. Actuellement, cette destination comporte trois champs d’identité cible auxquels vous pouvez mapper.

>[!NOTE]
>
>*Toutes les sources d’identité* peuvent mapper sur n’importe quelle identité cible `magnite_deviceId`.

| Identité cible | Description | Considérations |
|:--------------------------- |:------------------------------------------------------------------------------------------------ |:------------------------------------------------------------------------------------- |
| magnite_deviceId_GAID | GOOGLE ADVERTISING ID | Sélectionnez cette identité cible lorsque votre identité source est un GAID |
| magnite_deviceId_IDFA | Identifiant Apple pour les annonceurs | Sélectionnez cette identité cible lorsque votre identité source est un IDFA. |
| magnite_deviceId_CUSTOM | Identifiant personnalisé/défini par l’utilisateur | Sélectionnez cette identité cible lorsque votre identité source n’est pas un IDFA ou GAID, ou s’il s’agit d’un identifiant personnalisé ou défini par l’utilisateur. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

| Origine de l’audience | Pris en charge | Description |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

| Élément | Type | Notes |
|-----------------------------|----------|----------|
| Type d’exportation | Exportation de l’audience | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans Magnite : destination du lot. |
| Fréquence des exportations | Lot | Les destinations par lots exportent des fichiers vers des plateformes en aval par incréments de trois, six, huit, douze ou vingt-quatre heures. En savoir plus sur les [destinations basées sur des fichiers](/help/destinations/destination-types.md). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Une fois que votre utilisation de destination a été approuvée et que la diffusion en continu Magnite a partagé vos informations d’identification, suivez les étapes ci-dessous pour vous authentifier, mapper et partager des données.

### S’authentifier auprès de la destination {#authenticate}

Localisez Magnite : destination du lot dans le catalogue de l’expérience d’Adobe. Cliquez sur le bouton des options supplémentaires (\..), puis configurez la connexion/l’instance de destination.

Si vous disposez déjà d’un compte, vous pouvez le localiser en définissant l’option Type de compte sur &quot;Compte existant&quot;. Sinon, vous allez créer un compte ci-dessous :

Pour créer un compte et l’authentifier à la destination pour la première fois, renseignez les champs &quot;Clé d’accès S3&quot; et &quot;Clé secrète S3&quot; requis (fournis à vous par l’intermédiaire de votre gestionnaire de compte), puis sélectionnez **[!UICONTROL Se connecter à la destination]**

![Champs d’authentification de configuration de destination vides](../../assets/catalog/advertising/magnite/destination-batch-config-auth-unfilled.png)

>[!NOTE]
>
>La politique de sécurité de Magnite Streaming nécessite une rotation régulière des clés S3. Vous prévoyez de mettre à jour votre compte à l’avenir avec de nouveaux accès S3 et clés secrètes S3. Il vous suffit de mettre à jour le compte lui-même. Les destinations qui utilisent ce compte utiliseront automatiquement les clés mises à jour. Si vous ne chargez pas les nouvelles clés, les données ne seront pas envoyées vers cette destination.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : nom par lequel vous reconnaîtrez cette connexion/instance de destination dans la variable
future.
* **[!UICONTROL Description]** : description qui vous aidera à identifier ceci
connexion/instance de destination à l’avenir.
* **[!UICONTROL Nom de votre partenaire source]** : nom que vous souhaitez utiliser comme source dans la plateforme de diffusion en continu Magnite.

![Champs d’authentification de configuration de destination renseignés](../../assets/catalog/advertising/magnite/destination-batch-config-auth-filled.png)

>[!NOTE]
>
>Si vous prévoyez d’envoyer plusieurs types d’ID (GAID, IDFA, etc.) à l’aide de la destination de lot, une nouvelle connexion/instance de destination est requise pour chacune d’elles. Pour plus d’informations, contactez votre gestionnaire de compte Magnite.

Vous pouvez ensuite procéder en sélectionnant **[!UICONTROL Suivant]**

Dans l’écran suivant, intitulé &quot;Stratégie de gouvernance et actions d’application (facultatif)&quot;, vous pouvez éventuellement sélectionner toute stratégie de gouvernance des données appropriée. L’option &quot;Exportation de données&quot; est généralement sélectionnée pour la destination Magnite : lot.

![Stratégie de gouvernance et actions d’application facultatives](../../assets/catalog/advertising/magnite/destination-batch-config-grouping-policy.png)

Une fois sélectionné, ou si vous souhaitez ignorer cet écran facultatif, sélectionnez **[!UICONTROL Créer]**

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapper les attributs et les identités {#map}

Dans le **[!UICONTROL champ Source]**, vous pouvez sélectionner n’importe quel attribut ou identité pour vos appareils. Dans cet exemple, nous avons sélectionné une carte d’identité personnalisée appelée &quot;DeviceId&quot;.
![ mappez les champs de données souhaités avec le champ device_id](../../assets/catalog/advertising/magnite/destination-batch-active-audience-field-mapping.png)

Dans le **[!UICONTROL champ cible]** :
![sélectionnez l’identité cible de type d’appareil appropriée](../../assets/catalog/advertising/magnite/destination-batch-active-audience-select-device-type.png) Voir [Identités prises en charge](#supported-identities) pour plus d’informations.
Dans cet exemple, nous avons sélectionné le **[!UICONTROL champ cible]** : magnite_deviceId_CUSTOM, car notre **[!UICONTROL champ Source]** a été défini comme une carte d’identité personnalisée : DeviceID.

>[!NOTE]
>
>Si vous prévoyez d’envoyer/de mapper plusieurs types d’ID (GAID, IDFA, etc.) à l’aide de la destination de lot, une nouvelle connexion/instance de destination est requise pour chacune d’elles. Pour plus d’informations, contactez votre gestionnaire de compte Magnite.


Dans l&#39;écran &quot;Configurer un nom de fichier et un planning d&#39;export pour chaque audience&quot;, vous devez maintenant configurer une date de début (obligatoire), une date de fin (facultatif) et un identifiant de mapping (obligatoire) pour chaque audience.

>[!IMPORTANT]
>
> Un ID de mappage ou &quot;AUCUN&quot; est requis pour cette destination.
>
> Un identifiant de mappage doit être fourni lorsqu’une audience possède un identifiant de segment préexistant précédemment connu pour la diffusion en continu Magnite. Dans le cas contraire, &quot;NONE&quot; doit être utilisé comme ID de mappage.
>
> Lors de la configuration du nom de fichier pour chaque audience, vous devez inclure l&#39;identifiant du mapping via le champ &quot;Texte personnalisé&quot; à ajouter. L’ID de mappage sera ajouté comme suit : `{previous_filename}\_\[MAPPING_ID\].` Si cette audience est une nouvelle audience de la diffusion en continu Magnite et que vous ne fournissez pas d’ID de mappage, &quot;AUCUN&quot; doit être entré dans le champ &quot;Texte personnalisé&quot;. Dans ce cas, le nouveau nom de fichier doit être : `{previous_filename}\_\[NONE\]`.

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois vos audiences chargées, vous pouvez vérifier qu’elles ont été créées et chargées correctement.

* La destination Magnite : un lot permet de diffuser des fichiers S3 en flux continu Magnite à une cadence quotidienne. Après la diffusion et l’ingestion, les audiences/segments doivent apparaître dans la diffusion en continu Magnite et peuvent être appliqués à une transaction. Vous pouvez le confirmer en recherchant l’identifiant du segment ou le nom du segment qui a été partagé lors des étapes d’activation dans Adobe Experience Platform.

>[!NOTE]
>
>Audiences activées/diffusées vers Magnite : la destination par lots *remplacera* les mêmes audiences qui ont été activées/diffusées via la destination en temps réel de Magnite. Si vous recherchez un segment à l’aide du nom du segment, il se peut que vous ne trouviez pas le segment en temps réel tant que le lot n’a pas été ingéré et traité par la plateforme de diffusion en continu Magnite.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour obtenir une aide supplémentaire, consultez le [Centre d’aide Magnite](https://help.magnite.com/help).
