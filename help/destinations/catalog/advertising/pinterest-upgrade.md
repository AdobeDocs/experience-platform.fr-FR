---
title: Migration de la destination pinterest vers une nouvelle API. Action du client requise.
description: Pinterest rend obsolète l’API de l’annonceur v4 actuellement utilisée par la destination Pinterest dans Real-Time CDP. Comprenez vos éléments d’action afin de passer facilement à la nouvelle API sans perturber vos campagnes Pinterest.
hide: true
hidefromtoc: true
source-git-commit: 10bf63677c66366c226d647b1174093c1704a8b9
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Mise à niveau de la destination pinterest vers la nouvelle API. Action client requise d’ici le 15 décembre 2023

## Que se passe-t-il ?

Pinterest rend obsolète l’API de l’annonceur v4 actuellement utilisée par la variable [Destination pinterest](/help/destinations/catalog/advertising/pinterest.md) dans Real-Time CDP. Adobe fonctionne avec Pinterest et met à jour la destination afin d’utiliser la variable [API de l’annonceur v5](https://developers.pinterest.com/docs/getting-started/migration/). Lisez cette page pour comprendre vos éléments d’action afin de passer facilement à la nouvelle API sans perturber vos campagnes Pinterest.

## Pourquoi suis-je informé ?

Nous avons identifié votre organisation comme ayant des flux de données actifs pour activer les audiences vers Pinterest.

## Quel est le plan ?

Adobe publie une nouvelle carte de destination Pinterest qui utilise l’API Pinterest v5 et préserve vos flux de données existants dans la nouvelle connexion.

## Dois-je faire quoi que ce soit pour que mes audiences activées fonctionnent ?

Oui, une fois la mise à niveau terminée par Adobe (prévue le 16 novembre), vous devrez vous réauthentifier à Pinterest avec votre compte publicitaire Pinterest dans Adobe Experience Platform. Consultez les instructions détaillées ci-dessous.

### Réauthentification à Pinterest {#reauthenticate}

1. Accédez à **[!UICONTROL Destinations > Comptes]** et utilisez le filtre à l’écran pour filtrer uniquement la destination Pinterest.
   ![Filtrage des comptes Pinterest uniquement](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. Sur le **(Nouveau) Pinterest** destination, sélectionnez le symbole des trois points, puis sélectionnez **[!UICONTROL Modifier les détails]**.
   ![Sélectionner Modifier les détails](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Sélectionner **[!UICONTROL Reconnecter OAuth]** et connectez-vous à votre compte Pinterest.
   ![Sélectionnez Reconnecter OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Faites savoir à Adobe que vous êtes réauthentifié dans la variable **[!UICONTROL (Nouveau) Pinterest]** destination.

### Désactiver les flux existants vers l’ancienne destination et activer les flux vers la nouvelle destination {#disable-old-enable-new-flows}

Vous devez ensuite désactiver manuellement les flux existants sur l’ancienne carte et activer les flux sur la nouvelle carte.

>[!IMPORTANT]
>
>Après la réauthentification, vous pouvez contacter Adobe et nous allons effectuer cette deuxième étape pour vous. Si vous préférez effectuer cette étape manuellement, procédez comme suit :

1. Accédez à **[!UICONTROL Destinations > Parcourir]** et utilisez le filtre à l’écran pour filtrer la variable **[!UICONTROL (Nouveau) Pinterest]** et **[!UICONTROL pinterest (obsolète)]** destinations uniquement.
   ![Filtrage des flux de données Pinterest uniquement dans l’onglet Parcourir](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Sélectionnez le nom de la connexion avec lien hypertexte (campagne de fidélité dans l’exemple de capture d’écran ci-dessus) et basculez le **[!UICONTROL Activer]** bascule vers **off** pour l’ancienne connexion et à **on** pour la nouvelle connexion.
   ![Activation pour les nouvelles connexions et désactivation pour les anciennes connexions](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle.png)
3. Comparez la liste des audiences activées dans l’ancien et le nouveau flux de données et assurez-vous que les nouveaux flux ne contiennent aucune nouvelle audience.

Bien qu’aucune interruption de vos campagnes ne soit attendue, pensez à vérifier dans l’interface utilisateur de Pinterest que tout fonctionne comme prévu.

## Pouvez-vous partager des échéances générales ?

Oui, voir ci-dessous :

**D&#39;ici le 16 novembre**: la nouvelle destination est prête et vous devriez voir deux cartes Pinterest côte à côte dans le catalogue, et tous vos flux de données existants vers la carte Pinterest actuelle sont copiés vers la nouvelle destination.

![Ancienne et nouvelle destination Pinterest côte à côte](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Après le 16 novembre, la destination Pinterest héritée est marquée **[!UICONTROL Obsolète]**. <span class="preview">Toute modification apportée aux flux de données vers la destination Pinterest (obsolète) après le 16 novembre sera *not* être automatiquement transféré vers la nouvelle destination Pinterest. </span>
>Par exemple, nous *ne pas recommander* que vous activez de nouvelles audiences vers l’ancienne destination après le 16 novembre. Si vous le faites, vous devrez alors suivre le [étapes d’activation standard](/help/destinations/ui/activate-segment-streaming-destinations.md) pour ajouter l’audience à la nouvelle destination une fois les actions du client effectuées.

**Le 15 décembre**: <span class="preview">Action client</span>. Vous devez vous reconnecter à Pinterest afin que la nouvelle carte soit connectée à Pinterest (instructions plus haut). Une fois que vous avez fait ça, contactez-nous.

Les flux de données vers Pinterest dans l’ancienne carte doivent être désactivés et ceux de la nouvelle carte doivent être activés. Vous pouvez le faire manuellement dans l’interface utilisateur, ou vous pouvez contacter l’Adobe et nous le ferons pour vous.

## Autres éléments à noter

Après avoir activé les flux de données sur la nouvelle carte de destination et désactivé les flux de données sur les anciennes cartes de destination, vous ne devriez constater aucune interruption dans vos campagnes ni dans le nombre de profils qualifiés dans les audiences qui arrivent d’Adobe Real-Time CDP.
