---
title: Prise en charge de l’intégrité des sous-ressources (SRI)
description: Découvrez comment l’intégrité des sous-ressources (SRI) est prise en charge dans Adobe Experience Platform.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 100%

---

# Prise en charge de l’intégrité des sous-ressources (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Ce document présente la façon dont l’intégrité des sous-ressources (SRI) est prise en charge dans Adobe Experience Platform.

Les sites web d’aujourd’hui sont créés en référençant des images, du contenu et des scripts provenant de divers emplacements du Web. La SRI permet à un navigateur de vérifier que le contenu d’un fichier demandé n’a pas été modifié de manière inattendue.

Bien que leurs cas pratiques se complètent, l’intégrité des ressources diffère d’une politique de sécurité du contenu (CSP), qui garantit que seuls les fichiers provenant de sources fiables sont autorisés sur votre site web. L’intégrité des ressources va plus loin en s’assurant que le contenu de ces fichiers correspond à vos attentes.

>[!NOTE]
>
>Pour plus d’informations sur la SRI, consultez la [documentation web MDN](https://developer.mozilla.org/fr-FR/docs/Web/Security/Subresource_Integrity).

Le processus de validation de la SRI peut se résumer comme suit :

1. Vous générez un hachage cryptographique de la ressource que vous souhaitez valider.
1. Sur votre site web, le hachage est placé dans l’attribut `integrity` de l’élément HTML qui charge le fichier.
1. Lorsque le navigateur voit l’attribut `integrity`, il demande la ressource et génère indépendamment sa propre version du hachage cryptographique.
1. Le navigateur compare le hachage `integrity` à celui qu’il a généré. S’ils correspondent, la ressource est autorisée. S’ils ne correspondent pas, la ressource est bloquée.

## Limites des systèmes de gestion des balises

En tant que système de gestion des balises (TMS), dans Adobe Experience Platform les balises fournissent une version de bibliothèque JavaScript compilée que vous chargez sur vos pages avec un seul élément `<script>` (code incorporé). La fonctionnalité dynamique offerte par le TMS est accomplie en remplaçant dynamiquement le contenu de ce script sans que vous ayez à changer quoi que ce soit d’autre.

Cependant, lorsque le contenu du script change, le hachage cryptographique de ce contenu change également. Par conséquent, la seule façon de faire fonctionner la SRI avec un TMS est de mettre à jour votre code incorporé en même temps que vous publiez une nouvelle version. Pour beaucoup, cela va à l’encontre de l’objectif principal de l’utilisation d’un TMS en premier lieu.

La prochaine option de sécurité optimale concernant les balises consiste à mettre en œuvre une politique de sécurité du contenu. Pour plus dʼinformations, voir le guide sur les [CSP et les balises](./content-security-policy.md).

## Intégration de la SRI dans le déploiement de la version

Si vous souhaitez toujours utiliser la SRI pour vos versions de bibliothèque, vous devez utiliser l’auto-hébergement. Si vous utilisez l’hébergement géré par Adobe, il n’est pas possible d’utiliser la SRI sans que le contenu de la nouvelle version ne corresponde pas à l’attribut `integrity` du code incorporé pendant un certain temps.

L’automatisation du processus de mise à jour de votre code incorporé varie en complexité selon la structure de votre site, mais les étapes générales peuvent être résumées comme suit :

1. Récupérez la compilation de la version de la bibliothèque de production, soit par diffusion SFTP, soit en téléchargeant l’archive depuis l’interface utilisateur.
1. Générez le hachage cryptographique de la version principale.
1. Veillez à ce que l’attribut `integrity` du code incorporé soit mis à jour vers le nouveau hachage et que la version référencée soit mise à jour dans le cadre du même déploiement.

>[!IMPORTANT]
>
>Cette approche ne couvre que la version principale. Elle n’inclut aucun des fichiers plus petits qui peuvent exister.

## Étapes suivantes

Ce document couvrait les limites de lʼutilisation de la SRI avec des balises et les étapes nécessaires pour lʼintégrer dans les déploiements de version de bibliothèque, en dépit de ces limites. Si ce nʼest déjà fait, il est fortement recommandé de lire le guide sur les [CSP et les balises](./content-security-policy.md) pour découvrir une autre option de sécurité.
