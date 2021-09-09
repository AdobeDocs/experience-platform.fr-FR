---
title: Autorisations utilisateur pour les balises
description: Découvrez les différents types d’autorisations disponibles pour les balises et quelques stratégies de mise en oeuvre de base pour différents cas d’utilisation professionnels.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: 88593d921d6ad97fc4dfb059f0272817caee06c7
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 24%

---

# Autorisations utilisateur pour les balises

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les autorisations utilisateur des balises dans Adobe Experience Platform sont attribuées aux utilisateurs via Adobe Admin Console. Plutôt que d’être affectés à des utilisateurs individuels, différents ensembles d’autorisations sont configurés séparément en tant que profils de produit. Les utilisateurs sont ensuite affectés à ces profils de produit afin d’obtenir les autorisations pour lesquelles ils ont été configurés.

Ce guide présente un aperçu des différents types d’autorisations disponibles pour les balises, les fonctionnalités auxquelles elles donnent accès et quelques stratégies de mise en oeuvre de base pour différents cas d’utilisation commerciale.

>[!NOTE]
>
>Pour savoir comment configurer les autorisations pour les utilisateurs utilisant Admin Console, reportez-vous au tutoriel sur la [gestion des autorisations pour les balises](./manage-permissions.md).

## Types d’autorisations

Dans un profil de produit, les autorisations pour les balises sont divisées en quatre catégories :

1. Plateformes
1. Propriétés
1. Droits de propriété
1. Droits d’entreprise

### Plateformes

Chaque propriété de balise possède une plateforme. Vous pouvez actuellement utiliser deux plateformes pour les balises : Web et Mobile. Vous pouvez utiliser ce type d’autorisation pour restreindre ou accorder l’accès à un type particulier de propriété. Cela peut s’avérer utile lorsque l’équipe qui gère vos applications mobiles diffère de celle qui gère vos sites web.

### Propriétés

Par défaut, les profils de produit accordent l’accès à toutes les propriétés qui existent au sein de votre entreprise, à la fois actuellement et à l’avenir. Avec ce type d’autorisation, vous pouvez restreindre ou accorder l’accès à des propriétés existantes spécifiques par nom.

### Droits de propriété {#property-rights}

Toute propriété que vous créez dans l’interface utilisateur de la collecte de données est disponible dans Admin Console, ce qui vous permet de regrouper la propriété avec des droits de propriété spécifiques dans le même profil de produit.

Par exemple, si un profil de produit donné n’a pas accès à Propriété A1, les utilisateurs qui appartiennent à ce profil ne peuvent pas voir ni modifier les paramètres de la propriété A1.

Si un utilisateur appartient à un profil qui a accès à Propriété A1, les actions qu’il peut effectuer dans Propriété A1 sont déterminées par les droits qui lui ont été octroyés à partir de ce profil. Si un utilisateur dispose d’autorisations pour Propriété A1 mais ne dispose pas de droits attribués, il dispose d’un accès en lecture seule pour cette propriété.

Le tableau suivant décrit les droits de propriété disponibles et les fonctionnalités auxquelles ils donnent accès :

| Droit de propriété | Description |
| --- | --- |
| **Développer** | Vous pouvez ainsi effectuer les actions suivantes :<ul><li>Création de règles et d’éléments de données</li><li>Créer des bibliothèques et les créer dans des environnements de développement existants</li><li>Soumettre une bibliothèque pour approbation</li></ul>La plupart des tâches quotidiennes dans lʼinterface utilisateur de la collecte de données requièrent ce droit. |
| **Approuver** | Vous pouvez ainsi prendre une bibliothèque envoyée et la créer dans l’environnement d’évaluation. Vous pouvez également approuver une bibliothèque en vue de la publier une fois le test terminé. |
| **Publier** | Vous pouvez ainsi publier des bibliothèques approuvées dans l’environnement de production. |
| **Gérer les extensions** | Vous pouvez ainsi effectuer les actions suivantes : <ul><li>Installation de nouvelles extensions sur une propriété</li><li>Modification de la configuration d’une extension déjà installée</li><li>Suppression d’une extension</li></ul>Consultez la documentation de présentation des extensions pour [plus dʼinformations sur les extensions](../managing-resources/extensions/overview.md). Ce rôle appartient généralement au service informatique ou au marketing, selon votre organisation. |
| **Gérer les environnements** | Vous pouvez ainsi créer et modifier des environnements. Pour plus dʼinformations, consultez la [documentation sur les environnements](../publishing/environments.md). Ce rôle appartient généralement au groupe informatique. |

{style=&quot;table-layout:auto&quot;}

### Droits d’entreprise

Les droits d’entreprise s’appliquent aux autorisations qui s’appliquent à plusieurs propriétés. Ces informations sont présentées dans le tableau ci-dessous :

| Droit de l’entreprise | Description |
| --- | --- |
| **Gérer les propriétés** | Vous pouvez ainsi effectuer les actions suivantes :<ul><li>Création de propriétés</li><li>Modification des métadonnées et des paramètres au niveau de la propriété</li><li>Suppression des propriétés</li></ul>Les administrateurs assument généralement ce rôle. Pour plus d’informations, consultez la [documentation sur les propriétés](companies-and-properties.md) . |
| **Développer des extensions** | Permet de créer et de modifier des modules d’extension dont l’entreprise est propriétaire, y compris les versions privées et les demandes de publication publique. |
| **Gérer les configurations d&#39;application** | Cette option n’est disponible que si vous disposez d’une licence pour Adobe Journey Optimizer ou d’une autre solution qui accorde l’accès aux messages in-app et push mobiles.  Cela permet de gérer les applications dont Experience Cloud a connaissance, ainsi que les informations dʼidentification push nécessaires pour communiquer avec le service Firebase Cloud Messaging et le service de notification push Apple. |

{style=&quot;table-layout:auto&quot;}

## Autorisations utilisateur totales

Les autorisations totales d’un utilisateur individuel sont déterminées par son appartenance totale à différents profils de produit. Si un utilisateur appartient à plusieurs profils de produit, les autorisations de chaque profil sont additionnées plutôt que multipliées.

Par exemple, le profil de produit A vous accorde le droit de développement pour Propriété 1. Le profil de produit B vous accorde le droit de publication pour Propriété 2. Dans ce cas, vous pouvez développer dans Propriété 1 et publier dans Propriété 2, mais vous ne pouvez pas publier dans Propriété 1 ni développer dans Propriété 2, car vous n’avez pas reçu de droits explicites à cet effet.

## Scénarios de droits

Différentes entreprises ont des besoins différents lors de la création de profils de produit. Ces besoins varient en fonction de la taille de l’entreprise, de la structure de l’entreprise, du nombre de sites, du nombre de personnes impliquées dans la gestion des balises, etc.

Vous trouverez ci-dessous quelques scénarios courants et un point de départ recommandé lorsque vous envisagez de créer des profils de produit et d’y ajouter des utilisateurs.

### Affichage unique

Si vous dirigez une petite entreprise comptant une personne responsable de tout, accordez à cet utilisateur des autorisations pour toutes les propriétés et attribuez-lui tous les droits répertoriés ci-dessus.

### Séparation des tâches

Supposons que de nombreuses personnes de votre entreprise soient impliquées dans le balisage. Vous disposez d’un ensemble de personnes (par exemple, un consultant externe) qui créent des règles et des éléments de données, mais vous ne souhaitez pas qu’elles aient accès à l’environnement de production. Dans ce cas, vous souhaitez vous assurer que personne ne se déploie vers Production, à l’exception de l’équipe informatique.

Pour ce faire :

1. Créez un compte pour vos consultants et accordez-leur uniquement le droit de développement .
1. Le consultant crée et teste dans les limites que vous avez définies.
1. Si le consultant souhaite une nouvelle extension ou est prêt à publier, un représentant de votre entreprise (disposant des droits appropriés) effectue ces actions.

### Entreprise

Une entreprise peut avoir plusieurs sites divisés géographiquement, avec différentes équipes responsables de chaque région. Au sein de ces équipes, différentes personnes se chargent du développement et de la publication.

Cela se rapproche de la section « Séparation des tâches » ci-dessus, à l’exception de l’organisation par zone géographique. Par exemple, vous pouvez créer un profil &quot;Développer&quot; et un profil &quot;Publier&quot; pour l’Amérique du Nord, et créer des groupes &quot;Développer&quot; et &quot;Publier&quot; distincts pour l’Europe.

## Exemples de rôles

Le tableau suivant fournit quelques exemples des types de rôles que vous pouvez avoir dans votre organisation et des autorisations que vous devez leur attribuer :

| Rôle | Description | Propriétés | Droits de propriété | Droits d’entreprise |
| --- | --- | --- | --- | --- |
| Le gestionnaire | Souhaite voir ce qui se passe dans le système, mais ne devrait pas être en mesure d’apporter des modifications. | Inclusion automatique | (Aucun) | (Aucun) |
| Le spécialiste marketing | Peut installer des extensions et configurer de nouvelles balises pour les propriétés existantes, mais ne peut pas publier dans les environnements d’évaluation ou de production. | Inclusion automatique | <ul><li>Développer</li><li>Gérer les extensions</li></ul> | <ul><li>Gérer des propriétés</li></ul> |
| Le développeur d’applications mobiles | est chargé de mettre en oeuvre des solutions tierces et d’Adobe dans une application mobile native. | Inclusion automatique | <ul><li>Développer</li><li>Gérer les extensions</li></ul> | <li>Gérer des propriétés</li><li>Gérer les configurations d’application</li> |
| L’équipe informatique | ne modifie pas les balises, mais ils ont un contrôle total sur les environnements d’évaluation et de production et sur ce qu’elles contiennent. | Inclusion automatique | (Aucun) | <ul><li>Approuver</li><li>Publiez</li><li>Gérer les environnements</li></ul> |
| Le développeur d’extensions | Développe des extensions et peut les soumettre pour approbation, mais ne peut pas les publier ni les ajouter aux propriétés existantes. | Inclusion automatique | <ul><li>Développer</li></ul> | <ul><li>Gérer des propriétés</li><li>Développer des extensions</li></ul> |
| Le super utilisateur | Fait tout. | Inclusion automatique | <ul><li>Développer</li><li>Approuver</li><li>Publiez</li><li>Gérer les extensions</li><li>Gérer les environnements</li></ul> | <ul><li>Gérer des propriétés</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Étapes suivantes

Ce document fournit un aperçu des autorisations disponibles pour les balises dans Experience Platform. Pour obtenir des instructions sur la configuration des profils de produit pour les balises dans Adobe Admin Console, consultez le guide sur la [gestion des autorisations d’utilisateur](./manage-permissions.md).
