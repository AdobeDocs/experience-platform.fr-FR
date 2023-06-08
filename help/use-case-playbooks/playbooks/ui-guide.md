---
solution: Experience Platform
title: Guide de l’interface utilisateur des livres de lecture
description: Découvrez comment utiliser l’interface utilisateur de l’Experience Platform pour afficher et activer les livres de lecture.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 2%

---


# (Version bêta) Comment activer et réutiliser un manuel de lecture

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Pour utiliser un manuel, accédez à **[!UICONTROL Cas d’utilisation des classeurs] > [!UICONTROL Livres]**. Parcourez et utilisez les différentes options de recherche et de filtrage de la page pour sélectionner et commencer à utiliser un playbook spécifique.

## Recherche et filtrage {#search-and-filter}

Utilisez la fenêtre de recherche et les filtres disponibles sur la page pour trouver le playbook approprié à votre cas d’utilisation.

Vous pouvez, par exemple, filtrer les playbooks que vous utilisez en fonction de l’étape dans l’entonnoir marketing que vous souhaitez cibler : conversion, engagement ou rétention. Vous pouvez également filtrer les playbooks affichés selon le secteur dans lequel vous vous trouvez ou le droit au produit auquel vous avez accès : Adobe Journey Optimizer ou la plateforme de données clients en temps réel.

![Filtrage des classeurs par entonnoir marketing, secteur industriel ou produit](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

Vous pouvez également utiliser la fonctionnalité de recherche pour trouver le playbook approprié. Vous trouverez ci-dessous un exemple de la manière de trouver un playbook qui vous aide à interagir avec les utilisateurs qui ont peut-être abandonné leur panier.

![Contactez les utilisateurs qui ont peut-être abandonné leur panier.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Vous pouvez également filtrer les playbooks disponibles selon les canaux que vous prévoyez d’utiliser pour atteindre vos clients, comme vous pouvez le voir ci-dessous :

![Filtrage par canal](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Testez les options de recherche et de filtres et recherchez le playbook approprié.

## Affichage du manuel et génération de ressources {#view-playbook-generate-assets}

Avant de vous connecter à un playbook et de créer des instances de celui-ci, vous devez l’examiner pour vous assurer qu’il correspond à vos besoins. Pour vous aider à mieux comprendre les cas d’utilisation qu’ils couvrent, tous les playbooks contiennent les sections répertoriées ci-dessous. Lorsque vous êtes prêt à continuer et à générer des ressources, sélectionnez **[!UICONTROL Créer une instance]**.

### Mindmap {#mindmap}

Utilisez la section carte mentale d’un manuel de lecture pour comprendre les étapes du processus que ce dernier peut vous aider à résoudre. Visualisez le flux de la manière dont tous les objets générés peuvent vous aider à réaliser le cas d’utilisation, du point de vue de la personne ciblée dans le cas d’utilisation.

La carte mentale commence par une définition de qui est atteint dans le parcours utilisateur et décrit à chaque étape si quelque chose est diffusé par Adobe, comme un nouveau message ou un rappel, ou s’il s’agit d’une chose que la personne ciblée a faite qui déclenche le message ou l’événement suivant.

![La carte de l&#39;esprit des livres de jeu est mise en évidence.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Résumé {#summary}

Inspect de la section de résumé pour identifier les ressources qui sont générées une fois que vous avez créé des instances à partir du playbook. Les ressources générées pour chaque playbook sont adaptées au cas d’utilisation activé par le playbook. Obtenez plus d’informations ci-dessous sur tous les éléments de la section de résumé.

| Élément | Description |
---------|----------|
| **[!UICONTROL Public cible]** | Décrit les personnes que vous souhaitez atteindre via ce manuel de cas d’utilisation. |
| **[!UICONTROL Canaux marketing]** | Décrit les canaux utilisés pour atteindre les personnes ciblées dans le playbook. |
| **[!UICONTROL Ressources techniques]** | Liste des ressources techniques générées après la création d’instances du manuel de lecture. Les ressources générées diffèrent par playbook, selon le cas d’utilisation. Certains playbooks peuvent générer des schémas, des segments et des parcours. D’autres peuvent générer des destinations. Reportez-vous à la section [Présentation des ressources générées](#understand-assets) pour plus d’informations sur l’utilisation et la réutilisation des ressources générées, reportez-vous à la section ci-dessous. |

{style="table-layout:auto"}

![Résumé du manuel mis en surbrillance](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instances {#instances}

Faites défiler jusqu’à la section instances pour obtenir un aperçu des instances de ce manuel que vous ou les membres de votre équipe avez déjà créées. Vous pouvez utiliser différents contrôles pour trier et filtrer les instances affichées, par exemple pour ne voir que celles que vous avez créées. Vous pouvez également consulter diverses informations sur chaque instance, comme indiqué ci-dessous.

| Élément | Description |
|---------|----------|
| **[!UICONTROL Nom]** | Nom de l’instance basé sur le playbook. Vous pouvez personnaliser le nom et la description d’une instance. Lisez la section ci-dessous sur [modification des métadonnées d’instance](#edit-instance-metadata) pour plus d’informations. |
| **[!UICONTROL Statut]** | Indique le statut de l’instance. A **[!UICONTROL submit]** est prête à être utilisée. |
| **[!UICONTROL Créé]** | Indique le moment où l’instance a été créée. |
| **[!UICONTROL Créée par]** | Indique qui a créé l’instance. |
| **[!UICONTROL Dernière modification]** | Indique la date de la dernière modification de l’instance. |

{style="table-layout:auto"}

![L’instance du manuel est mise en surbrillance.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Activation du playbook {#enable-playbook}

Lorsque vous êtes prêt à poursuivre un playbook et à créer une instance, sélectionnez **[!UICONTROL Créer une instance]** pour poursuivre le playbook et générer des ressources techniques.

![Créez une instance d’un playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Cette action génère plusieurs ressources que vous pouvez utiliser pour réaliser le cas d’utilisation décrit par le playbook.

![Vue Playbook des ressources générées après activation.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilisez les commandes de configuration pour modifier les noms et descriptions des instances. {#edit-instance-metadata}

Après avoir créé une instance basée sur un playbook, vous pouvez la personnaliser pour la distinguer des autres instances créées à partir du même playbook. Sélectionnez le contrôle de configuration comme illustré ci-dessous. Modifiez le nom, la description et les notes, puis sélectionnez **[!UICONTROL Enregistrer]** lorsque vous avez terminé.

![Modifiez le nom et la description d’une instance.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Présentation des ressources générées {#understand-assets}

>[!IMPORTANT]
>
>Pas besoin de vous inquiéter ! C&#39;est un espace sûr pour expérimenter et vous ne pouvez rien casser. Aucune donnée n’est encore associée aux ressources que vous créez. Vous devez d’abord ingérer des données pour réaliser les cas d’utilisation.

Il est important de comprendre que les ressources générées diffèrent selon le cas d’utilisation que vous activez :

* Différentes ressources sont générées pour différents types de livres de lecture. Ces ressources sont créées spécifiquement pour le cas d’utilisation réalisé via le manuel de lecture. Par exemple, un playbook génère un schéma, un segment, un parcours et des messages. Un autre playbook génère un schéma, un segment et une destination vers lesquels activer les données.
* Les ressources elles-mêmes diffèrent d’un playbooks à l’autre. Par exemple, pour la variable **[!UICONTROL Envoyer Un Message D’Anniversaire Aux Invités]** playbook, l’audience créée comporte la règle `birthday=today AND year=any`.

Pour illustrer un exemple, pour le **[!UICONTROL Panier abandonné : Marchandisage]** playbook, vous pouvez constater qu’un parcours spécifique est créé et contient les messages créés pour ce cas d’utilisation.

![Parcours créé à partir du scénario d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Utilisation et modification des ressources générées {#use-and-edit-assets}

Lorsque vous explorez les ressources qui sont générées après avoir créé une instance d’un playbook, vous pouvez modifier l’une des ressources créées.

Si vous ou un membre de votre équipe créez une autre instance du playbook, les ressources modifiées sont conservées et de nouvelles ressources sont créées pour la nouvelle instance du playbook.

Le comportement décrit ci-dessus est vrai pour toutes les ressources qui sont créées, à l’exception des schémas. Dans le cas des schémas, les nouveaux schémas ne sont pas créés lorsqu’une nouvelle instance d’un playbook est créée. Vous allez donc utiliser le schéma modifié d’une autre instance du playbook dans l’instance nouvellement créée.

>[!TIP]
>
>Testez dans l’environnement de test de développement et passez en production lorsque vous êtes prêt.
>
>Une fois les objets générés, vous pouvez continuer à les tester dans les environnements de test de développement en ajoutant des données. Vous pouvez tester les ressources tant que vous le souhaitez dans l’environnement de test de développement et vous pouvez répliquer la logique des ressources (définitions de segment, parcours, schémas, etc.) dans l’environnement de test de production lorsque vous êtes prêt.

### Réutilisation des classeurs {#reuse-playbooks}

En créant plusieurs instances du même playbook, vous pouvez mettre en oeuvre le même cas d’utilisation ultérieurement, sans modifier les détails de votre mise en oeuvre précédente du cas d’utilisation.

### Partage du playbook et des ressources générées avec d’autres membres de l’équipe {#share-playbook}

Vous pouvez partager l’instance et les ressources générées avec d’autres membres de l’équipe. Pour ce faire, copiez le lien URL du navigateur et partagez-le avec votre équipe afin de leur donner un aperçu des ressources générées.

![URL mise en surbrillance dans une vue playbook de cas d’utilisation.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Étapes suivantes {#next-steps}

En lisant ce guide de l’interface utilisateur, vous savez maintenant comment interpréter les différentes sections d’un manuel et comment utiliser les ressources générées après la création d’une instance d’un manuel. Vous pouvez ensuite parcourir le catalogue des livres de jeu pour trouver le manuel adapté à votre cas d’utilisation et lire le guide de dépannage si vous rencontrez des erreurs.