---
title: Activation des audiences de compte vers les destinations
type: Tutorial
description: Découvrez comment activer les audiences de compte vers les destinations
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: 1c31dd978298191dd10500b60eb446d2ca37139c
workflow-type: tm+mt
source-wordcount: '836'
ht-degree: 7%

---

# Activation des audiences de compte

>[!AVAILABILITY]
>
>La fonctionnalité permettant d’activer les audiences de compte vers les destinations est disponible pour les entreprises qui ont acheté les versions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Cet article explique le processus requis pour exporter les [audiences de compte](/help/segmentation/ui/account-audiences.md) de Adobe Experience Platform vers votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Utilisez le filtre **[!UICONTROL Types de données]** et sélectionnez **[!UICONTROL Comptes]** pour afficher les destinations qui prennent en charge l’activation des audiences de compte. Actuellement, l’exportation d’audiences de compte n’est disponible que pour certaines destinations de stockage dans le cloud ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Stockage Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Zone d’entrée de données](/help/destinations/catalog/cloud-storage/data-landing-zone.md) et [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) et les audiences [Demandbase](/help/destinations/catalog/advertising/demandbase.md) et [(Entreprises) LinkedIn) 13} destination de diffusion en continu.](/help/destinations/catalog/social/linkedin-b2b.md)

![Destinations qui prennent en charge les audiences de compte.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Vue d’ensemble des vidéos

Consultez la vidéo ci-dessous pour une vue d’ensemble de la création et de l’activation d’audiences de compte, ainsi que des cas d’utilisation pris en charge lors de l’activation d’audiences de compte.

>[!VIDEO](https://video.tv.adobe.com/v/338252/?learn=on)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer les [profils de compte](/help/rtcdp/accounts/account-profile-overview.md) et créer les [audiences de compte](/help/segmentation/ui/account-audiences.md) avant de pouvoir les activer vers les destinations en aval.
* Pour activer les audiences du compte vers des destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [catalogue des destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Pour plus d’informations, consultez le tutoriel sur l’interface utilisateur de [connexion aux destinations](./connect-destination.md) .

### Autorisations nécessaires {#permissions}

Pour activer les audiences de compte, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès  . Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences de compte, parcourez le catalogue des destinations. Si une destination possède un contrôle **[!UICONTROL Activer]**, vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionnez **[!UICONTROL Activer]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter des audiences de compte sont indiquées par une icône dans le coin supérieur droit de la carte, similaire à la destination mise en évidence ci-dessous. Vous pouvez également utiliser le filtre de type de données pour afficher uniquement les destinations qui peuvent exporter des audiences de compte, comme [illustré plus haut sur la page](#supported-destinations).

![Page de destination Demandbase qui peut exporter les audiences de profil en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/demandbase-icon-activate-account-audiences.png)

1. Sélectionnez **[!UICONTROL Comptes de type de données]**, suivi de la connexion de destination vers laquelle vous souhaitez exporter les jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de compte, sélectionnez **[!UICONTROL Configurer une nouvelle destination]** pour déclencher le workflow [Se connecter à la destination](/help/destinations/ui/connect-destination.md) et [sélectionner des comptes comme type de données](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Workflow d’activation de la destination avec le contrôle des comptes en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Passez à la section suivante : [sélectionnez les audiences de votre compte](#select-profile-audiences) pour l’exportation.

## Sélectionner les audiences de votre compte {#select-account-audiences}

Utilisez les cases à cocher situées à gauche des noms d’audiences du compte pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**. Notez que seules les *audiences de compte* s’affichent dans cette vue et qu’aucun autre type d’audience ne s’affiche.

![ Le workflow d&#39;exportation des jeux de données affiche l&#39;étape Sélectionner les audiences où vous pouvez sélectionner les audiences de compte à exporter.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation permettant d’exporter les audiences de compte, lisez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Passez de l’ [étape d’exportation de l’audience de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Si vous activez les audiences de compte vers la destination **[!UICONTROL (Sociétés) Audiences mappées LinkedIn]**, lisez le tutoriel sur l’activation des destinations de diffusion en continu. Passez de l’ [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Notez que lors de l’étape de planification lors de l’exportation des audiences de compte vers des destinations de stockage dans le cloud, le workflow d’activation des audiences de compte vous permet uniquement d’exporter les [fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et les [ fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _selon une planification quotidienne_. Les exportations horaires ne sont pas prises en charge. Notez également que **[!UICONTROL Après l’évaluation de l’audience]** est le seul type d’évaluation pris en charge.

## Légendes importantes et limites connues {#important-callouts-known-limitations}

Notez les légendes importantes et les limites connues suivantes pour la mise à jour générale de la fonctionnalité d’activation des audiences de compte.

### Paires de mappage requises à l’étape de mappage lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Sociétés) LinkedIn Matched Audiences]** {#required-mappings}

Lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Entreprises) Audiences mappées LinkedIn]**, notez que les deux paires de mappage suivantes sont obligatoires pour exporter les données avec succès :

![Le mappage LinkedIn nécessite des champs.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Champ source | Champ cible |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (sélectionnez ce champ dans la vue **[!UICONTROL Sélectionner l’espace de noms d’identité]**, lors de la sélection du **[!UICONTROL champ cible]**). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations."){width="100" zoomable="yes"} |

### Application de la gouvernance des données {#data-governance-enforcement}

Le consentement est appliqué au niveau de la personne ou du profil pour les *audiences du client et des prospects*. Par conséquent, l’ [évaluation de la stratégie de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas prise en charge lors de l’activation des audiences de compte vers les destinations. À l’étape de révision du processus d’activation, vous pouvez voir un contrôle hors zone grisé pour **[!UICONTROL Afficher les stratégies de consentement applicables]**.

![Étape de révision du workflow d’activation des audiences de compte avec le contrôle d’application du consentement grisé.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

D’autres mécanismes de gouvernance des données dans Real-Time CDP tels que les [contrôles de stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) et le [contrôle d’accès basé sur les attributs](/help/destinations/home.md#attribute-based-access) sont pris en charge.
