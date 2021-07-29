---
title: Supprimer des ressources d’une bibliothèque
description: Découvrez comment supprimer des ressources d’une bibliothèque de balises.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 87%

---

# Supprimer des ressources d’une bibliothèque

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Lorsque vous ne souhaitez plus qu’une ressource ait de l’effet dans une version, vous devez la supprimer de la bibliothèque qui contient cette ressource et créer une version.

>[!IMPORTANT]
>
>Les ressources des bibliothèques sont interdépendantes. La suppression d’une ressource d’une version peut modifier le comportement des autres ressources de la version.

Le processus de suppression fonctionne légèrement différemment selon l’état dans lequel se trouve la bibliothèque.

## Bibliothèques de développement

Il est possible de manipuler directement des ressources de bibliothèques de développement.

1. Ouvrez la bibliothèque.
1. Supprimez la ressource.
1. Enregistrez la bibliothèque.
1. Créez la bibliothèque.

## Bibliothèques envoyées et approuvées

Les ressources figurant dans les bibliothèques envoyées ou approuvées ne peuvent pas être manipulées directement. Vous devrez déplacer à nouveau la bibliothèque vers l’état Development (Développement).

1. Rejetez la bibliothèque (la renvoyer vers Development (Développement)).
1. Suivez les étapes décrites dans la section « Bibliothèques de développement » ci-dessus pour supprimer des ressources des bibliothèques de développement.

## Bibliothèques de production

La suppression de ressources d’une bibliothèque de production est le cas le plus complexe. En effet, vous ne pouvez pas manipuler les ressources de bibliothèque dans cet état ni déplacer à nouveau ces bibliothèques vers l’état Development (Développement).

Vous devez plutôt désactiver la ressource. Cette désactivation est une modification que vous ajoutez ensuite à une bibliothèque de développement comme n’importe quelle autre modification. Une fois cette modification mise en production, la ressource est déplacée depuis votre bibliothèque de production.

1. Désactivez la ressource.
   1. Sélectionnez la ressource dans la vue de la liste.
   1. Sélectionnez **[!UICONTROL Désactiver]**.
1. Créez une bibliothèque de développement.
1. Ajoutez la `latest` version de la ressource désactivée.
1. Enregistrez et générez.
1. Suivez votre processus habituel pour promouvoir des bibliothèques vers Production.
1. Publiez dans Production pour supprimer la ressource.
