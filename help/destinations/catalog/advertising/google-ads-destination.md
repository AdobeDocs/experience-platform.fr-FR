---
keywords: Publicités Google ; publicités Google ; mots-clés Google ; mots-clés Google AdWords ; mots-clés Google
title: Destination Google Ads
seo-title: Destination Google Ads
description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
seo-description: Google Ads, appelé auparavant Google AdWords, est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos YouTube et des affichages mobiles in-app.
translation-type: tm+mt
source-git-commit: bb2fc2658d32c59b476dd9d526eb8bc2f055a1af
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 30%

---


# [!DNL Google Ads] Destination

## Présentation

[!DNL Google Ads], appelé auparavant , est un service de publicité en ligne qui permet aux entreprises faire de la publicité avec paiement par clic sur des recherches textuelles, des affichages graphiques, des vidéos et des affichages mobiles in-app.[!DNL Google AdWords][!DNL YouTube]

## Spécifications de la destination

Notez les détails suivants spécifiques aux destinations [!DNL Google Ads] :

* Vous pouvez envoyer les [identités](../../../identity-service/namespaces.md) suivantes à [!DNL Google Ads] destinations : [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), ID de cookie Google, IDFA, GAID, ID de Roku, ID Microsoft et ID TV Amazon Fire.
   * Google utilisera [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) pour les utilisateurs de la cible en Californie, ainsi que l’ID de cookie Google pour tous les autres utilisateurs.
* Les audiences activées sont créées par programmation dans la plate-forme [!DNL Google].
* La plate-forme n’inclut pas actuellement de mesure pour valider l’activation réussie. Consultez le nombre d’audiences dans Google pour valider l’intégration et comprendre la taille de ciblage des audiences.

>[!IMPORTANT]
>
>Si vous souhaitez créer votre première destination avec [!DNL Google Ads] et que vous n’avez pas activé la fonctionnalité de synchronisation des identifiants [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) dans le service d’identification des Experience Cloud par le passé (avec Audience Manager ou d’autres applications), contactez le service de conseil en Adobe ou le service à la clientèle pour activer la synchronisation des identifiants. Si vous aviez précédemment configuré des intégrations Google dans l’Audience Manager, les synchronisations d’ID que vous avez configurées sont transférées à la plateforme.

### Type d&#39;exportation {#export-type}

**Exportation**  de segment : vous exportez tous les membres d’un segment (audience) vers la destination Google.

## Conditions préalables

### Compte [!DNL Google Ads] existant

>[!IMPORTANT]
>
> [!DNL Google] a abandonné les nouvelles intégrations de  [!DNL Google Ads] cookies avec des fournisseurs tiers. Pour exécuter les étapes de liste autorisée de la section suivante, vous devez disposer d&#39;une intégration existante avec [!DNL Google Ads]. Par conséquent, l&#39;approche recommandée pour l&#39;utilisation de [!DNL Google Ads] consiste à configurer une intégration [!DNL Google Customer Match]. Pour plus d&#39;informations sur la création d&#39;une intégration [!DNL Google Customer Match], consultez le didacticiel sur la création d&#39;une connexion [[!DNL Google Customer Match]](./google-customer-match.md).

### Liste autorisée

>[!NOTE]
>
>La liste autorisée est obligatoire avant de configurer votre première destination [!DNL Google Ads] dans Platform. Veuillez vous assurer que le processus de liste autorisée décrit ci-dessous a été terminé par [!DNL Google] avant de créer une destination.

Avant de créer la destination [!DNL Google Ads] dans Platform, vous devez contacter [!DNL Google] pour que l&#39;Adobe soit mis sur la liste des fournisseurs de données autorisés et que votre compte soit ajouté à la liste autorisée. Contactez [!DNL Google] et fournissez les informations suivantes :

* **Identifiant de compte** : il s’agit de l’identifiant de compte d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* **Identifiant client** : il s’agit de l’identifiant client d’Adobe avec [!DNL Google]. Contactez l’assistance clientèle d’Adobe ou votre représentant Adobe pour obtenir cet identifiant.
* Votre type de compte : **AdWords**
* **Identifiant**  Google AdWords : C&#39;est votre carte d&#39;identité avec  [!DNL Google]. Le format d’identifiant est généralement 123-456-7890.

## Configurer la destination

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez [!DNL Google Ads], puis **[!UICONTROL Configurer]**.

![Connexion à la destination Google Ads](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape **Configuration** du flux de travail de création de destination, renseignez les [!UICONTROL Informations de base] pour la destination.

![Informations de base de Google Ads](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : facultatif. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination.
* **[!UICONTROL Type de compte]** : AdWords est la seule option disponible.
* **[!UICONTROL Identifiant de compte]** : renseignez votre identifiant de compte avec [!DNL Google Ads]. Le format d’identifiant est généralement 123-456-7890.
* **[!UICONTROL Cas]** d’utilisation marketing : Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d&#39;informations sur les cas d&#39;utilisation marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

## Activer les segments dans [!DNL Google Ads]

Pour savoir comment activer des segments dans [!DNL Google Ads], voir [Activer les données vers les destinations](../../ui/activate-destinations.md).

## Données exportées

Pour vérifier si les données ont bien été exportées vers la destination [!DNL Google Ads], vérifiez votre compte [!DNL Google Ads]. Si l’activation a réussi, les audiences sont renseignées dans votre compte.