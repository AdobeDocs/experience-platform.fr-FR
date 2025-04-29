---
keywords: Experience Platform;accueil;rubriques populaires;jeu de données;jeu de données;durée de vie;ttl;durée-de-vie;pseudonyme;profils pseudonymes;expiration des données;expiration;
solution: Experience Platform
title: Expiration des données de profils pseudonymes
description: Ce document fournit des conseils généraux sur la configuration de l’expiration des données de profils pseudonymes dans Adobe Experience Platform.
exl-id: e8d31718-0b50-44b5-a15b-17668a063a9c
source-git-commit: aeb9d6636f0d843bf13d09bcb4c12754e2890046
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 51%

---

# Expiration des données de profils pseudonymes

Dans Adobe Experience Platform, vous pouvez configurer les délais d’expiration des données des profils pseudonymes, ce qui vous permet de supprimer automatiquement des données de la banque de profils qui ne sont plus valides ou utiles pour vos cas d’utilisation.

## Profil pseudonyme {#pseudonymous-profile}

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile"
>title="Qu’est-ce qu’un profil pseudonyme ?"
>abstract="Un profil pseudonyme est un profil dont l’espace de noms d’identité est pseudonyme ou inconnu, ou un profil pour lequel aucune activité n’a eu lieu pendant une période donnée."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_profile_pseudonymousprofile_dataexpiration"
>title="Expiration des données de profils pseudonymes"
>abstract="L’expiration des données de profils pseudonymes représente le nombre de jours pendant lesquels un profil pseudonyme reste dans Adobe Experience Platform avant d’être supprimé. Cette valeur doit être définie sur au moins 1. Notez que la suppression du profil pseudonyme peut prendre jusqu’à trois jours."

Un profil est pris en compte pour l’expiration des données pseudonymes s’il répond aux conditions suivantes :

- Les espaces de noms d’identité du profil assemblé correspondent à l’espace de noms d’identité pseudonyme ou inconnu indiqué par le client ou la cliente.
   - Par exemple, si l’espace de noms d’identité du profil est `ECID`, `GAID` ou `AAID`. Le profil assemblé ne comporte aucun identifiant provenant d’un autre espace de noms d’identité. Dans cet exemple, un profil assemblé ne possède **pas** d’identité d’e-mail ou de gestion de la relation client.
- Aucune activité n’a eu lieu au cours d’une période définie par l’utilisateur ou l’utilisatrice. L’activité répertorie les événements d’expérience ingérés ou les mises à jour des attributs de profil initiées par le client ou la cliente.
   - Il s’agit, par exemple, d’un nouvel événement de page vue ou d’une mise à jour d’un attribut de page. Cependant, la mise à jour de l’appartenance à une audience non initiée par l’utilisateur ou l’utilisatrice n’est **pas** considérée comme une activité. Actuellement, pour calculer l’expiration des données, le suivi au niveau du profil est basé sur l’heure de l’événement pour les événements d’expérience et sur l’heure d’ingestion pour les attributs de profil.

## Accès {#access}

>[!AVAILABILITY]
>
>Pour accéder à cette fonctionnalité, vous devez disposer des autorisations suivantes :
>
>- Gérer les paramètres de profil
>- Affichage des profils
>
>L&#39;autorisation **Gérer les paramètres de profil** permet de définir les expirations des données, tandis que l&#39;autorisation **Afficher les profils** permet d&#39;afficher les expirations des données.
>
>Vous trouverez plus d’informations sur les autorisations dans Experience Platform dans la [présentation du contrôle d’accès](../access-control/home.md#permissions).

Pour ajouter l’expiration des données de profils pseudonymes à votre organisation, accédez au tableau de bord Profil et sélectionnez **[!UICONTROL Paramètres]**.

![Le bouton Paramètres du tableau de bord du profil est mis en surbrillance.](./images/pseudonymous-profiles/profile-settings.png)

La fenêtre contextuelle [!UICONTROL Paramètres du profil] s’affiche. Sur cette fenêtre contextuelle, vous pouvez définir le nombre de jours d’expiration des données de profils pseudonymes, ainsi que l’espace de noms d’identité utilisé pour l’expiration des données.

Pour les sandbox de production, l’expiration par défaut des données de profil pseudonymes est de 14 jours, avec une durée minimale de 1 jour et une durée maximale de 365 jours. Pour les sandbox de développement, l’expiration par défaut des données de profil pseudonymes est de 3 jours, avec un minimum de 1 jour et un maximum de 365 jours.

Sélectionnez **[!UICONTROL Appliquer]** pour enregistrer vos paramètres d’expiration des données.

![Fenêtre contextuelle permettant d’ajouter l’expiration des données de profils pseudonymes aux profils de votre organisation. Le bouton Appliquer est mis en surbrillance.](./images/pseudonymous-profiles/profile-settings-data-expiry.png){width="800" zoomable="yes"}

## Questions fréquentes {#faq}

Consultez les questions fréquentes sur l’expiration des données de profils pseudonymes dans la section suivante :

### En quoi l’expiration des données de profils pseudonymes diffère-t-elle de l’expiration des données d’événements d’expérience ?

+++ Réponse

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

+++

### Comment utiliser l’expiration des données de profils pseudonymes en parallèle avec l’expiration des données d’événements d’expérience ?

+++ Réponse

L’expiration des données de profils pseudonymes et l’expiration des données d’événements d’expérience peuvent être utilisées pour se compléter.

Nous vous recommandons **toujours** de configurer l’expiration des données d’événements d’expérience dans vos jeux de données, en fonction de vos besoins de conservation des données sur votre clientèle existante. Une fois l’expiration des données d’événements d’expérience configurée, vous pouvez utiliser l’expiration des données de profils pseudonymes pour supprimer automatiquement les profils pseudonymes. En règle générale, la période d’expiration des données des profils pseudonymes est inférieure à celle des événements d’expérience.

Dans un cas d’utilisation standard, définissez l’expiration des données d’événements d’expérience en fonction des valeurs des données utilisateur connues. Définissez ensuite l’expiration des données de profils pseudonymes sur une durée beaucoup plus courte, afin de limiter l’impact des profils pseudonymes sur la conformité de votre licence Experience Platform.

+++

### Pour quels types de cas d’utilisation dois-je utiliser l’expiration des données de profils pseudonymes ?

+++ Réponse

- Si vous utilisez Web SDK pour envoyer directement des données à Experience Platform.
- Si vous disposez d’un site web qui accueille en masse des clients et clientes non authentifié(e)s.
- Si vos jeux de données contiennent un nombre trop élevé de profils, en raison d’un espace de noms d’identité basé sur des cookies anonymes.
   - Pour le vérifier, utilisez le rapport de chevauchement des espaces de noms d’identité. Vous trouverez plus d’informations sur ce rapport dans la [section de rapport de chevauchement des identités](./api/preview-sample-status.md#identity-overlap-report) du guide de l’API sur les exemples de statut de prévisualisation.

+++

### Quelles informations importantes dois-je connaître avant d’utiliser l’expiration des données de profils pseudonymes ?

+++ Réponse

- L’expiration des données de profils pseudonymes s’exécute au niveau du **sandbox**. Vous pouvez appliquer différentes configurations pour les sandbox de production et de développement.
- Une fois la fonctionnalité activée, la suppression des profils est **permanente**. Vous ne pouvez **pas** annuler la suppression ou restaurer un profil supprimé.
- Il ne s’agit **pas** d’une tâche de suppression ponctuelle. L’expiration des données de profils pseudonymes s’exécute une fois par jour et supprime les profils qui correspondent aux données saisies par le client ou la cliente.
- **Tous** les profils définis comme des profils pseudonymes sont sujets à l’expiration des données de profils pseudonymes. **Peu importe** si le profil est uniquement un événement d’expérience ou ne contient que des attributs de profil.
- La suppression se produit **uniquement** au niveau du profil. Il se peut que le service d’identités continue à afficher les identités supprimées dans le graphique si le profil possède plusieurs identités pseudonymes associées (telles que `AAID` et `ECID`). Nous apporterons une solution à cette incohérence dans une prochaine mise à jour.
- L’expiration des données de profils pseudonymes n’est **pas** immédiate et peut prendre jusqu’à trois jours.

+++

### Comment l’expiration des données de profils pseudonymes interagit-elle avec les mécanismes de sécurisation pour les données Identity Service ?

+++ Réponse

- Le système de suppression « premier entré, premier sorti »](../identity-service/guardrails.md) d’Identity Service [ supprimer les ECID du graphique d’identités, qui sont stockés dans Identity Service.
- Si ce comportement de suppression entraîne le stockage d’un profil ECID uniquement dans le profil client en temps réel (magasin de profils), l’expiration des données de profils pseudonymes supprime ce profil du magasin de profils.

+++

## Étapes suivantes

Vous êtes arrivé au bout de ce guide. À présent, vous savez comment afficher et créer des expirations de données de profils pseudonymes. Pour plus d’informations sur la gestion des données dans Experience Platform dans son ensemble, consultez le [ Guide des bonnes pratiques relatives aux droits de licence de gestion des données ](../landing/license-usage-and-guardrails/data-management-best-practices.md).

