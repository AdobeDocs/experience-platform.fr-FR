---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de l’utilisateur du Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 667aadde831a1d010f8cbbbb20bd92f914558bd1
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 3%

---


# Guide de l’utilisateur du Profil client en temps réel

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, GRC et tierces.

Ce document sert de guide pour l’interaction avec le Profil client en temps réel dans l’interface utilisateur d’Adobe Experience Platform.

## Prise en main

Ce guide d’utilisation nécessite une bonne connaissance des différents services de la plate-forme d’expérience impliqués dans la gestion du Profil client en temps réel. Avant de lire ce guide d&#39;utilisation, consultez la documentation relative aux services suivants :

* [Profil](../home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Service](../../identity-service/home.md)d&#39;identité : Permet le Profil client en temps réel en rapprochant les identités des sources de données disparates qui sont incorporées dans la plate-forme.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

## Présentation du profil

Dans l’interface utilisateur [de la plateforme](http://platform.adobe.com)d’expérience, cliquez sur **Profils** dans le volet de navigation de gauche pour ouvrir l’onglet _Aperçu_ dans l’espace de travail _Profils._ Cet onglet affiche plusieurs widgets qui fournissent des informations de haut niveau sur le magasin de Profils, notamment l’audience adressable totale, le nombre d’enregistrements de Profil qui ont été ingérés au cours de la semaine écoulée, ainsi que des statistiques sur les enregistrements réussis et ayant échoué pour la même période.

![](../images/user-guide/profile-overview.png)

## Exemples de profil de Vue

Cliquez sur **Parcourir** pour vue un exemple de liste de profils disponibles. Cet exemple comprend jusqu’à 50 profils du nombre [total de](#profile-count)profils. Les exemples sont actualisés par une tâche automatique qui sélectionne les nouvelles données de profil lors de leur assimilation. Chaque profil répertorié affiche son identifiant, son prénom, son nom et son adresse électronique personnelle. Cliquez sur l’ID d’un profil répertorié pour afficher ses détails dans le lecteur de [Profil](#profile-viewer).

![](../images/user-guide/profile-samples.png)

Vous pouvez personnaliser les attributs affichés dans la liste en cliquant sur l’icône du sélecteur de colonnes. Cette option affiche une liste déroulante contenant des attributs de profil courants que vous pouvez ajouter ou supprimer.

![](../images/user-guide/column-selector.png)

### Nombre de Profils {#profile-count}

Le nombre de profils affiche le nombre total de profils dont votre organisation dispose dans la plate-forme d’expérience, une fois que la stratégie de fusion par défaut de votre organisation a fusionné des fragments de profil pour former un profil unique pour chaque client. En d’autres termes, votre entreprise peut avoir plusieurs fragments de profil liés à un client unique qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés ensemble (selon la stratégie de fusion par défaut) et renvoient un nombre de profils &quot;1&quot; car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils dotés d’attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de série chronologique (événement), tels que les profils Adobe Analytics. Le nombre de profils est régulièrement actualisé afin de fournir un nombre total de profils actualisé au sein de la Plateforme.

Lorsque l’ingestion de profils dans le Profil Store augmente ou diminue le nombre de plus de 5 %, une tâche est déclenchée pour mettre à jour le nombre. Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, une tâche est automatiquement déclenchée pour mettre à jour le nombre de profils. Pour l&#39;assimilation par lot, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre de profils.

![](../images/user-guide/profile-count.png)

### Recherche de Profil

Si vous connaissez une identité liée pour un profil particulier (comme son adresse électronique), vous pouvez rechercher ce profil en cliquant sur **Rechercher un profil**. Il s&#39;agit de la manière la plus fiable d&#39;accéder à un profil spécifique, qu&#39;il apparaisse dans la liste des échantillons.

![](../images/user-guide/find-a-profile.png)

Dans la boîte de dialogue qui s’affiche, sélectionnez un espace de nommage d’ID approprié dans la liste déroulante (&quot;Courriel&quot; dans cet exemple) et saisissez la valeur d’ID ci-dessous avant de cliquer sur **OK**. Si cette option est trouvée, les détails du profil ciblé s’affichent dans le lecteur de profil, comme décrit dans la section suivante.

![](../images/user-guide/find-a-profile-details.png)

### Visionneuse de profils {#profile-viewer}

Lors de la sélection ou de la recherche d’un profil spécifique, l’écran _Détails_ de la visionneuse de profils s’affiche. Cette page affiche des informations sur le profil sélectionné, telles que les attributs de base du profil, les identités liées et les canaux de contact disponibles. Les informations de profil affichées ont été fusionnées à partir de plusieurs fragments de profil pour former une seule vue du client.

![](../images/user-guide/profile-viewer-detail.png)

Le lecteur de profil fournit également des onglets qui vous permettent de vue de événements et de segmenter les adhésions associées à ce profil, le cas échéant.

![](../images/user-guide/profile-viewer-events-seg.png)

## Stratégies de fusion

Cliquez sur **Fusionner les stratégies** pour vue une liste de stratégies de fusion appartenant à votre organisation. Chaque stratégie répertoriée affiche son nom, qu’il s’agisse ou non de la stratégie de fusion par défaut et le schéma auquel elle s’applique.

![](../images/user-guide/profile-merge-policies.png)

Pour plus d’informations sur l’utilisation des stratégies de fusion dans l’interface utilisateur, voir le guide [d’utilisation](merge-policies.md)Fusionner les stratégies.

## schéma Union

Cliquez sur Schéma **** d’Unionpour vue les schémas d’union de votre banque de données de profil. Un schéma d’union est une fusion de tous les champs de modèle de données d’expérience (XDM) de la même classe, dont les schémas ont été activés pour une utilisation dans le Profil client en temps réel. Cliquez sur une classe dans la liste de gauche pour vue la structure de son schéma d&#39;union dans la trame.

![](../images/user-guide/profile-union-schema.png)

Pour plus d&#39;informations sur les schémas d&#39;union et leur rôle dans le Profil client en temps réel, consultez la section sur les schémas d&#39;union du guide [de composition des](../../xdm/schema/composition.md) schémas.

## Étapes suivantes

En lisant ce guide, vous savez maintenant comment vue et gérer vos données de Profil à l’aide de l’interface utilisateur de la plateforme d’expérience. Pour plus d’informations sur la manière d’exploiter les données du Profil client en temps réel pour générer des segments d’audience, voir la documentation [sur la](../../segmentation/home.md)segmentation.