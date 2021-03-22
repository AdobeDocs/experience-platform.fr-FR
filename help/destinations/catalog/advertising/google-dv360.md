---
keywords: DoubleClick Bid Manager ; DoubleClick bid manager ; DoubleClick ; Display & Video 360 ; display 360 ; video 360 ; Video 360 ; Display 360 ; display et video
title: Connexion Google Display & Video 360
description: Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 39%

---


# [!DNL Google Display & Video 360] connexion

[!DNL Display & Video 360], connu précédemment sous le nom de , est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.[!DNL DoubleClick Bid Manager]

## Caractéristiques de la destination {#specifics}

Notez les détails suivants spécifiques aux destinations [!DNL Google Display & Video 360] :

* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plate-forme n’inclut pas actuellement de mesure pour valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>Si vous cherchez à créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service Experience Cloud ID par le passé (dans Adobe Audience Manager ou dans d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer les synchronisations des identifiants. Si vous aviez précédemment configuré des intégrations Google dans l’Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à la plateforme.

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

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Display & Video 360] dans Platform. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination [!DNL Google Display & Video 360] dans Platform, vous devez contacter Google pour demander que l&#39;Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Votre type de compte** : utilisez **[!DNL Invite advertiser]** pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360 ou utilisez **[!DNL Invite partner]** pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.

## Configurer la destination

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Display & Video 360], puis **[!UICONTROL Configurer]**.

![Connexion à une destination Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre [!UICONTROL Activer] et [!UICONTROL Configurer], consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l&#39;étape **Configuration** du processus de création de destination, renseignez les [!UICONTROL Informations de base] de la destination, ainsi que les actions marketing qui doivent s&#39;appliquer à cette destination.

![Informations de base Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `Invite Advertiser` pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360.
   * Utilisez `Invite Partner` pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** avec Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.
* **[!UICONTROL Action]** marketing : Les actions marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des actions marketing définies par Adobe ou créer votre propre action marketing. Pour plus d&#39;informations sur les actions marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

>[!NOTE]
>
>Lors de la configuration d&#39;une destination [!DNL Google Display & Video 360], demandez à votre [!DNL Google Account Manager] ou représentant d&#39;Adobe de vous identifier.

## Activer les segments dans [!DNL Google Display & Video 360]

Pour savoir comment activer des segments dans [!DNL Google Display & Video 360], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Display & Video 360], vérifiez votre compte [!DNL Google Display & Video 360]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.