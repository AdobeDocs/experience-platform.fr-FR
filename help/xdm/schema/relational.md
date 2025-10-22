---
keywords: Experience Platform;accueil;rubriques populaires;schéma relationnel;schémas relationnels;schéma;schéma;xdm;modèle de données d’expérience;
solution: Experience Platform
title: Schémas relationnels
description: Découvrez les schémas relationnels (anciennement appelés schémas basés sur des modèles) dans Adobe Experience Platform, y compris les fonctionnalités, les champs obligatoires, les relations et les limitations.
badge: Disponibilité limitée
exl-id: 397e5937-b892-4fd3-b90e-29ed9229dc69
source-git-commit: 605c169c9de7a978e6d2f0bdc809371c82cd3280
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# Schémas relationnels

>[!AVAILABILITY]
>
>Les schémas Data Mirror et relationnels sont disponibles pour les détenteurs de licence Adobe Journey Optimizer **Campagnes orchestrées**. Ils sont également disponibles en tant que **version limitée** pour les utilisateurs de Customer Journey Analytics, selon votre licence et l’activation des fonctionnalités. Contactez votre représentant Adobe pour obtenir l’accès.

Les schémas relationnels fournissent un modèle de modélisation contrôlé et flexible pour représenter les données structurées dans le lac de données Adobe Experience Platform. Ils prennent en charge les clés primaires appliquées, les relations au niveau du schéma et un contrôle affiné des enregistrements, le tout sans recourir à des schémas d’union ou à des systèmes de base de données relationnelle complets.

>[!IMPORTANT]
>
>Les considérations relatives à la suppression des données s’appliquent à toutes les implémentations de schéma relationnel. Les applications qui utilisent ces schémas doivent comprendre comment les suppressions affectent les jeux de données associés, les exigences de conformité et les processus en aval. Planifiez les scénarios de suppression et examinez les [conseils d’hygiène des données](../../hygiene/ui/record-delete.md#relational-record-delete) avant la mise en œuvre.

>[!NOTE]
>
>Dans les versions antérieures de la documentation de Adobe Experience Platform, les schémas relationnels étaient auparavant appelés schémas basés sur des modèles.

Utilisez des schémas relationnels pour :

* Assurer l’intégrité des données à l’aide de clés primaires composites ou à champ unique appliquées.
* Activez le suivi précis des modifications à l’aide du contrôle de version pour les insertions, les mises à jour et les suppressions.
* Définissez des relations réutilisables au niveau du schéma pour modéliser des connexions d’entités du monde réel.
* Évitez de dupliquer les structures de schéma entre les applications en prenant en charge plusieurs modèles de données.
* Ignorez les contraintes de schéma d’union pour rationaliser l’intégration, réduire la surcharge du schéma et éviter les modifications de schéma indésirables.

## Différences entre les schémas relationnels et les schémas XDM standard

Les schémas XDM standard d’Experience Platform adoptent l’un des trois comportements de données suivants : enregistrement, série temporelle ou ad hoc. Pour obtenir des définitions et des détails, voir [Comportements des données XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home#data-behaviors).

Dans le modèle traditionnel, les schémas d’enregistrement et de série temporelle participent aux [schémas d’union](../api/unions.md) (consultez également le guide de l’interface utilisateur du schéma d’union [&#128279;](../../profile/ui/union-schema.md)). Ces schémas évoluent automatiquement à mesure que les [groupes de champs](./composition.md#field-group) partagés sont mis à jour et que les champs personnalisés doivent être imbriqués sous un espace de noms client. Bien que puissant, ce modèle peut ralentir l’intégration, produire des schémas trop complexes avec des champs inutilisés et nécessiter un mappage ou une transformation des données supplémentaires. Ces facteurs augmentent la courbe d’apprentissage et l’effort de maintenance continu.

Les schémas relationnels suppriment les dépendances de schéma d’union, ce qui élimine les mises à jour automatiques des groupes de champs partagés et permet de définir directement des champs sans restriction d’espace de noms client. Vous avez un contrôle explicite sur les clés primaires, les relations et la conception initiale du schéma, ce qui facilite la modélisation des données en fonction de vos besoins au moment de la création.

## Fonctionnalités des schémas relationnels

Utilisez les fonctionnalités suivantes pour modéliser des données structurées dans le lac de données tout en préservant la gouvernance, l’intégrité et l’interopérabilité.

* **Prise en charge du comportement des schémas** : configuration d’avec :
   * **Comportement d’enregistrement** : capture le statut actuel d’une entité, tel qu’un client, un compte ou une campagne.
   * **Comportement de série temporelle** : capture les événements et l’heure à laquelle ils se produisent, ce qui est utile pour le suivi des séquences ou des modifications au fil du temps.
* **Application des clés de Principal** : définissez une clé primaire pour identifier de manière unique chaque enregistrement et empêcher les doublons lors de l&#39;ingestion.
* **Gestion des versions** : utilisez un **identifiant de version** (descripteur) pour vous assurer que les mises à jour sont appliquées dans le bon ordre, même si les enregistrements arrivent en dehors de la séquence.
* **Mappage des relations** : créez des relations un-à-un ou plusieurs-à-un entre les schémas relationnels ou entre les schémas relationnels et standard. Les définitions de relation sont stockées sous forme de descripteurs pour activer des jointures efficaces.
* **Évolution simplifiée** : les schémas relationnels ne participent pas aux vues d’union et ne sont pas mis à jour lorsque les groupes de champs partagés changent, ce qui empêche toute modification inattendue en aval.
* **Définition de champ flexible** : ajoutez des champs directement sans espace de noms d’ID client. Les schémas relationnels ne prennent pas en charge les groupes de champs XDM.
* **Aucune dépendance aux schémas d’union** : améliore les performances des requêtes et réduit la surcharge opérationnelle de la gestion des vues de schéma global.
* **Ordre des événements et de l’heure** : pour les schémas de série temporelle, utilisez un **identifiant d’horodatage** pour classer les événements par heure d’occurrence au lieu de l’heure d’ingestion.

## Champs obligatoires

Les schémas relationnels nécessitent certains descripteurs, à savoir des métadonnées dans la définition du schéma qui contrôlent les comportements et contraintes clés. Ajoutez les descripteurs suivants dans le cadre de votre définition de schéma.

### descripteur de clé de Principal

Utilisez un descripteur de clé primaire pour vous assurer que chaque enregistrement est identifiable de manière unique. Les configurations prises en charge sont les suivantes :

* **Clé primaire à champ unique** : utilisez un champ avec une valeur unique pour chaque enregistrement.
* **Clé primaire composite** : utilisez plusieurs champs pour former un identifiant unique. Pour les schémas de série temporelle, la clé composite doit inclure le champ d’horodatage identifié par le descripteur d’horodatage.

>[!NOTE]
>
>Dans l’éditeur de schéma de l’interface utilisateur, le descripteur de version et les descripteurs d’horodatage apparaissent respectivement sous la forme « [!UICONTROL Version identifier] » et « [!UICONTROL Timestamp identifier] ».

**Exemple (champ unique) :**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": "customerId"
}
```

**Exemple (composite pour une série temporelle)**

```json
{
  "xdm:descriptor": "xdm:descriptorPrimaryKey",
  "xdm:sourceProperty": ["customerId", "eventTimestamp"]
}
```

### Descripteur de version (identifiant)

Définissez un descripteur de version (identifiant) pour conserver un état d’enregistrement correct et vous assurer que la dernière mise à jour est appliquée. Lorsque plusieurs enregistrements partagent la même clé primaire, l&#39;enregistrement ayant la valeur de version la plus élevée est considéré comme le plus récent.

**Exemple :**

```json
{
  "xdm:descriptor": "xdm:descriptorVersion",
  "xdm:sourceProperty": "lastModified"
}
```

### Descripteur d’horodatage (identifiant)

Pour les schémas de série temporelle, définissez un descripteur d’horodatage (identifiant) afin de définir l’heure de l’événement à classer.

**Exemple :**

```json
{
  "xdm:descriptor": "xdm:descriptorTimestamp",
  "xdm:sourceProperty": "eventTimestamp"
}
```

>[!NOTE]
>
>Les descripteurs font partie des métadonnées de définition de schéma et ne sont pas stockés dans les lignes de données.

Pour obtenir des instructions sur la création de descripteurs dans l’éditeur de schémas, voir [Créer des descripteurs dans l’éditeur de schémas](../tutorials/relationship-ui.md). Pour la création basée sur l’API, voir [Création de descripteurs à l’aide de l’API](../tutorials/relationship-api.md).

## Prise en charge des relations {#relationship-support}

La modélisation des données relationnelles est une utilisation principale des schémas relationnels. Les cas d’utilisation des applications peuvent même faire référence à ces schémas en tant que « schémas relationnels ». Les descripteurs de relation permettent ces connexions en liant les jeux de données entre les schémas sans incorporer de clés étrangères dans les lignes de données. Ils améliorent l’intégrité du référentiel, activent des modèles de modélisation réutilisables et prennent en charge les requêtes connectées entre les applications.

Créez des descripteurs de relation au niveau du schéma pour la résolution dynamique au moment de la requête. Les valeurs de cardinalité (1:1, plusieurs-à-un) fournissent des conseils, mais n’appliquent pas de contraintes lors de l’ingestion, ce qui permet une modélisation des données flexible sur les jeux de données connectés.

Avant d’ajouter des descripteurs de relation, déterminez le type et la cible appropriés :

* **Un-à-un** - Chaque enregistrement du schéma source correspond à au plus un enregistrement du schéma de destination.
* **Plusieurs-à-un** - Plusieurs enregistrements du schéma source peuvent référencer le même enregistrement dans le schéma de destination.

>[!NOTE]
>
>Vous pouvez définir des relations entre deux schémas relationnels ou entre un schéma relationnel et un schéma standard. Les relations avec les schémas ad hoc ne sont pas prises en charge.

**Exemple : relation un-à-un**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "accountId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/account",
  "xdm:destinationProperty": "accountId"
}
```

**Exemple : relation multiple-à-un**

```json
{
  "xdm:descriptor": "xdm:descriptorRelationship",
  "xdm:sourceProperty": "customerId",
  "xdm:destinationSchema": "https://ns.adobe.com/xdm/context/customer",
  "xdm:destinationProperty": "customerId"
}
```

Pour obtenir la liste des types de descripteur de relation et de la syntaxe associée, reportez-vous à la [référence de l’API descriptors](../api/descriptors.md).Pour apprendre à appliquer ces concepts en pratique, suivez les tutoriels [définir une relation dans l’API](../tutorials/relationship-api.md) ou [créer une relation dans l’interface utilisateur](../tutorials/relationship-ui.md).

>[!NOTE]
>
>Comme les relations sont définies au niveau du schéma, veillez à joindre explicitement les jeux de données associés dans vos requêtes. Utilisez un outil tel que Data Distiller pour résoudre ces relations pendant le temps de requête.

>[!IMPORTANT]
>
>La cardinalité de relation est informative et n’est pas appliquée lors de l’ingestion. Elle est appliquée uniquement lors de la résolution de relations pendant la requête ou l’analyse. Ne vous fiez pas aux paramètres de cardinalité pour valider vos données lors de l’ingestion. Vérifiez et nettoyez vos données vous-même, et assurez-vous que les règles de relation que vous définissez correspondent à la manière dont vous avez l’intention d’interroger ou d’analyser les données.

>[!NOTE]
>
>Les schémas relationnels peuvent être liés à des schémas standard, mais pas à des schémas ad hoc.

## Considérations relatives à la suppression des données et à l’hygiène {#data-hygiene-support}

Les schémas relationnels permettent des suppressions précises au niveau des enregistrements, avec des implications universelles pour toutes les applications et tous les cas d’utilisation. Les descripteurs de clé de Principal, de version et d’horodatage fournissent la base d’une identification précise des enregistrements lors des opérations de suppression.

### Incidences de la suppression universelle

Toutes les applications qui utilisent des schémas relationnels doivent tenir compte des points suivants :

* **Intégrité référentielle** : les suppressions peuvent affecter les enregistrements associés aux jeux de données connectés
* **Exigences de conformité** : certains secteurs d’activité nécessitent des comportements de suppression et des pistes d’audit spécifiques
* **Comportement de l’application** : les systèmes en aval peuvent avoir besoin de gérer les événements de suppression de manière appropriée
* **Cohérence des données** : les jeux de données associés doivent maintenir la cohérence pendant les opérations de suppression
* **Planification des suppressions** : tenez compte des impacts en aval sur tous les jeux de données et applications connectés pendant la phase de conception

Pour obtenir des conseils d’implémentation, voir [&#x200B; Suppression d’enregistrements des jeux de données en fonction de schémas relationnels &#x200B;](../../hygiene/ui/record-delete.md#relational-record-delete).

## Restrictions et considérations {#limitations}

Examinez les limites suivantes avant d’utiliser des schémas relationnels :

* Les schémas relationnels ne participent pas aux schémas d’union.
* L’évolution des schémas est manuelle et n’est pas mise à jour automatiquement lorsque les groupes de champs changent.

>[!IMPORTANT]
>
>L’évolution des schémas devient limitée une fois qu’un jeu de données est initialisé à l’aide du schéma. Planifiez soigneusement les noms et les types de champs à l’avance, car une fois les données ingérées, les champs ne peuvent pas être supprimés ni modifiés.

* Les relations sont limitées à un-à-un et à plusieurs-à-un.
* La disponibilité dépend de l’activation de votre licence ou de votre fonctionnalité.
* Des clés primaires composites sont requises pour les schémas de série temporelle.
