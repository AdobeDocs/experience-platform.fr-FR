---
title: Activer les audiences de compte vers les destinations
type: Tutorial
description: Découvrez comment activer les audiences de compte vers les destinations
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 6%

---

# Activer les audiences de compte

>[!AVAILABILITY]
>
>La fonctionnalité d’activation des audiences de compte vers les destinations est disponible pour les sociétés qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Cet article explique le processus requis pour exporter des [audiences de compte](/help/segmentation/types/account-audiences.md) de Adobe Experience Platform vers votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** . Utilisez le filtre **[!UICONTROL Data types]** et sélectionnez **[!UICONTROL Accounts]** pour afficher les destinations qui prennent en charge l’activation des audiences de compte. Actuellement, l’exportation des audiences de compte n’est disponible que pour certaines destinations d’espace de stockage dans le cloud ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Stockage Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Zone d’atterrissage des données](/help/destinations/catalog/cloud-storage/data-landing-zone.md) et [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) et la destination de diffusion en continu [Demandbase](/help/destinations/catalog/advertising/demandbase.md) et [(Entreprises) LinkedIn Matched Audiences](/help/destinations/catalog/social/linkedin-b2b.md).

![Destinations qui prennent en charge les audiences de compte.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Vue d’ensemble des vidéos

Regardez la vidéo ci-dessous pour obtenir un aperçu sur la création et l’activation des audiences de compte, ainsi que sur les cas d’utilisation pris en charge lors de l’activation des audiences de compte.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer des [profils de compte](/help/rtcdp/accounts/account-profile-overview.md) et créer des [audiences de compte](/help/segmentation/types/account-audiences.md) avant de pouvoir les activer vers des destinations en aval.
* Pour activer les audiences de compte vers les destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [catalogue de destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Pour plus d’informations, consultez le tutoriel de l’interface utilisateur sur [connexion aux destinations](./connect-destination.md).

### Autorisations nécessaires {#permissions}

Pour activer les audiences de compte, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Activate Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences de compte, parcourez le catalogue des destinations. Si une destination dispose d’un contrôle **[!UICONTROL Activate]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connections > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalog]** .

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activate]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter les audiences de compte sont indiquées par une icône dans le coin supérieur droit de la carte, similaire à la destination mise en surbrillance ci-dessous, ou vous pouvez utiliser le filtre de type de données pour afficher uniquement les destinations pouvant exporter les audiences de compte, comme [indiqué plus haut sur la page](#supported-destinations).

![Page de destination Demandbase pouvant exporter les audiences de profil mises en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Sélectionnez **[!UICONTROL Data type Accounts]**, suivi de la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Next]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de compte, sélectionnez **[!UICONTROL Configure new destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md) et [sélectionner les comptes comme type de données](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Workflow d’activation de destination avec le contrôle des comptes mis en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Passez à la section suivante pour [sélectionner les audiences de votre compte](#select-profile-audiences) à exporter.

## Sélectionner les audiences de votre compte {#select-account-audiences}

Utilisez les cases à cocher situées à gauche des noms des audiences de compte pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Next]**. Notez que seules les *audiences de compte* s’affichent dans cette vue, et aucun autre type d’audience ne s’affiche.

![Workflow d’exportation des jeux de données présentant l’étape de sélection des audiences permettant de sélectionner les audiences de compte à exporter.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation afin d’exporter les audiences de compte, consultez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Continuez à partir de l’étape [planifier l’exportation de l’audience](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Si vous activez des audiences de compte vers la destination **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, consultez le tutoriel sur l’activation des destinations de diffusion en streaming. Passez à l’étape [Mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Notez que lors de l’étape de planification lors de l’exportation d’audiences de compte vers des destinations d’espace de stockage, le workflow d’activation des audiences de compte ne vous permet d’exporter que des [fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et des [fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _selon un planning quotidien_. Les exportations horaires ne sont pas prises en charge. Notez également que **[!UICONTROL After audience evaluation]** est le seul type d’évaluation pris en charge.

## Légendes importantes et limites connues {#important-callouts-known-limitations}

Notez les importantes légendes suivantes et les limites connues pour la mise à disposition générale de la fonctionnalité d’activation des audiences de compte.

### Paires de mappage obligatoires à l’étape de mappage lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Companies) LinkedIn Matched Audiences]** {#required-mappings}

Lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Companies) LinkedIn Matched Audiences]**, notez que les deux paires de mappage suivantes sont obligatoires pour exporter des données :

![Mappage LinkedIn des champs obligatoires.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Champ source | Champ cible |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (sélectionnez ce champ dans la vue **[!UICONTROL Select Identity namespace]** lors de la sélection du **[!UICONTROL Target Field]**). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations."){width="100" zoomable="yes"} |

### Application de la gouvernance des données {#data-governance-enforcement}

Le consentement est appliqué au niveau de la personne ou du profil pour les *audiences de clients et de prospects*. Par conséquent, l’[évaluation des politiques de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas prise en charge lors de l’activation des audiences de compte vers les destinations. Dans l’étape de révision du workflow d’activation, vous pouvez voir un contrôle grisé pour **[!UICONTROL View applicable consent policies]**.

![L’étape Vérifier du workflow d’activation des audiences de compte avec le contrôle d’application du consentement grisé.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

D’autres mécanismes de gouvernance des données dans Real-Time CDP, tels que [contrôles des politiques d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) et [contrôle d’accès basé sur les attributs](/help/destinations/home.md#attribute-based-access) sont pris en charge.
