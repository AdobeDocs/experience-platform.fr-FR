---
title: Améliorations de la composition de l’audience
description: Découvrez les améliorations apportées à la composition de l’audience avec l’enrichissement de l’audience et une activation plus rapide.
hide: true
hidefromtoc: true
source-git-commit: 9c790f0b47161301fa8c02c4afb7edfb925e1499
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Améliorations de la composition de l’audience

Vous avez désormais accès à **deux** améliorations de la composition de l’audience :

- [Enrichissement de l’audience](#audience-enrichment)
- [Activation plus rapide](#faster-activation)

## Enrichissement de l’audience {#audience-enrichment}

L’enrichissement d’audience vous permet de générer le tableau de valeurs qui permettent à vos profils de se qualifier pour l’audience que vous avez créée.

Pour ajouter des enrichissements d’audience à votre composition, sélectionnez le bloc de **[!UICONTROL Audience]** le plus haut dans la zone de travail. Après avoir donné un nom à l’audience, sélectionnez **[!UICONTROL Build rule]** pour ouvrir la zone de travail du créateur de règles.

![Le bloc Audience est mis en surbrillance, ainsi que le bouton Créer une règle.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

La zone de travail du créateur de règles s’affiche. Vous pouvez maintenant créer un critère de filtre pour l’enrichissement de votre audience. Ce critère de filtre **doit** inclut un attribut qui se trouve dans un tableau. L’attribut étant un tableau dépend de la structure de schéma de votre organisation. Après avoir créé vos critères de filtre, sélectionnez **[!UICONTROL Delivery]** dans le panneau de droite.

![La zone de travail du créateur de règles présente un exemple d’audience pouvant avoir des enrichissements. Le bouton Diffusion est également mis en surbrillance.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Sélectionnez le tableau d’objets à utiliser pour l’enrichissement dans la liste du panneau de gauche. S’il n’y a qu’un seul tableau sur le profil, le tableau est automatiquement sélectionné pour vous. Sélectionnez **[!UICONTROL Save]** pour revenir à la composition de l’audience.

<!-- , as well as the fields you want to be used in the enrichment. -->

![L’arborescence du schéma pour l’arborescence d’enrichissement s’affiche.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Dans la composition de l’audience, votre bloc de [!UICONTROL Audience] est désormais de type « [!UICONTROL Rule builder with enhancement] ». Sélectionnez **[!UICONTROL Publish]** pour activer votre audience avec le lot quotidien suivant.

![Le bloc Audience est mis en surbrillance, ce qui indique qu’une audience avec enrichissement est ajoutée.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Détails de comportement et mécanismes de sécurisation

Gardez les détails et mécanismes de sécurisation suivants à l’esprit lors de l’utilisation de l’enrichissement de l’audience :

- Vous ne pouvez utiliser l’enrichissement d’audience que dans les audiences créées dans la composition de l’audience
- Le premier bloc utilisé dans la composition **doit** est une audience basée sur des règles.
- Vous **ne pouvez pas** utiliser d’autres opérations dans la composition.
- Une fois publiée, vous **pouvez pas** la composition sur l’audience basée sur des règles.
   - Vous *pouvez* copier la composition dans un brouillon et modifier le brouillon si vous souhaitez apporter des modifications à la composition de base ou à l’audience basée sur des règles.
- Un seul tableau d’objets **one** peut être utilisé pour générer la payload d’enrichissement dans une seule audience
   - Le tableau de payload peut être imbriqué dans un objet (jusqu’à sept calques dans le schéma de profil), mais **ne peut pas** être contenu dans un autre tableau.
   - Le tableau de payload **doit** comporte 50 lignes ou moins.
   - Toutes les colonnes générées dans la payload **doivent** sont d’un type primitif.
   - Seules les **vingt premières colonnes** tableau sont générées.
- Seules **dix** compositions d’audience sont disponibles pour le moment

## Activation plus rapide {#faster-activation}

Une activation plus rapide vous permet d’activer votre audience vers une destination en aval immédiatement après l’évaluation de la composition. Par conséquent, si votre destination est définie pour s’activer après l’évaluation du segment, vous n’avez plus besoin d’attendre 24 heures pour que la tâche d’évaluation se termine.

Pour plus d’informations, consultez le guide [Activer les audiences vers des destinations de profils par lots](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
