---
title: Surveillance des activités dans le transfert d’événements
description: Découvrez comment surveiller l’utilisation, les erreurs et calculer la durée dans vos propriétés de transfert d’événement.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: f8988d08e7009cc613a00f34e8151e8560c479d4
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 4%

---

# Surveillance des activités dans le transfert d’événement (Beta)

>[!IMPORTANT]
>
>Cette fonctionnalité est actuellement en version bêta et votre organisation n’y a peut-être pas encore accès. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

L’onglet **[!UICONTROL Surveillance]** de l’interface utilisateur de la collecte de données vous permet de surveiller les schémas d’utilisation, les erreurs et l’heure de calcul des propriétés de transfert d’événement. Ce guide donne un aperçu général de la manière d’afficher et de comprendre les rapports affichés dans l’onglet .

![Image montrant l’onglet de surveillance dans l’interface utilisateur de la collecte de données](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Conditions préalables

Ce guide suppose que vous avez acheté le transfert d’événement et que vous connaissez le fonctionnement du transfert d’événement. Pour plus d’informations, consultez la [présentation du transfert d’événement](./overview.md) .

## Vue d’ensemble des vidéos

Regardez la vidéo suivante pour obtenir un aperçu général de la fonction de surveillance :

>[!VIDEO](https://video.tv.adobe.com/v/3411267?quality=12&learn=on&captions=fre_fr)

## Sélection des propriétés et des environnements

Vous pouvez afficher les mesures au sein d’un environnement et d’une propriété spécifique ou dans toutes les propriétés et tous les environnements appartenant à votre entreprise.

Pour afficher les mesures d’une seule propriété, sélectionnez le menu déroulant des propriétés, puis la propriété qui vous intéresse dans la liste. Une fois que vous avez choisi une propriété, vous pouvez également utiliser la liste déroulante d’environnement pour sélectionner un environnement intéressant.

![Image montrant les menus déroulants de l’environnement des propriétés dans l’interface utilisateur](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Utilisation]

>[!NOTE]
>
>Les données d’utilisation sont actualisées tous les mois après la fin du mois précédent.

Le rapport **[!UICONTROL Utilisation]** affiche les appels entrants et sortants pour une période donnée. Les appels entrants représentent les données envoyées au transfert d’événement. Les appels sortants représentent les données envoyées à partir du transfert d’événement. Le nombre **[!UICONTROL Total des événements]** dans le volet de gauche est la somme des appels entrants et sortants pour une période donnée.

## [!UICONTROL Événements d’erreur]

Le rapport **[!UICONTROL Événements d’erreur]** affiche des erreurs dans l’agrégat et ventilées par code de réponse HTTP lorsque vous placez le curseur sur le graphique en courbes. Les erreurs affichées proviennent des appels sortants et les codes de réponse proviennent du point de terminaison avec lequel le transfert d’événement interagit.

Les erreurs s’affichent pour une période donnée, qui peut être ajustée à partir du menu déroulant fourni.

![Image montrant le menu déroulant de la période pour le rapport Événements d’erreur](../../images/ui/event-forwarding/monitoring/error-time.png)

La zone de recherche de l’événement d’erreur vous permet d’interroger le transfert d’événement pour comprendre les erreurs d’un domaine de point de terminaison donné. Vous devez saisir le domaine exact, car la fonction de recherche n’accepte pas les approximations ou les correspondances &quot;floues&quot;. Une fois que vous avez fourni un domaine exact pour lequel il existe des données d’erreur sortantes, appuyez sur Entrée pour actualiser le rapport afin d’afficher les erreurs sortantes pour ce domaine. Par exemple, pour voir les erreurs provenant du point d’entrée de l’API de conversion Facebook, le domaine doit être écrit en tant que `https://graph.facebook.com`.

## [!UICONTROL Temps de calcul]

Le rapport **[!UICONTROL Durée de calcul]** indique l’heure de calcul de toutes les règles sur les serveurs de transfert d’événements.

>[!NOTE]
>
>Les heures affichées ne représentent pas de latence de bout en bout. Le transfert d’événement est limité à un temps de calcul de 50 millisecondes. Si cette limite est dépassée, les données associées seront ignorées.

Les facteurs suivants affectent le temps de calcul :

1. Nombre de règles
2. La complexité des règles, généralement liée au nombre de JavaScript personnalisées exécutées

Par exemple, si une action dans le transfert d’événement atteint un point de terminaison et que ce point de terminaison prend deux secondes pour répondre, cette latence de deux secondes ne sera pas prise en compte par rapport au temps de calcul, car le transfert d’événement attend simplement et ne calcule rien de manière active. Le temps de réponse ne peut pas dépasser 30 secondes, sinon les données seront perdues.
