---
title: Surveillance de l’utilisation de la licence de requête par lots
description: L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence Data Distiller de votre entreprise.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
hide: true
hidefromtoc: true
recommendations: noCatalog, display
source-git-commit: fa573dcf03eb711e946afe40d107871f5166ff58
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 15%

---

# (Alpha) Surveillance de l’utilisation des licences de requête par lots {#monitor-license-usage}

>[!IMPORTANT]
>
>La possibilité de surveiller l’utilisation des licences de requête par lots via l’interface utilisateur n’est pas encore disponible pour tous les utilisateurs. Cette fonctionnalité est en version alpha et est encore en cours de test. Ce document est sujet à modification.

L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence Query Service de votre entreprise.

Vous trouverez des instructions détaillées sur l’accès au tableau de bord d’utilisation de la licence et les interactions avec celui-ci dans l’interface utilisateur, ainsi que des informations sur les mesures disponibles affichées dans le tableau de bord, dans le [guide de tableau de bord d’utilisation de la licence](../../dashboards/guides/license-usage.md).

Veuillez lire la [Présentation des tableaux de bord](../../dashboards/home.md) pour un résumé de toutes les fonctionnalités du tableau de bord dans Experience Platform.

## Widgets {#widgets}

Le tableau de bord de l’utilisation des licences est constitué de widgets qui affichent des mesures en lecture seule fournissant des informations importantes sur l’utilisation des licences de votre entreprise. Les mesures visibles dépendent des licences spécifiques à votre entreprise.

Sélectionnez un bouton radio pour choisir un environnement de test à analyser et utilisez la liste déroulante pour sélectionner une période pour l’analyse. Les options disponibles sont une période de 30 jours, 90 jours, 12 mois, la dernière année, la période de contrat complète ou une date personnalisée.

## Calculer les heures {#compute-hours}

Le [!UICONTROL Calculer les heures] Le widget utilise un graphique linéaire pour visualiser le temps de traitement des requêtes par lots de votre entreprise chaque jour. Le widget affiche trois mesures indiquées par un nombre dans le coin supérieur gauche du widget. Voici les

- [!UICONTROL Réels]: Nombre total d’heures de calcul pour la période choisie dans la liste déroulante de présentation. Cette mesure est également indiquée sur le graphique par une ligne continue.
- [!UICONTROL Sous licence]: Nombre total d’heures de calcul autorisées par le contrat de licence de votre entreprise. Cette mesure est également indiquée sur le graphique par une ligne pointillée.
- [!UICONTROL Utilisation]: Il s’agit du pourcentage de votre utilisation par rapport au nombre maximal d’heures de calcul convenu par votre licence.

>[!IMPORTANT]
>
>Le [!UICONTROL Calculer les heures] ne s’applique qu’aux clients disposant de la licence Data Distiller pour les requêtes par lots.

![Le tableau de bord de l’utilisation des licences avec le widget des heures de calcul en surbrillance.](../images/data-distiller/compute-hours.png)

