---
title: Interface utilisateur des paramètres d’identité
description: Découvrez comment utiliser l’interface utilisateur des paramètres d’identité.
badge: Version bêta
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 04b04807196bb5902e398403612429eae0de3988
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 2%

---

# Interface utilisateur des paramètres d’identité

>[!AVAILABILITY]
>
>Les règles de liaison de graphiques d’identités sont actuellement en version bêta. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Les paramètres d’identité sont une fonctionnalité de l’interface utilisateur du service Adobe Experience Platform Identity que vous pouvez utiliser pour désigner des espaces de noms uniques et configurer la priorité des espaces de noms.

Lisez ce guide pour savoir comment configurer vos paramètres d’identité dans l’interface utilisateur.

## Conditions préalables

Lisez les documents suivants avant de commencer à utiliser les paramètres d’identité :

* [Guide de configuration des règles de liaison de graphique d’identités](./configuration.md)
* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Priorité d’espace de noms](./namespace-priority.md)
* [Simulation graphique](./graph-simulation.md)

## Configuration des paramètres d’identité

Pour accéder aux paramètres d’identité, accédez à l’espace de travail Identity Service dans l’interface utilisateur de Adobe Experience Platform, puis sélectionnez **[!UICONTROL Paramètres]**.

![Bouton des paramètres d&#39;identité sélectionné.](../images/rules/identities-ui.png)

La page des paramètres d’identité est divisée en deux sections : [!UICONTROL Espaces de noms de personne] et [!UICONTROL Espaces de noms d’appareil ou de cookie]. Les espaces de noms de personne sont des identifiants pour des individus uniques. Il peut s’agir d’identifiants multi-appareils, d’adresses électroniques et de numéros de téléphone. Les espaces de noms d’appareil ou de cookie sont des identifiants pour les appareils et les navigateurs web et ne peuvent pas avoir une priorité plus élevée que les espaces de noms de personne. Vous ne pouvez pas non plus désigner un espace de noms d’appareil ou de cookie comme espace de noms unique.

### Configurer la priorité des espaces de noms

Pour configurer la priorité des espaces de noms, sélectionnez un espace de noms dans le menu des paramètres d’identité, puis faites glisser-le et déposez-le dans l’ordre de votre choix. Placez un espace de noms plus haut sur la liste pour lui donner une priorité plus élevée, et inversement, placez un espace de noms plus bas sur la liste pour lui donner une priorité plus faible. L’espace de noms ayant la priorité la plus élevée doit également être désigné comme un espace de noms unique.

![Espace de travail des paramètres d’identité avec un espace de noms de personne en surbrillance.](../images/rules/namespace-priority.png)

### Désigner votre espace de noms unique

Pour désigner un espace de noms unique, cochez la case [!UICONTROL Unique per graph] correspondant à cet espace de noms. Vous pouvez sélectionner plusieurs espaces de noms uniques pour la configuration des paramètres d’identité.

![Deux espaces de noms sélectionnés et définis comme uniques.](../images/rules/unique-namespace.png)

Une fois vos espaces de noms uniques définis, les graphiques ne pourront plus avoir plusieurs identités contenant un espace de noms unique. Par exemple, si vous avez désigné CRMID comme espace de noms unique, un graphique ne peut avoir qu’une seule identité avec l’espace de noms CRMID. Pour plus d’informations, consultez la [présentation de l’algorithme d’optimisation des identités](./identity-optimization-algorithm.md#unique-namespace).

Lorsque vos configurations sont terminées, sélectionnez **[!UICONTROL Suivant]**. Un message de confirmation s’affiche. Utilisez cette opportunité pour vérifier que vos configurations sont correctes, puis sélectionnez **[!UICONTROL Terminer]**.

![ La page de validation avec l’option Terminer mise en surbrillance.](../images/rules/finish.png)

Un message d’avertissement s’affiche, indiquant que les graphiques existants ne seront affectés par l’algorithme graphique que si les graphiques sont mis à jour **après avoir enregistré vos paramètres** et que l’identité principale des fragments d’événement sur Real-time Customer Profile ne sera pas mise à jour même après les modifications de la priorité de l’espace de noms. De plus, vous êtes averti que la prise en compte de vos nouveaux paramètres prendra jusqu’à **six heures**. Pour confirmer, saisissez le nom de votre environnement de test, puis sélectionnez **[!UICONTROL Confirmer]**.

![Fenêtre de confirmation qui affiche un avertissement de retard de six heures avant le traitement des configurations.](../images/rules/confirm-settings.png)

## Étapes suivantes

Vous avez maintenant configuré les priorités de vos espaces de noms et désigné vos espaces de noms uniques à l’aide de la page d’interface utilisateur des paramètres d’identité. Pour plus d’informations, consultez la [présentation des règles de liaison de graphiques d’identités](./overview.md).
