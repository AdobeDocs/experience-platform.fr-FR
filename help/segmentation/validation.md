---
title: Validation de l’audience
description: Découvrez comment Experience Platform valide vos audiences pour s’assurer qu’elles fonctionnent bien en aval.
source-git-commit: 52439e55d3c48631488b17b6b04256bcbbe37bcb
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 1%

---


# Validation de l’audience

Lorsque vous écrivez une définition d’audience dans Adobe Experience Platform, la validation d’audience fournit des validations intégrées et des mécanismes de sécurisation pour vous assurer que vos audiences sont non seulement exactes, mais également stables et évolutives.

En adhérant aux bonnes pratiques en matière de définition des audiences, vous vous assurez que vos audiences peuvent évaluer plus rapidement, que votre logique reste efficace même lorsque la taille de votre audience augmente et que le risque d’échecs d’évaluation pendant les périodes de trafic élevé est réduit. Les audiences optimisées améliorent également la vitesse d’activation des destinations, réduisent la latence de la personnalisation en temps réel et maintiennent la stabilité globale des sandbox.

Experience Platform exécute ces validations en temps réel au fur et à mesure que vous créez votre audience dans le créateur de segments. Lorsque vous ajoutez des événements ou des attributs qui dépassent les seuils de validation, vous recevez immédiatement des commentaires dans l’interface du créateur de segments.

## Types de validation {#validation-types}

Lorsque la validation de l’audience s’exécute sur vos audiences, deux types de constructions différents peuvent être enfreints : les constructions de validation critiques et les constructions d’optimisation des performances.

Si une structure de validation critique est enfreinte, le système vous empêche d’enregistrer votre audience afin de protéger la stabilité de votre sandbox. En cas de violation d’une structure d’optimisation des performances, vous pourrez enregistrer votre audience, mais il est *vivement recommandé* de mettre à jour votre définition d’audience pour éviter des problèmes de performances.

## Contrôles de validation {#validation-checks}

Actuellement, les validations suivantes sont prises en charge :

| Contrôle de validation | Type | Seuil |
| ---------------- | ---- | --------- |
| Complexité logique | Validation critique | La définition de l’audience contient trop de requêtes, ce qui entraîne une complexité logique inutile. |
| Événements séquentiels | Validation critique | Il existe plus de 6 événements séquentiels dans une définition d’audience. |
| Comptage agrégé | Optimisation des performances | Il existe plus de 3 fonctions d’agrégation dans une définition d’audience. |
| Données imbriquées | Optimisation des performances | Il existe plus de 2 niveaux de profondeur de données imbriquées (types de données de tableau ou de mappage) dans une définition d’audience. |
| Taille de l’audience | Optimisation des performances | La taille de qualification de l’audience est supérieure à 30 % du nombre total de profils dans le sandbox. |

### [!BADGE Validation critique]{type=Negative} Complexité logique {#logical-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_rewritescheck"
>title="Alerte relative à l’efficacité des requêtes"
>abstract="Votre audience contient trop de requêtes, ce qui entraîne une complexité logique inutile. Simplifiez la définition de votre audience avant de continuer."

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_cnfcomplexitycheck"
>title="Complexité logique"
>abstract="Votre audience contient trop de requêtes, ce qui entraîne une complexité logique inutile. Simplifiez la définition de votre audience avant de continuer."

La validation de la complexité logique analyse la structure de vos instructions logiques (AND, OR, NOT) au sein de votre définition d’audience. Plus précisément, il recherche les définitions d’audience qui forceront le système à effectuer un nombre excessif de comparaisons par profil.

Si votre définition d’audience comporte un nombre excessif de comparaisons par profil, cette complexité accrue ralentit l’évaluation par profil. Cela augmente donc le temps global nécessaire à l’évaluation de l’audience.

Pour éviter de déclencher cette validation, restez simple dans votre définition d’audience. Si vous ne comprenez pas votre propre définition d’audience, c’est trop compliqué et Experience Platform peut prendre plus de temps pour évaluer l’audience.

**Exemple**

Supposons que vous souhaitiez trouver des clients qui vivent dans certains États. Vous _pouvez_ écrire ceci de manière inefficace en vérifiant si le profil possède la valeur pour un état qui correspond à l’une des 45 valeurs répertoriées, comme suit :

+++ Définition d’audience inefficace

```
State.equals("AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA","HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT")
```

+++

Cependant, en utilisant une vérification not , vous n’avez qu’à vérifier si le profil ne possède pas l’une des 5 valeurs répertoriées, ce qui se traduit par une requête beaucoup plus efficace.

+++ Définition efficace d’une audience

```
not(State.equals("VT", "VA", "WA", "WV", "WI", "WY" ))
```

+++

Supposons que vous vouliez trouver des clients qui sont des Canadiens dans votre plan d&#39;essai. Une approche moins efficace consisterait à rechercher des Canadiens dans votre plan d&#39;essai en excluant manuellement tous les autres plans, un par un, et en vérifiant que le profil ne figure dans aucun d&#39;entre eux.

+++ Définition d’audience inefficace

```
NOT(
    plan.equals("basic") OR
    plan.equals("standard") OR
    plan.equals("premium") OR
    plan.equals("enterprise")
) AND NOT (
    region.equals("us-east") OR
    region.equals("us-west") OR
    region.equals("eu-central") OR
    region.equals("apac")
)
```

+++

Au lieu de cela, vous devez être direct et cibler le plan spécifique que vous souhaitez inclure.

+++ Définition efficace d’une audience

```
plan.equals("trial") AND region.equals("canada")
```

+++

### [!BADGE Validation critique]{type=Negative} complexité des événements séquentiels {#sequential-event-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_chaincountcheck"
>title="Limite de séquence d’événements"
>abstract="Votre audience contient trop d’événements séquentiels. Vous ne pouvez avoir qu’un maximum de 6 événements séquentiels dans votre définition d’audience. Supprimez certains événements séquentiels de votre définition d’audience avant de continuer."

La validation de la complexité des événements séquentiels limite le nombre d’événements séquentiels dans une séquence à 6 événements.

La segmentation séquentielle est l’une des opérations les plus complexes d’un point de vue informatique dans Experience Platform, car le système doit analyser l’historique complet des événements d’expérience d’un client, les trier par horodatage et vérifier si l’ordre spécifié correspond à votre requête. En conséquence, lorsque la chaîne augmente, le nombre de permutations que le système doit calculer augmente considérablement.

Pour éviter de déclencher cette validation, concentrez-vous sur les principes de base de votre chaîne séquentielle en définissant le début, le milieu et la fin du parcours. Les étapes immédiates sont souvent impliquées dans la conversion finale.

**Exemple**

Supposons que vous souhaitiez cibler les utilisateurs et utilisatrices qui ont consulté un produit, l’ont ajouté au panier et l’ont acheté. Une approche moins efficace consisterait à vérifier chaque état individuel du chemin de l’utilisateur. Par exemple, la requête suivante passe par cette séquence d’événements : Se connecte au site web -> Recherche de produit -> Consulte une page de produit -> Ajoute au panier -> Accède à la commande -> Événement d’achat

+++ Définition d’audience inefficace

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "login"), B: WHAT(eventType = "search"), C: WHAT(eventType = "productView"), D: WHAT(eventType = "addToCart"), E: WHAT(eventType = "checkout"), F: WHAT(eventType = "purchase") ])
```

+++

Cependant, en réduisant la séquence au début, au milieu et à la fin, il vous suffit d’avoir une séquence d’événements de 3 événements de long, ce qui se traduit par une requête plus efficace. Par exemple, la requête suivante parcourt cette séquence d’événements : affiche une page de produit -> Ajoute au panier -> Événement d’achat

+++ Définition efficace d’une audience

```
chain(xEvent, timestamp, [ A: WHAT(eventType = "productView"), B: WHAT(eventType = "addToCart"), C: WHAT(eventType = "purchase") ])
```

+++

### [!BADGE Optimisation des performances]{type=Caution} Nombre agrégé {#aggregated-count}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_countaggregationcheck"
>title="Avertissement du filtre de comptage"
>abstract="Votre audience comporte trop d’événements d’agrégation. Vous devez utiliser un maximum de 3 événements d’agrégation dans votre audience. Pour éviter tout problème de performances, vous devez supprimer certains événements d’agrégation de votre définition d’audience."

La vérification du nombre agrégé limite à 3 conditions le nombre d’événements d’agrégation utilisés dans votre audience.

Un événement standard ne doit trouver qu’un seul événement correspondant pour qualifier un utilisateur. Cependant, un événement d’agrégation doit lire et analyser l’**historique complet** des événements d’un utilisateur avant de pouvoir prendre une décision, ce qui ralentit les temps de traitement et utilise davantage d’événements d’agrégation.

Pour éviter de déclencher cette validation, n’utilisez des nombres spécifiques que lorsque cela est strictement nécessaire pour la définition de l’audience. Par exemple, si vous devez uniquement savoir si un utilisateur s’est engagé une seule fois, vous pouvez utiliser la logique « Existe » standard, plutôt qu’un événement « Comptage > 0 ».

### [!BADGE Optimisation des performances]{type=Caution} complexité des données imbriquées {#nested-data-complexity}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_arraydepthcheck"
>title="Avertissement relatif aux données imbriquées"
>abstract="Votre audience comporte trop de couches de données imbriquées. Vous devez utiliser un maximum de 2 couches de données au sein de votre audience. Pour éviter tout problème de performances, aplatissez votre définition d’audience."

La validation de la complexité des données imbriquées limite à 2 calques le nombre de données imbriquées dans une définition d’audience.

Bien qu’Experience Platform prenne en charge l’utilisation d’objets de tableau et de mappage pour stocker des types de données complexes, la décompression de structures imbriquées pour rechercher une valeur nécessite une logique de traversée plus complexe. Plus les données sont imbriquées dans un tableau, plus leur récupération pour validation prend du temps.

Si vous effectuez fréquemment une segmentation sur un attribut profondément imbriqué, vous devrez peut-être contacter votre équipe d’ingénierie de données pour copier l’attribut à un niveau supérieur dans le schéma de profil pour un accès plus facile.

### [!BADGE Optimisation des performances]{type=Caution} Taille de l’audience {#audience-size}

>[!CONTEXTUALHELP]
>id="platform_segmentation_segmentbuilder_profilestorecheck"
>title="Avertissement relatif à la taille de l’audience"
>abstract="Votre audience est écrite de manière trop large. Évitez d’écrire une définition d’audience qui qualifie plus de 30 % du total des profils de votre sandbox. Pour éviter tout problème de performances, il est recommandé de renforcer la définition de votre audience."

La validation de la taille de l’audience vérifie si votre définition d’audience est si large que plus de 30 % du total des profils de votre sandbox remplissent les critères pour l’audience.

Bien qu’Experience Platform puisse gérer des audiences volumineuses, une définition d’audience trop vague (par exemple, Tous les clients et clientes actifs) peut augmenter le temps d’évaluation et la latence d’activation.

Si vous devez créer une audience qui qualifie plus de 30 % de votre banque de profils, assurez-vous que la première évaluation de l’audience est effectuée à l’aide de l’évaluation d’audience flexible. L’évaluation de l’audience avec une évaluation à la demande peut réduire l’impact global d’une audience importante sur la tâche de segmentation quotidienne.

## Étapes suivantes

Vous êtes arrivé au bout de ce guide, vous comprenez mieux comment Experience Platform exécute des validations automatiques afin d’améliorer l’évaluation, la stabilité et l’évolutivité. Pour plus d’informations sur la création d’audiences à l’aide de l’interface utilisateur, consultez la [documentation du créateur de segments](./ui/segment-builder.md).

## Annexe

L’annexe suivante répertorie les questions fréquentes sur la validation des audiences dans Experience Platform.

### Questions fréquentes {#faq}

**Que se passe-t-il si j’ignore les avertissements et que j’enregistre l’audience ?**

+++ Réponse

Pour les avertissements d’optimisation des performances, l’audience est enregistrée et le système tente de l’évaluer. Cependant, les temps de traitement peuvent être considérablement plus lents. Dans des situations extrêmes, si le volume de données est suffisamment élevé, la tâche de segmentation peut échouer ou expirer, ce qui vous force à reconcevoir votre audience.

Pour les erreurs de validation critiques, vous ne pourrez pas enregistrer l’audience.

+++

**Puis-je demander une augmentation de la limite « Événement séquentiel » ?**

+++ Réponse

Non. Il s’agit d’un mécanisme de sécurisation solide conçu pour protéger la stabilité de l’ensemble de l’environnement Experience Platform. Si votre séquence nécessite plus de 6 étapes, cela indique clairement que la logique doit être simplifiée ou divisée en deux audiences différentes (une audience « Engagement » et une audience « Conversion », par exemple).

+++

**Ces nouvelles validations interrompront-elles mes audiences existantes ?**

+++ Réponse

Ces validations s’exécutent au moment de la **création**. Par conséquent, vos audiences existantes continueront à s’exécuter telles quelles. Cependant, si vous tentez de modifier une audience existante qui enfreint ces règles, vous devrez l’optimiser avant de pouvoir enregistrer vos modifications.

+++

**J’ai des exigences complexes en matière de données. Comment éviter l’avertissement « Données imbriquées » ?**

+++ Réponse

Il est préférable d’éviter l’avertissement « Données imbriquées » au niveau de la couche de modélisation des données. Quelques conseils incluent la collaboration avec votre équipe d’ingénierie de données pour aplatir votre schéma XDM et apporter des attributs critiques (tels que `subscriptionStatus` et `loyaltyTier`) au niveau supérieur du profil.

+++

**Ces vérifications s’appliqueront-elles aux audiences tant Brouillon que Publié ?**

+++ Réponse

Oui, ces vérifications s’appliquent à *toutes* les audiences évaluées dans Experience Platform.

+++
