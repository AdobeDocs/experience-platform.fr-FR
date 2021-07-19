---
title: Notes de mise à jour
description: Notes de mise à jour les plus récentes pour les balises dans Adobe Experience Platform.
source-git-commit: f1e6741de9aa00652e9af290a89f73788e0f1d83
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 54%

---

# Notes de mise à jour

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

## 19 juillet 2021

**Ajustements du droit &quot;Gérer les propriétés&quot;**  : le droit Gérer les propriétés a rencontré un problème en raison duquel un utilisateur était autorisé à créer une propriété, mais ne pouvait pas la voir une fois créée (comme indiqué dans le fil de la communauté  [ici](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/technical-advisory-adjustments-to-the-manage-properties/ba-p/399176)). Un correctif est maintenant en ligne avec les autorisations appliquées comme décrit dans l’article.

>[!NOTE]
>
>Si vous attribuez le nouveau droit &quot;Modifier la propriété&quot; à un groupe d’utilisateurs, l’interface utilisateur ne se mettra pas à jour pour activer les champs dans l’écran de configuration des propriétés. Un correctif pour ce problème sera mis en oeuvre dans une prochaine version.

## 17 mai 2021

**Amélioration de la gestion des modifications non enregistrées** : avant, lorsque vous quittiez une vue de paramètres (extensions, éléments de données et composants de règle), une invite vous demandait si vous souhaitiez ignorer vos modifications. Cependant, la logique employée pour ce processus n’était pas optimale, si bien que la plupart du temps, il vous était demandé d’enregistrer vos modifications même si vous n’en aviez pas effectué. Cela a été corrigé. Désormais, vous ne devriez voir cette invite que lorsque vous avez réellement apporté des modifications.

## 10 mai 2021

**Publication simplifiée** : la création dans l’environnement d’évaluation n’est plus nécessaire. Si vous disposez des droits appropriés, vous pouvez ignorer entièrement l’étape soumission et publier directement à partir de l’étape de développement, à condition que la version soit correctement créée et qu’il n’y ait pas d’autres bibliothèques en amont.

## 22 avril 2021

**Collecte de données dans Adobe Experience Platform**  : l’envoi de données à Adobe ne concerne pas uniquement le déploiement de balises sur votre site ou la configuration sur votre application.  L’utilisation des SDK Experience Platform et du réseau Edge nécessite l’accès à d’autres fonctionnalités de Platform.  Auparavant, cela nécessitait une connexion à divers outils. Désormais, ils sont réunis en un seul endroit.

La collecte de données dans Platform se compose de six fonctionnalités, et votre navigation nouvellement rationalisée ne contiendra que les éléments auxquels votre société et votre compte utilisateur ont accès.  Certains noms de fonctionnalités ont également été mis à jour pour correspondre aux modèles de nommage d’Experience Platform.

* Client (anciennement accessible en tant que côté client)
* Flux de données (anciennement accessible en tant que configurations Edge)
* Serveur (anciennement accessible en tant que côté serveur)
* Configurations des applications
* Schémas
* Identités

Retrouvez d’autres mises à jour au fur et à mesure de l’évolution d’Experience Platform et de la collecte de données.

## 18 février 2021

* Mise à jour de l’interface utilisateur de collecte de données pour qu’elle réagisse au spectre v3
* Mise à jour des cartes d’extension vers les derniers modèles Spectrum
* Augmentation de la taille des champs de nom dans l’ensemble de l’application

## 13 janvier 2021

**Disponibilité générale : Event** ForwardingEnvoyez des données au niveau de l’événement à Adobe Experience Platform Edge Network, puis utilisez le transfert d’événement pour transformer, enrichir et envoyer ces données à un point de terminaison non-Adobe à l’aide des serveurs d’Adobe et non du client, avec une faible latence.

Pour plus d’informations, consultez la [présentation du transfert d’événement](../ui/event-forwarding/overview.md) et le [guide de prise en main](../ui/event-forwarding/getting-started.md) .
