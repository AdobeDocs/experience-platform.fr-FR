---
title: Connexion PX Gainsight
description: Utilisez la destination Gainsight PX pour envoyer des informations de segmentation à la plateforme Gainsight PX.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 24%

---

# Connexion PX Gainsight {#gainsight-px}

## Vue d’ensemble {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) est une plateforme d’expérience de produit qui permet aux équipes produit de comprendre comment les utilisateurs utilisent leurs produits, de recueillir des commentaires et de créer des engagements in-app tels que des présentations de produit afin de stimuler l’intégration des utilisateurs et l’adoption de produits.

>[!IMPORTANT]
>
>Le connecteur de destination et la page de documentation sont créés et gérés par l’équipe *Gainsight PX*. Pour toute question ou demande de mise à jour, contactez directement l’équipe d’Amazon Ads au *`pxsupport@gainsight.com`*.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination *Gainsight PX*, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Ciblage des engagements In-App {#targeting-in-app-engagements}

Une entreprise SaaS souhaite interagir avec ses clients au moyen d&#39;un guide intégré à l&#39;application conçu sur Gainsight PX. Une audience pour recevoir cet engagement a été créée sur Adobe Experience Platform. La destination de Gainsight PX reçoit l’audience et la rend disponible dans l’environnement Gainsight PX.

## Conditions préalables {#prerequisites}

* Contactez l’équipe d’assistance [!DNL Gainsight] et demandez l’activation des fonctionnalités de segment externes pour votre abonnement.
* Générez une valeur secrète OAuth pour votre abonnement PX à l’aide du bouton **[!UICONTROL Generate New Secret]** situé au bas de la page [Détails de l’entreprise](https://app.aptrinsic.com/settings/subscription)
  ![Écran Détails de l’entreprise dans Gainsight PX affichant le bouton Générer un nouveau secret](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Identités prises en charge {#supported-identities}

Gainsight PX prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](../../../identity-service/features/namespaces.md).

| Identité cible | Description |
|---|----|
| IdentifiantID | Identifiant utilisateur commun qui identifie de manière unique un utilisateur dans Gainsight PX et Adobe Experience Platform |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audience que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---|---|---|
| Type d’exportation | **[!UICONTROL Segment export]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Gainsight PX]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Manage Destinations]** [Access Control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

![Capture d’écran d’authentification](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Password]** : mot de passe utilisé pour se connecter à [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL Client ID]** : ID d’abonnement Gainsight PX sur la page [&#x200B; Détails de l’entreprise &#x200B;](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Client secret]** : secret OAuth généré au bas de la page [Détails de l’entreprise](https://app.aptrinsic.com/settings/subscription) dans l’interface utilisateur de [!DNL Gainsight PX].
* **[!UICONTROL Username]** : adresse e-mail utilisée pour se connecter à l’interface utilisateur de [[!DNL Gainsight PX]](https://app.aptrinsic.com)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Écran de détails de la destination dans l’interface utilisateur d’Experience Platform indiquant comment remplir les champs Nom et Description](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [Activer les profils et les segments vers les destinations d’exportation de segments de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mapping d’identités {#map}

Cette destination prend en charge le mappage des attributs de profil et des espaces de noms d’identité. Le mapping de ciblage doit toujours être l’espace de noms d’identité **[!UICONTROL IDENTIFY_ID]**.

Consultez les exemples ci-dessous pour mieux comprendre comment configurer le mappage.

#### Mapper un attribut de profil {#map-profile-attribute}

Dans l’exemple illustré ci-dessous, le champ source est un attribut de profil XDM qui est mappé à l’espace de noms cible IDENTIFY_ID.

![Écran de mappage d’exemple d’espace de noms d’identité montrant comment sélectionner les valeurs source et cible](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Mappage d’un espace de noms d’identité {#map-identity-namespace}

Dans l’exemple ci-dessous, le champ source est un espace de noms d’identité (**[!UICONTROL ECID]**) qui est mappé à l’espace de noms cible **[!UICONTROL IDENTIFY_ID]**.

![Écran de mappage d’exemples d’attributs montrant comment sélectionner les valeurs source et cible](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Les données de segmentation sont diffusées en continu d’Experience Platform vers Gainsight PX.

Les métadonnées de segment sont visibles dans l’écran Segments de l’interface utilisateur de [!DNL Gainsight PX].

![Écran de liste de segments dans Gainsight PX affichant les segments externes.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

Les informations sur l’appartenance à un segment sont visibles dans l’onglet Segments de l’écran Explorateur d’audiences de l’interface utilisateur de [!DNL Gainsight PX].

![Écran Audience Explorer dans Gainsight PX affichant les segments associés à un utilisateur.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).
