---
title: Activation des audiences de compte vers les destinations
type: Tutorial
description: Découvrez comment activer les audiences de compte vers les destinations
badgeB2B: label="Édition B2B" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: ad69d0a8-bf5b-42ac-97a3-401eadda62cd
source-git-commit: f07eb12b4625bce117e1fe524727c00b7188aa5e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 7%

---

# Activation des audiences de compte

>[!AVAILABILITY]
>
>La fonctionnalité d’activation des audiences de compte vers les destinations est disponible pour les entreprises qui achètent la variable [Entreprise à entreprise](/help/rtcdp/overview.md#rtcdp-b2b) et [Entreprise à personne](/help/rtcdp/overview.md#rtcdp-b2b) éditions de Real-time Customer Data Platform.

Cet article explique le workflow requis pour l’exportation [audiences de compte](/help/segmentation/ui/account-audiences.md) de Adobe Experience Platform à votre destination préférée.

## Destinations prises en charge {#supported-destinations}

Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Utilisez la variable **[!UICONTROL Types de données]** filtrer et sélectionner **[!UICONTROL Comptes]** pour afficher les destinations qui prennent en charge l’activation des audiences de compte. Actuellement, l’exportation d’audiences de compte n’est disponible que pour certaines destinations de stockage dans le cloud ([Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [ADLS Gen 2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Stockage Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [Zone d’entrée des données](/help/destinations/catalog/cloud-storage/data-landing-zone.md), et [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)) et la variable [(Sociétés) Audiences mappées LinkedIn](/help/destinations/catalog/social/linkedin.md) destination.

![Destinations qui prennent en charge les audiences de compte.](/help/destinations/assets/ui/activate-account-audiences/data-types-filter.png)

## Conditions préalables {#prerequisites}

* Vous devez d’abord ingérer [profils de compte](/help/rtcdp/accounts/account-profile-overview.md) et créez [audiences de compte](/help/segmentation/ui/account-audiences.md) avant de pouvoir les activer vers les destinations en aval.
* Pour activer les audiences du compte vers des destinations, vous devez avoir réussi à vous connecter à une destination. Si vous ne l’avez pas déjà fait, accédez au [destinations](../catalog/overview.md), parcourez les destinations prises en charge et configurez la destination que vous souhaitez utiliser. Lisez le tutoriel de l’interface utilisateur sur [connexion aux destinations](./connect-destination.md) pour plus d’informations.

### Autorisations nécessaires {#permissions}

Pour activer les audiences de compte, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Activation des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour vous assurer que vous disposez des autorisations nécessaires pour activer les audiences de compte, parcourez le catalogue des destinations. Si une destination comporte une variable **[!UICONTROL Activer]** contrôlez, puis vous disposez des autorisations appropriées.

## Sélectionner votre destination {#select-destination}

Suivez les instructions pour sélectionner une destination vers laquelle vous pouvez exporter vos jeux de données :

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destination avec le contrôle Catalogue mise en surbrillance.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Sélectionner **[!UICONTROL Activer]** sur la carte correspondant à la destination vers laquelle vous souhaitez exporter des jeux de données.

>[!TIP]
>
>Les destinations pouvant exporter des audiences de compte sont signalées par une icône dans le coin supérieur droit de la carte, semblable à la destination mise en évidence ci-dessous. Vous pouvez également utiliser le filtre de type de données pour afficher uniquement les destinations qui peuvent exporter des audiences de compte, comme [affiché plus haut sur la page](#supported-destinations).

![Page de destination Amazon S3 qui peut exporter les audiences de profil mises en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/amazon-s3-icon-activate-account-audiences.png)

1. Sélectionner **[!UICONTROL Comptes de type de données]**, suivi de la connexion de destination vers laquelle vous souhaitez exporter des jeux de données, puis sélectionnez **[!UICONTROL Suivant]**.

>[!TIP]
> 
>Si vous souhaitez configurer une nouvelle destination pour activer les audiences de compte, sélectionnez **[!UICONTROL Configuration d’une nouvelle destination]** pour déclencher la variable [Se connecter à la destination](/help/destinations/ui/connect-destination.md) workflow et [sélection des comptes comme type de données](/help/destinations/ui/connect-destination.md#segment-activation-or-dataset-exports).

![Workflow d’activation de la destination avec le contrôle des comptes en surbrillance.](/help/destinations/assets/ui/activate-account-audiences/activate-account-audiences-highlighted.png)

1. Passez à la section suivante pour [sélectionner les audiences de votre compte ;](#select-profile-audiences) pour l’exportation.

## Sélectionner les audiences de votre compte {#select-account-audiences}

Utilisez les cases à cocher situées à gauche des noms des audiences du compte pour sélectionner les audiences que vous souhaitez exporter vers la destination, puis sélectionnez **[!UICONTROL Suivant]**. Notez que *audiences de compte* s’affichent dans cette vue et aucun autre type d’audience ne s’affiche.

![Le workflow d’exportation des jeux de données affiche l’étape Sélectionner les audiences dans laquelle vous pouvez sélectionner les audiences de compte à exporter.](/help/destinations/assets/ui/activate-account-audiences/select-account-audiences.png)

## Planification et étapes suivantes

Pour le reste du workflow d’activation permettant d’exporter les audiences de compte, lisez le tutoriel sur l’activation des données vers des destinations basées sur des fichiers. Continuez à partir du [étape planifier l’exportation de l’audience](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling). Si vous activez les audiences du compte dans la variable **[!UICONTROL (Sociétés) Audiences mappées LinkedIn]** destination, lisez le tutoriel sur l’activation des destinations de diffusion en continu. Continuez à partir du [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

>[!NOTE]
>
>Notez que, à l’étape de planification de l’exportation des audiences de compte vers des destinations de stockage dans le cloud, le workflow d’activation des audiences de compte vous permet uniquement d’exporter les audiences de compte. [fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) _selon une planification quotidienne_. Les exportations horaires ne sont pas prises en charge. Notez également que **[!UICONTROL Après l’évaluation de l’audience]** est le seul type d’évaluation pris en charge.

## Légendes importantes et limites connues {#important-callouts-known-limitations}

Notez les légendes importantes et les limites connues suivantes pour la mise à jour générale de la fonctionnalité d’activation des audiences de compte.

### Paires de mappage requises à l’étape de mappage lors de l’activation des audiences de compte vers le **[!UICONTROL (Sociétés) Audiences mappées LinkedIn]** destination {#required-mappings}

Lors de l’activation des audiences de compte dans la variable **[!UICONTROL (Sociétés) Audiences mappées LinkedIn]** destination, notez que les deux paires de mappage suivantes sont obligatoires pour exporter les données avec succès :

![Mappage linkedIn des champs obligatoires.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Champ source | Champ cible |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (sélectionnez ce champ dans la **[!UICONTROL Sélectionner un espace de noms d’identité]** lors de la sélection de l’option **[!UICONTROL Champ cible]**). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations."){width="100" zoomable="yes"} |

### Application de la gouvernance des données {#data-governance-enforcement}

Le consentement est appliqué au niveau de la personne ou du profil pour *audiences de clients et de prospects*. Par conséquent,  [évaluation des stratégies de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) n’est actuellement pas pris en charge lors de l’activation des audiences de compte vers les destinations. Dans l’étape de révision du workflow d’activation, vous pouvez voir un contrôle hors zone grisé pour **[!UICONTROL Affichage des stratégies de consentement applicables]**.

![Consultez l’étape du workflow d’activation des audiences de compte avec le contrôle d’application du consentement grisé.](/help/destinations/assets/ui/activate-account-audiences/consent-checks-greyed-out.png)

Autres mécanismes de gouvernance des données dans Real-Time CDP, tels que [vérifications de la stratégie d’utilisation des données](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) et [contrôle d’accès basé sur les attributs](/help/destinations/home.md#attribute-based-access) sont prises en charge.
