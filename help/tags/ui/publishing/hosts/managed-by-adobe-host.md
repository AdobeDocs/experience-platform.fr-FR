---
title: Présentation des hôtes gérés par Adobe
description: Découvrez l’option d’hébergement par défaut pour le déploiement des versions de bibliothèque de balises dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 66%

---

# Présentation des hôtes gérés par Adobe

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les hôtes gérés par Adobe sont le paramètre d’hôte par défaut pour le déploiement des versions de votre bibliothèque de balises dans Adobe Experience Platform. Lorsque vous créez une propriété via l’interface utilisateur de collecte de données, un hôte géré par Adobe par défaut est créé pour vous.

Avec les hôtes gérés par Adobe, les versions de bibliothèque sont diffusées à un réseau de diffusion de contenu (CDN) tiers avec lequel Adobe a conclu un contrat. Ces réseaux de diffusion de contenu fonctionnent indépendamment d’Adobe. Ainsi, même lorsque Platform  est en cours de maintenance ou est hors service, votre code déployé continuera à fonctionner normalement sur vos sites et applications. Le code incorporé pour un hôte géré par Adobe indique l’emplacement du fichier de bibliothèque principal sur le réseau de diffusion de contenu afin qu’un appareil client puisse récupérer les fichiers au moment de l’exécution.

Ce document présente les hôtes gérés par Adobe dans Platform et décrit les étapes à suivre pour créer un hôte géré par Adobe dans l’interface utilisateur.

## Akamai

Actuellement, le principal fournisseur de réseau CDN pour Adobe est [Akamai](https://www.akamai.com/fr). Le puissant réseau de diffusion de contenu d’Akamai est conçu pour fournir du contenu à une audience globale et volumineuse de visiteurs Web. Le réseau de diffusion de contenu exécute des réseaux redondants de nœuds équilibrés en charge et optimisés géographiquement afin de diffuser le contenu le plus rapidement possible aux visiteurs du monde entier.

Plus précisément Akamai exécute plus de 137 000 serveurs dans 87 pays sur plus de 1 150 réseaux. En termes de redondance, le réseau CDN achemine non seulement d’un serveur à un autre, mais peut également acheminer d’un noeud de serveurs à un autre noeud de serveurs, si nécessaire. En d’autres termes, chaque nœud est constitué de plusieurs serveurs, de sorte qu’un serveur qui tombe en panne ne constitue jamais un problème, car les autres serveurs du même nœud peuvent prendre le relais.

Si un noeud entier tombe en panne, Akamai diffuse depuis le noeud le plus proche avec le même contenu mis en cache. Les nœuds sont sélectionnés dynamiquement en fonction de l’emplacement du visiteur, de la charge de trafic et d’autres facteurs afin que le contenu soit systématiquement fourni à partir du meilleur nœud local pour chaque visiteur.

Les fichiers hébergés sur Akamai ont un domaine `assets.adobedtm.com`. Il peut être référencé de manière sécurisée ou non (`http://` ou `https://`) en fonction de la manière dont il est appelé dans votre code `<script>` incorporé.

>[!WARNING]
>
>Si votre bibliothèque n’est pas disponible sur le réseau Akamai, Platform  ne peut pas empêcher les erreurs qui pourraient en résulter.

## Caching de la création de bibliothèque

Lors de l’utilisation d’hôtes gérés par Adobe, les versions de votre bibliothèque sont mises en cache à deux emplacements :

* [Caching d’Edge](#edge)
* [Caching du navigateur](#browser)

### Caching d’Edge {#edge}

L’objectif Principal d’un CDN est de distribuer intelligemment du contenu aux serveurs géographiquement plus proches des utilisateurs finaux afin que le contenu puisse être récupéré plus rapidement par les appareils clients. Pour ce faire, les réseaux CDN mettent à disposition des copies du contenu sur des serveurs répartis géographiquement dans le monde (« nœuds de périphérie »).

Une fois que votre version a été déployée sur l’hôte géré par Adobe, le réseau CDN la distribue sur plusieurs serveurs centralisés (« origines »), qui envoient ensuite des copies de la version à de nombreux noeuds de périphérie dans le monde entier pour le caching. Les versions mises en cache de la version stockée sur ces nœuds de périphérie sont ensuite finalement diffusées sur les appareils client.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Pour les hôtes gérés par Adobe, la première bibliothèque publiée dans un nouvel environnement peut prendre jusqu’à 5 minutes pour se propager dans le réseau mondial de diffusion de contenu.

Lorsqu’un noeud de périphérie reçoit une demande pour un fichier spécifique (tel que la version de votre bibliothèque), il vérifie d’abord la valeur de durée de vie (TTL) du fichier. Si la durée de vie n’a pas expiré, les nœuds de périphérie diffusent la version mise en cache. Si la durée de vie a expiré, le nœud de périphérie demande une nouvelle copie à l’origine la plus proche, diffuse cette copie actualisée, puis met en cache la copie actualisée avec une nouvelle durée de vie.

>[!NOTE]
>
>Outre le caching des nœuds de périphérie, il peut également exister des réseaux intermédiaires (tels que les réseaux d’entreprise ou mobiles) qui effectuent leur propre caching. Si vos versions ne sont pas mises en cache comme prévu, ces réseaux peuvent en être la cause sous-jacente.

#### Invalidation du cache Edge {#invalidation}

Lorsque vous chargez une nouvelle version de bibliothèque, les caches sur tous les noeuds de périphérie applicables sont invalidés. Cela signifie que chaque noeud considère sa version mise en cache comme non valide, quelle que soit la date à laquelle il a récupéré une nouvelle copie. La prochaine fois qu’un nœud de périphérie reçoit une demande pour ce fichier, il récupère une nouvelle copie de l’origine.

Comme Akamai dispose de plusieurs serveurs d’origine qui répliquent des fichiers entre eux et qu’il n’existe aucun moyen de savoir quelle origine a reçu votre fichier en premier, ces requêtes de noeud peuvent atteindre une origine qui n’a pas la dernière version. Il mettrait ensuite à nouveau en cache l’ancienne version. Pour éviter cela, plusieurs invalidations du cache sont effectuées pour chaque nouvelle version sur les intervalles suivants :

* Immédiatement après le téléchargement
* 5 minutes après le téléchargement
* 60 minutes après le téléchargement

Ces invalidations échelonnées du cache donnent aux groupes de serveurs d’origine le temps de répliquer la dernière version du fichier entre eux afin qu’ils disposent tous de la dernière version une fois le fichier extrait.

### Caching du navigateur {#browser}

Les versions de bibliothèque sont également mises en cache sur le navigateur à l’aide de l’en-tête HTTP `cache-control`. Lors de l’utilisation d’hôtes gérés par Adobe, vous n’avez aucun contrôle sur les en-têtes renvoyés dans les réponses de l’API. Par conséquent, le paramètre Adobe par défaut pour le caching est utilisé. En d’autres termes, vous ne pouvez pas utiliser d’en-têtes personnalisés pour les hôtes gérés par Adobe. Si vous avez besoin d’un en-tête `cache-control` personnalisé, vous pouvez envisager l’[auto-hébergement](self-hosting-libraries.md) à la place.

La durée de vie (TTL) de la version de votre bibliothèque mise en cache par le navigateur (déterminée par l’en-tête `cache-control` ) varie en fonction de l’environnement de balise utilisé :

| Environnement | Valeur `cache-control` |
| --- | --- |
| Développement | `max-age=0, no-cache, no-store` |
| Évaluation | `max-age=0, no-cache, no-store` |
| Production | `max-age=3600` |

Comme l’indique le tableau ci-dessus, le caching du navigateur n’est pas pris en charge sur les environnements de développement et d’évaluation. Par conséquent, vous ne devez pas utiliser les codes incorporés de développement ou intermédiaires dans les contextes à trafic élevé ou de production.

Les en-têtes de contrôle du cache ne sont appliqués que pour la version de bibliothèque principale. Toutes les sous-ressources situées sous la bibliothèque principale sont toujours considérées comme des sous-ressources nouvelles et il n’est donc pas nécessaire de les mettre en cache dans le navigateur.

## Utilisation de l’hébergement géré par les Adobes dans l’interface utilisateur de la collecte de données

Lorsque vous créez une propriété pour la première fois dans l’[interface utilisateur de collecte de données](http://launch.adobe.com/fr), un hôte géré par l’Adobe est automatiquement créé. Tous les environnements disponibles possédant des propriétés immédiatement utilisables sont également affectés par défaut à l’hôte géré par l’Adobe.

>[!NOTE]
>
>Si l’affectation de l’hôte géré par Adobe par défaut est supprimée de tous les environnements, l’hôte peut être supprimé. Si vous souhaitez revenir à un hôte géré par Adobe après cette opération, vous pouvez créer un nouvel hôte en procédant comme suit :
>
>1. Sélectionnez l’onglet **[!UICONTROL Hôtes]** sur votre propriété, puis cliquez sur **[!UICONTROL Ajouter l’hôte]**.
>1. Attribuez un nom à l’hôte, sélectionnez **[!UICONTROL Géré par Adobe]** comme type d’hôte, puis cliquez sur **[!UICONTROL Enregistrer]**.

>
>
Vous pouvez ensuite réaffecter vos environnements à l’hôte géré par Adobe selon vos besoins.

## Étapes suivantes

Ce document fournit un aperçu de l’hébergement géré par Adobe pour les bibliothèques de balises dans Adobe Experience Platform. Pour plus d’informations sur les autres options d’hébergement, consultez la documentation suivante :

* [Hébergement SFTP](./sftp-host.md)
* [Bibliothèques auto-hébergées](./self-hosting-libraries.md)

Pour plus d’informations sur la gestion des hôtes pour vos environnements, consultez le [guide des environnements](../environments.md).
