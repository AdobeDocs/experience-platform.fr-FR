---
title: Mesure du volume total de données
description: Découvrez la nouvelle mesure Volume total de données et comment elle remplace la mesure de richesse de profil moyenne précédente.
hide: true
hidefromtoc: true
source-git-commit: 9aba85d4e5a481b0eff53e1d87311c395934f585
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---


# Mesure Volume total de données

À compter du 24 septembre 2024, la mesure Volume total de données remplacera la mesure précédente de Richesse moyenne du profil.

Le volume total de données représente la quantité totale de données disponibles pour le profil client en temps réel de Adobe Experience Platform à utiliser dans les workflows d’engagement. Cette valeur équivaut à la mesure Audience adressable multipliée par la Richesse moyenne du profil.

## Questions fréquentes {#faq}

La section suivante répertorie les questions fréquentes sur cette mise à jour.

### Pourquoi ce changement a-t-il été fait ?

Cette modification a été apportée pour simplifier le processus de conformité aux mesures de droits de licence. Nous avons souvent entendu des clients dire qu’ils trouvent la Richesse moyenne du profil difficile à comprendre et à gérer. Grâce à ce changement, nous espérons que vous pourrez mieux comprendre et gérer votre utilisation sous licence de Real-time Customer Profile.

### Cette modification de la mesure change-t-elle mes droits de banque de profils ?

Non. Le droit de votre banque de profils restera le même qu’auparavant, puisque le volume total de données est équivalent à l’audience adressable multipliée par votre richesse moyenne de profil.

### Cette modification affecte-t-elle les modules de droits que j’ai achetés ?

Non. Vous bénéficierez toujours des avantages des modules de droits que vous avez précédemment achetés.

### Comment se fait-il qu’une valeur différente s’affiche pour mon volume total de données par rapport aux droits de ma banque de profils ?

Le volume total de données représente la quantité **totale** de données disponibles pour Profile à utiliser dans les workflows d’engagement. La mesure a été mise à jour pour être plus déterministe et plus explicable. La plupart des utilisateurs ne doivent **pas** voir un changement significatif entre leur volume total de données et le stockage total de leur profil. Si vous avez des questions, veuillez soumettre un ticket à votre représentant du service clientèle.

### Dois-je recréer mes modifications pour continuer à gérer la richesse moyenne de mon profil ?

Non. Toutes les actions, telles que le filtrage, la désactivation du profil pour les jeux de données, ainsi que la configuration de l’expiration des événements d’expérience et de l’expiration des données du profil pseudonyme continueront à jouer un rôle dans la gestion du volume total de données.

### Pourquoi le fichier que j’ai ingéré dans l’environnement de test a-t-il une taille différente de celle du volume total de données ?

Profile optimise les données pour un traitement rapide afin d’exécuter les workflows de personnalisation et d’engagement pour lesquels le système est conçu. La taille du fichier côté client peut être différente du volume total de données en raison de facteurs tels que le type de codage, la compression et le format.

### Cette modification s’applique-t-elle aux SKU ayant une limite partagée pour Profile et pour le lac de données ?

Les clients qui utilisent des SKU ayant partagé la richesse moyenne du profil entre Profile et le lac de données continueront à voir la mesure Total du stockage consommé et **not** verront la mesure Richesse moyenne du profil .
