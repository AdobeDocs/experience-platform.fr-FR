---
keywords: DoubleClick Bid Manager;gestionnaire d’offres DoubleClick;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display et video
title: Connexion à Google Display & Video 360
description: Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 7e2f6f54e754c52c8de7f98372d041b2a6520d46
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 35%

---

# [!DNL Google Display & Video 360] connection

## Présentation {#overview}

[!DNL Display & Video 360], connu précédemment sous le nom de , est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.[!DNL DoubleClick Bid Manager]

## Spécificités de la destination {#specifics}

Notez les détails suivants qui sont spécifiques aux destinations [!DNL Google Display & Video 360] :

* Les audiences activées sont créées par programmation dans la plateforme Google.
* [!DNL Platform] n’inclut pas actuellement de mesure pour valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>Si vous cherchez à créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service Experience Cloud ID par le passé (dans Adobe Audience Manager ou dans d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer les synchronisations des identifiants. Si vous avez précédemment configuré les intégrations Google dans Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à Platform.

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

## Type d’exportation {#export-type}

**Exportation de segments**  : vous exportez tous les membres d’un segment (audience) vers la destination Google.

## Conditions préalables

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Display & Video 360] dans Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été terminé par Google avant de créer une destination.

Avant de créer la destination [!DNL Google Display & Video 360] dans Platform, vous devez contacter Google pour demander que l’Adobe soit placé sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez Google et fournissez les informations suivantes :

* **ID** du compte : Identifiant de compte de l’Adobe avec Google. ID de compte : 87933855.
* **ID de client** : Identifiant du compte client de l’Adobe avec Google. ID de client : 89690775.
* **Votre type de compte** : utilisez **[!DNL Invite advertiser]** pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360 ou utilisez **[!DNL Invite partner]** pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.

## Configuration de la destination

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Display & Video 360], puis **[!UICONTROL Configurer]**.

![Connexion à une destination Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d’informations sur la différence entre [!UICONTROL Activer] et [!UICONTROL Configurer], consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l’espace de travail de destination.

À l’étape **Configuration** du processus de création de destination, renseignez les [!UICONTROL Informations de base] de la destination, ainsi que les actions marketing qui doivent s’appliquer à cette destination.

![Informations de base Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `Invite Advertiser` pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360.
   * Utilisez `Invite Partner` pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** avec Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.
* **[!UICONTROL Action]** marketing : Les actions marketing indiquent l’intention pour laquelle les données seront exportées vers la destination. Vous pouvez effectuer un choix parmi des actions marketing définies par l’Adobe ou créer votre propre action marketing. Pour plus d’informations sur les actions marketing, consultez la [Présentation des stratégies d’utilisation des données](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Lors de la configuration d’une destination [!DNL Google Display & Video 360], veuillez travailler avec votre [!DNL Google Account Manager] ou représentant de l’Adobe pour comprendre le type de compte dont vous disposez.

## Activation des segments vers [!DNL Google Display & Video 360]

Pour plus d’informations sur l’activation des segments vers [!DNL Google Display & Video 360], voir [Activation des données vers les destinations](../../ui/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Display & Video 360], vérifiez votre compte [!DNL Google Display & Video 360]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.
