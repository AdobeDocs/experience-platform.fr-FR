---
title: Connexion CRM The Trade Desk
description: Activez les profils sur votre compte Trade Desk pour le ciblage et la suppression d'audiences en fonction des données CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 17%

---

# La connexion [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Avec la publication de l’EUID (European Unified ID), deux destinations [!DNL The Trade Desk - CRM] dans le [catalogue de destinations](/help/destinations/catalog/overview.md) sont maintenant affichées.
>* Si vos données proviennent de l’UE, utilisez la destination **[!DNL The Trade Desk - CRM (EU)]**.
>* Si vos données proviennent des régions APAC ou NAMER, utilisez la destination **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe *[!DNL Trade Desk]*. Pour toute demande ou information, veuillez contacter votre représentant [!DNL Trade Desk].

## Vue d’ensemble {#overview}

Découvrez comment activer des profils sur votre compte [!DNL Trade Desk] pour le ciblage et la suppression d’audiences en fonction des données CRM.

Ce connecteur envoie des données au point d’entrée propriétaire [!DNL The Trade Desk]. L’intégration entre Adobe Experience Platform et [!DNL The Trade Desk] ne prend pas en charge l’exportation de données vers le point d’entrée tiers [!DNL The Trade Desk].

[!DNL The Trade Desk(TTD)] ne gère à aucun moment directement le fichier de chargement des adresses e-mail et ne stocke [!DNL The Trade Desk] vos e-mails bruts (non hachés).

>[!TIP]
>
>Utilisez des destinations CRM [!DNL The Trade Desk] pour le mappage des données CRM, telles que l’adresse e-mail ou l’adresse e-mail hachée. Utilisez la [autre destination Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) dans le catalogue Adobe Experience Platform pour les cookies et les mappages d’ID d’appareil.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>Avant de pouvoir activer des audiences dans The Trade Desk, vous devez contacter votre gestionnaire de compte [!DNL Trade Desk] pour signer le contrat d’intégration CRM. [!DNL The Trade Desk] autorisera l’utilisation d’UID2/EUID et partagera d’autres détails pour vous aider à configurer la destination.

## Exigences de correspondance des identifiants {#id-matching-requirements}

Selon le type d’identifiants ingérés dans Adobe Experience Platform, vous devez respecter les exigences correspondantes. Pour plus d’informations, consultez la [présentation de l’espace de noms d’identité](/help/identity-service/features/namespaces.md).

## Identités prises en charge {#supported-identities}

[!DNL The Trade Desk] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Suivez les instructions de la section Exigences de correspondance des identifiants et utilisez les espaces de noms appropriés pour le texte brut et les adresses électroniques hachées, respectivement.

| Identité cible | Description | Considérations |
|---|---|---|
| E-mail | Adresses e-mail (texte clair) | Saisissez `email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut d’e-mail. |
| Email_LC_SHA256 | Les adresses e-mail doivent être hachées à l’aide de SHA256 et en minuscules. Vous ne pourrez pas modifier ce paramètre ultérieurement. | Saisissez `hashed_email` comme identité cible lorsque votre identité source est un espace de noms ou un attribut Email_LC_SHA256. |

{style="table-layout:auto"}

## Exigences en matière de hachage des e-mails {#hashing-requirements}

Vous pouvez hacher les adresses e-mail avant de les ingérer dans Adobe Experience Platform ou utiliser des adresses e-mail brutes.

Pour en savoir plus sur l’ingestion d’adresses e-mail dans Experience Platform, consultez la [présentation de l’ingestion par lots](/help/ingestion/batch-ingestion/overview.md).

Si vous choisissez de hacher les adresses e-mail vous-même, veillez à respecter les exigences suivantes :

* Supprimez les espaces de début et de fin.
* Convertissez tous les caractères ASCII en minuscules.
* Dans `gmail.com` adresses e-mail, supprimez les caractères suivants de la partie nom d’utilisateur de l’adresse e-mail :
   * La période (. (Code ASCII 46). Par exemple, normalisez `jane.doe@gmail.com` sur `janedoe@gmail.com`.
   * Le signe plus (+ (code ASCII 43)) et tous les caractères suivants. Par exemple, normalisez `janedoe+home@gmail.com` sur `janedoe@gmail.com`.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (e-mail ou e-mail haché) utilisés dans la destination Trade Desk. |
| Fréquence des exportations | **[!UICONTROL Lot quotidien]** | Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le profil (les identités) est mis à jour une fois par jour en aval de la plateforme de destination. En savoir plus sur les [ exportations par lots ](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

### Authentification à la destination {#authenticate}

[!DNL The Trade Desk] destination CRM est un chargement quotidien de fichiers par lots qui ne nécessite pas d’authentification de l’utilisateur.

### Renseigner les détails de la destination {#fill-in-details}

Avant de pouvoir envoyer ou activer des données d’audience vers une destination, vous devez configurer une connexion à votre propre plateforme de destination. Pendant la [configuration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) de cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Type de compte]** : veuillez choisir l’option **[!UICONTROL Compte existant]**.
* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID publicitaire]** : votre [!DNL Trade Desk Advertiser ID], qui peut être partagé par votre gestionnaire de compte [!DNL Trade Desk] ou qui se trouve sous [!DNL Advertiser Preferences] dans l’interface utilisateur de [!DNL Trade Desk].

![Capture d’écran de l’interface utilisateur d’Experience Platform montrant comment remplir les détails de destination.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Lors de la connexion à la destination , la définition d’une politique de gouvernance des données est complètement facultative. Veuillez consulter la présentation de la gouvernance des données [Experience Platform](/help/data-governance/policies/overview.md) pour plus d’informations.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les données d’audience vers des destinations d’exportation de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers une destination.

Sur la page **[!UICONTROL Planification]**, vous pouvez configurer le planning et les noms des fichiers pour chaque audience que vous exportez. La configuration du planning est obligatoire, mais la configuration du nom de fichier est facultative.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Toutes les audiences activées vers [!DNL The Trade Desk] destination CRM sont automatiquement définies sur une fréquence quotidienne et une exportation de fichiers complets.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour planifier l’activation de l’audience.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Sur la page **[!UICONTROL Mappage]**, vous devez sélectionner des attributs ou des espaces de noms d’identité dans la colonne source et les mapper à la colonne cible.

![Capture d’écran de l’interface utilisateur d’Experience Platform pour mapper l’activation des audiences.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’activation d’audiences vers [!DNL The Trade Desk] destination CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] destination CRM n’accepte pas les adresses e-mail brutes et hachées en tant qu’identités dans le même flux d’activation. Créez des flux d’activation distincts pour les adresses e-mail brutes et hachées.

Sélection des champs sources :

* Sélectionnez l’espace de noms ou l’attribut `Email` comme identité source si vous utilisez l’adresse e-mail brute lors de l’ingestion des données.
* Sélectionnez l’espace de noms ou l’attribut `Email_LC_SHA256` comme identité source si vous avez haché les adresses e-mail des clients lors de l’ingestion des données dans Experience Platform.

Sélection des champs cibles :

* `email` d’entrée comme identité cible lorsque l’espace de noms ou l’attribut source est `Email`.
* `hashed_email` d’entrée comme identité cible lorsque l’espace de noms ou l’attribut source est `Email_LC_SHA256`.

## Valider l’exportation des données {#validate}

Pour vérifier que les données sont correctement exportées hors d’Experience Platform et vers [!DNL The Trade Desk], recherchez les audiences sous la mosaïque de données Adobe 1PD dans [!DNL The Trade Desk] Data Management Platform (DMP). Pour trouver l’identifiant correspondant dans l’interface utilisateur de [!DNL Trade Desk], procédez comme suit :

1. Sélectionnez tout d’abord l’onglet **[!UICONTROL Données]**, puis passez en revue la section **[!UICONTROL Propriétaire]**.
2. Faites défiler la page vers le bas, sous **[!UICONTROL Données importées]**, vous trouverez la **[!UICONTROL vignette Adobe 1PD]**.
3. Cliquez sur la mosaïque **[!UICONTROL Adobe 1PD]** pour répertorier toutes les audiences activées vers la destination [!DNL Trade Desk] pour votre annonceur. Vous pouvez également utiliser la fonction de recherche.
4. L’identifiant de segment n° d’Experience Platform s’affiche en tant que nom de segment dans l’interface utilisateur de [!DNL Trade Desk].

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
