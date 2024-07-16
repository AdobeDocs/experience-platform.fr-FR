---
title: (Beta) Le bureau commercial - connexion CRM
description: Activez les profils dans votre compte de bureau Commerce pour le ciblage et la suppression des audiences en fonction des données CRM.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 18%

---

# (Beta) [!DNL Trade Desk] - Connexion CRM

>[!IMPORTANT]
>
>La destination [!DNL The Trade Desk - CRM] de Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.
>
>Avec la publication de l’EUID (European Unified ID), deux destinations [!DNL The Trade Desk - CRM] dans le [catalogue de destinations](/help/destinations/catalog/overview.md) sont maintenant affichées.
>* Si vos données proviennent de l’UE, utilisez la destination **[!DNL The Trade Desk - CRM (EU)]**.
>* Si vos données proviennent des régions APAC ou NAMER, utilisez la destination **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Les deux destinations en Experience Platform sont actuellement en version bêta. Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *[!DNL Trade Desk]*. Pour toute question ou demande de mise à jour, contactez votre représentant [!DNL Trade Desk]. La documentation et les fonctionnalités peuvent être modifiées.

## Vue d’ensemble {#overview}

Ce document est conçu pour vous aider à activer les profils sur votre compte [!DNL Trade Desk] pour le ciblage et la suppression des audiences en fonction des données CRM.

[!DNL The Trade Desk(TTD)] ne gère pas directement le fichier de téléchargement des adresses électroniques à tout moment et [!DNL The Trade Desk] ne stocke pas vos adresses électroniques brutes (non hachées).

>[!TIP]
>
>Utilisez les destinations de gestion de la relation client [!DNL The Trade Desk] pour le mappage des données de gestion de la relation client, telles que les adresses électroniques ou hachées. Utilisez la [autre destination de bureau commercial](/help/destinations/catalog/advertising/tradedesk.md) du catalogue Adobe Experience Platform pour les cookies et les mappages d’identifiants d’appareil.

## Conditions préalables {#prerequisites}

Avant de pouvoir activer les audiences vers [!DNL The Trade Desk], vous devez contacter votre gestionnaire de compte [!DNL The Trade Desk] pour signer le contrat d’intégration CRM. [!DNL The Trade Desk] donnera alors l’autorisation et partagera votre identifiant publicitaire pour configurer votre destination.

## Exigences de correspondance des identifiants {#id-matching-requirements}

Selon le type d’ID que vous ingérez dans Adobe Experience Platform, vous devez respecter les exigences correspondantes. Pour plus d’informations, consultez la [présentation de l’espace de noms d’identité](/help/identity-service/features/namespaces.md) .

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section Exigences de correspondance des identifiants et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement.

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresses électroniques (texte en clair) | Saisissez `email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut Email. |
| Email_LC_SHA256 | Les adresses électroniques doivent être hachées à l’aide de SHA256 et mises en minuscules. Vous ne pourrez pas modifier ce paramètre ultérieurement. | Saisissez `hashed_email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut Email_LC_SHA256. |

{style="table-layout:auto"}

## Exigences en matière de hachage des emails {#hashing-requirements}

Vous pouvez hacher des adresses électroniques avant de les ingérer dans Adobe Experience Platform ou utiliser des adresses électroniques brutes.

Pour en savoir plus sur l’ingestion d’adresses électroniques dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md).

Si vous choisissez de hacher vous-même les adresses électroniques, veillez à respecter les exigences suivantes :

* Supprimer les espaces de début et de fin.
* Convertissez tous les caractères ASCII en minuscules.
* Dans les adresses électroniques `gmail.com`, supprimez les caractères suivants de la partie nom d’utilisateur de l’adresse électronique :
   * Le point (. (Code ASCII 46). Par exemple, normalisez `jane.doe@gmail.com` sur `janedoe@gmail.com`.
   * Le signe plus (+ (code ASCII 43)) et tous les caractères suivants. Par exemple, normalisez `janedoe+home@gmail.com` sur `janedoe@gmail.com`.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (email ou email haché) utilisés dans la destination du bureau de commerce. |
| Fréquence des exportations | **[!UICONTROL Lot quotidien]** | Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le profil (identités) est mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur les [exportations de lots](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

### Authentification à la destination {#authenticate}

[!DNL The Trade Desk] La destination CRM est un chargement de fichier par lots quotidien qui ne nécessite pas d’authentification de l’utilisateur.

### Renseignement des détails de destination {#fill-in-details}

Avant de pouvoir envoyer ou activer des données d’audience vers une destination, vous devez configurer une connexion à votre propre plateforme de destination. Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Type de compte]** : sélectionnez l’option **[!UICONTROL Compte existant]** .
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant publicitaire]** : votre [!DNL Trade Desk Advertiser ID], qui peut être partagé par votre gestionnaire de compte [!DNL Trade Desk] ou se trouver sous [!DNL Advertiser Preferences] dans l’interface utilisateur [!DNL Trade Desk].

![Copie d’écran de l’interface utilisateur de Platform montrant comment remplir les détails de destination.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Lors de la connexion à la destination, la définition d’une stratégie de gouvernance des données est complètement facultative. Pour plus d’informations, consultez la [présentation de la gouvernance des données](/help/data-governance/policies/overview.md) de l’Experience Platform.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez la section [Activation des données d’audience vers des destinations d’exportation de profil de lot](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers une destination.

Sur la page **[!UICONTROL Planification]** , vous pouvez configurer le planning et les noms des fichiers pour chaque audience que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

![Copie d’écran de l’interface utilisateur de Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Toutes les audiences activées vers la destination CRM [!DNL The Trade Desk] sont automatiquement définies sur une fréquence quotidienne et une exportation de fichiers complète.

![Copie d’écran de l’interface utilisateur de Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Dans la page **[!UICONTROL Mapping]**, vous devez sélectionner des attributs ou des espaces de noms d’identité à partir de la colonne source et les mapper à la colonne cible.

![Copie d’écran de l’interface utilisateur de Platform pour mapper l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation d’audiences vers la destination CRM [!DNL The Trade Desk].

>[!IMPORTANT]
>
> [!DNL The Trade Desk] La destination CRM n’accepte pas les adresses électroniques brutes et hachées comme identités dans le même flux d’activation. Créez des flux d’activation distincts pour les adresses électroniques brutes et hachées.

Sélection des champs sources :

* Sélectionnez l’espace de noms ou l’attribut `Email` comme identité source si vous utilisez l’adresse électronique brute lors de l’ingestion des données.
* Sélectionnez l’espace de noms ou l’attribut `Email_LC_SHA256` comme identité source si vous avez haché les adresses électroniques du client lors de l’ingestion des données dans Platform.

Sélection des champs cibles :

* Saisissez `email` comme identité cible lorsque votre espace de noms ou votre attribut source est `Email`.
* Saisissez `hashed_email` comme identité cible lorsque votre espace de noms ou votre attribut source est `Email_LC_SHA256`.

## Validation de l’exportation des données {#validate}

Pour vérifier que les données sont correctement exportées depuis l’Experience Platform vers [!DNL The Trade Desk], recherchez les audiences sous la mosaïque de données 1PD d’Adobe dans [!DNL The Trade Desk] Data Management Platform (DMP). Voici les étapes pour trouver l’ID correspondant dans l’interface utilisateur de [!DNL Trade Desk] :

1. Cliquez d’abord sur l’onglet **[!UICONTROL Data]** et passez en revue **[!UICONTROL First-Party]**.
2. Faites défiler la page vers le bas, sous **[!UICONTROL Données importées]**, vous trouverez la **[!UICONTROL mosaïque Adobe 1PD]**.
3. Cliquez sur la mosaïque **[!UICONTROL Adobe 1PD]** et répertorie toutes les audiences activées vers la destination [!DNL Trade Desk] de votre annonceur. Vous pouvez également utiliser la fonction de recherche.
4. Le numéro d’ID de segment de l’Experience Platform apparaîtra comme nom de segment dans l’interface utilisateur de [!DNL Trade Desk].

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
