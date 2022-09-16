---
title: (Version bêta) Bureau commercial - Connexion CRM
description: Activez les profils dans votre compte de bureau Commerce pour le ciblage et la suppression des audiences en fonction des données CRM.
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: a761ab634dce31bd0a06297f703d9d815c2f0ea2
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 11%

---

# (Beta) Connexion CRM The[!DNL Trade Desk]

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] destination dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

>[!IMPORTANT]
>
> Cette page de documentation a été créée par la fonction *[!DNL Trade Desk]* l&#39;équipe. Pour toute question ou demande de mise à jour, veuillez contacter votre [!DNL Trade Desk] représentant.

Ce document est conçu pour vous aider à activer les profils dans votre [!DNL Trade Desk] compte pour le ciblage et la suppression des audiences en fonction des données CRM.

>[!TIP]
>
>Utilisation [!DNL The Trade Desk] Destination CRM pour le mappage des données CRM, comme une adresse email ou une adresse email hachée. Utilisez la variable [autre destination de bureau commercial](/help/destinations/catalog/advertising/tradedesk.md) dans le catalogue Adobe Experience Platform pour les cookies et les mappages des identifiants d’appareil.

[!DNL The Trade Desk] (TTD) ne gère pas directement le fichier de téléchargement des adresses électroniques à un moment donné et ne gère pas [!DNL The Trade Desk] stockez vos emails bruts (non hachés).

## Conditions préalables {#prerequisites}

Avant d’activer des segments dans [!DNL The Trade Desk], vous devez contacter votre [!DNL The Trade Desk] gestionnaire de compte pour signer le contrat d’intégration CRM. [!DNL The Trade Desk] donnera ensuite l’autorisation et partagera votre identifiant publicitaire pour configurer votre destination.

## Exigences de correspondance des identifiants {#id-matching-requirements}

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes. Veuillez lire la [Présentation d’Identity Namespace](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr) pour plus d’informations.

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

Adobe Experience Platform prend en charge le texte brut et les adresses électroniques hachées SHA256. Suivez les instructions de la section Exigences de correspondance des identifiants et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement.

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresses électroniques (texte en clair) | Sélectionnez la `Email` identité cible lorsque votre identité source est un espace de noms ou un attribut de courriel. |
| Email_LC_SHA256 | Les adresses électroniques doivent être hachées à l’aide de SHA256 et mises en minuscules. Veillez à suivre les [normalisation des emails](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) règles requises. Vous ne pourrez pas modifier ce paramètre ultérieurement. | Sélectionnez la `Email_LC_SHA256` identité cible lorsque votre identité source est un espace de noms ou un attribut Email_LC_SHA256. |

{style=&quot;table-layout:auto&quot;}

## Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser des adresses électroniques brutes.

Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, voir [Présentation de l’ingestion par lots](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=en).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Supprimez les espaces de début et de fin.
* Convertissez tous les caractères ASCII en minuscules.
* Dans `gmail.com` Supprimez les caractères suivants de la partie nom d’utilisateur de l’adresse électronique :
   * Le point (. (Code ASCII 46). Par exemple, normaliser `jane.doe@gmail.com` to `janedoe@gmail.com`.
   * Le signe plus (+ (code ASCII 43)) et tous les caractères suivants. Par exemple, normaliser `janedoe+home@gmail.com` to `janedoe@gmail.com`.

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) avec les identifiants (email ou email haché) utilisés dans la destination du bureau de commerce. |
| Fréquence des exports | **[!UICONTROL Lot quotidien]** | Comme un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le profil (identités) est mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur [téléchargements par lots](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

### Authentification à la destination {#authenticate}

[!DNL The Trade Desk] La destination CRM est un chargement de fichier par lots quotidien qui ne nécessite pas d’authentification de l’utilisateur.

### Renseignement des détails de destination {#fill-in-details}

Avant de pouvoir envoyer ou activer des données d’audience vers une destination, vous devez configurer une connexion à votre propre plateforme de destination. Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Type de compte]**: Veuillez choisir la **[!UICONTROL Compte existant]** .
* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL Identifiant publicitaire]**: your [!DNL Trade Desk Advertiser ID], qui peut être partagé par votre [!DNL Trade Desk] Gestionnaire de compte ou sous [!DNL Advertiser Preferences] dans le [!DNL Trade Desk] Interface utilisateur.

Lors de la connexion à la destination, la définition d’une stratégie de gouvernance des données est complètement facultative. Veuillez consulter l’Experience Platform [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) pour plus d’informations.

## Activer des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de profils par lots](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=fr) pour obtenir des instructions sur l’activation des segments d’audience vers une destination.

Sur la page **[!UICONTROL Planification]**, vous pouvez configurer le planning et les noms des fichiers pour chaque segment que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

>[!NOTE]
>
>Tous les segments activés dans [!DNL The Trade Desk] Les destinations CRM sont automatiquement définies sur une fréquence quotidienne et une exportation de fichiers complète.

Dans le **[!UICONTROL Mappage]** , vous devez sélectionner des attributs ou des espaces de noms d’identité dans la colonne source et les mapper à la colonne cible.

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation de segments vers [!DNL The Trade Desk] Destination CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] La destination CRM n’accepte pas les adresses électroniques brutes et hachées comme identités dans le même flux d’activation. Créez des flux d’activation distincts pour les adresses électroniques brutes et hachées.

Sélection des champs sources :

* Sélectionnez la `Email` espace de noms ou attribut comme identité source si vous utilisez l’adresse électronique brute lors de l’ingestion des données.
* Sélectionnez la `Email_LC_SHA256` espace de noms ou attribut comme identité source si vous avez haché des adresses électroniques client lors de l’ingestion de données dans Platform.

Sélection des champs cibles :

* Sélectionnez la `Email` espace de noms comme identité cible lorsque votre espace de noms ou votre attribut source est `Email`.
* Sélectionnez la `Email_LC_SHA256` espace de noms comme identité cible lorsque votre espace de noms ou votre attribut source est `Email_LC_SHA256`.

## Validation de l’exportation des données {#validate}

Pour vérifier que les données sont correctement exportées depuis l’Experience Platform et vers [!DNL The Trade Desk], recherchez les segments sous la mosaïque de données Adobe 1PD dans [!DNL The Trade Desk] Plateforme de gestion des données (DMP). Vous trouverez ci-dessous les étapes à suivre pour trouver l’identifiant correspondant dans la variable [!DNL Trade Desk] Interface utilisateur :

1. Tout d’abord, cliquez sur le **[!UICONTROL Données]** Onglet et révision **[!UICONTROL Premier niveau]**.
2. Faites défiler la page vers le bas, sous **[!UICONTROL Données importées]**, vous trouverez la variable **[!UICONTROL Mosaïque Adobe 1PD]**.
3. Cliquez sur le lien**[!UICONTROL Adobe 1PD]** et répertorie tous les segments activés dans la [!DNL Trade Desk] destination de votre annonceur. Vous pouvez également utiliser la fonction de recherche.
4. Le numéro d’ID de segment de l’Experience Platform apparaît comme nom de segment dans la variable [!DNL Trade Desk] Interface utilisateur.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).
