---
title: Mesure du volume total de données
description: Découvrez la nouvelle mesure Volume total de données et comment elle remplace la mesure de richesse du profil moyen précédente.
exl-id: 4b21d25c-b82b-4d1a-83ce-b510f02fd160
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Mesure Volume total de données

Le volume total de données remplace la mesure précédente Richesse moyenne du profil comme un moyen plus simple et plus explicable de suivre l’utilisation par rapport aux droits de votre banque de profils.

**Volume total de données = Audience adressable × Richesse de profil moyenne**

Cette mesure reflète la quantité totale de données stockées dans le **magasin de profils** et disponibles pour une utilisation dans les workflows d’engagement du profil client en temps réel. Il n’inclut **pas** de données stockées dans le **lac de données**. Cette modification offre une vue plus ciblée et plus transparente des données relatives à la personnalisation et à l’engagement basés sur les profils.

## Questions fréquentes {#faq}

La section suivante répertorie les questions fréquentes sur cette mise à jour.

### Pourquoi ce changement a-t-il été apporté ?

Cette modification a été effectuée pour simplifier le processus de mise en conformité avec les mesures de droits de licence. Nous avons souvent entendu des clients dire qu’ils trouvaient la richesse moyenne du profil difficile à comprendre et à gérer. Grâce à cette modification, nous espérons que vous serez en mesure de mieux comprendre et gérer votre utilisation sous licence du profil client en temps réel.

### Cette modification de la mesure modifie-t-elle mes droits de magasin de profils ?

Non. Les droits de votre banque de profils resteront les mêmes qu’auparavant, puisque le volume total de données équivaut à l’audience adressable multipliée par votre richesse moyenne de profil autorisée.

### Cette modification affecte-t-elle les packages de droits que j’ai achetés ?

Non. Vous bénéficierez toujours des avantages des packages de droits que vous avez précédemment achetés.

### Comment se fait-il que je vois une valeur différente pour mon volume total de données par rapport à mes droits de banque de profils ?

Le volume total de données représente la quantité **totale** de données disponible pour que Profile puisse les utiliser dans les workflows d’engagement. La mesure a été mise à jour pour être plus déterministe et explicable. La plupart des utilisateurs ne devraient **pas** voir de changement significatif entre leur volume total de données et leur stockage de profil total. Si vous avez des préoccupations, veuillez envoyer un ticket à votre représentant du service client.

### Comment le volume total de données est-il calculé ? Cela inclut-il le stockage dans le lac de données ?

Le volume total de données est calculé à l’aide de la formule suivante :

**Volume total de données = Audience adressable × Richesse de profil moyenne**

Cette mesure reflète la quantité totale de données stockées dans la banque de profils qui est disponible pour le profil client en temps réel à utiliser dans les workflows d’engagement. Il n’inclut **pas** de données stockées dans le lac de données.

Auparavant, certaines offres héritées utilisaient une mesure « stockage total » qui combinait l’utilisation du magasin de profils et du lac de données. Cependant, le volume total de données est limité au magasin de profils uniquement, ce qui offre une vue plus ciblée des données relatives à l’engagement basé sur les profils.

### Dois-je recréer mes modifications pour continuer à gérer ma richesse moyenne de profil ?

Non. Toutes les actions, telles que le filtrage, la désactivation du profil pour les jeux de données, ainsi que la configuration des expirations d’événements d’expérience et des expirations de données de profils pseudonymes, continueront à jouer un rôle dans la gestion du volume total de données.

### Pourquoi le fichier que j’ai ingéré dans le sandbox est-il d’une taille différente du volume total de données ?

Profile optimise les données pour un traitement rapide afin d’exécuter les workflows de personnalisation et d’engagement pour lesquels le système est conçu. La taille du fichier côté client peut être différente du volume total de données en raison de facteurs tels que le type de codage, la compression et le format.

### Cette modification s’applique-t-elle aux SKU qui ont une limite partagée pour le profil et le lac de données ?

Les clients qui se trouvent sur des SKU qui ont partagé la richesse de profil moyenne entre le profil et le lac de données continueront à voir la mesure Stockage total consommé et **verront pas** mesure Richesse de profil moyenne .
