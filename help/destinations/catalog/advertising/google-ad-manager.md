---
keywords: gestionnaire de publicités Google;publicité Google;double-eclick;DoubleClick AdX;DoubleClick;Google Ad Manager;gestionnaire de publicités Google; DFP
title: Connexion à Google Ad Manager
description: Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 23%

---

# [!DNL Google Ad Manager] connection

## Présentation {#overview}

[!DNL Google Ad Manager], anciennement  [!DNL DoubleClick for Publishers] (DFP) ou  [!DNL DoubleClick AdX], est une plateforme de service publicitaire issue de  [!DNL Google] laquelle permet aux éditeurs de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Ad Manager] :

* Les audiences activées sont créées par programmation dans la plateforme [!DNL Google].
* [!DNL Platform] n’inclut pas actuellement de mesure pour valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

## Identités prises en charge {#supported-identities}

[!DNL Google Ad Manager] prend en charge l’activation des identités décrites dans le tableau ci-dessous.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), également appelé  [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par l’Audience Manager à chaque appareil avec lequel elle interagit. | Google utilise [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) pour cibler les utilisateurs en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| [!DNL Google] ID de cookie | [!DNL Google] ID de cookie | [!DNL Google] utilise cet identifiant pour cibler les utilisateurs situés en dehors de la Californie. |
| RIDA | Identifiant Roku pour la publicité. Cet identifiant identifie de manière unique les appareils Roku. |  |
| MAID | Identifiant Microsoft Advertising. Cet identifiant identifie de manière unique les périphériques exécutant Windows 10. |  |
| Identifiant Amazon Fire TV | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

## Type d&#39;export {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) vers la destination Google.

## Conditions préalables

Si vous souhaitez créer votre première destination avec [!DNL Google Ad Manager] et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’ID Experience Cloud par le passé (avec Audience Manager ou d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer la synchronisation des identifiants. Si vous avez précédemment configuré des intégrations [!DNL Google] dans Audience Manager, les synchronisations des identifiants que vous avez configurées sont transférées vers Platform.

## Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ad Manager] dans Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.

Avant de créer la destination [!DNL Google Ad Manager] dans Platform, vous devez contacter [!DNL Google] pour que l’Adobe soit placé sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez [!DNL Google] et fournissez les informations suivantes :

* **ID** du compte : Identifiant de compte de l’Adobe avec Google. ID de compte : 87933855.
* **ID de client** : Identifiant du compte client de l’Adobe avec Google. ID de client : 89690775.
* **Identifiant réseau** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* **Identifiant du lien d’audience** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* Votre type de compte. DFP de Google ou AdX buyer.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `DFP by Google` pour for Publishers[!DNL DoubleClick]
   * Utilisez `AdX buyer` pour [!DNL Google AdX]
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google]. Il peut s’agir de votre identifiant réseau ou de votre identifiant du lien d’audience. En règle générale, il s’agit d’un identifiant à huit chiffres.

>[!NOTE]
>
>Lors de la configuration d’une destination [!DNL Google Ad Manager], veuillez travailler avec votre [!DNL Google Account Manager] ou représentant d’Adobe pour comprendre le type de compte dont vous disposez.

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers une destination](../../ui/activate-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers des destinations.

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Ad Manager], vérifiez votre compte [!DNL Google Ad Manager]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
