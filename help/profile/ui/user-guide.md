---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de l’utilisateur du Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: da3793a528fa919633e777423d77e7be9cbc0154
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---


# Guide de l’utilisateur du Profil client en temps réel

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, GRC et tierces.

Ce document sert de guide pour l’interaction avec le Profil client en temps réel dans l’interface utilisateur de l’Adobe Experience Platform.

## Prise en main

Ce guide d&#39;utilisation nécessite une compréhension des différents services d&#39;Experience Platform impliqués dans la gestion des Profils clients en temps réel. Avant de lire ce guide d&#39;utilisation, consultez la documentation relative aux services suivants :

* [Profil](../home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Service](../../identity-service/home.md)d&#39;identité : Permet le Profil client en temps réel en rapprochant les identités de sources de données disparates lors de leur assimilation dans Platform.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.

## Présentation

Dans l’interface utilisateur [de l’](http://platform.adobe.com)Experience Platform, cliquez sur **Profils** dans le volet de navigation de gauche pour ouvrir l’onglet _Aperçu_ . Cet onglet contient des liens vers la documentation et des vidéos pour vous aider à comprendre et à commencer à travailler avec des profils.

![](../images/user-guide/profiles-overview.png)

## Parcourir Profil

Cliquez sur l’onglet **Parcourir** pour parcourir les profils par identité.

### Mesures de Profil {#profile-metrics}

Sur le côté droit de l&#39;onglet **Parcourir** se trouvent plusieurs mesures de profil importantes liées à vos données de profil, y compris le nombre [total de](#profile-count) profils ainsi qu&#39;une liste des [profils par espace de nommage](#profiles-by-namespace).

Ces mesures de profil sont évaluées à l’aide de la stratégie de fusion par défaut de votre organisation. Pour plus d’informations sur l’utilisation des stratégies de fusion, y compris sur la manière de définir une stratégie de fusion par défaut, voir le guide [d’utilisation](merge-policies.md)Fusionner les stratégies.

Outre ces mesures, la section Mesures de profil fournit également une date et une heure de *dernière mise à jour* , indiquant le moment où les mesures ont été évaluées pour la dernière fois.

![](../images/user-guide/profiles-browse.png)

### Nombre de Profils {#profile-count}

Le nombre de profils affiche le nombre total de profils dont votre organisation dispose dans l’Experience Platform, après que la stratégie de fusion par défaut de votre organisation a fusionné des fragments de profil pour former un seul profil pour chaque client. En d’autres termes, votre entreprise peut avoir plusieurs fragments de profil liés à un client unique qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés ensemble (selon la stratégie de fusion par défaut) et renvoient un nombre de profils &quot;1&quot; car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de séries chronologiques (événement), telles que les profils Adobe Analytics. Le nombre de profils est régulièrement actualisé afin de fournir un nombre total de profils actualisé à Platform.

Lorsque l’ingestion de profils dans le Profil Store augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour le nombre. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l&#39;assimilation par lot, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre de profils.

### Profils par espace de nommage {#profiles-by-namespace}

La mesure *Profils par espace de nommage* affiche le nombre total et la ventilation des espaces de nommage sur l’ensemble des profils fusionnés dans votre Profil Store. Le nombre total de profils par espace de nommage (en d’autres termes, l’ajout des valeurs affichées pour chaque espace de nommage) sera toujours supérieur à la mesure Nombre de profils, car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

Tout comme la mesure du nombre [de](#profile-count) profils, lorsque l’assimilation de profils dans le magasin de Profils augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour les mesures d’espace de nommage. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l’assimilation par lot, dans les 15 minutes qui suivent l’importation d’un lot dans le magasin de Profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour les mesures.

### Fusionner la stratégie

Le sélecteur de stratégies **de** fusion sélectionne automatiquement la stratégie de fusion par défaut pour votre organisation. Si vous ne souhaitez pas utiliser cette stratégie de fusion, vous pouvez sélectionner la stratégie de fusion `X` en regard de la stratégie de fusion par défaut pour ouvrir une boîte de dialogue *Sélectionner la stratégie* de fusion dans laquelle vous pouvez choisir une autre stratégie de fusion. Pour en savoir plus sur les stratégies de fusion, consultez le guide [de l’utilisateur](merge-policies.md)Fusionner les stratégies.

![](../images/user-guide/profiles-search-merge-policy.png)

### espace de nommage d&#39;identité

Le sélecteur d&#39;espace de nommage **** d&#39;identité ouvre une boîte de dialogue dans laquelle vous pouvez choisir l&#39;espace de nommage d&#39;identité à rechercher et personnaliser les attributs affichés à partir de votre recherche en sélectionnant l&#39;icône de filtre et en choisissant les attributs à ajouter ou à supprimer.

![](../images/user-guide/profiles-search-filter.png)

Dans la boîte de dialogue *Sélectionner un espace de nommage* d&#39;identité, choisissez l&#39;espace de nommage de recherche ou utilisez la barre de **recherche** de la boîte de dialogue pour commencer à saisir le nom d&#39;un espace de nommage. Vous pouvez sélectionner un espace de nommage pour vue d&#39;autres détails, et une fois que vous avez trouvé l&#39;espace de nommage, vous pouvez sélectionner le bouton radio et appuyer sur **Sélectionner** pour continuer.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valeur d’identité

Après avoir sélectionné un espace de nommage **d&#39;** identité, vous revenez à l&#39;onglet *Parcourir* où vous pouvez saisir une valeur **d&#39;** identité. Cette valeur est spécifique à un profil client individuel et doit être une entrée valide pour l’espace de nommage fourni. Par exemple, la sélection de l’espace de nommage **d’** identité &quot;courriel&quot; exigerait une valeur **d’** identité sous la forme d’une adresse électronique valide.

![](../images/user-guide/profiles-show-profile.png)

Une fois qu’une valeur a été saisie, sélectionnez **Afficher le profil** et un seul profil correspondant à la valeur est renvoyé. Sélectionnez l’ID **de** Profilpour vue les détails du profil.

![](../images/user-guide/profiles-display-profile.png)

### Détails du Profil

Lorsque vous sélectionnez l’ID **de** Profil, l’onglet _Détails_ s’ouvre. Cette page affiche des informations sur le profil sélectionné, y compris les attributs de base, les identités liées et les canaux de contact disponibles. Les informations de profil affichées ont été fusionnées à partir de plusieurs fragments de profil pour former une seule vue du client.

![](../images/user-guide/profiles-profile-detail.png)

Vous pouvez vue des informations supplémentaires relatives au profil, y compris les attributs, les Événements et les segments auxquels le profil est membre.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Stratégies de fusion

Cliquez sur **Fusionner les stratégies** pour vue une liste de stratégies de fusion appartenant à votre organisation. Chaque stratégie répertoriée affiche son nom, qu’il s’agisse ou non de la stratégie de fusion par défaut et le schéma auquel elle s’applique.

For more information on merge policies, see the [Merge Policies user guide](merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## schéma Union

Cliquez sur Schéma **** d’Union pour vue les schémas d’union de votre Profil Store. Un schéma d’union est une fusion de tous les champs de modèle de données d’expérience (XDM) de la même classe, dont les schémas ont été activés pour une utilisation dans le Profil client en temps réel. Cliquez sur une classe dans la liste de gauche pour vue la structure de son schéma d&#39;union dans la trame.

Par exemple, la sélection de &quot;Profil XDM&quot; affiche le schéma d’union pour la classe de Profil XDM individuel.

Pour plus d&#39;informations sur les schémas d&#39;union et leur rôle dans le Profil client en temps réel, consultez la section sur les schémas d&#39;union du guide [de composition des](../../xdm/schema/composition.md) schémas.

![](../images/user-guide/profiles-union-schema.png)

## Étapes suivantes

En lisant ce guide, vous savez maintenant comment vue et gérer vos données de Profil à l’aide de l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur la manière d’exploiter les données du Profil client en temps réel pour générer des segments d’audience, voir la documentation [sur la](../../segmentation/home.md)segmentation.