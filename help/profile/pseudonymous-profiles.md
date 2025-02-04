---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;jeu de données;durée de vie;ttl;durée-de-vie;pseudonyme;profils pseudonymes;expiration des données;expiration;
solution: Experience Platform
title: Expiration des données de profils pseudonymes
description: Ce document fournit des conseils généraux sur la configuration de l’expiration des données de profils pseudonymes dans Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: 9d38fdae0fc65048d02a4337375004edafedd1b6
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 65%

---

# Expiration des données de profils pseudonymes

Dans Adobe Experience Platform, vous pouvez configurer les délais d’expiration des données des profils pseudonymes, ce qui vous permet de supprimer automatiquement des données de la banque de profils qui ne sont plus valides ou utiles pour vos cas d’utilisation.

## Profil pseudonyme {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Qu&#39;est-ce qu&#39;un profil pseudonyme ?"
>abstract="Un profil pseudonyme est un profil qui possède un espace de noms d’identité pseudonyme ou inconnu, ou un profil qui n’a eu aucune activité pendant une période donnée."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Expiration des données de profils pseudonymes"
>abstract="L’expiration des données de profils pseudonymes représente le nombre de jours pendant lesquels un profil pseudonyme reste dans Adobe Experience Platform avant d’être supprimé."

Un profil est pris en compte pour l’expiration des données pseudonymes s’il répond aux conditions suivantes :

- Les espaces de noms d’identité du profil assemblé correspondent à l’espace de noms d’identité pseudonyme ou inconnu indiqué par le client ou la cliente.
   - Par exemple, si l’espace de noms d’identité du profil est `ECID`, `GAID` ou `AAID`. Le profil assemblé ne comporte aucun identifiant provenant d’un autre espace de noms d’identité. Dans cet exemple, un profil assemblé ne possède **pas** d’identité d’e-mail ou de gestion de la relation client.
- Aucune activité n’a eu lieu au cours d’une période définie par l’utilisateur ou l’utilisatrice. L’activité répertorie les événements d’expérience ingérés ou les mises à jour des attributs de profil initiées par le client ou la cliente.
   - Il s’agit, par exemple, d’un nouvel événement de page vue ou d’une mise à jour d’un attribut de page. Cependant, la mise à jour de l’appartenance à une audience non initiée par l’utilisateur ou l’utilisatrice n’est **pas** considérée comme une activité. Actuellement, pour calculer l’expiration des données, le suivi au niveau du profil est basé sur l’heure de l’événement pour les événements d’expérience et sur l’heure d’ingestion pour les attributs de profil.

## Accéder à {#access}

L’expiration des données de profils pseudonymes ne peut pas être configurée via l’interface utilisateur ou les API Platform. Pour activer cette fonctionnalité, contactez l’assistance clientèle. Lorsque vous contactez l’assistance, incluez les informations suivantes :

- Les espaces de noms d’identité à prendre en compte lors des suppressions des profils pseudonymes.
   - Par exemple : `ECID` uniquement, `AAID` uniquement ou une combinaison d’`ECID` et d’`AAID`.
- Le temps d’attente avant la suppression d’un profil pseudonyme. Le temps d’attente recommandé pour les clients et clientes est de 14 jours. Cependant, cette valeur peut varier en fonction du cas d’utilisation.

## Questions fréquentes {#faq}

Consultez les questions fréquentes sur l’expiration des données de profils pseudonymes dans la section suivante :

### En quoi l’expiration des données de profils pseudonymes diffère-t-elle de l’expiration des données d’événements d’expérience ?

L’expiration des données de profils pseudonymes et l’expiration des données d’événements d’expérience sont des fonctionnalités complémentaires.

#### Granularité

L’expiration des données de profils pseudonymes s’applique à la **sandbox**. Par conséquent, l’expiration des données affecte tous les profils de la sandbox.

L’expiration des données d’événements d’expérience s’applique au **jeu de données**. Par conséquent, chaque jeu de données peut avoir un paramètre d’expiration de données différent.

#### Types d’identité

L’expiration des données de profils pseudonymes prend **uniquement** en compte les profils dont les graphiques d’identités contiennent des espaces de noms d’identité sélectionnés par le client ou la cliente, tels que `ECID`, `AAID` ou d’autres types de cookies. Si le profil contient **un** espace de noms d’identité supplémentaire qui ne figurait **pas** dans la liste sélectionnée par le client ou la cliente, le profil n’est **pas** supprimé.

L’expiration des données d’événements d’expérience supprime les événements **uniquement** sur la base de la date et de l’heure de l’enregistrement de l’événement. Les espaces de noms d’identité inclus sont **ignorés** pour les besoins de l’expiration.

#### Éléments supprimés

L’expiration des données de profils pseudonymes supprime les enregistrements d’événement **et** de profil. Les données de classe de profil sont donc également supprimées.

L’expiration des données d’événements d’expérience supprime **uniquement** les événements et **non** les données de la classe de profil. Les données de classe de profil ne sont supprimées que lorsque les données de **tous** les jeux de données sont supprimées et qu’il n’existe **aucun** enregistrement de classe de profil restant pour le profil.

### Comment utiliser l’expiration des données de profils pseudonymes en parallèle avec l’expiration des données d’événements d’expérience ?

L’expiration des données de profils pseudonymes et l’expiration des données d’événements d’expérience peuvent être utilisées pour se compléter.

Nous vous recommandons **toujours** de configurer l’expiration des données d’événements d’expérience dans vos jeux de données, en fonction de vos besoins de conservation des données sur votre clientèle existante. Une fois l’expiration des données d’événements d’expérience configurée, vous pouvez utiliser l’expiration des données de profils pseudonymes pour supprimer automatiquement les profils pseudonymes. En règle générale, la période d’expiration des données des profils pseudonymes est inférieure à celle des événements d’expérience.

Dans un cas d’utilisation standard, définissez l’expiration des données d’événements d’expérience en fonction des valeurs de vos données utilisateur connues. Définissez ensuite l’expiration des données de profils pseudonymes sur une durée beaucoup plus courte, afin de limiter l’impact des profils pseudonymes sur la conformité de votre licence Platform.

### À qui s’adresse la fonctionnalité d’expiration des données de profils pseudonymes ?

- Si vous utilisez le SDK Web pour envoyer directement des données à Platform.
- Si vous disposez d’un site web qui accueille en masse des clients et clientes non authentifié(e)s.
- Si vos jeux de données contiennent un nombre trop élevé de profils, en raison d’un espace de noms d’identité basé sur des cookies anonymes.
   - Pour le vérifier, utilisez le rapport de chevauchement des espaces de noms d’identité. Vous trouverez plus d’informations sur ce rapport dans la [section de rapport de chevauchement des identités](./api/preview-sample-status.md#identity-overlap-report) du guide de l’API sur les exemples de statut de prévisualisation.

### Quelles informations importantes dois-je connaître avant d’utiliser l’expiration des données de profils pseudonymes ?

- L’expiration des données de profils pseudonymes s’exécute au niveau du **sandbox**. Vous pouvez appliquer différentes configurations pour les sandbox de production et de développement.
- Une fois la fonctionnalité activée, la suppression des profils est **permanente**. Vous ne pouvez **pas** annuler la suppression ou restaurer un profil supprimé.
- Il ne s’agit **pas** d’une tâche de suppression ponctuelle. L’expiration des données de profils pseudonymes s’exécute une fois par jour et supprime les profils qui correspondent aux données saisies par le client ou la cliente.
- **Tous** les profils définis comme des profils pseudonymes sont sujets à l’expiration des données de profils pseudonymes. **Peu importe** si le profil est uniquement un événement d’expérience ou ne contient que des attributs de profil.
- La suppression se produit **uniquement** au niveau du profil. Il se peut que le service d’identités continue à afficher les identités supprimées dans le graphique si le profil possède plusieurs identités pseudonymes associées (telles que `AAID` et `ECID`). Nous apporterons une solution à cette incohérence dans une prochaine mise à jour.
- L’expiration des données de profils pseudonymes n’est **pas** immédiate et peut prendre jusqu’à trois jours.

### Comment l’expiration des données de profils pseudonymes interagit-elle avec les mécanismes de sécurisation pour les données Identity Service ?

- Le système de suppression « premier entré, premier sorti »](../identity-service/guardrails.md) d’Identity Service [ supprimer les ECID du graphique d’identités, qui sont stockés dans Identity Service.
- Si ce comportement de suppression entraîne le stockage d’un profil ECID uniquement dans le profil client en temps réel (magasin de profils), l’expiration des données de profils pseudonymes supprime ce profil du magasin de profils.
