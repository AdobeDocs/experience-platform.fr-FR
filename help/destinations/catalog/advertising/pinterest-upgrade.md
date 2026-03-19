---
title: Migration de la destination Pinterest vers la nouvelle API. Action du client requise.
description: Pinterest rend obsolète l’API de l’annonceur v4 actuellement utilisée par la destination Pinterest dans Real-Time CDP. Découvrez vos éléments d’action pour passer facilement à la nouvelle API sans interrompre vos campagnes Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Mise à niveau de la destination Pinterest vers la nouvelle API. Action du client requise d’ici le 18 janvier 2024.

>[!IMPORTANT]
>
>Les éléments d’action du client de cette page s’appliquent à vous si votre organisation a configuré des flux de données pour exporter des données vers Pinterest avant le 16 novembre 2023, date à laquelle la nouvelle destination **[!UICONTROL Pinterest]**, à l’aide de la dernière API Pinterest, a été ajoutée au catalogue de destinations.

## Que se passe-t-il ? {#what-is-happening}

Pinterest a rendu obsolète l’API de l’annonceur v4 utilisée par la destination [Pinterest](/help/destinations/catalog/advertising/pinterest.md) dans Real-Time CDP. Adobe a mis à jour la destination pour utiliser l’API de l’annonceur [v5](https://developers.pinterest.com/docs/getting-started/migration/). Lisez cette page pour comprendre vos éléments d’action afin de passer facilement à la nouvelle API sans interrompre vos campagnes Pinterest.

## Pourquoi suis-je averti ? {#why-notified}

Nous avons identifié votre organisation comme ayant des flux de données actifs pour activer les audiences dans Pinterest.

## Quel est le plan ? {#what-is-the-plan}

Adobe a publié une nouvelle carte de destination Pinterest qui tire parti de l’API Pinterest v5 et qui conserve vos flux de données existants dans la nouvelle connexion.

## Dois-je faire quelque chose pour que mes audiences activées continuent à fonctionner ? {#action-required}

Oui, avant le 18 janvier 2024, vous devez vous authentifier auprès de la nouvelle destination Pinterest avec votre compte d’annonceur Pinterest dans Real-Time CDP. Voir les instructions détaillées ci-dessous.

### Se réauthentifier sur Pinterest {#reauthenticate}

1. Accédez à **[!UICONTROL Destinations > Accounts]** et utilisez le filtre à l’écran pour filtrer la destination Pinterest uniquement.
   ![Filtrer les comptes Pinterest uniquement](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Sur la destination **Pinterest**, sélectionnez le symbole des trois points ... et sélectionnez **[!UICONTROL Edit details]**.
   ![Sélectionnez Modifier les détails](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Sélectionnez **[!UICONTROL Reconnect OAuth]** et connectez-vous à votre compte Pinterest.
   ![Sélectionnez Reconnecter OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Accédez à l’élément d’action dans la section ci-dessous

### Activer les flux vers une nouvelle destination {#disable-old-enable-new-flows}

Ensuite, vous devez activer les flux de données pour la nouvelle carte **[!UICONTROL Pinterest]**.

1. Accédez à **[!UICONTROL Destinations > Browse]** et utilisez le filtre à l’écran pour filtrer la destination **[!UICONTROL Pinterest]** uniquement.
   ![Filtrer les flux de données Pinterest uniquement dans l’onglet Parcourir](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Sélectionnez le nom de la connexion liée par un lien hypertexte (Campagne de fidélité dans l’exemple de capture d’écran ci-dessus) vers la destination **[!UICONTROL Pinterest]** et activez le bouton (bascule) **[!UICONTROL Enable]** sur **activé**.
   ![Activer/désactiver pour les nouvelles connexions et désactiver pour les anciennes](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Pouvez-vous nous faire part de certains échéanciers généraux? {#high-level-timelines}

Oui, voir ci-dessous :

**D’ici le 16 novembre 2023** : la nouvelle destination est prête et vous devriez voir deux cartes Pinterest côte à côte dans le catalogue jusqu’à ce que Pinterest cesse de prendre en charge l’ancienne API v4. Tous les flux de données existants vers la carte Pinterest actuelle sont copiés vers la nouvelle destination.

![Côte à côte de l’ancienne et de la nouvelle destination Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**D’ici le 15 décembre 2023** : <span class="preview">Action client 1</span>. Vous devez vous authentifier à nouveau auprès de Pinterest afin que la nouvelle carte soit connectée à Pinterest. Consultez les instructions complètes dans [cette section](#reauthenticate).

<span class="preview">Action du client 2</span>. Ensuite, vous devez activer les flux de données dans la nouvelle carte. Consultez les instructions complètes dans [cette section](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Après le 18 janvier 2024** : <span class="preview">Pinterest a désactivé l’accès à l’API de l’annonceur V4. Tous les clients Real-Time CDP qui n’ont pas effectué la mise à niveau vers la nouvelle destination verront désormais leurs flux de données vers la destination Pinterest échouer. [Authentifiez-vous à nouveau sur Pinterest](#reauthenticate) et [activez les flux de données](#disable-old-enable-new-flows) vers la destination mise à niveau pour reprendre vos campagnes sur Pinterest.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
