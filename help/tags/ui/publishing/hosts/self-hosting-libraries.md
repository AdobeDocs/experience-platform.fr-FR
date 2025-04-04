---
title: Bibliothèques auto-hébergées
description: Découvrez comment mettre en œuvre l’auto-hébergement pour vos versions de bibliothèque de balises dans Adobe Experience Platform.
exl-id: 8c3bf202-de7a-46e0-801f-0cede24865fd
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 90%

---

# Bibliothèques auto-hébergées

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

La fonctionnalité Balises dans Adobe Experience Platform permet la production d’un ensemble de fichiers appelé [version](../builds.md). Cet ensemble de fichiers contrôle le comportement de votre application au moment de l’exécution.

Les versions doivent être hébergées quelque part afin que les appareils clients puissent les récupérer au moment de l’exécution.

Experience Platform peut gérer l’hébergement de ces fichiers pour vous ou vous pouvez le faire vous-même.

## Géré par Adobe {#managed-by-adobe}

Adobe n’est pas spécialisé dans l’hébergement web. Si vous choisissez de confier la gestion de votre hébergement à Adobe, vos versions sont diffusées sur un réseau de diffusion de contenu (CDN) tiers avec lequel nous avons un accord.

Actuellement, le fournisseur principal de réseau de diffusion de contenu est Akamai. Les fichiers hébergés sur Akamai ont un domaine `assets.adobedtm.com`.

### Pourquoi utiliser l’hébergement géré par Adobe ?

La raison principale d’utiliser l’hébergement géré par Adobe est la simplicité. Il est plus facile de créer l’hôte requis et vous n’avez pas à vous soucier de la maintenance.

## Auto-hébergement

Si vous ne souhaitez pas qu’Adobe gère vos fichiers hébergés, vous devez les héberger vous-même. Pour héberger vos fichiers, vous devez obtenir les versions finalisées à partir d’Experience Platform et être responsable de l’obtention des fichiers via le cycle de publication de votre entreprise sur les serveurs que vous gérez.

### Pourquoi utiliser l’auto-hébergement ?

Vous pouvez choisir d’héberger vos propres fichiers de version pour plusieurs raisons.

* Certains navigateurs bloquent le domaine assets.adobedtm.com en raison des paramètres de confidentialité configurés par l’utilisateur final.
* L’auto-hébergement réduit le nombre requis de recherches DNS.
* Vous devez définir des en-têtes spécifiques pour des raisons de sécurité.
* Vos exigences de contrôle du cache sont différentes des paramètres par défaut d’Adobe.
* Vous souhaitez avoir plus de contrôle sur l’emplacement des nœuds en périphérie.
* Votre organisation a des exigences de sécurité et légales qui vous empêchent d’opter pour un hébergement géré par Adobe.

### Comment auto-héberger vos versions

Vous pouvez utiliser deux méthodes pour obtenir les versions finalisées à auto-héberger.

* Téléchargement
* Diffusion directe

#### Téléchargement

Les versions peuvent être diffusées sous la forme d’un fichier .zip empaqueté (avec chiffrement facultatif). Vous pouvez ensuite décompresser le package et insérer le contenu dans le cycle de publication pour le placer sur vos propres serveurs.

Utilisez un hôte [Managed by Adobe](self-hosting-libraries.md) (Géré par Adobe) et sélectionnez l’option [Archive](../environments.md) dans votre environnement. L’environnement vous fournit un lien de téléchargement. Chaque fois qu’une version est créée, vous pouvez la récupérer à partir du lien de téléchargement de l’environnement.

#### Diffusion directe

Les versions peuvent également être diffusées directement à un serveur SFTP que vous avez créé. Vous prenez la responsabilité de les placer dans votre cycle de publication et de les rendre disponibles.

Pour effectuer une diffusion directe, vous devez créer un [hôte SFTP](sftp-host.md) et affecter cet hôte à votre environnement. Chaque fois que vous créez une bibliothèque dans cet environnement, les fichiers sont diffusés sur votre serveur SFTP.
