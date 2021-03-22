---
keywords: gestionnaire de publicités Google ; publicité Google ; doubleclick ; DoubleClick AdX ; DoubleClick ; Google Ad Manager ; Google Ad Manager
title: Connexion à Google Ad Manager
description: 'Google Ad Manager, anciennement appelé DoubleClick for Publishers ou DoubleClick AdX, est une plateforme de service publicitaire de Google qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.  '
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 30%

---


# [!DNL Google Ad Manager] connexion

## Présentation {#overview}

[!DNL Google Ad Manager], anciennement appelé for Publishers ou , est une plateforme de service publicitaire de qui donne aux éditeurs les moyens de gérer l’affichage des publicités sur leurs sites web, par le biais de vidéos et dans des applications mobiles.[!DNL DoubleClick][!DNL DoubleClick AdX][!DNL Google]

## Caractéristiques de la destination {#specifics}

Notez les détails suivants spécifiques aux destinations [!DNL Google Ad Manager] :

* Les audiences activées sont créées par programmation dans la plate-forme [!DNL Google].
* [!DNL Platform] n’inclut pas actuellement de mesure pour valider une activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

## Identités prises en charge {#supported-identities}

[!DNL Google Ad Manager] prend en charge l&#39;activation des identités décrites dans le tableau ci-dessous.

| Identité de cible | Description | Considérations |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Sélectionnez cette identité de cible lorsque votre identité source est un espace de nommage IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), également appelé  [!DNL Device ID]. Identifiant numérique à 38 chiffres associé par l’Audience Manager à chaque périphérique avec lequel elle interagit. | Google utilise [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) pour les utilisateurs de la cible en Californie et l’ID de cookie Google pour tous les autres utilisateurs. |
| [!DNL Google] identifiant de cookie | [!DNL Google] identifiant de cookie | [!DNL Google] utilise cet identifiant pour les utilisateurs de cible en dehors de la Californie. |
| RIDA | Identifiant Roku pour la publicité. Cet identifiant identifie de manière unique les périphériques Roku. |  |
| MAID | ID de publicité Microsoft. Cet identifiant identifie de manière unique les périphériques exécutant Windows 10. |  |
| ID TV Amazon Fire | Cet identifiant identifie de manière unique les téléviseurs Amazon Fire. |  |

## Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) vers la destination Google.

## Conditions préalables

Si vous souhaitez créer votre première destination avec [!DNL Google Ad Manager] et que vous n’avez pas activé la fonctionnalité de synchronisation des identifiants [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’identification des Experience Cloud par le passé (avec Audience Manager ou d’autres applications), contactez le service de conseil en Adobe ou le service à la clientèle pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations [!DNL Google] dans l&#39;Audience Manager, les synchronisations d&#39;ID que vous avez configurées sont transférées à Platform.

## Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ad Manager] dans Platform. Veuillez vous assurer que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.

Avant de créer la destination [!DNL Google Ad Manager] dans Platform, vous devez contacter [!DNL Google] pour que l&#39;Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez [!DNL Google] et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant réseau** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* **Identifiant du lien d’audience** : il s’agit de votre compte avec [!DNL Google Ad Manager]
* Votre type de compte. DFP de Google ou AdX buyer.

## Configurer la destination

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez **[!DNL Google Ad Manager]**, puis **[!UICONTROL Configurer]**.

![Connexion à la destination Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape **Configuration** du flux de travail de création de destination, renseignez les [!UICONTROL Informations de base] pour la destination.

![Informations de base de Google Ad Manager](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `DFP by Google` pour for Publishers[!DNL DoubleClick]
   * Utiliser `AdX buyer` pour [!DNL Google AdX]
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google]. Il peut s’agir de votre identifiant réseau ou de votre identifiant du lien d’audience. En règle générale, il s’agit d’un identifiant à huit chiffres.
* **[!UICONTROL Action]** marketing : Les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Lors de la configuration d&#39;une destination [!DNL Google Ad Manager], demandez à votre [!DNL Google Account Manager] ou représentant d&#39;Adobe de vous identifier.

## Activer les segments dans [!DNL Google Ad Manager]

Pour savoir comment activer des segments dans [!DNL Google Ad Manager], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Ad Manager], vérifiez votre compte [!DNL Google Ad Manager]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.