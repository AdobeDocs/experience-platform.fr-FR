---
title: Suppression de ressources
description: Découvrez comment supprimer des ressources de balises dans Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
TQID: https://experienceleague.adobe.com/1T9DW9nd4xkPFETnQV9Ir-foFsR7uenbZr8qhNhCv-Q
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: abc02dd6-664f-446a-9aaa-675bc0f2fe4aid: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: e2b4267c-3fe4-4c51-b9f5-7aefcfa5996cid: f6ff4d13-7b5c-4533-8556-95e76673d4cbid: f9a2105e-7a47-4e85-9193-31a519a2cb83
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 514
ht-degree: 90%

---

# Suppression de ressources

La suppression d’une ressource entraîne la suppression définitive de cette ressource dans Adobe Experience Platform. Si vous souhaitez supprimer une ressource d’une bibliothèque de balises spécifique tout en souhaitant que cette ressource puisse être utilisée dans d’autres bibliothèques, consultez le guide sur la [suppression de ressources d’une bibliothèque](remove-resources-from-library.md).

Vous pouvez supprimer des éléments de données, des règles, des extensions, des hôtes, des environnements et des propriétés. Une fois supprimées, il n’est pas possible de récupérer ces ressources.

Les ressources qui sont ajoutées aux bibliothèques (éléments de données, règles et extensions) revêtent des considérations spéciales lorsque vous les supprimez.

## Préparer la suppression d’une ressource

Les ressources existent dans différents états et elles dépendent les unes des autres. Avant de supprimer une ressource, vous devez vous assurer qu’elle est dans un état lui permettant d’être supprimée.

La préparation de la suppression d’une ressource comprend deux étapes de base :

1. Résoudre les dépendances
1. Supprimer des bibliothèques

### Résoudre les dépendances

Les règles, les éléments de données et les extensions sont interdépendants. Par conséquent, la plupart du temps, lorsque vous en supprimez un, il existe un effet domino et vous avez alors d’autres éléments à supprimer.

#### Règles

Les règles dépendent d’autres ressources (extensions et éléments de données), mais elles ne contiennent aucune ressource qui en dépend. La suppression d’une règle implique que vous ne pouvez plus l’utiliser dans une bibliothèque ou même l’afficher, mais vous n’aurez aucune dépendance à supprimer ultérieurement.

#### Éléments de données

Les éléments de données dépendent des extensions. Cependant, contrairement aux règles, les éléments de données peuvent comporter des règles et des extensions qui dépendent d’eux. Si vous supprimez un élément de données, toutes les règles ou extensions qui en dépendent seront affectées.

Après suppression, l’élément de données ne renvoie plus la valeur correcte au moment de l’exécution. Il renvoie alors soit une chaîne vide, soit le nom de l’élément de données supprimé encapsulé dans %% (par exemple : `%data-element-name%`). Il est possible de configurer ce comportement dans Property Settings (Paramètres de propriété).

Vous pouvez résoudre ces dépendances avant ou après la suppression de l’élément de données.

#### Extensions

Toutes les autres ressources (règles, composants de règles et éléments de données) sont fournies par des extensions.

Le comportement des composants de règles et des éléments de données dépend d’extensions, et c’est également le cas pour leur affichage dans l’interface utilisateur de collecte de données. Si vous supprimez l’extension avant de résoudre les dépendances, vous ne pourrez plus afficher ces ressources orphelines. Ces ressources orphelines apparaissent dans les vues Liste, mais vous recevrez une erreur si vous essayez d’ouvrir la vue détaillée.

C’est pourquoi vous devez faire particulièrement attention lorsque vous supprimez des extensions et résoudre les dépendances avant de les supprimer.

### Supprimer des bibliothèques

Avant de pouvoir supprimer une ressource, vous devez la supprimer des bibliothèques qui la contiennent. Ce processus diffère selon l’état de la bibliothèque.

#### Développement

1. Ouvrez la bibliothèque.
1. Supprimez la ressource.
1. Enregistrez la bibliothèque.
1. Supprimez la ressource.

#### Envoyé ou approuvé

1. Rejetez la bibliothèque (la renvoyer vers Développement).
1. Suivez les étapes ci-dessus pour supprimer une ressource d’une bibliothèque de développement.

#### Production

1. Désactivez la ressource.
1. Publiez la ressource désactivée jusqu’à Production.
1. Supprimez la ressource.

## Supprimer une ressource

Dans la vue de liste appropriée, sélectionnez la ressource à supprimer, puis sélectionnez **[!UICONTROL Supprimer]**.
