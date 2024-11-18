---
title: Connexion de destination en temps réel Magnite
description: Utilisez cette destination pour fournir en temps réel des audiences CDP d’Adobe à la plateforme de diffusion en continu Magnite.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: da05db9376893bdbe8f0aa291f19a507e4a73d4f
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 31%

---

# Magnite : connexion de destination en temps réel

## Vue d’ensemble {#overview}

Les destinations [!DNL Magnite: Real-Time] et [Magnite: Batch](/help/destinations/catalog/advertising/magnite-batch.md) dans Adobe Experience Platform vous aident à mapper et exporter des audiences pour le ciblage et l’activation sur la plateforme de diffusion en continu Magnite.

L’activation des audiences vers la plateforme [!DNL Magnite Streaming] est un processus en deux étapes qui nécessite l’utilisation de Magnite : destinations en temps réel et de Magnite : destinations par lot.

Pour activer vos audiences vers [!DNL Magnite Streaming], vous devez :

* Activez les audiences sur la destination [!DNL Magnite: Real-Time], comme illustré dans cette page.
* Activez la même audience sur Magnite : destination du lot. La destination [!DNL Magnite: Batch] est un composant obligatoire. Si vous n’activez pas l’audience sur la destination [!DNL Magnite Streaming] par lot, l’intégration échouera et vos audiences ne seront pas activées.

Remarque : Lors de l’utilisation de la destination en temps réel, [!DNL Magnite Streaming] recevra des audiences en temps réel, mais Magnite ne peut stocker les audiences en temps réel que temporairement sur sa plateforme, et elles seront supprimées du système dans les quelques jours. Pour cette raison, si vous souhaitez utiliser la destination Magnite : Temps réel, vous devrez *également* utiliser la destination Magnite : lot : chaque audience que vous activez vers la destination Temps réel, vous devrez également l’activer vers la destination Lot.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe [!DNL Magnite]. Pour toute question ou demande de mise à jour, contactez-les directement à l’adresse `adobe-tech@magnite.com`.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Magnite: Real-Time], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Activation et ciblage {#activation-and-targeting}

Cette intégration à Magnite permet aux clients de transmettre leurs audiences CDP de Adobe Experience Platform vers Magnite pour le ciblage publicitaire. Les audiences peuvent être sélectionnées dans Magnite pour un ciblage positif et un ciblage négatif (suppression).

## Conditions préalables {#prerequisites}

Pour utiliser les destinations [!DNL Magnite] dans Adobe Experience Platform, vous devez d’abord disposer d’un compte [!DNL Magnite Streaming]. Si vous disposez d’un compte [!DNL Magnite Streaming], contactez votre gestionnaire de compte [!DNL Magnite] pour qu’il vous fournisse les informations d’identification lui permettant d’accéder aux destinations [!DNL Magnite's].
Si vous ne disposez pas d’un compte [!DNL Magnite Streaming], contactez adobe-tech@magnite.com

## Identités prises en charge {#supported-identities}

La destination [!DNL Magnite: Real-Time] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Identifiant unique d’un appareil ou d’une identité. Nous acceptons tous les identifiants d’appareil et propriétaires, quel que soit leur type. | Les types d’identités pris en charge par Magnite incluent, sans s’y limiter, les identifiants PPUID, GAID, IDFA et d’appareil TV. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Magnite: Real-Time]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin de l’**[!UICONTROL affichage des destinations]** et de l’**[!UICONTROL gestion des destinations]** [ autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

![Champs d’authentification de configuration de destination vides](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Nom d’utilisateur]** : nom d’utilisateur qui vous a été fourni par [!DNL Magnite].
* **[!UICONTROL Mot de passe]** : mot de passe fourni par [!DNL Magnite].

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Nom de votre société]** : nom de votre client/société. Seuls les clients [!DNL Magnite Streaming] pris en charge peuvent être sélectionnés.

>[!NOTE]
>
>Le nom de l’entreprise doit être une chaîne correspondant au nom du compartiment de diffusion Amazon S3 que vous avez configuré avec Magnite et configuré à l’étape [s’authentifier à la destination](#authenticate). Les caractères pris en charge sont &quot;a-z&quot;, &quot;A-Z&quot;, &quot;0-9&quot;, &quot;-&quot; (tiret) ou &quot;_&quot; (trait de soulignement).

![Champs d’authentification de configuration de destination renseignés](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Une fois que vous avez terminé, cliquez sur le bouton **[!UICONTROL Créer]** .

![Stratégie de gouvernance et actions d’application facultatives](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des **** destinations d’affichage, **[!UICONTROL activer les destinations]**, **** profils d’affichage et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

Une fois la connexion de destination créée, vous pouvez passer au flux d’activation de l’audience. La section suivante décrit comment activer des audiences à l’aide de la destination Temps réel.

### Mapper les attributs et les identités {#map}

L’étape suivante consiste à mapper les identifiants de source à l’identifiant de Magnite device_id.

* Vous pouvez ajouter autant de mappages que nécessaire en sélectionnant **[!UICONTROL Ajouter un nouveau mappage]**.

Cet exemple utilisant la destination en temps réel affiche une ligne qui contient un identifiant source deviceId générique mappé sur le champ cible Magnite device_id . Lorsque vous utilisez les mappages, sélectionnez [!UICONTROL Suivant].

![ Mappez les champs de données de votre choix avec le champ device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Veillez à définir les identifiants de mappage sur toutes les audiences activées ou à définir AUCUN si aucun identifiant de mappage n’est présent.

![Veillez à définir les identifiants de mappage sur toutes les audiences activées, ou à définir AUCUN si aucun identifiant de mappage n&#39;est présent](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Vous devez maintenant configurer une date de début (obligatoire), une date de fin (facultatif) et un identifiant de mappage pour chaque audience.

**Identifiant de mappage**

* Utilisez le champ **[!UICONTROL ID de mappage]** lorsqu’une audience a un identifiant de segment préexistant précédemment connu de Magnite.

* Pour ajouter un **[!UICONTROL ID de mappage]** à une audience, sélectionnez chaque ligne d’audience individuellement, puis saisissez les données dans la colonne de droite (voir l’image ci-dessus). Si vous ne souhaitez pas ajouter d’ID de mappage, saisissez NONE dans le champ ID de mappage .

Sélectionnez **[!UICONTROL Suivant]** et finalisez le flux d’activation.

![Sélectionnez le flux d’activation suivant et finalisez-le.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une fois les audiences chargées, vous pouvez vérifier que les audiences ont été créées et chargées correctement en procédant comme suit :

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Après l’ingestion, les audiences doivent apparaître dans [!DNL Magnite Streaming] dans les quelques minutes et peuvent être appliquées à une transaction. Vous pouvez le confirmer en recherchant l’identifiant du segment qui a été partagé lors des étapes d’activation dans Adobe Experience Platform.

## Activez les mêmes audiences via la destination [!DNL Magnite: Batch]

Les audiences partagées avec [!DNL Magnite Streaming] à l’aide de la destination en temps réel devront également être partagées à l’aide de la destination Magnite : lot. Lorsqu’ils sont correctement configurés, les noms de segment dans l’interface utilisateur de [!DNL Magnite Streaming] sont mis à jour pour prendre en compte ceux utilisés dans la mise à jour post-quotidienne de Adobe Experience Platform.

Enfin, si une destination de lot n’a pas été configurée pour votre intégration, configurez-la maintenant via le document Magnite : destination de lot .

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Pour obtenir une aide supplémentaire, consultez le [Centre d’aide Magnite](https://help.magnite.com/help).
