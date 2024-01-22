---
title: (Version bêta) Le bureau de commerce - connexion CRM
description: Activez les profils dans votre compte de bureau Commerce pour le ciblage et la suppression des audiences en fonction des données CRM.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 18%

---

# (Version Bêta) Le [!DNL Trade Desk] - Connexion CRM

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] destination dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.
>
>Avec la publication de l’EUID (European Unified ID), deux destinations [!DNL The Trade Desk - CRM] dans le [catalogue de destinations](/help/destinations/catalog/overview.md) sont maintenant affichées.
>* Si vos données proviennent de l’UE, utilisez la destination **[!DNL The Trade Desk - CRM (EU)]**.
>* Si vos données proviennent des régions APAC ou NAMER, utilisez la destination **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Les deux destinations en Experience Platform sont actuellement en version bêta. Cette page de documentation et de connecteur de destination est créée et conservée par *[!DNL Trade Desk]* l&#39;équipe. Pour toute question ou demande de mise à jour, veuillez contacter votre [!DNL Trade Desk] représentative, la documentation et la fonctionnalité peuvent faire l’objet de modifications.

## Vue d’ensemble {#overview}

Ce document est conçu pour vous aider à activer les profils dans votre [!DNL Trade Desk] compte pour le ciblage et la suppression des audiences en fonction des données CRM.

[!DNL The Trade Desk(TTD)] ne gère pas directement le fichier de téléchargement des adresses électroniques à un moment donné et ne gère pas [!DNL The Trade Desk] stockez vos emails bruts (non hachés).

>[!TIP]
>
>Utilisation [!DNL The Trade Desk] Destinations CRM pour le mappage des données CRM, telles que les adresses électroniques hachées ou de messagerie électronique. Utilisez la variable [autre destination de bureau commercial](/help/destinations/catalog/advertising/tradedesk.md) dans le catalogue Adobe Experience Platform pour les cookies et les mappages des identifiants d’appareil.

## Conditions préalables {#prerequisites}

Avant d’activer des audiences vers [!DNL The Trade Desk], vous devez contacter [!DNL The Trade Desk] gestionnaire de compte pour signer le contrat d’intégration CRM. [!DNL The Trade Desk] donnera ensuite l’autorisation et partagera votre identifiant publicitaire pour configurer votre destination.

## Exigences de correspondance des identifiants {#id-matching-requirements}

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes. Veuillez lire la [Présentation d’Identity Namespace](/help/identity-service/namespaces.md) pour plus d’informations.

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section Exigences de correspondance des identifiants et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement.

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresses électroniques (texte en clair) | Entrée `email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut Email. |
| Email_LC_SHA256 | Les adresses électroniques doivent être hachées à l’aide de SHA256 et mises en minuscules. Vous ne pourrez pas modifier ce paramètre ultérieurement. | Entrée `hashed_email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut Email_LC_SHA256. |

{style="table-layout:auto"}

## Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser des adresses électroniques brutes.

Pour en savoir plus sur l’ingestion d’adresses électroniques en Experience Platform, lisez le [Présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Supprimer les espaces de début et de fin.
* Convertissez tous les caractères ASCII en minuscules.
* Dans `gmail.com` Supprimez les caractères suivants de la partie nom d’utilisateur de l’adresse électronique :
   * Le point (. (Code ASCII 46). Par exemple, normaliser `jane.doe@gmail.com` to `janedoe@gmail.com`.
   * Le signe plus (+ (code ASCII 43)) et tous les caractères suivants. Par exemple, normaliser `janedoe+home@gmail.com` to `janedoe@gmail.com`.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (email ou email haché) utilisés dans la destination du bureau de commerce. |
| Fréquence des exportations | **[!UICONTROL Lot quotidien]** | Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le profil (identités) est mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur [exports par lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

### Authentification à la destination {#authenticate}

[!DNL The Trade Desk] La destination CRM est un chargement de fichier par lots quotidien qui ne nécessite pas d’authentification de l’utilisateur.

### Renseignement des détails de destination {#fill-in-details}

Avant de pouvoir envoyer ou activer des données d’audience vers une destination, vous devez configurer une connexion à votre propre plateforme de destination. Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Type de compte]**: choisissez la variable **[!UICONTROL Compte existant]** .
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant publicitaire]**: votre [!DNL Trade Desk Advertiser ID], qui peut être partagé par votre [!DNL Trade Desk] Gestionnaire de compte ou sous [!DNL Advertiser Preferences] dans le [!DNL Trade Desk] Interface utilisateur.

![Capture d’écran de l’interface utilisateur de Platform montrant comment remplir les détails de destination.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Lors de la connexion à la destination, la définition d’une stratégie de gouvernance des données est complètement facultative. Veuillez consulter l’Experience Platform [présentation de la gouvernance des données](/help/data-governance/policies/overview.md) pour plus d’informations.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lecture [Activation des données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers une destination.

Dans le **[!UICONTROL Planification]** , vous pouvez configurer le planning et les noms des fichiers pour chaque audience que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

![Copie d’écran de l’interface utilisateur de Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Toutes les audiences activées [!DNL The Trade Desk] Les destinations CRM sont automatiquement définies sur une fréquence quotidienne et une exportation de fichiers complète.

![Copie d’écran de l’interface utilisateur de Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Dans le **[!UICONTROL Mappage]** , vous devez sélectionner des attributs ou des espaces de noms d’identité dans la colonne source et les mapper à la colonne cible.

![Copie d’écran de l’interface utilisateur de Platform pour mapper l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation d’audiences vers [!DNL The Trade Desk] Destination CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] La destination CRM n’accepte pas les adresses électroniques brutes et hachées comme identités dans le même flux d’activation. Créez des flux d’activation distincts pour les adresses électroniques brutes et hachées.

Sélection des champs sources :

* Sélectionnez la variable `Email` espace de noms ou attribut comme identité source si vous utilisez l’adresse électronique brute lors de l’ingestion des données.
* Sélectionnez la variable `Email_LC_SHA256` espace de noms ou attribut comme identité source si vous avez haché des adresses électroniques client lors de l’ingestion de données dans Platform.

Sélection des champs cibles :

* Entrée  `email` comme identité cible lorsque votre espace de noms ou votre attribut source est `Email`.
* Entrée  `hashed_email` comme identité cible lorsque votre espace de noms ou votre attribut source est `Email_LC_SHA256`.

## Validation de l’exportation des données {#validate}

Pour vérifier que les données sont correctement exportées depuis l’Experience Platform et vers [!DNL The Trade Desk], recherchez les audiences sous la mosaïque de données Adobe 1PD dans [!DNL The Trade Desk] Data Management Platform (DMP). Vous trouverez ci-dessous les étapes à suivre pour trouver l’identifiant correspondant dans la variable [!DNL Trade Desk] Interface utilisateur :

1. Tout d’abord, cliquez sur le **[!UICONTROL Données]** Onglet et révision **[!UICONTROL Premier niveau]**.
2. Faites défiler la page vers le bas, sous **[!UICONTROL Données importées]**, vous trouverez la variable **[!UICONTROL Mosaïque Adobe 1PD]**.
3. Cliquez sur le lien**[!UICONTROL Adobe 1PD]** et répertorie toutes les audiences activées sur la page [!DNL Trade Desk] destination de votre annonceur. Vous pouvez également utiliser la fonction de recherche.
4. Le numéro d’ID de segment de l’Experience Platform apparaît comme nom de segment dans la variable [!DNL Trade Desk] Interface utilisateur.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
