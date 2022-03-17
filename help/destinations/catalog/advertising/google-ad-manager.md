---
keywords: gestionnaire de publicités Google;publicité Google;double-clic;DoubleClick AdX;DoubleClick;Google Ad Manager;gestionnaire de publicités Google; DFP
title: Connexion à Google Ad Manager
description: Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 23%

---

# [!DNL Google Ad Manager] connection

## Présentation {#overview}

[!DNL Google Ad Manager], anciennement connu sous le nom de [!DNL DoubleClick for Publishers] (DFP) ou [!DNL DoubleClick AdX], est une plateforme de service publicitaire de [!DNL Google] qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques à [!DNL Google Ad Manager] destinations :

* Les audiences activées sont créées par programmation dans le [!DNL Google] plateforme.
* [!DNL Platform] n’inclut pas actuellement de mesure pour valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

## Identités prises en charge {#supported-identities}

[!DNL Google Ad Manager] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), également appelé [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par l’Audience Manager à chaque appareil avec lequel elle interagit. | Utilisation de Google [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) pour cibler les utilisateurs en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utilise cet identifiant pour cibler les utilisateurs situés en dehors de la Californie. |
| RIDA | Identifiant Roku pour la publicité. Cet identifiant identifie de manière unique les appareils Roku. |  |
| MAID | Microsoft Advertising ID. Cet identifiant identifie de manière unique les périphériques exécutant Windows 10. |  |
| Identifiant Amazon Fire TV | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d&#39;export | **[!UICONTROL Exportation des segments]** | Vous exportez tous les membres d’un segment (audience) vers la destination Google. |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Conditions préalables {#prerequisites}

Si vous souhaitez créer votre première destination avec [!DNL Google Ad Manager] et n’ont pas activé la variable [Fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez déjà configuré [!DNL Google] intégrations dans Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à Platform.

### Liste autorisée {#allow-listing}

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première [!DNL Google Ad Manager] destination dans Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.

Avant de créer la variable [!DNL Google Ad Manager] destination dans Platform, vous devez contacter [!DNL Google] pour que l’Adobe soit placé sur la liste des fournisseurs de données autorisés et pour que votre compte soit ajouté à la liste autorisée. Contact [!DNL Google] et fournissez les informations suivantes :

* **Identifiant de compte**: Identifiant de compte de l’Adobe avec Google. ID de compte : 87933855.
* **ID de client**: Identifiant du compte client de l’Adobe avec Google. ID de client : 89690775.
* **Identifiant réseau** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* **Identifiant du lien d’audience** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* Votre type de compte. DFP de Google ou AdX buyer.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `DFP by Google` pour for Publishers[!DNL DoubleClick]
   * Utilisation `AdX buyer` pour [!DNL Google AdX]
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google]. Il peut s’agir de votre identifiant réseau ou de votre identifiant du lien d’audience. En règle générale, il s’agit d’un identifiant à huit chiffres.

>[!NOTE]
>
>Lors de la configuration d’une [!DNL Google Ad Manager] destination, veuillez travailler avec votre [!DNL Google Account Manager] ou représentant de l’Adobe pour déterminer le type de compte dont vous disposez.

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers des destinations d’exportation de segments par flux](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Pour vérifier si les données ont bien été exportées vers la variable [!DNL Google Ad Manager] destination, vérifiez votre [!DNL Google Ad Manager] compte . Si l’activation a réussi, les audiences sont renseignées dans votre compte.
