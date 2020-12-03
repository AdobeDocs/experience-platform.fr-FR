---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Destination Google Display & Video 360
seo-title: Destination Google Display & Video 360
description: Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.
seo-description: 'Display & Video 360, anciennement appelé DoubleClick Bid Manager, est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile. '
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 50%

---


# [!DNL Google Display & Video 360] Destination

## Présentation

[!DNL Display & Video 360], connu précédemment sous le nom de , est un outil utilisé pour exécuter le reciblage et des campagnes numériques ciblées dans des sources d’inventaire Display, Video et Mobile.[!DNL DoubleClick Bid Manager]

## Spécifications de la destination

Note the following details that are specific to [!DNL Google Display & Video 360] destinations:

* You can send the following [identities](../../../identity-service/namespaces.md) to [!DNL Google Display & Video 360] destinations: Google cookie ID, IDFA, GAID, Roku IDs, Microsoft IDs, and Amazon Fire TV IDs.
* Les audiences activées sont créées par programmation dans la plateforme Google.
* La plateforme CDP en temps réel n’inclut actuellement aucune mesure permettant de valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>Si vous cherchez à créer votre première destination avec Google Display &amp; Video 360 et que vous n’avez pas activé la [fonctionnalité de synchronisation des identifiants](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service Experience Cloud ID par le passé (dans Adobe Audience Manager ou dans d’autres applications), veuillez contacter Adobe Consulting ou l’assistance clientèle pour activer les synchronisations des identifiants. Si vous aviez précédemment configuré des intégrations Google dans l’Audience Manager, les synchronisations d’identifiants que vous avez configurées sont transférées au CDP en temps réel.

### Type d’exportation {#export-type}

**Exportation** de segments : vous exportez tous les membres d’un segment (audience) vers la destination Google.

## Conditions préalables 

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première [!DNL Google Display & Video 360] destination dans le CDP en temps réel. Assurez-vous que le processus de liste autorisée décrit ci-dessous a été effectué par Google avant de créer une destination.

Avant de créer la destination dans le CDP en temps réel, vous devez contacter Google pour demander que l’Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. [!DNL Google Display & Video 360] Contactez Google et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec Google. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec Google. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Votre type de compte** : utilisez **[!DNL Invite advertiser]** pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360 ou utilisez **[!DNL Invite partner]** pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.

## Configurer la destination

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Display & Video 360], puis **[!UICONTROL Configurer]**.

![Connexion à une destination Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre [!UICONTROL Activer] et [!UICONTROL Configurer], consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape de **configuration** du processus de création de destination, renseignez les informations [!UICONTROL de] base de la destination, ainsi que les cas d’utilisation marketing qui doivent s’appliquer à cette destination.

![Informations de base Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : sélectionnez une option, en fonction de votre compte avec Google :
   * Utilisez `Invite Advertiser` pour ne partager les audiences que vers une marque spécifique de votre compte Display &amp; Video 360.
   * Utilisez `Invite Partner` pour partager les audiences vers toutes les marques de votre compte Display &amp; Video 360.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte **[!DNL Invite partner]** ou **[!DNL Invite advertiser]** avec Google. En règle générale, il s’agit d’un identifiant à six ou sept chiffres.
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../../data-governance/policies/overview.md#core-actions)données.

>[!NOTE]
>
>When setting up a [!DNL Google Display & Video 360] destination please work with your [!DNL Google Account Manager] or Adobe representative to understand which account type you have.

## Activate segments to [!DNL Google Display & Video 360]

For instructions on how to activate segments to [!DNL Google Display & Video 360], see [Activate Data to Destinations](../../ui/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la [!DNL Google Display & Video 360] destination, vérifiez votre [!DNL Google Display & Video 360] compte. Si l’activation a réussi, les audiences sont renseignées dans votre compte.